# Part 1 - Creating a Kendra Index

- Clone this github repo to your desktop

- Extract the zip file, this will contain all of the materials you will need to complete the workshop

- Log into your AWS Account

- In the AWS Region selector on the top right hand side of your screen, make sure you are working in the "N. Virginia" region 

![](https://github.com/aws-samples/enterprise-search-with-amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-02-24%20at%202.39.12%20PM.png)

- Click on the "services" button at the top left hand side of your screen

- Type "kendra" into the search box, and select "Amazon Kendra" from the list below


![](https://github.com/aws-samples/enterprise-search-with-amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-02-20%20at%204.01.40%20PM.png)


- On the Kendra homepage, click on "Launch Amazon Kendra"


![](https://github.com/aws-samples/enterprise-search-with-amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-02-20%20at%204.02.31%20PM.png)


- This will take you to the "Create Index" screen, where we will create our first Amazon Kendra search index.

- In the index name field type "kendra-demo-index"

- For IAM role, select "Create a new role". This will be the role that Kendra uses to push logging and metrics to Amazon Cloudwatch.

- Once selected, the Role Name field will appear. Enter "demo-index-role" into this box

![](https://github.com/aws-samples/enterprise-search-with-amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-02-20%20at%204.05.20%20PM.png)

- Click "Create"

- You will be forwarded to the console page for your index, with a message stating that your index is being created. You will need to wait for this index to finish before proceeding. **This takes between 15 and 20 minutes.** You will not need to refresh the page.

![](https://github.com/aws-samples/enterprise-search-with-amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-02-20%20at%204.06.40%20PM.png)

- Once your index is finished creating, go to the bar in the top left, click on "Services", type S3 in the search box, and click on the S3 entry to go to the S3 Console


![](https://github.com/aws-samples/enterprise-search-with-amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-02-20%20at%203.51.43%20PM.png)


- Once inside the S3 service, click on Create Bucket:


![](https://github.com/aws-samples/enterprise-search-with-amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-02-20%20at%203.52.25%20PM.png)


- Enter a bucket name in the format "initials-birthdate-kendra-demo-bucket" (e.g. gz-0206-kendra-demo-bucket)

- Select your region as "US East (N.Virginia)"


![](https://github.com/aws-samples/enterprise-search-with-amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-02-20%20at%203.55.37%20PM.png)


- Click Create

- Click on your newly created bucket


![](https://github.com/aws-samples/enterprise-search-with-amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-02-20%20at%203.56.41%20PM.png)


- Hit the Upload button, and then drag the "html" and "pdfs" folders from your desktop onto the dialog box

- You should see 2 folders ready to be uploaded

- Hit the upload button.


![](https://github.com/aws-samples/enterprise-search-with-amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-02-20%20at%203.58.05%20PM.png)


- It should take a moment or 2 to upload the necessary files. You will see a progress bar on the bottom.

- Once that is completed, click on the services button at the top left hand side of your screen

- Type "kendra" into the search box, and select "Amazon Kendra" from the list below.


![](https://github.com/aws-samples/enterprise-search-with-amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-02-20%20at%204.01.40%20PM.png)


- On the Kendra homepage, click on "Launch Amazon Kendra"

![](https://github.com/aws-samples/enterprise-search-with-amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-02-20%20at%204.02.31%20PM.png)


- Click the "Add data sources" button, so we can add data to the index.


![](https://github.com/aws-samples/enterprise-search-with-amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-02-20%20at%205.03.05%20PM.png)


- We will be using an Amazon S3 connector for our data source in this demo. Click "Add Connector" under Amazon S3.


![](https://github.com/aws-samples/enterprise-search-with-amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-02-20%20at%205.03.59%20PM.png)


- Here we will name our data source. Type "demo-s3-datasource" in the "Data source name" field.


![](https://github.com/aws-samples/enterprise-search-with-amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-02-20%20at%205.06.33%20PM.png)


- Click Next

- On the next screen we will configure our data source connection to S3.

- In the data source location field, either enter the s3 bucket path (e.g. s3://gz-0206-kendra-demo-bucket), or click the "Browse S3" button to search for it.

- In the IAM Role section, choose "Create a new role". This will be the role that Kendra uses to index the S3 data.

- In Role name, enter "demo-s3-datasource-role"

- In the "Set sync run schedule" section, under Frequency, select "Run on demand".


![](https://github.com/aws-samples/enterprise-search-with-amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-02-20%20at%205.11.47%20PM.png)


- Click Next

- On the Review and create screen, click "Create"


![](https://github.com/aws-samples/enterprise-search-with-amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-02-20%20at%205.12.31%20PM.png)


- A new IAM role will be created, and you will be returned to the index home page.

- Wait for your data source status to change to "Active"

![](https://github.com/aws-samples/enterprise-search-with-amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-02-20%20at%205.14.04%20PM.png)

- Once your data source is Active, you can synchronize it. Click the "Sync now" button near the top right corner of your screen.

- Once started, an entry in the 'Sync run history' will show up as "Syncing" and wait for that to complete. It should take about 1 minute.


![](https://github.com/aws-samples/enterprise-search-with-amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-02-20%20at%205.15.19%20PM.png)


- When the Sync run status changes to "Succeeded", that means Kendra has indexed all of our data and it is ready to be searched!


![](https://github.com/aws-samples/enterprise-search-with-amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-02-20%20at%205.19.10%20PM.png)


- In the left hand menu, click "Search Console" to view the Kendra Demo Console.


![](https://github.com/aws-samples/enterprise-search-with-amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-02-20%20at%206.42.38%20PM.png)


- In the search console, you can submit search queries for the data that we have in S3. Our index is comprised of documentation for Amazon Sagemaker and a few whitepapers for Machine Learning topics.


![](https://github.com/aws-samples/enterprise-search-with-amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-02-20%20at%205.22.39%20PM.png)


- Run a few queries and look at the results. 
  
  Example queries are:

  - Sagemaker
  - What is reinforcement learning?
  - What is deep learning?
  - time series forecasting


![](https://github.com/aws-samples/enterprise-search-with-amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-02-20%20at%205.34.52%20PM.png)


- Congratulations, you've successfully created an enterprise search instance with Amazon Kendra!

- In the next section we will add some enhancements to Kendra to allow for Frequently Asked Question support, faceted search, and customizing metadata.


[Part 2 - Adding a FAQ](https://github.com/aws-samples/enterprise-search-with-amazon-kendra-workshop/blob/master/Part%202%20-%20Adding%20a%20FAQ.md)
