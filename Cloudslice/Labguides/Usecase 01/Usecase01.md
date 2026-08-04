# Usecase 1: Implement a data engineering solution for moving and transforming data with Fabric Data Factory

**Scenario**

**Wide World Importers (WWI)** is a global retail organization that
operates hundreds of stores across multiple regions. Customer
information is collected from various operational systems, including
point-of-sale (POS) applications, CRM platforms, and e-commerce
channels. The data is stored as CSV files and is received daily from
different business units.

The company's analytics team currently spends significant time manually
importing files, validating data quality, and preparing datasets for
reporting. These manual processes lead to delays in generating customer
insights and make it difficult for business users to access consistent
and reliable information.

To modernize its analytics platform, Wide World Importers has adopted
**Microsoft Fabric** as its unified data platform. The data engineering
team has been tasked with implementing a scalable solution using
**Microsoft Fabric Data Factory** and **Lakehouse** to centralize
customer data, enable efficient data management, and simplify reporting.

As a Data Engineer, your responsibility is to create a Fabric workspace,
provision a Lakehouse, ingest customer data into OneLake, convert the
source files into managed Delta tables, validate the imported data using
SQL Analytics Endpoint, create a Direct Lake semantic model, and
generate a Power BI report that enables business stakeholders to analyze
customer information with minimal latency.

By implementing this solution, Wide World Importers can eliminate manual
data preparation, provide a single source of truth for customer
analytics, and enable faster, data-driven business decisions using
Microsoft Fabric.

**Introduction**

In this usecase, you will build a complete data engineering solution by
using **Microsoft Fabric Data Factory** and **Fabric Lakehouse**.
Starting with a new Fabric workspace, you will ingest data into a
Lakehouse, convert files into managed Delta tables, query the data using
SQL analytics endpoints, create semantic models, and generate
interactive Power BI reports.

Throughout the lab, you will explore how Microsoft Fabric unifies data
integration, storage, transformation, analytics, and reporting into a
single Software-as-a-Service (SaaS) platform. By completing this
hands-on exercise, you will understand how modern data engineering
workflows are implemented using Fabric Data Factory while following
industry best practices for data ingestion, management, and analytics.

**Objectives**:

- Create and configure a Microsoft Fabric workspace.

- Build and configure a Fabric Lakehouse.

- Ingest source data into OneLake.

- Load files into managed Delta tables.

- Query Lakehouse data using the SQL Analytics Endpoint.

- Create a Direct Lake semantic model.

- Generate and explore Power BI reports from Fabric data.

- Understand how Fabric Data Factory integrates data engineering and
  analytics into a unified platform.

## Exercise 1: Set Up the Microsoft Fabric Data Engineering Environment 

Before building a data engineering solution, you need to prepare the
Microsoft Fabric environment. In this exercise, you will sign in to
Microsoft Fabric, create a dedicated workspace, and provision a
Lakehouse that will serve as the centralized storage for your analytics
solution.

### Task 1: Sign in to Power BI account

1.  Open your browser, navigate to the address bar, and type or paste
    the following URL:!!https://app.fabric.microsoft.com/!! then press
    the **Enter** button.

![](./media/image1.png)

2.  In the **Microsoft Fabric** window, enter your credentials, and
    click on the **Submit** button.

| Credential | Value |
|---|---|
| Username | +++@lab.CloudPortalCredential(User1).Username+++ |
| Password | +++@lab.CloudPortalCredential(User1).Password+++ |

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image2.png)

3.  Then, In the **Microsoft** window enter the password and click on
    the **Sign in** button.

> ![A login screen with a red box and blue text AI-generated content may
> be incorrect.](./media/image3.png)

4.  In **Stay signed in?** window, click on the **Yes** button.

5.  You’ll be directed to Power BI Home page.

> ![](./media/image4.png)

6.  Select the default Power BI icon at the bottom left of the screen,
    and select **Fabric**.

> ![](./media/image5.png)
>
> ![](./media/image6.png)

### Task 2: Create a Fabric workspace

In this task, you create a Fabric workspace. The workspace contains all
the items needed for this lakehouse tutorial, which includes lakehouse,
dataflows, Data Factory pipelines, the notebooks, Power BI datasets, and
reports.

1.  Fabric home page, select **+New workspace** tile.

![](./media/image7.png)

2.  In the **Create a workspace** pane that appears on the right side,
    enter the following details, and click on the **Apply** button.

| Property | Value |
|---|---|
| Name | !!Fabric Dataengineering-DataFactoryXXXXXX!! |
| Advanced | Under License mode, select Fabric |
| Default storage format | Small dataset storage format |

![](./media/image8.png)

Note: To find your lab instant ID, select 'Help' and copy the instant
ID.

![A screenshot of a computer Description automatically
generated](./media/image9.png)

![](./media/image10.png)

