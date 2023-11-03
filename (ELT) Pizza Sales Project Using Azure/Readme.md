# SQL Server -> ADF -> blob storage -> Databricks -> PowerBI <br>
### Extract and Load Data <br>
1) first import the pizza_sales.csv into SQL server as table
![sqltable](https://github.com/BasitAli05/DataEngineering-Projects/assets/106751594/a0a5e584-7cab-445d-9f1f-e5d832e32855)
2) create a resource group for this project 
<pre>   -) create storage account (here we are using blob storage) 
   -) create a container named raw (here we will store data from SQL server)
   -) create data factory, Launch DF studio and create new pipeline
      -) create a copy data activity 
      ** For Source **
      -) select source option as SQL server
      -) Now for on-prem to cloud we have to create self hosted integration runtime, create that one
         -) After that, copy-paste one key into Microsoft Integration runtime configuration manager and register
	 -) Fill all credentials like databse, server.. Test the connection and create new linked service
      -) Select the table and click on OK
      ** For Sink **
      -) Select sink option as blob storage or ADLS depending on your requirements (also select file format)
      -) ceate linked service (Will be Autoresolve integration) and provide all details required click create
      -) provide file path where you want to store the data.. click on ok
      ** Now our source and sink is ready click on validate and then publish all ** </pre>
3) Now our pipeline is created and saved.. click on trigger now (Now the pipeline is running)
![ADF](https://github.com/BasitAli05/DataEngineering-Projects/assets/106751594/315eb9ee-0b90-453f-b958-445e74089d05)
4) goto monitor tab, You can see the pipeline is running
5) After the pipeline is run successfully, we can see that the SQL table is Extracted and loaded into blob storage
![blobstorage](https://github.com/BasitAli05/DataEngineering-Projects/assets/106751594/44fbed1d-c38e-475b-b87d-a0954851f6bd)

### Connect storage to databricks
<pre>-) goto storage account -> access keys and copy 1 key 
-) Code for mounting your folder
dbutils.fs.mount(
  source = "wasbs://<container-name>@<storage-account>.blob.core.windows.net",
  mount_point = "/mnt/folder_name",
  extra_configs = {"fs.azure.account.key.mystorageproject01.blob.core.windows.net":"paste your access-key"}
  OR   {"fs.azure.account.key.mystorageproject01.blob.core.windows.net":dbutils.secret.get(scope = "<scope-name>", key = "<key-name>")}
)
-) do some transformations as per requirements
</pre>
### Connect PowerBI with databricks
-) here you can do all the visualizations and generate business insights
