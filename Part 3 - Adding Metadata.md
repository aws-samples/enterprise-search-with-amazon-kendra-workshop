# Part 3 - Adding Metadata

The last area we are going to explore in this workshop is what kendra calls "metadata files". These are optional files that can live alongside of our documents and enrich them beyond their raw content. Some examples of metadata that we can add are Document Attributes (category, last updated time, version, custom attributes), Access Control Lists, Document Title, and Content Type. You can learn more about S3 Document Metadata in the Kendra Documentation: https://docs.aws.amazon.com/kendra/latest/dg/s3-metadata.html

In order to add metadata files, there are a few rules:

- There are 2 options for folder structure:
  - **Metadata with Documents** - You are allowed to have your metadata files live inside of your document folders, right alongside the documents. We will not be taking this approach for this lab. Instead we will be separating the documents from their metadata.
  - **Metadata separate from Documents** - We can store the metadata in a separate folder structure from the actual documents themselves. The folder structure inside of the metadata folder needs to mirror the document structure of the bucket. For example, if our documents live in s3://gz-0206-kendra-demo-bucket/html, and our metadata folder is "metadata", those metadata files would reside in s3://gz-0206-kendra-demo-bucket/metadata/html
- Metadata filenames should be the same as the corresponding file, with an added .metadata.json extension. (e.g. document.html would have a metadata file named document.html.metadata.json)
- Metadata files must be JSON documents.

There are some prebuilt metadata files inside the workshop content that we will be working with. They are located in the "metadata" folder.

Here is an example of one of the files in that folder (blazingtext_hyperparameters.md.html.metadata.json):

```json
{
	"Title":"BlazingText Hyperparameters (overridden)",
	"Attributes":{
		"_category": "Algorithms",
		"tags":["Machine Learning", "Algorithms", "BlazingText"]
	}
}
```

- In this file, we added a "Title" to override the default title for the HTML document we uploaded to S3. We have also added some attributes to allow us to add faceted search on items like "category" and "tags".

- Lets add the metadata files to S3 first, then we will build/enable the facets, and finally re-index our content.

- Click "Services" at the top left hand side of your screen, type S3 into the search box, and click S3.

- Once in the S3 console, open the S3 bucket we have been using for this workshop. (e.g. gz-0206-kendra-demo-bucket)

