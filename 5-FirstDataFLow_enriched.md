# Create your first Data Flow ( < 10 min ) (Enriched)

From Azure Portal: Click *Launch Studio* (new window opens)

Click: *Author* (right side menu, crayon 🖍️)

Click *'+'* /Data flow/Data flow

Toogle *Data flow debug* ON

Click: *OK* button

Rename: Enrich Crime

## Extract

Click Add Source/Add Source

Name: CSVSource (no funny stuff naming, and no spacing or special characters)

Source Type: Data Set

Dataset: (new) CrimeCSV
-   NEW
    - Select Azure Data Lake Storage Gen2
    - Click *Continue*
    - Select *DelimitedText*
    - Click *Continue*
    - Name: *CrimeCSV*
    - (new) LinkedService
    - Name: *ADLS_Crime*
    - From Azure Subscription
    - Select appropritate subscription (housing the storage account)
    - Select Storage Account Name
    - Click *Create*
-   Click: the arrow to the far right, next to the folder.
-   Select: From root
-   Browse until you see the csv files.
-   Click: OK
-   FilePath: data/
-   Check: "First row as header"
-   Click *OK*

Navigate back to data flow tab (select the source you just created)

On Source settings, set Sampling = Enable

Click *Projection*

Click *Import projection* (can take a few minutes depending on files)

Click *Data Preview*

Click *Refresh*

Observe the expected sample rows

## Transform

Click *'+' after SourceCSV container

Add *Derive Column*

Rename: DeriveDate

Open Expression builder

Rename Column Name: *Date*

Set Expression = 'toDate(left(Date, 10), "MM/dd/yyyy")'

Click *Save and finish*

Click *Data Preview*

Click *Refresh*

CLick *'+' after DeriveDate container

Add *Derive Column*

Rename: DeriveYearMonth

Open *Expression Builder*

Rename Column: Year

Set Expression = year(Date)

Add new Column

Rename Column: Month

Set Expression = month(Date)

Click *Save and Finish*

Click *Data Preview*

Click *Refresh*

Scroll far right, observe Months as numbers

## Load

**Sink**

Click *'+'* after DeriveYearMonth

Add Sink

Rename: TargetDelta

Sink Type: Inline

Inline Dataset Type: Delta

Linked Service: ADLS_Crime

**Settings**

Click *Settings*

Browse for data/enriched (if the path does not exist, create it in Azure Storage Explorer)

Click *Mapping*

Uncheck *Auto Mapping*

Remove Column: *_c0* 

Rename all columns that include blank spaces: Case Number, Primary Type, Location Description, Community Area, FBI Code, X Coordinate, Y Coordinate, Updated On

Click *Optimize*

Set *Partition Option* to *Set partitioning*

Select Key Columns: *Year*

Click *'+'* after *Year* column

Select Key Columns: *Month*

Click *Data Preview*

Click *Refresh*

Observe that data is as expected

Click *Publish All*
