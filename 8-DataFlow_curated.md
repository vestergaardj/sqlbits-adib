# Create a data flow to curate the data

Ensure *Data flow debug* ON

Click *Author*

Click *'+'/Data flow/Data flow

Rename: Curate Crime

## Extract 
Click Add Source/Add Source

Name: Delta_Source

Source Type: Inline

Source dataset type: Delta

Linked Services: ADLS_Crime

Set *Sampling* **Enabled**

Set Rows Limit = 10

Click *Source Options*

Browse for folder path *data/enriched/Year=2010*

Select Compression Type: snappy

Click: *Projection*

Click: *Import schema* (if option is disabled, check to see if *Data flow debug* is enabled)

Click: *OK*

Click *Data Preview* 

Click *Refresh*

Observe the data... praise the data!

## Transform

Click *'+'* after the *Delta Source*

Add *Filter*

Set *Output Stream Name* = *FilterOutliers*

Open *Expression Builder*

Set *Expression* = Latitude >= 41 && Longitude >= -88

Click *Save and Finish*

Click *Data Preview*

Observe the data :)

## Load

Click *'+'* after the *FilterOutliers* container

Add sink

Rename *Output Stream* = *DeltaTarget*

Set *Sink type* = *Inline*

Set *Inline dataset type* to 

Set *Linked service* = ADLS_Crime

Click *Settings*

Browse to data/curated *(if folder does not exist, create it using the Azure Storage Explorer)*

Set *TableAction* = truncate

Click *Optimize*

Set *Partition option* = *Set partition*

Select *Year* as partition column

Click *Data Preview*

Observe data is as good as can be :)

Select: *Settings*

Set *Sampling* to **Diable** 

Click *Publish All*
