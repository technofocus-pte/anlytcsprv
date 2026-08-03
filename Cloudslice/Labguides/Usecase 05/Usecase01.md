## Use Case 1 - From Semantics to Insights: Leveraging Fabric IQ Ontology with Fabric Data Agents

**Introduction**

In modern data platforms, enterprises often need a **business-centric
semantic layer** that unifies meaning across diverse data sources and
analytical models. The *Ontology (preview)* feature in Microsoft Fabric
IQ enables you to build this layer by defining **enterprise concepts**
(like products, stores, and events) and **their relationships**, then
binding these definitions to real data across your lakehouse, semantic
models, and event streams.

In the scenario, a fictional company called **Lakeshore Retail**, which
sells ice cream at multiple locations. Using sample data, the tutorial
shows how to set up your environment and begin building an ontology that
captures business concepts such as *Store*, *Products*, and *SaleEvent*.
You’ll also connect streaming data (like freezer temperatures from
Eventhouse) to these concepts so the ontology can support **cross-domain
reasoning and queries**, for instance: *“Which stores have lower ice
cream sales when freezer temperature rises above –18 °C?”*

**Objectives**

- Prepare a Microsoft Fabric workspace with required services, including
  Lakehouse, Eventhouse, and Ontology (preview).

- Build a business-centric ontology by defining core entity types such
  as Store, Products, SaleEvent, and Freezer.

- ind static data from OneLake tables and time-series data from
  Eventhouse to ontology entities.

- Create meaningful relationships between entities to represent real
  business processes (for example, Store has SaleEvent and Store
  operates Freezer).

- Explore and validate the ontology using entity instances, relationship
  graphs, and query builder filters.

- Enable natural language querying by integrating the ontology with a
  Fabric Data Agent (preview).

# Exercise 1: Environment Setup

## Task 1: Create a Fabric workspace

In this task, you create a Fabric workspace. The workspace contains all
the items needed for this lakehouse tutorial, which includes lakehouse,
dataflows, Data Factory pipelines, the notebooks, Power BI datasets, and
reports.

1.  Open your browser, navigate to the address bar, and type or paste
    the following URL: +++https://app.fabric.microsoft.com/+++
    then press the **Enter** button and sign in with your credentials

| Credential | Value |
|------------|-------|
| Username | +++@lab.CloudPortalCredential(User1).Username+++ |
| Password | +++@lab.CloudPortalCredential(User1).Password+++ |
2. In the portal, switch to Fabric Mode before proceeding to create workspace.
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/imga1.png)
3.  In the Workspaces pane, click on **+New workspace** tile

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image1.png)

3.  In the **Create a workspace** pane that appears on the right side,
    enter the following details, and click on the **Apply** button.

| Setting | Value |
|----------|----------|
| Name | +++Fabric IQ OntologyXXXX+++ **(XXXX can be a unique number)** |
| Advanced | Under **License mode**, select **Fabric capacity** |
| Default storage format | **Small dataset storage format** |

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image2.png)
>
> ![](./media/image3.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image4.png)

## Task 2: Create a lakehouse

1.  Create a new lakehouse by clicking on the **+New item** button in
    the navigation bar.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image5.png)

2.  Filter by, and select, the **+++Lakehouse+++** tile.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image6.png)

3.  In the **New lakehouse** dialog box, enter **+++IQ_Lakehouse+++** in the **Name** field and **unselect** the lakehouses schemas.
    Click on the **Create** button and open the new lakehouse.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image7.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image8.png)

4.  You will see a notification stating **Successfully created SQL
    endpoint**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image9.png)

## Task 3: Ingest sample data

1.  In the **IQ_Lakehouse** page, navigate to **Get data in your
    lakehouse** section, and click on **Upload files as shown in the
    below image.**

> ![](./media/image10.png)

2.  On the Upload files tab, click on the folder under the Files

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image11.png)

3.  Browse to **C:\LabFiles\Lab1** on your VM, then
    select **DimProducts.csv, DimStore.csv, FactSale.csv** and
    **Freezer.csv** file and click on **Open** button.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image12.png)

4.  Then, click on the **Upload** button and close the **Upload
    files** dialog by selecting the **X** icon for the dialog.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image13.png)