![](./media/image11.png)

3.  Wait for the deployment to complete. It takes 2-3 minutes to
    complete.

![](./media/image12.png)

### Task 3: Create a lakehouse

1.  Create a new lakehouse by clicking on the **+New item** button in
    the navigation bar.

![](./media/image13.png)

2.  Click on the "**Lakehouse**" tile.

![](./media/image14.png)

3.  In the **New lakehouse** dialog box, enter **!!wwilakehouse!!** in
    the **Name** field and **unselect** the lakehouses schemas. Click on
    the **Create** button and open the new lakehouse.

**Note**: Ensure to remove space before **wwilakehouse**.

![](./media/image15.png)

4.  You will see a notification stating **Successfully created SQL
    endpoint**.

![](./media/image16.png)

### Task 4: **Ingest sample data**

1.  In the **wwilakehouse** page, navigate to **Get data in your
    lakehouse** section, and click on **Upload files** as shown in the
    below image.

![](./media/image17.png)

2.  On the Upload files tab, click on the folder under the Files

![](./media/image18.png)

3.  Browse to **C:\LabFiles** on your VM, then
    select **dimension_customer.csv** file and click on **Open** button.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image19.png)

4.  Then, click on the **Upload** button and close

![](./media/image20.png)

5.  **Close** the Upload files pane.

![](./media/image21.png)

6.  Click and select refresh on the **Files**. The file appears.

![](./media/image22.png)

7.  In the **Lakehouse** page, Under the Explorer pane select Files.
    Now, however your mouse to **dimension_customer.csv** file. Click on
    the horizontal ellipses **(…)** beside **dimension_customer**.csv.
    Navigate and click on **Load Table**, then select **New table**.

![](./media/image23.png)

> ![](./media/image24.png)

8.  In the **Load file to new table** dialog box, click on
    the **Load** button.

![](./media/image25.png)

9.  Now **dimension_customer** table is successfully created.

![](./media/image26.png)

10. Select **dimension_customer** table under the Tables.

![](./media/image27.png)

11. You can also use the SQL endpoint of the lakehouse to query the data
    with SQL statements. Select **SQL analytics endpoint** from
    the **Analyze data with** drop-down menu at the top right of the
    screen.

![](./media/image28.png)

12. In the **wwilakehouse** page, under Explorer select
    the **dimension_customer** table to preview its data and
    select **New SQL query** to write your SQL statements.

![](./media/image29.png)

13. The following sample query aggregates the row count based on
    the **BuyingGroup column** of the **dimension_customer** table. SQL
    query files are saved automatically for future reference, and you
    can rename or delete these files based on your need. Paste the code
    as shown in the below image, then click on the play icon
    to **Run** the script:
```
SELECT BuyingGroup, Count(*) AS Total
FROM dimension_customer
GROUP BY BuyingGroup
```

![](./media/image30.png)

**Note**: If you encounter an error during the execution of the script,
then crosscheck the script syntax that it should not have any
unnecessary spaces.

14. Previously all the lakehouse tables and views were automatically
    added to the semantic model. With the recent updates, for new
    lakehouses, you have to manually add your tables to the semantic
    model.

15. From the lakehouse **Home** tab, select **New semantic model** and
    select the tables that you want to add to the semantic model.

> ![](./media/image31.png)

16. In the **New semantic model** dialog enter
    !!**wwwsemanticmodel**!! and then select
    the **dimension_customer** table from the list of tables and
    select **Confirm** to create the new model.

![](./media/image32.png)

### Task 5: Build a report

1.  In the left navigation pane, select **Fabric
    Dataengineering-DataFactory-XX**.

![](./media/image33.png)

2.  In your workspace, find the semantic model you created, select
    the **...** (ellipsis) menu, and then select **Auto-create report**.

![](./media/image34.png)

![](./media/image35.png)

4.  Now that the report is ready, click on **View report now** to open
    and review it.

> ![](./media/image36.png)

![](./media/image37.png)

5.  Since the table is a dimension and there are no measures in it,
    Power BI creates a measure for the row count and aggregates it
    across different columns, and creates different charts as shown in
    the following image.

6.  Save this report for the future by selecting **Save** from the top
    ribbon.

![](./media/image38.png)

7.  In the **Save your report** dialog box, enter a name for your report
    as !!dimension_customer-report!! and select **Save.**

![](./media/image39.png)

8.  You will see a notification stating **Report saved**.

![](./media/image40.png)

## Exercise 2:Ingest and Manage Data in the Fabric Lakehouse

In this exercise, you ingest additional dimensional and fact tables from
the Wide World Importers (WWI) into the lakehouse.

### Task 1: Ingest data

1.  In the left navigation pane, select **Fabric
    Dataengineering-DataFactory-XX**.

![](./media/image41.png)

