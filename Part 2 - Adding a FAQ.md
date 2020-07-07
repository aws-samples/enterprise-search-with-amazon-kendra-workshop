# Part 2 - Adding a FAQ to Kendra

Next we will add some enhancements to Kendra to allow for Frequently Asked Question support, faceted search, and customizing metadata.

Adding Frequently Asked Question support:

First, we will need to upload a set of FAQs into Amazon S3. Click "Services" at the top left hand side of your screen, type S3 into the search box, and click S3.

Once in the S3 console, open the S3 bucket we have been using for this workshop. (e.g. gz-0206-kendra-demo-bucket)

After you've browsed into the bucket, click the "Upload" button.

Drag the "faqs" folder from your workshop folder into the box.

![](https://github.com/giuseppe-zappia/amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-02-20%20at%205.50.56%20PM.png)

Click Upload.

Now we can go back to Kendra to index our FAQ.

Click on the services button at the top left hand side of your screen.

Type "kendra" into the search box, and select "Amazon Kendra" from the list below.

On the Kendra homepage, click on "Launch Amazon Kendra"

Select kendra-demo-index from the list of indexes.

![](https://github.com/giuseppe-zappia/amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-02-20%20at%205.53.20%20PM.png)

On the index homepage, in the getting started section, there will be an area called "Add FAQs". Click the "Add FAQs" button.

![](https://github.com/giuseppe-zappia/amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-02-20%20at%205.53.33%20PM.png)

In the FAQ name field, type "kendra-demo-sagemaker-faq"

In the FAQ settings section, in the S3 location field, either type in the S3 location where we uploaded our FAQ (e.g. s3://gz-0206-kendra-demo-bucket/faqs/sagemaker_faq.csv) or click the Browse S3 button, and select your bucket, the faqs folder, then the sagemaker_faq.csv item and click "Choose"

![](https://github.com/giuseppe-zappia/amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-02-20%20at%205.58.48%20PM.png)

In the IAM role field, we will re-use the role from our S3 data source since it already has the correct permissions. Select the "AmazonKendra-demo-s3-datasource-role" item.


![](https://github.com/giuseppe-zappia/amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-02-20%20at%206.00.45%20PM.png)

Click Add

You will be forwarded to the FAQs section of the Kendra console, and the status will be set to "Creating". 

![](https://github.com/giuseppe-zappia/amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-02-20%20at%206.01.33%20PM.png)

Wait for this process to finish (around 30 seconds). It will change to "Active".

![](https://github.com/giuseppe-zappia/amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-02-20%20at%206.03.15%20PM.png)

From here, we can go back to our search console and test the FAQ functionality.

In the left hand menu, click "Search Console" to go to the Kendra Search console.

![](https://github.com/giuseppe-zappia/amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-02-20%20at%206.42.38%20PM.png)

In order to trigger the functionality for FAQs in the console, we will have to actually ask Kendra a frequently asked question.

Examples of search terms that will trigger the FAQ functionality are:

- What is sagemaker?
- What is reinforcement learning?
- Spot training

![](https://github.com/giuseppe-zappia/amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-02-20%20at%206.09.15%20PM.png)

To explore this further, you can open up the sagemaker_faq.csv file on your desktop to see the list of frequently asked questions that we uploaded.

[Part 3 - Adding Metadata](https://github.com/giuseppe-zappia/amazon-kendra-workshop/blob/master/Part%203%20-%20Adding%20Metadata.md)