>
> ![A screenshot of a upload box AI-generated content may be
> incorrect.](./media/image14.png)

5.Select **Files**. The file appears in the Files pane.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image15.png)

6.  In the **Lakehouse** page, Under the Explorer pane select **Files**.
    Now, hover your mouse over the **DimProducts.csv** file. Click on
    the horizontal ellipses **(…)** beside **DimProducts.csv** .
    Navigate and click on **Load Table**, then select **New table**.

> ![](./media/image16.png)
>
> ![](./media/image17.png)

7.  In the **Load file to new table** dialog box, click on
    the **Load** button.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image18.png)

8.  Now successfully created **DimProducts** table

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image19.png)

9.  Select the **DimProducts** table to preview the data.

\[!note\]**Note**: You may need to select the **Refresh** button more
than once to preview the data.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image20.png)

10. Repeat Steps 7 through 9 to push the remaining files into the
    tables.

![](./media/image21.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image22.png)

> ![](./media/image23.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image24.png)
>
> ![](./media/image25.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image26.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image27.png)

11. From the left navigation bar, select **Fabric IQ Ontology**.

> ![](./media/image28.png)

## Task 4: Prepare the eventhouse

Follow these steps to upload the device streaming data file to a KQL
database in Eventhouse.

1.  On the **Fabric IQ Ontology** home page, select **+New item** and
    select **Eventhouse**. 

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image29.png)

2.  Name the Eventhouse +++**TelemetryDataEH**+++ and click on
    the **Create** button.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image30.png)

3.  The eventhouse opens when it's ready
   ![A screenshot of a computer
    AI-generated content may be incorrect.](./media/image31.png)

4.  Open the KQL database by selecting its name.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image32.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image33.png)

5.  On the lower ribbon of your **KQL database**, click on **Get data**,
    then select **Local file** to upload files from your local system
    into the database.![A screenshot of a computer AI-generated content
    may be incorrect.](./media/image34.png)

6.  Select the target option to ingest data into a new table, click +
    New table, and enter a table name as +++**FreezerTelemetry**+++.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image35.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image36.png)

7.  Select the destination table, then drag and drop the files or click
    *Browse for files* to upload the data.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image37.png)

8.  Browse to **C:\LabFiles\Lab1** on your VM, then
    select ***FreezerTelemetry*.csv** file and click on **Open** button.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image38.png)

9.  Click on **Next** button

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image39.png)

10. Then click on the **Finish** button.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image40.png)

11. Wait for the Data ingestion to be completed, and click **Close**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image41.png)

12. The KQL database shows the **FreezerTelemetry** table when you're
    done:

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image42.png)

13. Select **Fabric IQ Ontology** in the left navigation pane.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image43.png)

# Exercise 2: Building an ontology from OneLake

## Task 1: Create ontology (preview) item

1.  In your Fabric workspace, select **+ New item**. Search for and
    select the **Ontology (preview)** item.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image44.png)

2.  Enter +++**RetailSalesOntology+++** for the **Name** of your
    ontology and select **Create**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image45.png)
>
> **Tip:** Ontology names can include numbers, letters, and
> underscores. Don't use spaces or dashes.

3.  The ontology opens when it's ready.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image46.png)
>
> Next, create entity types, data bindings, and relationships based on
> data from your lakehouse tables.

## Task 2: Create entity types and data bindings

> First, create entity types. Entity types represent types of objects in
> a business. This step has three entity types: *Store*, *Products*,
> and *SaleEvent*. After you create the entity types, create their
> properties by binding source data columns in
> the ***IQ_Lakehouse*** lakehouse tables.

### Add first entity type (Store)

1.  From the top ribbon or the center of the configuration canvas,
    select **Add entity type**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image47.png)

2.  Enter +++**Store+++ **for the name of your entity type and
    select **Add Entity Type**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image48.png)

3.  The *Store* entity type is added to the configuration canvas, and
    the **Entity type configuration** pane is visible.

> ![](./media/image49.png)

4.  On the configuration canvas, select **...** next to the entity name
    and select **Bind data**.

> ![](./media/image50.png)

5.  Select **Add data binding \> Lakehouse table**.

> ![](./media/image51.png)

6.  Next, choose your data source.Select the **IQ_Lakehouse** lakehouse
    and select **Next**.

