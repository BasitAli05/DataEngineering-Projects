1) create a resource group in which we create Azure datafactory, SQL server and SQL database
2) created an azure sql database (basit,Test1234#) , set firewall in SQL server if access is not granted with your current IP Address
3) create 2 tables (one for source and other for sink)
4) create a pipeline
   -) create lookup function (source dataset = sink table)
       -) write query to find max(InsertTime) and pass it to copydata function
   -) create copydata function select source table and write query for selecting specific tables and 
       -) Apply condition where InsertTime > '@{activity('lookup').output.firstrow.maxdate}' for inserting new records
   -) select sink table 
5) debug  to check your pipeline is working fine