## Create a sample Power BI report

Open Power BI Desktop

Click *Get Data*

Select *Azure*

Select *Azure Data Lake Storage Gen2*

Open Azure Storage Explorer

Navigate to the targeted subscription

Expand storage accounts on the subscription

Copy the *DFS Endpoint*

Paste into URL in Power BBI desktop dialog

Click *OK*

Switch back to Azure Storage Explorer

Navigate to *Primary Key*

Click the eye-icon

Copy the key now visible

Paste into Account Key in Power BI dialog

Select *Transform Data*

Filter column *Folder Path* to select only rows that begin with **https://<insert storage account>.dfs.core.windows.net/<insert path>/Year%3D2010**

Click *Combine Files* on the header of the *Content* column

Click *OK* in the dialog

Make sure the data types are correct (IUCR, FBICode as text)

In Query Properties: rename to *"Enriched"*

Click *Close and Apply*

##### The Data Load can take some time - advance to next step while you wait

Navigate to the *Data* pane in PBI Desktop

Set data category Longitude for column *Longitude*

Set data category Latitude for column *Latitude*

Set *Summarization* for column *District* to *Don't summarize*

Set *Summarization* for column *Community Area* to *Don't summarize*

Click the ... on the table and select *New measure*

Type in: Incidents = CALCULATE( COUNT( Enriched[ID] ))

Validate the calculation by clicking the V

Select the *Report* pane

Select *District* as Page Filter

Select only District = 1

Select *Community Area* as Page Filter

Select only Community Area = 32

Create a *Map* visualization

Maximize the visual on the canvas

Select *Latitude* for Latitude

Select *Longitude* for Longitude

Select *Incidents* for Bubble Size

Optionally select *Primary Type* as Legend

Observe differences in bubble size

Observe if longitude/latitude has outliers