> ![](./media/image52.png)

7.  Select the **dimstore** table and select **Select**.

![](./media/image53.png)

8.  Fields from the source table populate the data binding
    configuration. Observe the sections of the configuration page:

- **Entity type key**: Identifies the field (or fields) that can be used
  to uniquely identify each record of ingested data.

- **Binding selection**: Identifies the source table that holds the data
  for the binding.

- **Entity type key mapping**: Identifies the column(s) in the source
  data table that map to the entity type key property. You can select
  string and integer columns from your source data as the entity type
  key. Together, the columns you select uniquely identify a record.

- **Properties**: Lists the columns from the source data that will be
  represented as properties on the *Store* entity type. The **Source
  column** side populates automatically with the columns from
  the *dimstore* table, and the **Property name** side lists their
  corresponding property names on the *Store* entity type within
  ontology. For this tutorial, keep the default property names.

![](./media/image54.png)

9.  Select **Define entity type key** at the top of the configuration.

![](./media/image55.png)

10. Select **StoreId** from the property list and select **Save**.

![](./media/image56.png)

11. **Save** the data binding.

![](./media/image57.png)

![](./media/image58.png)

12. Confirm that the entity type updated successfully, then
    select **Cancel** to close the configuration options.

![](./media/image59.png)

13. You see the **Configure** page of the entity type details. This page
    surfaces important information about the entity type, including its
    properties and data bindings. View your configured data bindings.

![](./media/image60.png)

14. Select **Home** to return to the configuration canvas and add new
    entity types.

![](./media/image61.png)

### Add other entity types (Products, SaleEvent)

15. Follow the same steps that you used for the **Store **entity type to
    create the entity types described in the following table. Each
    entity has a static data binding with the default columns from its
    source table.

| Entity Type Name | Source Table in IQ_Lakehouse | Entity Type Key |
|------------------|------------------------------|-----------------|
| +++Products+++<br><br>**Note:** Use the plural form **Products** to avoid conflict with the GQL reserved word **PRODUCT**. | **dimproducts** | **ProductId** |
| +++SaleEvent+++ | **factsales** | **SaleId** |

![](./media/image62.png)

> ![](./media/image63.png)

![](./media/image64.png)

![](./media/image65.png)

![](./media/image66.png)

![](./media/image67.png)

![](./media/image68.png)

![](./media/image69.png)

![](./media/image70.png)

![](./media/image71.png)

![](./media/image72.png)

16. Select **Home** to return to the configuration canvas and add
    **SaleEvent** entity types.

![](./media/image73.png)

![](./media/image74.png)

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image75.png)
>
> ![](./media/image76.png)
>
> ![](./media/image77.png)
>
> ![](./media/image78.png)
>
> ![](./media/image79.png)
>
> ![](./media/image80.png)
>
> ![](./media/image81.png)
>
> ![](./media/image82.png)
>
> ![](./media/image83.png)
>
> ![](./media/image84.png)

17. When you're done, you see these entity types listed in the **Entity
    Types** pane.

![](./media/image85.png)

## Task 3: Create relationship types

Next, create relationship types between the entity types to represent
contextual connections in your data.

### SaleEvent from Store

1.  Select the **SaleEvent** entity type from the Explorer.

> ![](./media/image86.png)

2.  Select **Add relationship** from the menu ribbon.

> ![](./media/image87.png)

3.  Enter the following relationship type details and select **Add
    relationship type**.

- **Relationship type name**: +++from+++

- **Source entity type**: **SaleEvent**

- **Target entity type**: **Store**

> ![](./media/image88.png)
>
> ![](./media/image89.png)

4.  The relationship is added to the semantic canvas. Select it to open
    the relationship details configuration. Observe the sections of the
    configuration page:

- **Origin entity type**: Lists details of the origin entity
  (**SaleEvent** in this case).

- **Relationship type**: Sets details of the relationship type.

- **Target entity type**: Lists details of the target entity
  (**Store**in this case).

> ![](./media/image90.png)
>
> ![](./media/image91.png)

5.  In the middle section, enter the following details.

&nbsp;

1.  **Mapping table**: **Browse available sources** and select
    the **factsales** table. This table in the source data can
    link *Store* and *SaleEvent* entities together, because it contains
    identifying information for both entity types. Each row in this
    table references a store and a sale event by ID.