2.  In the **Fabric Dataengineering-DataFactory-XX** workspace page,
    navigate and click on **+New item** button, then
    select **Pipeline**.

![](./media/image42.png)

3.  In the New pipeline dialog box, specify the name
    as **!!IngestDataFromSourceToLakehouse!!** and
    select **Create.** A new data factory pipeline is created and
    opened.

![](./media/image43.png)

![](./media/image44.png)

4.  From your new pipeline's **Home** tab, select **Pipeline
    activity** \> **Copy data**.

![](./media/image45.png)

5.  Select the new **Copy data** activity from the canvas. Activity
    properties appear in a pane below the canvas, organized across tabs
    including **General**, **Source**, **Destination**, **Mapping**,
    and **Settings**. You might need to expand the pane upwards by
    dragging the top edge.

![](./media/image46.png)

6.  On the **General** tab, enter !!**Data Copy to Lakehouse!!** in
    the **Name** field. Leave the other fields with their default
    values.

![](./media/image47.png)

7.  On the **Source** tab, select the **Connection** dropdown and then
    select **Browse all**.

![](./media/image48.png)

8.  In the **Choose a data source to get started** page, search for and
    select **Azure blobs**.

![](./media/image49.png)

9.  Enter the following details in the **Connect data source** page.
    Then select **Connect** to create the connection to the data source.
    For this tutorial, all the sample data is available in a public
    container of Azure blob storage. You connect to this container to
    copy data from it.

| Property | Value |
|---|---|
| Account name or URL | !!https://fabrictutorialdata.blob.core.windows.net/sampledata/!! |
| Connection | Create new connection |
| Connection name | !!wwisampledata!! |
| Authentication kind | Anonymous |

![](./media/image50.png)

10. On the **Source** tab, the newly created connection is selected by
    default. Specify the following properties before moving to the
    destination settings.

| Property | Value |
|---|---|
| Connection | wwisampledata |
| File path type | File path |
| File path | Container name (first text box): !!sampledata!!<br>Directory name (second text box): !!WideWorldImportersDW/parquet!! |
| Recursively | Checked |
| File format | Binary |

![](./media/image51.png)

11. On the **Destination** tab, specify the following properties:

| Property | Value |
|---|---|
| Connection | wwilakehouse (choose your lakehouse if you named it differently) |
| Root folder | Files |
| File path | Directory name (first text box): !!wwi-raw-data!! |
| File format | Binary |

![](./media/image52.png)

12. Click on **Run** to run the copy data.

![](./media/image53.png)

13. Click on **Save and run** button so that pipeline will be save and
    run.

> ![](./media/image54.png)

14. The data copy process takes approximately 1-2 minutes to complete.

![](./media/image55.png)

15. Under the Output tab, select **Data Copy to Lakehouse** to look at
    the details of the data transfer. After seeing
    the **Status** as **Succeeded**, click on the **Close** button.

![](./media/image56.png)

![](./media/image57.png)

16. After the successful execution of the pipeline, go to your lakehouse
    (**wwilakehouse**) and open the explorer to see the imported data.

![](./media/image58.png)

17. Refresh the **Files** section to see the ingested data. A new
    folder **wwi-raw-data** appears in the files section, and data from
    Azure Blob tables is copied there.
    ![](./media/image59.png)

## Exercise 3: Prepare and transform data in the lakehouse

### Task 1: Transform data and load to silver Delta table

1.  In the left navigation pane, select **Fabric
    Dataengineering-DataFactory-XX**.

![](./media/image60.png)

2.  In the **Fabric** page, navigate and click on **Import** drop in the
    command bar, then select **New notebook\> From this computer**.

![](./media/image61.png)

3.  Select **Upload** from the **Import status** pane that opens on the
    right side of the screen.

> ![](./media/image62.png)

4.  Browse to **C:\LabFiles** on your VM, then select **Prepare and
    transform data – PySpark** notebook and click on **Open** button.

> ![](./media/image63.png)
>
> ![](./media/image64.png)

5.  Select the **wwilakehouse** lakehouse to open it, so that the
    notebook you open next is linked to it.

![](./media/image65.png)

6.  From the toolbar, select the **Analyze data** with drop-down menu,
    point to **Notebook**, and then select **Existing notebook**.

> ![](./media/image66.png)

7.  Select the imported notebook, **Prepare and transform data –
    PySpark**, and then click **Open.**

> ![](./media/image67.png)
>
> ![](./media/image68.png)

### Task 2: Create Delta tables

> In this task, you run the notebook cells to create Delta tables from
> the raw data.
>
> The tables follow a star schema, which is a common pattern for
> organizing analytical data:

- A **fact table** (fact_sale) contains the measurable events of the
  business — in this case, individual sales transactions with
  quantities, prices, and profit.