![](https://github.com/aws-samples/enterprise-search-with-amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-02-20%20at%203.56.41%20PM.png)

- After you've browsed into the bucket, click the "Upload" button.

- Drag the "metadata" folder from your workshop folder into the box.

![](https://github.com/aws-samples/enterprise-search-with-amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-02-20%20at%209.02.07%20PM.png)

- Click Upload.

- Now that our metadata is uploaded to S3, we will go back to Kendra to do the rest.

- Click on the services button at the top left hand side of your screen.

- Type "kendra" into the search box, and select "Amazon Kendra" from the list below.

![](https://github.com/aws-samples/enterprise-search-with-amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-02-20%20at%204.01.40%20PM.png)

- On the Kendra homepage, click on "Create an Index"

![](https://github.com/aws-samples/enterprise-search-with-amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-08-04%20at%209.38.50%20AM.png)

- Select kendra-demo-index from the list of indexes.

![](https://github.com/aws-samples/enterprise-search-with-amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-02-20%20at%205.53.20%20PM.png)

- Before we can reindex our data, we will have to add the custom facet "tags" that is in our metadata files. If we try to reindex without adding the necessary facet data, it will fail.

- On the left hand menu, click "Facet definition"

![](https://github.com/aws-samples/enterprise-search-with-amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-02-20%20at%206.42.38%20PM%20-%20facet.png)

- Here we will be adding a custom facet "tags", and enabling the "category" facet. We will add the custom facet first.

- In the "Index Fields" area, click "Add Field" on the top right.

![](https://github.com/aws-samples/enterprise-search-with-amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-08-04%20at%2012.49.30%20PM.png)

- In the "Field name" box, enter "tags"

- In the "Data type" box, select "String list", since this field is an array of tag items.

- Under usage types, check the 3 available items: 

	- Facetable (allows facets to be created)
	- Searchable (allows field to participate in determining relevancy to the query)
	- and Displayable (whether we are going to return this facey in the query response)

![](https://github.com/aws-samples/enterprise-search-with-amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-08-04%20at%2012.51.59%20PM.png)

- Click Add

- Now we will enable the "category" facet as well, since we included it in our metadata.

- Inside of the "Index fields" section, find the "Field name" of "category" and check all 4 boxes next to it, similarly to what we did for our custom facet. (Facetable, Searchable, and Displayable). You can leave 

![](https://github.com/aws-samples/enterprise-search-with-amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-08-04%20at%2012.53.50%20PM.png)

- Click "Save" at the bottom of the section.

- Now that we added the necessary metadata files to S3 and added the matching facets to Kendra, we can add the mapping to the datasource and re-index our data.

- On the left hand menu, click "Data sources"

- Check the box next to "demo-s3-datasource" item, and hit "edit"

- On the Name and description section, no changes are necessary. Click "Next"

- On the next page, under "Configure S3 connector", find the field "Metadata files prefix folder location".

- Enter "metadata/" or click "Browse S3" and select your bucket, check the box next to the "metadata" folder, and click "Choose"

![](https://github.com/aws-samples/enterprise-search-with-amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-02-20%20at%207.00.29%20PM.png)

- Click "Next"

![](https://github.com/aws-samples/enterprise-search-with-amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-02-20%20at%207.01.20%20PM.png)

- On the Review and Create Page, click "Confirm Changes"

- We can now re-index our data. We should now be back on the Data sources page.

- Select the radio button next to demo-s3-instance, and click the "Sync now" button near the top of the section.

- The "Current sync state" attribute will change to "Syncing - crawling". Wait for it to complete (around 1 minute).

![](https://github.com/aws-samples/enterprise-search-with-amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-08-04%20at%2012.55.41%20PM.png)

- If "Last sync status" is "Succeeded" and "Current sync state" goes to "Idle" then your synchronization job was a success.

![](https://github.com/aws-samples/enterprise-search-with-amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-08-04%20at%2012.56.12%20PM.png)

- Now we can go back to the search console and see our faceted search in action.

- Click "Search Console" on the left hand navigation.

![](https://github.com/aws-samples/enterprise-search-with-amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-02-20%20at%206.42.38%20PM.png)

- We added metadata for a few items, with 2 of them being the Machine Learning algorithms XGBoost and BlazingText. Lets try searching for "algorithms".

![](https://github.com/aws-samples/enterprise-search-with-amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-02-20%20at%207.09.53%20PM.png)

- Our search was successful, and we got a list of algorithm based results. Lets see what we have for facets.

- You will notice that now on the left hand side of our results, there is a section that says "Filter search results" that we did not have previously. Click on it to expand the menu.

![](https://github.com/aws-samples/enterprise-search-with-amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-02-20%20at%207.10.09%20PM-2.png)

- As you can see here, we have the "category" and "tags" facets that were part of our item metadata. Click on the "BlazingText" facet to filter down to just results for BlazingText.

![](https://github.com/aws-samples/enterprise-search-with-amazon-kendra-workshop/blob/master/images/Screen%20Shot%202020-02-20%20at%207.11.47%20PM.png)

- On the following results page, we've filtered our result set down to only the items that are tagged with "BlazingText" in our item metadata. You can also see that the last article for BlazingText Hyperparameters is using our updated title metadata of "BlazingText Hyperparameters (overridden)".

- That's it! In this workshop we created an Enterprise Search instance, created a database of frequently asked questions, and added faceted search. For more information on Amazon Kendra, please head to the homepage at: https://aws.amazon.com/kendra/