> ![](./media/image92.png)

2.  **Matched SaleEvent: SaleId**: Select **SaleId**. This setting
    specifies the column in the relationship source data table whose
    values match the key property defined on the *SaleEvent* entity. In
    this case, the relationship data source and the entity data source
    both use the *factsales* table, so you're selecting the same column
    (SaleId).

3.  **Matched Store: StoreId**: Select **StoreId**. This setting
    specifies the column in the relationship source data table
    (*factsales \>* StoreId) whose values match the key property defined
    on the *Store* entity (*dimstore \>* StoreId). In the tutorial data,
    the column name is the same (StoreId) in both tables.

> ![](./media/image93.png)

**Important:** Make sure to select the correct **Matched** columns that
match the entity type key properties.

6.  **Save** the relationship type. Confirm that the relationship type
    updated successfully, then select **Cancel** to close the
    configuration options.

> ![](./media/image94.png)
>
> ![](./media/image95.png)
>
> ![](./media/image96.png)
>
> Now the first relationship is created, and bound to data in your
> source table. Continue to the next section to create another
> relationship type.

### **SaleEvent sold Products**

1.  Select **Home** to return to the configuration canvas where you can
    add new entity types.

![](./media/image97.png)

2.  Follow the same steps that you used for the first relationship type
    to create a second relationship from the **SaleEvent **entity type
    that has the details described in the following table.

| Relationship Type Name | Origin Entity Type | Target Entity Type | Mapping Table | Matched SaleEvent: SaleId | Matched Products: ProductId |
|------------------------|-------------------|-------------------|---------------|--------------------------|----------------------------|
| `sold` | `SaleEvent` | `Products` | `factsales` | `SaleId` | `ProductId` |

![](./media/image98.png)

![](./media/image99.png)

![](./media/image100.png)

![](./media/image101.png)

![](./media/image102.png)

![](./media/image103.png)

![](./media/image104.png)

# Exercise 3:Enrich the ontology with additional data

In this exercise, you enrich your ontology by adding a
new ***Freezer* **entity type. This entity type adds more domain context
and introduces properties for time series data, which reflects live
operational information.

** Note**

For both static and time series data, you can create properties without
binding data and bind data later, or create properties and bind data to
them in a single step. This article demonstrates both approaches.

Finally, you create a new relationship type to represent the connection
between a store and its freezers.

## Task 1: Create Freezer entity type and add properties

Follow these steps to create the *Freezer* entity type and add
properties to it. The properties aren't bound to data yet.

1.  Select **Add entity type** from the top ribbon.
    Enter +++**Freezer*+++*** for the name of your entity type and
    select **Add Entity Type**.

> ![](./media/image105.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image106.png)

2.  With the Freezer entity type selected in the **Explorer**,
    select **View entity type details** from the top ribbon.

> ![](./media/image107.png)

3.  The **Configure** page of the entity type details opens. This page
    surfaces important information about the entity type, including its
    properties and data bindings.

Expand **Manage property bindings** and select **Add properties**.

![](./media/image108.png)

4.  Add the following properties and select **Save**.

| Name | Property Type |
|------|---------------|
| `FreezerId` | `String` |
| `Model` | `String` |
| `minSafeTempC` | `Double` |
| `StoreId` | `String` |

![](./media/image109.png)

**Note:** Property names must be unique across all entity types.

![](./media/image110.png)

5.  The properties are added to the **Configure** page, unbound to any
    data source.

> ![](./media/image111.png)

## Task 2: Bind static data to properties

Next, bind static data to the properties you created on
the *Freezer* entity type.

1.  Expand **Manage property bindings** and select **Add binding and
    properties**.

> ![](./media/image112.png)

2.  Select **Add data binding \> Lakehouse table**.

> ![](./media/image113.png)

3.  Choose your data source.

- Select the **IQ_Lakehouse** lakehouse and select **Next**.

- Select the **freezer** table and **Select**.

> ![](./media/image114.png)
>
> ![](./media/image115.png)

4.  Fields from the source table populate the data binding
    configuration. Observe the sections of the configuration page:

- **Entity type key**: Identifies the field (or fields) that can be used
  to uniquely identify each record of ingested data.

