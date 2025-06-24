# Unstructured-Data-in-Salesforce

Step 1: Connect to an External Blob Store
Your unstructured data is stored in external blob stores such as Amazon S3, Microsoft Azure
Blob Storage, or Google Cloud Storage, and you will reference them directly by using
unstructured data lake objects (UDLO). To create a connection to an external blob store,
Administrative Access to the desired external system is necessary. From there, you will log in
with your credentials and create a new connection.
Step 2: Connect Unstructured Data to Data Cloud
Once a Connection is created, Sunshine Trails Hospitality will reference the unstructured data
from external blob stores to Data Cloud. Next, you will want to create a new unstructured data
lake object and select the desired external files. Then select your connector, for our example
Amazon S3. You will point to the specific folder or directory in your blob storage. Then create
and map the Unstructured Data Lake Object to an Unstructured Data Model Object (UDMO).
Let’s take a deep dive into these steps:
1. Navigate to Data Cloud > click Data Lake Objects >click New.
2. From the New Data Lake Object menu, select From External Files > click Next.
3. Choose which connector to use > click Next.
4. From the Select Connection dropdown list, select a connection.
5. In the Directory field, point to a specific folder or an entire directory in your blob store. All
folders and subfolders in a directory are included. Optionally, use wildcard characters to
specify a file name pattern for multiple files.
6. To add more directories, click More Files. You can include up to 5 directories > click
Next.
7. Add an Object Name and an Object API Name for the UDLO.
8. From the Data Space dropdown list, select a data space in which to create the new
UDMO or a data space from which to select an existing UDMO.
9. Map the UDLO to a UDMO.
i. • To create a new UDMO, click New.
ii. • To use an existing UDMO, click Existing, and select a UDMO from the
list.
10. Optionally, leave the checkbox selected to create a search index configuration for the
UDMO using system defaults that automatically selects text fields and a chunking
strategy for each field. You can deselect the checkbox and create a search index
configuration later if you choose not to do so now.
11. Click Next. (if you created a search index configuration, review the details, and save
your work).
Now that you have created a connection from the external blob storage, you are ready
to set up a file notification pipeline. This will notify Data Cloud whenever files are
added, updated, or deleted from your blob storage.
Step 3: Create File Notifications
File Notifications allow you to receive notifications whenever data files are added, updated, or
deleted from your external blob storage. This allows Data Cloud to know when to pick up new or
updated files from your external blob storage. The steps you follow will vary depending on
where your unstructured data is stored. You will want to follow the following steps in with your
external blob storage:
1. Create a Private-Public Key Pair and Certificate
2. Set up a Connected App and OAuth Settings
3. Download the Installer Script and Function specific to your external blob storage
4. Install the Script Setup with macOS or Linux
Step 4: Create a Search Index
Follow a few automated steps to create a hybrid search index configuration for an unstructured
data model object (UDMO). Data Cloud automatically applies defaults for the chunking and
vectorization strategies and creates chunk and index model objects. Chunking is important for
this process because we want to break it down into manageable meaningful chunks. This will allow
the data to be added to the Data Cloud search index and retrieved in search results.
Vectorization is the process of embedding your unstructured data into numerical representations
of data that machines can read. With easy setup, Salesforce will create a Search Index for us
that selects these defaults:
● Chunking strategy: Passage extraction
● Embedding model: E5-Large V2
● Search Type: Hybrid Search
These steps will create a search index:
1. From App Launcher, select Data Cloud.
2. In Data Cloud, click Search Index > New.
3. Click Easy Setup > Next.
4. From the New Search Index Configuration page, select a Data Space and one or more
UDMOs. A search index configuration is created for each object that you select.
5. Add a Search Index Configuration Name and Search Index Configuration API Name.
6. Click Next.
7. Review the configuration and the target data model objects, and click Save.
Step 5: Run the Search Query
Once your unstructured data has been chunked and vectorized, Data Cloud makes it easy to
perform searches on your unstructured data using prompt templates. When we created our
Search Index for Sunshine Trails Hospitality, we selected the Search Type of Hybrid. Hybrid
Searches merge the retrieved information including the vector search and keyword search and
rank the results to show the most relevant information.
With vector search and Einstein Copilot queries, you can search across structured and
unstructured data sources, and receive summarized responses that improve efficiency and
accuracy.
When running a search query, Einstein Copilot will follow these steps:
1. Einstein Copilot triggers a prompt template.
2. The prompt initiates a retriever, which is sent to Data Cloud vector search.
3. Data Cloud vector search retrieves matching excerpts from relevant unstructured data.
4. The prompt template is populated and sent to a large language model (LLM) for
summarization.
5. The LLM processes and returns a summarized response to the prompt template.
6. This response is then relayed back to Einstein Copilot.
7. The response is displayed to the user.
Agenforce invokes the search of your unstructured data. Once the unstructured data has been
brought into Salesforce using a prompt template, you will be able to begin to retrieve the data to
get relevant customer data.
Integrating Knowledge Article Data
Knowledge Articles contain both structured and unstructured data, this can be powerful data to
ground your Service Replies and prompts to understand a customer's use case. Knowledge
objects contain default mappings to the relevant DMOs in Data Cloud to save you time.
1. Create a new Data Stream in Data Cloud with the Salesforce CRM data source.
2. Select the Knowledge object.
3. Review the fields for the Knowledge objects included in your data stream.
a. Standard fields from the objects in your data kit are automatically mapped to the
relevant data model objects in Data Cloud. However, you must manually map any
custom fields.
4. Deselect any fields not required for your data stream.
5. Review the new data streams and objects to be deployed, and click Deploy.
Understanding Einstein Data Library
Einstein Data Libraries allow you to improve accuracy, add personalization, and build trust in
Einstein’s responses. Einstein Data Libraries can be another way to bring unstructured data
such as PDF. For our example of Sunshine Trails Hospitality, important information such as
FAQs, and Safety policies are stored in PDF. By uploading these PDFs to our Data Library this
allows Einstein to check the accuracy of responses against Sunshine Trails Hospitality’s unique
policies and information. To get started:
Step 1: Create and Configure a Data Library
Data Libraries allow you to create an index of Knowledge articles and fields or file uploads. This
determines where Einstein knows which information to base its responses on.
1. From the Einstein Data Library setup > select New Library.
2. Select a data space. After you choose a data space, you can’t change it later.
3. Enter a library name, and optionally, enter a description.
4. Click Save.
Step 2: Choose a Data Source for your Library
You will then select a Data Source for your Library either Knowledge or file uploads for the
library’s data source. A data library can’t support Knowledge and file uploads simultaneously.
Once you’ve saved your selections, data streams, a search index, and a retriever are created
automatically and available to view or edit in Data Cloud.
You can create multiple data libraries and assign them to multiple features such as
Agentforce, but each feature can only use one data library at a time.
Step 3: Assign Data Libraries to Agentforce
Once created, you will use your Data Library to ground your agent responses. Navigate to
Agent Builder and the Knowledge section. You will select the desired Data Source for your
agent. You can always adjust this selection or manage data sources later in the Agent Builder.
Best Practices
Common Discovery Questions Design Considerations
● Understanding the volume and types of
data across systems.
● Filter data from the source if the data is
not needed in Data Cloud
● Details about the systems where data is ● Ensure you choose the correct UDMO.
stored
● When unstructured data in the form of
files is connected to Data Cloud from an
external blob store, there are no billing
implications.
● In Data Cloud, unstructured data may
be chunked and vectorized using an
embedding model. understanding the
volume and types of data across
systems.
Conclusion
By utilizing Data Cloud, businesses can transform complex, unstructured data into actionable
insights. Data Cloud can ground Agentforce with customer insights, preferences, sentiment, and
more. Data Cloud’s ability to connect to external blob stores, create unstructured data lake
objects, and perform search queries provides a seamless process for managing unstructured
data. With the integration of Knowledge Article Data, businesses can further enhance their
service responses and understand customer use cases better. Salesforce Data Cloud offers a
comprehensive solution for managing and leveraging both structured and unstructured data,
enabling businesses to deliver deeper insights and enhanced customer experiences.