- **Dimension
  tables** (dimension_city, dimension_customer, dimension_date, dimension_employee, dimension_stock_item)
  contain the descriptive attributes that give context to the facts,
  such as where a sale happened, who made it, and when.

1.  **Cell 1 - Spark session configuration.** This cell enables two
    Fabric features that optimize how data is written and read in
    subsequent
    cells. [V-order](https://learn.microsoft.com/en-us/fabric/data-engineering/delta-optimization-and-v-order) optimizes
    the parquet file layout for faster reads and better
    compression. [Optimize
    write](https://learn.microsoft.com/en-us/fabric/data-engineering/tune-file-size#optimize-write) reduces
    the number of files written and increases individual file size.
```
spark.conf.set("spark.sql.parquet.vorder.enabled", "true")
spark.conf.set("spark.microsoft.delta.optimizeWrite.enabled", "true")
spark.conf.set("spark.microsoft.delta.optimizeWrite.binSize", "1073741824")
```

2.  **Run** this cell, and wait for it to finish before moving on to the
    next step.

> ![](./media/image69.png)
>
> ![](./media/image70.png)

3.  **Cell 2 - Fact - Sale.** This cell reads raw parquet data
    from Files/wwi-raw-data/full/fact_sale_1y_full, adds date part
    columns (**Year**, **Quarter**, and **Month**), and
    writes fact_sale as a Delta table partitioned
    by **Year** and **Quarter**.

4.  Run this cell, and wait for it to finish before moving on to the
    next step.

> ![](./media/image71.png)

5.  **Cell 3** - Dimensions. This cell reads the five dimension parquet
    datasets and writes them as Delta tables
    (dimension_city, dimension_customer, dimension_date, dimension_employee,
    and dimension_stock_item) under Tables/dbo/....

6.  **Run** this cell, and wait for it to finish before moving on to the
    next step.

> ![](./media/image72.png)

7.  To validate the created tables, right-click
    the **wwilakehouse** lakehouse in the explorer and then
    select **Refresh**. The tables appear.

> ![](./media/image73.png)
>
> ![](./media/image74.png)

### Task 3: Transforming Business Data for Aggregation

In task, you continue in the same notebook and run the next cells to
create aggregate tables from the Delta tables you created in the
previous section.

1.  Make sure the notebook is still linked to **wwilakehouse**.

2.  **Cell 4 - Load source tables for transformation (PySpark
    only).** If you're using the PySpark notebook, run this cell to load
    Delta tables into DataFrames for the aggregation steps that follow.

3.  Run this cell, and wait for it to finish before moving on to the
    next step.

![](./media/image75.png)

4.  **Cell 5 - Create aggregate_sale_by_date_city.** This cell joins
    sales, date, and city data, then creates the city-level aggregate
    table.

5.  Run this cell, and wait for it to finish before moving on to the
    next step.

> ![](./media/image76.png)

6.  **Cell 6 - Create aggregate_sale_by_date_employee.** This cell joins
    sales, date, and employee data, then creates the employee-level
    aggregate table.

7.  Run this cell, and wait for it to finish before moving on to the
    next step.

> ![](./media/image77.png)

8.  To validate the created tables, right-click
    the **wwilakehouse** lakehouse in the explorer and then
    select **Refresh**. The aggregate tables appear.

> ![](./media/image78.png)
>
> ![](./media/image79.png)

## Exercise 4: Transform Data with a Dataflow in Data Factory

### Task 1: Get Data from the Bronze Lakehouse Table

1.  From the left navigation pane, click on the workspace name **Fabric
    Dataengineering-DataFactory-@lab.LabInstance.Id** to return to the
    workspace view.

![](./media/image80.png)

2.  Click **+New item** in the navigation bar. From the list of
    available items select **Dataflow Gen2.**

![](./media/image81.png)

3.  In the Name field, enter !!**wwi_fact_sale_transform**!!, and then
    select **Create.**

![](./media/image82.png)

4.  From the new dataflow menu, under the Power Query pane click on
    **Get data** dropdown, then select **More**...

![](./media/image83.png)

5.  In the Choose data source tab, search for !!**Lakehouse**!! and
    click on the **Lakehouse** connector.

![](./media/image84.png)

6.  The Connect to data source dialog appears. A new connection is
    automatically created based on your signed-in user. Select **Next**.

![](./media/image85.png)

7.  The Choose data dialog is displayed. Expand workspace **Fabric
    Dataengineering-DataFactory** -@lab.LabInstance.Id, then expand
    Lakehouse - **wwilakehouse**, and select the fact_sale table from
    the list. Click **Create**.

![](./media/image86.png)

![](./media/image87.png)

8.  You will see that the canvas is now populated with the **fact_sale**
    data.

![](./media/image88.png)

### Task 2: Transform the Data Imported from the Lakehouse

1.  Select the data type icon in the column header of the
    **InvoiceDateKey** column to display a dropdown menu. Select the
    data type from the menu to convert the column from **Date/Time** to
    **Date** type.

![](./media/image89.png)

2.  On the **Home** tab of the ribbon, select the Choose columns option
    from the **Manage columns** group and select **Choose columns**

![](./media/image90.png)

3.  In the Choose columns dialog, deselect the **TaxRate** columns, then
    select **OK:**

> ![](./media/image91.png)

4.  Select the I**nvoiceDateKey** column sort and filter dropdown menu,
    then select Date filters, and choose the **Between...** filter.

![](./media/image92.png)

5.  In the Filter rows dialog, select dates between January 1, 2000 and
    January 31, 2000, then select OK.

![](./media/image93.png)

![](./media/image94.png)

###  Task 3: Connect to the dimension_city Table

Instead of a CSV file, you will load the **dimension_city** table that
is already in **wwilakehouse** from Usecase 01 to enrich the fact_sale
data with city and sales territory information.

1.  From the **Home** tab in the dataflow editor menu, select the **Get
    data** option, then choose **More...**

![](./media/image95.png)

2.  In the Choose data source tab, search for !!Lakehouse!! and click
    on the Lakehouse connector.

![](./media/image96.png)

3.  The Connect to data source dialog appears. A new connection is
    automatically created. Select **Next**.

![](./media/image97.png)

4.  The Choose data dialog is displayed. Expand workspace **Fabric
    Dataengineering-DataFactory-**@lab.LabInstance.Id, then expand
    Lakehouse - **wwilakehouse**, and select the **dimension_city**
    table. Click Create.

![](./media/image98.png)

5.  You will now see a second query — **dimension_city** — in the Power
    Query editor.

![](./media/image99.png)

###  Task 4: Transform the dimension_city Data

1.  Make sure the **dimension_city** query is selected in the Queries
    pane.

2.  On the Home tab of the ribbon, select Choose columns from the Manage
    columns group.

> ![](./media/image100.png)

3.  In the Choose columns dialog, keep only the following columns
    (deselect all others), then click **OK**:

- CityKey

- City

- StateProvince

- SalesTerritory

![](./media/image101.png)

4.  Select the **SalesTerritory** column's filter and sort dropdown.
    Deselect (blank) or (null) entries to remove rows without a
    territory. Then click OK.

![](./media/image102.png)

![](./media/image103.png)

###  Task 5: Combine fact_sale and dimension_city Data

The next step is to combine both tables into a single table that
includes city and territory context for each sale, and adds a calculated
profit margin column.

1.  First, toggle the Diagram view button so you can see both of your
    queries.

![](./media/image104.png)

2.  Select the **fact_sale** query. On the Home tab, select the
    **Combine** menu and choose **Merge queries**, then **Merge queries
    as new**.

![](./media/image105.png)

3.  In the Merge dialog box, select **dimension_city** as the right
    table, accept the suggested mapping of **CityKey** to **CityKey**,
    ensure Left outer is selected as the join kind, and then click OK.

![](./media/image106.png)

![](./media/image107.png)

![](./media/image108.png)

4.  Expand the **dimension_city** column, clear the **CityKey**
    checkbox, keep the remaining columns selected, and then click
    **OK**.

![](./media/image109.png)

![](./media/image110.png)

5.  To add a calculated column: select the **Add column** tab at the top
    of the editor, and choose **Custom column** from the General group.

![](./media/image111.png)

6.  In the Custom column dialog, configure the new column as
    follows**:**

| Property | Value |
|---|---|
| New column name | !!ProfitMargin!! |
| Data type | Currency |
| Custom column formula | !!if [TotalIncludingTax] > 0 then [Profit] / [TotalIncludingTax] else 0!! |

Then select **OK**.

![](./media/image112.png)

![](./media/image113.png)

7.  Select the newly created **ProfitMargin** column. Then select the
    Transform tab at the top of the editor window. On the Number column
    group, select the **Rounding** dropdown and then choose Round...

![](./media/image114.png)

8.  On the Round dialog, enter 4 for the number of decimal places and
    then click OK.

![](./media/image115.png)

![](./media/image116.png)

9.  Change the data type of the **InvoiceDateKey** column back from Date
    to **Date/Time.**

![](./media/image117.png)

![](./media/image118.png)

10. Finally, expand the Query settings pane from the right side of the
    editor and rename the query from Merge to !!Output!!.

![](./media/image119.png)

Note: ProfitMargin = Profit / TotalIncludingTax. A value of 0.35 means 35% profit margin on that sale. Rounded to 4 decimal places for reporting precision.

### Task 6: Load the Output Query to a Gold Table in the Lakehouse

With the Output query fully prepared, define the output destination.

1.  Select the **Output** merge query created previously. Then select
    the **+ icon** to add a data destination to this Dataflow.

2.  From the data destination list, select the Lakehouse option under
    New destination.

![](./media/image120.png)

3.  On the Connect to data destination dialog, your connection should
    already be selected. Select **Next** to continue.

![](./media/image121.png)

4.  Under Choose destination target, select New table, browse to
    **wwilakehouse** under the **Fabric Dataengineering-DataFactory-XX**
    workspace, enter !!**Gold_Sales_By_City!!** as the table name, and
    then click **Next**.

![](./media/image122.png)

5.  Click **Save settings**

![](./media/image123.png)

6.  Back in the main editor window, confirm that the Query settings pane
    shows Lakehouse as the output destination for the Output table.

![](./media/image124.png)

7.  Select **Save and Run** from the Home tab.

![](./media/image125.png)

8.  Wait for the dataflow run to complete (approximately 2-3 minutes).

![](./media/image126.png)

9.  Navigate back to wwilakehouse and click Refresh on the Tables
    section. Confirm that the Gold_Sales_By_City table now appears under
    Tables in the Explorer pane.

![](./media/image127.png)

![](./media/image128.png)

![](./media/image129.png)

10. Click on the **Gold_Sales_By_City** table to preview it and verify
    it contains City, StateProvince, SalesTerritory, Profit,
    TotalIncludingTax, and ProfitMargin columns.

![](./media/image130.png)

## Exercise 5: Automate and Send Notifications with Data Factory

### Task 1: Add an Office 365 Outlook Activity to Your Pipeline

1.  Navigate and click on **Fabric
    Dataengineering-DataFactory-**@lab.LabInstance.Id Workspace on the
    left-sided navigation menu.

2.  On the workspace page and select **Pipeline**.

![](./media/image131.png)

3.  Select the **Activities** tab in the pipeline editor and find the
    **Office Outlook** activity.

![](./media/image132.png)

4.  Select and drag the On Success path (a green checkbox on the top
    right side of the Copy activity) from your Copy activity to your new
    Office 365 Outlook activity.

![](./media/image133.png)

5.  Select the Office 365 Outlook activity from the pipeline canvas,
    then select the Settings tab of the property area below the canvas.
    Click on the Connection dropdown and select Browse all.

![](./media/image134.png)

6.  On the choose a data source window, select **Office 365 Email**
    source.

> ![](./media/image135.png)

7.  Sign in with the account from which you want to send the email. You
    can use the existing connection with the already signed in account.

8.  Click on **Connect** to proceed.

![](./media/image136.png)

9.  Select the Office 365 Outlook activity from the pipeline canvas. On
    the Settings tab of the property area below the canvas, configure
    the email.

10. Enter your email address in the To section. If you want to use
    several addresses, use ; to separate them.

![](./media/image137.png)

11. For the **Subject**, select the field so that the **Add dynamic**
    content option appears, and then select it to display the pipeline
    expression builder canvas.

![](./media/image138.png)

**The Pipeline expression builder dialog appears. Enter the following
expression, then select OK:**

!!@concat('WWI Data Pipeline Succeeded with Pipeline Run Id: ', pipeline().RunId)!!

![](./media/image139.png)

1.  For the Body, select the field again and choose the View in
    expression builder option when it appears below the text area. Add
    the following expression in the Pipeline expression builder dialog
    that appears, then select OK:
```
@concat('RunID = ', pipeline().RunId, ' ; ', 'Files Written: ', activity('Data Copy to Lakehouse').output.filesWritten, ' ; ', 'Throughput: ', activity('Data Copy to Lakehouse').output.throughput)
```
![](./media/image140.png)

![](./media/image141.png)

Note: Replace Copy data1 with the actual name of your pipeline copy activity if it was renamed.

2.  Finally select the Home tab at the top of the pipeline editor, and
    choose **Run**. Then select Save and run again on the confirmation
    dialog to execute these activities.

![](./media/image142.png)

![](./media/image143.png)

3.  After the pipeline runs successfully, check your email to find the
    confirmation email sent from the pipeline.

![](./media/image144.png)

![](./media/image145.png)

### Task 2: Schedule Pipeline Execution

Once you finish developing and testing your pipeline, you can schedule
it to execute automatically.

1.  On the Home tab of the pipeline editor window, select **Schedule**.

![](./media/image146.png)

![](./media/image147.png)

2.  Configure the schedule as required. The example below schedules the
    pipeline to execute daily at 8:00 PM until the end of the year.

| Property | Value |
|---|---|
| Repeat | Daily |
| Time | 8:00 PM |
| End date | December 31 of the current year |
| Time zone | Select your local time zone |

![](./media/image148.png)

3.  Click **Close** the schedule.

![](./media/image149.png)

### Task 3: Add a Dataflow Activity to the Pipeline

1.  On the **Activities** tab, drag and drop the **Dataflow** activity
    onto the pipeline canvas.

![](./media/image150.png)

2.  Choose Dataflow from the menu that appears.

3.  The newly created Dataflow activity is inserted between the Copy
    activity and the Office 365 Outlook activity, and selected
    automatically, showing its properties in the area below the canvas.

![](./media/image151.png)

4.  Select the Settings tab on the properties area, and then select the
    **wwi_fact_sale_transform** dataflow you created in Exercise 4.

![](./media/image152.png)

5.  Select the **Home** tab at the top of the pipeline editor, and
    choose **Run**. Then select Save and run again on the confirmation
    dialog to execute these activities.

![](./media/image153.png)

![](./media/image154.png)

6.  Monitor the Output tab to confirm all three activities (Copy data,
    Dataflow, Office 365 Outlook) complete with Status: Succeeded.

![](./media/image155.png)

![](./media/image156.png)

![](./media/image157.png)

## Exercise 6: Building reports in Microsoft Fabric

In this section of the tutorial, you create a Power BI data model and
create a report from scratch.

### Task 1: Explore data in the silver layer using the SQL endpoint

Power BI is natively integrated in the whole Fabric experience. This
native integration brings a unique mode, called DirectLake, of accessing
the data from the lakehouse to provide the most performant query and
reporting experience. DirectLake mode is a groundbreaking new engine
capability to analyze very large datasets in Power BI. The technology is
based on the idea of loading parquet-formatted files directly from a
data lake without having to query a data warehouse or lakehouse
endpoint, and without having to import or duplicate data into a Power BI
dataset. DirectLake is a fast path to load the data from the data lake
straight into the Power BI engine, ready for analysis.

In traditional DirectQuery mode, the Power BI engine directly queries
the data from the source to execute each query, and the query
performance depends on data retrieval speed. DirectQuery eliminates the
need to copy data, ensuring that any changes in the source are
immediately reflected in the query results during the import. On the
other hand, in Import mode performance is better because the data is
readily available in the memory without querying data from the source
for each query execution. However, the Power BI engine must first copy
the data into memory during data refresh. Only changes to the underlying
data source are picked up during the next data refresh(in scheduled as
well as on-demand refresh).

DirectLake mode now eliminates this import requirement by loading the
data files directly into memory. Because there's no explicit import
process, it's possible to pick up any changes at the source as they
occur, thus combining the advantages of DirectQuery and import mode
while avoiding their disadvantages. DirectLake mode is therefore the
ideal choice for analyzing very large datasets and datasets with
frequent updates at the source.

1.  From the left menu select the **Fabric
    Dataengineering-DataFactory-@lab.LabInstance.Id** then select your
    Semantic model named **wwisemanticmodel**.

> ![](./media/image158.png)

2.  Open the semantic model, select the mode drop-down in the
    upper-right corner, switch from Viewing to Editing, and then select
    Make any changes.

![](./media/image159.png)

5.  In the menu ribbon select **Edit tables** to display the table
    synchronization dialog.

![](./media/image160.png)

6.  On the **Edit semantic model** dialog **select all** the tables and
    then select **Confirm** at the bottom of the dialog to synchronize
    the Semantic model.

![](./media/image161.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image162.png)

7.  From the **fact_sale** table, drag the **CityKey** field and drop it
    on the **CityKey** field in the **dimension_city** table to create a
    relationship. The **Create Relationship** dialog box appears.

Note: Rearrange the tables by clicking on the table, dragging and
dropping to have the dimension_city and the fact_sale tables next to
each other. The same holds good for any two tables that you are trying
to create relationship. This is just to make the drag and drop of the
columns between the tables is easier. ![](./media/image163.png)

8.  In the **Create Relationship** dialog box:

    - **Table 1** is populated with **fact_sale** and the column
      of **CityKey**.

    - **Table 2** is populated with **dimension_city** and the column
      of **CityKey**.

    - Cardinality: **Many to one (\*:1)**

    - Cross filter direction: **Single**

    - Leave the box next to **Make this relationship active** selected.

    - Select the box next to **Assume referential integrity.**

    - Select **Save.**

![](./media/image164.png)

9.  Next, add these relationships with the same **Create
    Relationship** settings as shown above but with the following tables
    and columns:

    - **StockItemKey(fact_sale)** - **StockItemKey(dimension_stock_item)**

![](./media/image165.png)

![](./media/image166.png)

- **Salespersonkey(fact_sale)** - **EmployeeKey(dimension_employee)**

![](./media/image167.png)

10. Ensure to create the relationships between the below two sets using
    the same steps as above.

    - **CustomerKey(fact_sale)** - **CustomerKey(dimension_customer)**

    - **InvoiceDateKey(fact_sale)** - **Date(dimension_date)**

11. After you add these relationships, your data model should be as
    shown in the below image and is ready for reporting.

![](./media/image168.png)

### Task 2: Build Report

1.  From the top ribbon, select **File** and select **Create new
    report** to start creating reports/dashboards in Power BI.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image169.png)

2.  On the Power BI report canvas, you can create reports to meet your
    business requirements by dragging required columns from
    the **Data** pane to the canvas and using one or more of available
    visualizations.

![](./media/image170.png)

**Add a title:**

3.  In the Ribbon, select **Text box**. Type in **WW Importers Profit
    Reporting**. **Highlight** the **text** and increase size to **20**.

![](./media/image171.png)

4.  Resize the text box and place it in the **upper left** of the report
    page and click outside the textbox.

![](./media/image172.png)

**Add a Card:**

- On the **Data** pane, expand **fact_sales** and check the box next
  to **Profit**. This selection creates a column chart and adds the
  field to the Y-axis.

![](./media/image173.png)

5.  With the bar chart selected, select the **Card** visual in the
    visualization pane.

![](./media/image174.png)

6.  This selection converts the visual to a card. Place the card under
    the title.

![](./media/image175.png)

7.  Click anywhere on the blank canvas (or press the Esc key) so the
    Card that we just placed is no longer selected.

**Add a Bar chart:**

8.  On the **Data** pane, expand **fact_sales** and check the box next
    to **Profit**. This selection creates a column chart and adds the
    field to the Y-axis. 

![](./media/image176.png)

9.  On the **Data** pane, expand **dimension_city** and check the box
    for **SalesTerritory**. This selection adds the field to the
    Y-axis. 

![](./media/image177.png)

10. With the bar chart selected, select the **Clustered bar
    chart** visual in the visualization pane. This selection converts
    the column chart into a bar chart.

![](./media/image178.png)

11. Resize the Bar chart to fill in the area under the title and Card.

![](./media/image179.png)

12. Click anywhere on the blank canvas (or press the Esc key) so the bar
    chart is no longer selected.

**Build a stacked area chart visual:**

13. On the **Visualizations** pane, select the **Stacked area
    chart** visual.

![](./media/image180.png)

14. Reposition and resize the stacked area chart to the right of the
    card and bar chart visuals created in the previous steps.

![](./media/image181.png)

15. On the **Data** pane, expand **fact_sales** and check the box next
    to **Profit**. Expand **dimension_date** and check the box next
    to **FiscalMonthNumber**. This selection creates a filled line chart
    showing profit by fiscal month.

![](./media/image182.png)

16. On the **Data** pane, expand **dimension_stock_item** and
    drag **BuyingPackage** into the Legend field well. This selection
    adds a line for each of the Buying Packages.

![](./media/image183.png) ![](./media/image184.png)

17. Click anywhere on the blank canvas (or press the Esc key) so the
    stacked area chart is no longer selected.

**Build a column chart:**

18. On the **Visualizations** pane, select the **Stacked column
    chart** visual.

![](./media/image185.png)

19. On the **Data** pane, expand **fact_sales** and check the box next
    to **Profit**. This selection adds the field to the Y-axis.

20.  On the **Data** pane, expand **dimension_employee** and check the
    box next to **Employee**. This selection adds the field to the
    X-axis.

![](./media/image186.png)

21. Click anywhere on the blank canvas (or press the Esc key) so the
    chart is no longer selected.

22. From the ribbon, select **File** \> **Save**.

![](./media/image187.png)

23. Enter the name of your report as **Profit Reporting**.
    Select **Save**.

![](./media/image188.png)

24. You will get a notification stating that the report has been saved. 

![](./media/image189.png)

# Exercise 7: Clean up resources

You can delete individual reports, pipelines, warehouses, and other
items or remove the entire workspace. Use the following steps to delete
the workspace you created for this tutorial.

1.  Select your workspace, the **Fabric
    Dataengineering-DataFactory-@lab.LabInstance.Id** from the left-hand
    navigation menu. It opens the workspace item view.

&nbsp;

2.  Select the **...** option under the workspace name and
    select **Workspace settings**.

![](./media/image190.png)

3.  Select **General** and **Remove this workspace.**

![](./media/image191.png)

4.  Click on **Delete** in the warning that pops up.

![](./media/image192.png)

5.  Wait for a notification that the Workspace has been deleted, before
    proceeding to the next lab.

![](./media/image193.png)

**Summary**

In this lab, you implemented a complete Microsoft Fabric data
engineering workflow by creating a Fabric workspace and Lakehouse,
ingesting source data, loading it into Delta tables, validating the data
with SQL queries, building a semantic model, and generating a Power BI
report. These activities demonstrate how Microsoft Fabric simplifies
modern analytics by combining data integration, storage, transformation,
semantic modeling, and reporting within a unified platform. The skills
gained in this lab provide the foundation for developing scalable data
engineering solutions using Microsoft Fabric.
