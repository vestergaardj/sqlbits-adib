# Create you first Serverless Pool Table

## Used *Public Dataset* earlier?

Open Storage Explorer

Navigate to: *ADLS Gen 2 Storage Account Created Earlier*

Click: container *Data*

Navigate to: *Public Dataset* (blob)

Right-Click: container *source-files*

Select: Open in new Tab

Multi-Select: all csv files (crimes and crahses)

Select: Copy (in the ribbon)

Select: the other open tab (*Data* container)

Click: *New folder*

Type: *raw*

Double-Click: *raw* folder 

Click: *Paste* (in the ribbon)

Observe that the data is copied into your *raw* folder in the ADSL Gen2 storage account linked to the Synapse Workspace

## Data is ready

Navigate to the Azure Synapse Analytics resource created above

Open Synapse Studio 

Alternately use this link: https://web.azuresynapse.net/en/workspaces
Login and select appropriate workspace

Navigate to: Data

Navigate to: Linked 

Expand storage account *newport-ws/data*

Select the 'Data (Primary)'

Double-click the folder 'Raw'

Observe: file named 'Traffic_Crashes_-_Crashes_sample.csv' (found at [city of Chicago](https://data.cityofchicago.org/Transportation/Traffic-Crashes-Crashes/85ca-t3if))

Right-click file and select 'New SQL Script/Select Top 100 Rows'

Observe new script created

Click 'Run'

Observe result set displayed

Click Tab: 'Data'

Right-Click file and select 'New SQL Script/Create external table'

Check 'Infer column names'

Verify by clicking link 'Preview Data'

Click 'Continue'

Select Database: (new) newport-demo-sql

External table name: dbo.Crashes_samples

Check: Using SQL Script

Click: 'Open Script'

Observe four stages: 
- Create External File Format
- Create External Data Source
- Create External Table
- SELECT TOP 100 *

Click 'Run'

Observe obscure error message 🤯
Bulk load data conversion error (type mismatch or invalid character for the specified codepage) for row 1, column 1 (ID) in data file https://chicagodemosa.dfs.core.windows.net/data/Raw/Chicago_Crimes_sample3k.csv.


## Looking at the data

Click: *Data/Linked*

Click: *newport-ws/data*

Right-Click: *Traffic_Crashes_-_Crashes.csv*

Select: *New SQL script/Select TOP 100 rows*

`SELECT
    TOP 100 *
FROM
    OPENROWSET(
        BULK 'https://<replace storage account>.dfs.core.windows.net/data/Traffic_Crashes_-_Crashes.csv',
        FORMAT = 'CSV',
        PARSER_VERSION = '2.0',
        HEADER_ROW=true
    ) AS [result]
`
