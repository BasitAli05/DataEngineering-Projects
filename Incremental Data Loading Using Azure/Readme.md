# Incremental Data Load Using Azure DataFactory
1) create a resource group in which we create Azure datafactory, SQL server and SQL database
![1](https://github.com/BasitAli05/DataEngineering-Projects/assets/106751594/72c9d811-e840-4f30-895d-bd26a0afa0ce)
2) created an azure sql database (id: basit, Pass: T.......#) , set firewall in SQL server if access is not granted with your current IP Address
3) create 2 tables (one for source and other for sink)
![2](https://github.com/BasitAli05/DataEngineering-Projects/assets/106751594/dbf44d01-5ddd-4152-bff9-cf9601a7205c)
![3](https://github.com/BasitAli05/DataEngineering-Projects/assets/106751594/8779c5fb-10e5-49a3-be90-ab79fbeb2987)
<pre>
4) create a pipeline
   -) create lookup function/activity and write a query to find max(InsertTime) of sink table and pass it to copydata function
       -) The query will fetch the latest time at which the last record was added </pre>
   ![lookup](https://github.com/BasitAli05/DataEngineering-Projects/assets/106751594/f3ca8bb0-b80c-45ff-acf4-f08f705d903b)
   -) create copydata function select source table and write query for fetching latest rows
   ![copydata_source](https://github.com/BasitAli05/DataEngineering-Projects/assets/106751594/6982f054-4f9c-459f-b4c3-e708efc6ffad)
   -) select sink table
   ![copydata_sink](https://github.com/BasitAli05/DataEngineering-Projects/assets/106751594/e694ec64-eb1d-44a1-ba47-ce673e7f527f)

5) Now Add a new record in source table
![5](https://github.com/BasitAli05/DataEngineering-Projects/assets/106751594/07745b73-5b30-4ff6-b079-5260dbc2f8d4)
6) Last but not the least, debug the pipeline if it's working fine then publish it to save the changes
![publish-debug](https://github.com/BasitAli05/DataEngineering-Projects/assets/106751594/00bb147d-8927-4779-9791-21dbf6d6ef79)
7) At last, Check whether new records are added to sink table
![last](https://github.com/BasitAli05/DataEngineering-Projects/assets/106751594/7356c0d2-2c64-4fc6-b85c-1af29003dd73)