- **Binding selection**: Identifies the source table that holds the data
  for the binding.

- **Entity type key mapping**: Identifies the column(s) in the source
  data table that map to the entity type key property. You can select
  string and integer columns from your source data as the entity type
  key. Together, the columns you select uniquely identify a record.

- **Properties**: Lists the columns from the source data and
  corresponding properties on the **Freezer** entity type. The **Source
  column** side populates automatically with the columns from
  the **freezer** table, and the **Property name** side lists their
  corresponding property names on the **Freezer** entity type within
  ontology. For this tutorial, keep the default property names.

![](./media/image116.png)

5.  Select **Define entity type key** at the top of the configuration.
    Select FreezerId from the property list and select **Save**.

![](./media/image117.png)

![](./media/image118.png)

6.  **Save** the data binding. Confirm that the entity type updated
    successfully, then select **Cancel** to close the configuration
    options.

![](./media/image119.png)

![](./media/image120.png)

## Task 3: Bind time series data to additional properties

Next, add time series data on the **Freezer **entity, by creating new
properties and binding time series data to them in a single data binding
operation.

1.  In the **Configure** page, expand **Manage property bindings** and
    select **Add binding and properties** again to reopen the binding
    configuration.

![](./media/image121.png)

2.  Under **Binding selection**, expand **Add data binding** and
    select **Eventhouse table or materialized view**.

![](./media/image122.png)

3.  Choose your data source.

    1.  Select the **TelemetryDataEH **eventhouse and select **Add**.

![](./media/image123.png)

4.  Select the **FreezerTelemetry **table and **Add**.

![](./media/image124.png)

5.  A **Timeseries data** section appears in the configuration.
    For **Timestamp column**, select timestamp

![](./media/image125.png)

6.  Scroll down to the **Properties** section, where
    the **StoreId **shows an error because it is already bound in the
    static data binding. Use the trash icon to delete the duplicated
    property.

![](./media/image126.png)

7.  **Save** the data binding. Confirm that the entity type updated
    successfully, then select **Cancel** to close the configuration
    options.

![](./media/image127.png)

![](./media/image128.png)

8.  Back in the **Configure** page for *Freezer*, notice that there are
    now more entity type properties, and the new ones are bound to
    the *FreezerTelemetry* data source.

![](./media/image129.png)

Now the *Freezer* entity has two data bindings: one with static data
from the *freezer* lakehouse table and one with streaming data from
the *FreezerTelemetry* eventhouse table.

## Task 4: Add relationship type

Finally, create a new relationship type to represent the connection
between a store and its freezers.

**Create Store operates Freezer**

1.  In the **Configure** page, expand Manage relationships and select
    **Add new relationship**.

![](./media/image130.png)

2.  Enter the following relationship type details and select **Add
    relationship type**.

    1.  **Relationship type name**: **operates**

    2.  **Source entity type**: **Store**

    3.  **Target entity type**: **Freezer**

![](./media/image131.png)

3.  The relationship is added to the **Relationships** section. Select
    the **operates** relationship on the canvas to open the relationship
    details configuration. Observe the sections of the configuration
    page:

- **Origin entity type**: Lists details of the origin entity (*Store* in
  this case).

- **Relationship type**: Sets details of the relationship type.

- **Target entity type**: Lists details of the target entity
  (**Freezer** in this case).

![](./media/image132.png)

![](./media/image133.png)

4.  In the middle section, enter the following details.

- **Mapping table**: Select the **freezer** table. This table in the
  source data can link **Store** and **Freezer** entities together, because
  it contains identifying information for both entity types. Each row in
  this table references a store and a freezer by ID.

- **Matched Store: StoreId**: Select **StoreId**. This setting specifies
  the column in the relationship source data table (*freezer
  \>* StoreId) whose values match the key property defined on
  the *Store* entity (*dimstore \>* StoreId). In the tutorial data, the
  column name is the same (StoreId) in both tables.

- **Matched Freezer: FreezerId**: Select **FreezerId.** This setting
  specifies the column in the relationship source data table whose
  values match the key property defined on the *Freezer* entity. In this
  case, the relationship data source and the entity data source both use
  the *freezer* table, so you're selecting the same column (FreezerId).

