[//]: <> (AZ-104 Notes | Tim Warner | Pluralsight)

# ***Manage Storage Accounts***
---
## **Azure Storage Data Objects**
---
> - Contains all Azure storage objects
> - Unique namespace access to storage resources 
>   - Ex: https://stbloblstorage001.blob.core.windows.net/demo/az-104-outline.pdf
> - Highly Available
> - Secure & Scalable

#### *Data Types:*

 - Blob
 - File
 - Queue
 - Table
 - Disk

#### *Types of Storage Accounts*

> - General-purpose v2
>   - All types of Azure storage data objects, supports Data Lake Gen 2 data, recommended for most use cases
> - General-purpose v1
>   - Legacy accounts for blobs, files, queues and tables (upgrade to v1 when possible)
> - BlockBlobStorage
>   - Premium performance only for BlockBlobs and AppendBlobs, useful for scenarios with low storage latency, higher transaction rates, and the data objects are smaller.
> - FileStorage
>   - Premium tier performance for Files, only stores files, enterprise applications or high-performance scale applications
> - BlobStorage
>   - Legacy Blob only storage account (use General-purpose v2 whenever possible)


#### *Azure Storage Endpoint for BlobStorage*

```
https://sa-bloblstore-eastus-001.blob.core.windows.net/demo/az-104-outline.pdf

Storage Account Name == sa-bloblstore-eastus-00

Storage Service Endpoint == blob.core.windows.net

Object Name == az-104-outline.pdf
```
