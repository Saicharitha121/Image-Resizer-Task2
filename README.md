# Image-Resizer-Task2

Auto-Index Blob Metadata into Cosmos DB:----

This project automatically indexes metadata and text details from blobs uploaded into the documents container. When a new blob is created, Event Grid triggers a Function App, which extracts metadata + content and stores an indexed record in Cosmos DB.

**Prerequisites**: 
Azure Resources Required

1. Storage Account
   
- Must have a documents container.
  
- Event Grid must be enabled for blob-created events.

2. Azure Function App

Language: Python or C#

Must support Event Grid trigger.

3. Cosmos DB (Core SQL API)

- Database: DocumentsDB

- Container: Documents (Partition key: /id)

- Unique key: /id (to prevent duplicates)


**Local Development Requirements**

Visual Studio Code / Visual Studio

- Azure Functions Core Tools

- Python 3.9+ (if using Python implementation)

- Azure CLI

- Python libraries
  

**Event Flow Overview**

- A new blob is uploaded to documents container.

- Storage Account sends BlobCreated event to Event Grid.

- Event Grid triggers Azure Function.

Function extracts:

blobName
container
URL
contentType
size
title (first H1 or first line)
wordCount (for text files)
Inserts/upserts document into Cosmos DB with

**Expected Output**

- Cosmos DB contains a record for every uploaded blob.

- Re-uploading the same file updates the existing document.

- Function logs show successful indexing.