![](./media/image134.png)

**Important:** Make sure to select the correct source columns that match
the entity type key properties.

5.  **Save** the relationship type. Confirm that the relationship type
    updated successfully, then select **Cancel** to close the
    configuration options.

![](./media/image135.png)

![](./media/image136.png)

6.  You see the **Configure** page for the entity, where the updated
    relationship remains visible in the **Relationships** section.

![](./media/image137.png)

# Exercise 4: **View the ontology**

In this exercise, explore your ontology by using the preview experience.
Inspect entity instances that instantiate your entity types with data,
and explore graph-shaped context across sales and device streaming data.

## Task 1: **View instance list and static data**

When you bound data to your entity types in previous tutorial steps,
ontology automatically created instances of those entities that are tied
to the source data rows. In this section, you use the preview experience
to view those entity instances.

1.  Start in the Home configuration canvas of ontology. Select
    the **SaleEvent **entity type, and **View Entity Type details** from
    the top ribbon.

![](./media/image138.png)

2.  Open the **Instances** tab. Verify that it shows six entity
    instances with data populated from the **factsales **lakehouse
    table, like revenue and unit counts.

![](./media/image139.png)

## Task 2: View time series data

1.  In the top left corner of the page, use the selector next to the
    entity type name to switch to the **Freezer** entity type.

![](./media/image140.png)

2.  Open the **Overview** tab. The tab loads with empty charts, because
    the default time range of **Last 30 days** doesn't include any data.

![](./media/image141.png)

3.  Update the time range from the default of **Last 30 days** to a
    custom date range that begins on **Fri Aug 01 2025 at 12:00 AM,**
    ends on **Mon Aug 04 2025** *at* **12:00 AM**, and has a **Time
    granularity** of **5 minutes**.

![](./media/image142.png)

4.  Observe the time series data that's now visible from
    several **Freezer **entity instances in the time window you
    selected.

![](./media/image143.png)

## Task 3: **View ontology graph**

The **Overview** tab also contains a **Relationship graph**, which you
use to visualize your ontology in a graph of nodes and edges.

1.  Use the entity type selector to switch to the **SaleEvent** entity
    type. In the **Relationship graph** tile, select **Expand**.

> ![](./media/image144.png)

2.  he expanded graph view opens. Observe the details of the
    relationships from the **SaleEvent **entity type
    to **Products** and **Store.**

![](./media/image145.png)

3.  Use the entity type selector to switch to the **Store **entity type.
    **Expand** its **relationship graph.**

![](./media/image146.png)

4.  In the graph, observe the relationships that **Store** has
    with **Freezer **and **SaleEvent**. Then, select **Run query** in
    the query builder ribbon. This action runs the default query and
    shows a graph of entity instances alongside their connections

![](./media/image147.png)

![](./media/image148.png)

![](./media/image149.png)

## Task 4: Query graph instances

In the relationship graph view, you can query your ontology for entity
instances that meet certain criteria. Use the **Query builder** filters
in the top ribbon to craft queries.

![](./media/image150.png)

First, craft this query: **Show all freezers that are operated in the
Paris store.**

1.  In the *Store* entity's relationship graph, select **Add filter \>
    Store \> StoreId** from the query builder ribbon. Set the filter
    for **StoreId = S-PAR-01**. This value is the store ID for the Paris
    store.

![](./media/image151.png)

![](./media/imga2.png)

5.  In the **Components** section, uncheck *SaleEvent* so that the only
    checked fields are **Nodes \> Store**, **Nodes \> Freezer**,
    and **Edges \> operates**.

![](./media/image153.png)

6.  Select **Run query** and verify that the instance graph shows two
    freezers connected to the **Paris** store.

![](./media/image154.png)

![](./media/image155.png)

7.  Select **Clear query** to clear the query results.

![](./media/image156.png)

Next, craft this query: *Show all stores that have made a sale with a
revenue greater than 150.*

8.  Select **Add a node** and add a node for **SaleEvent.**

> ![](./media/image157.png)

9.  In the **Components** section, check the boxes next to **Nodes \>
    Store** and **Edges \> from** to add them to the graph.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/imga3.png)

10. From the query builder ribbon, select **Add filter \> SaleEvent \>
    RevenueUSD**. Set the filter for +++**RevenueUSD \> 150+++.**

