Utilize Azure Data Factory (ADF) to ingest "Orders data" , and execute fundamental transformations via Dataflow on the datasets.Ingest data from Http connector to ADLS Gen2.
Steps to follow- 
1) Create dashboard 
2) Create resource and resource group
3) create blob storage acc
4) Create ADLS Gen 2 acc --- Enable hierarchical namespace
5) After creating both storage accounts - Select individual storage acc-> settings-> configurations->enable "allow blob anonymous access" for both storage accounts.
6) pin all to dashboard
7) create Data factories
8)Create a Linked Service for Source (choose HTTP connector):BaseURL - https://files.cdn.thinkific.com
9) Create a Linked Service for sink (ADLS) 
10 ) Create a datasets for source - Relative URL - file_uploads/349536/attachments/c28/5fb/25b/orders.csv
11) Create a datasets for sink - with proper "filepath" of sink & "column delimiter" - tab
12) create pipeline- orders_pipeline ( copy data)
13) Create a data flow and click on the option “Add Source” and 
(the source for this data flow will be our “ordersoutput.csv” dataset so we will mention the database for it i.e “ds_orders_dataset_adls)
14) "data flow debug " mode ON 
15) Put all details of dataflow , then (+) SELECT 
(delete option to remove order_date column and rename order_customer_id
to customer_id)
16)Now click on “+” we will use “aggregate transformation”
(group by the “order_status” column)
(To calculate the count of each order status :
Click on “Aggregates” mention order_id column and click on “Open expression builder”
-> count(order_id) in “Expression”)
17) create the “result” directory in the “data” container in ADLS gen2 storage
18) Also create dataset “ds_orders_json_output” for storing “orders.json” data in this “result“
directory
19) For “orders_dataflow” click on “Optimize” option and select “Single partitioning” to store
the complete output in a single file.
20) Now click on “+” we will add “sink” to store the aggregated data -> Add the “ d s _ o r d e r s _j s o n _ o u t p u t ” in the dataset and test connection.
21) drag the dataflow in pipeline and debug/run