![](./media/image159.png)

![](./media/image160.png)

11. Select **Run query** and verify that the instance graph shows two
    stores that meet the filter for their connected sale events. You can
    also select the nodes in the graph to get details of the specific
    sale events

![](./media/image161.png)

![](./media/image162.png)

This process allows you to inspect the paths that connect operational
issues (like rising freezer temperature at certain stores) to business
outcomes (sales).

# Exercise 5: **Consume ontology from agents**

Ontology (preview) integrates with [Fabric data agent
(preview)](https://learn.microsoft.com/en-us/fabric/data-science/concept-data-agent) to
let you ask questions in natural language, and get answers grounded in
the ontology's definitions and bindings.

## Task 1:Create data agent with ontology (preview) source

Follow these steps to create a new data agent that connects to your
ontology (preview) item.

1.  Now, click on **Fabric IQ Ontology XX** on the left-sided navigation
    pane.

![](./media/image163.png)

2.  In the **Fabric** home page, select **+New item.** In the Filter by
    item type search box, enter +++**data agent**+++ and select the Data
    agent

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image164.png)

3.  Enter **+++RetailOntologyAgent+++** as the Data agent name and
    select **Create**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image165.png)

4.  In **RetailOntologyAgent** page, select **Add a data source**

> ![](./media/image166.png)

5.  In the OneLake catalog tab, select the **RetailSalesOntology**
    Ontology and select **Add.**

> ![](./media/image167.png)
>
> When the agent is ready, it opens.
>
> ![](./media/image168.png)

## Task 2: Provide agent instructions

** Note:** This step is added in response to a known issue affecting
aggregation in queries.

> Next, add a custom instruction to the agent.

1.  Select **Agent instructions** from the menu ribbon.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image169.png)

2.  At the bottom of the input box, add +++**Support group by in
    GQL**+++. This instruction enables better aggregation across
    ontology data.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image170.png)

3.  The instruction is applied automatically. Optionally, close
    the **Agent instructions** tab.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image171.png)

## Task 3: Query agent with natural language

> Next, explore your ontology with natural language questions.

1.  Enter the following text and click on the **Submit icon** as shown
    in the below image.

> **+++For each store, show any freezers operated by that store that
> ever had a humidity lower than 46 percent.+++**
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image172.png)

![A screenshot of a chat AI-generated content may be
incorrect.](./media/image173.png)

2.  Enter the following text and click on the **Submit icon** as shown
    in the below image.

> **+++What is the top product by revenue across all stores?+++**

![A screenshot of a chat AI-generated content may be
incorrect.](./media/image174.png)

![A screenshot of a chat AI-generated content may be
incorrect.](./media/image175.png)

> Notice that the responses reference entity types
> (**Store**, **Products**, **Freezer**) and their relationships, not just raw
> tables.
>
> ![Screenshot of the result of a query.](./media/image176.png)
>
> **Tip:** If you see errors that say there's no data while running the
> example queries, wait a few minutes to give the agent more time to
> initialize. Then, run the queries again.
>
> Continue exploring the data agent by trying out some prompts of your
> own.

## Task 4: Clean up resources

1.  Select your workspace, the **Fabric IQ OntologyXX** from the
    left-hand navigation menu. It opens the workspace item view.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image177.png)

2.  Select the ... option under the workspace name and select
    **Workspace settings**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image178.png)

3.  Navigate to the bottom of the General tab and select **Remove this
    workspace**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image179.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image180.png)

**Summary**

This use case demonstrates how Microsoft Fabric IQ Ontology (preview)
can be used to create a connected, semantic data model that represents
real-world business concepts and their relationships. By combining
structured lakehouse data with streaming telemetry data, the ontology
provides a unified, business-friendly view of enterprise data.

Through entity definitions, data bindings, and relationship modeling,
users can analyze how operational signals—such as freezer temperature or
humidity—relate to business outcomes like sales and revenue. The use
case also highlights how ontologies power graph exploration and natural
language queries through Fabric data agents, enabling deeper insights
without requiring users to understand underlying tables or schemas.

Overall, this use case shows how Fabric IQ Ontology helps bridge
operational data and analytics, supporting smarter decision-making
across domains.
