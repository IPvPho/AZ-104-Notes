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

#### *Storage Account Performance and Access Tiers*

*Standard:*

> - All storage account types
> - Backup and disaster recovery data
> - Media

*Premium:*

> - Available for:
>   - BlockBlob Storage
>   - FileStorage
>   - GPv1 & GPv2 (unmanaged VHDs only)
> - Interactive
> - Analytics
> - AI/ML

*No Conversion after deployment available!*

#### *Access Tiers*

*Hot:*

> - Highest Storage Cost
> - Lowest Access Cost

*Cool:*

> - Lower Storage Cost
> - Higher Access Cost
> - 30 Day Minimum before access

*Archive:*

> - Lowest Storage Cost
> - Highest Access Cost
> - 180 Day minimum before access or deletion, otherwise penalties will be incurred. 


### *Replication Options*

> - Local-Redundant Storage (LRS)
> - Zone-Redundant Storage (ZRS)
> - Geo-Redundant Storage (GRS)
> - Geo-Zone-Redundant Storage (GZRS)
> - Read-Access Geo-Redundant Storage (RA-GRS)
> - Read-Access Geo-Zone-Redundant Storage (RA-GZRS)

*Replication Questions to ask:*

> - What if an Azure DC fails?
> - What is an Azure Regions fails?
> - Do you need Read access?

#### *Redundancy in Primary Region*

*LRS:*

> - Minimum level of redundancy for Azure 
> - Provide 3 copies of storage in a primary region
> - Single physical location / availability zone

*ZRS:*

> - 3 copies in a primary region
> - Each copy in a separate availability zone, will survive a DC outage 
> - Resiliency in a single region

#### *Redundancy in a Secondary Region*

*GRS:*

> - 3 copies in a single location
> - 3 anchored copies in a second region chosen by Microsoft (Read-Only, must be initiated after failover)
> - Protects from loss of an entire region, not from a single DC within your primary region.
> - LRS in both primary and secondary region

*GZRS:*

> - 3 copies spread across 3 AZ's in a region
> - 3 copies stored in a second region (Read-Only if primary goes offline)
> - ZRS in Primary region, LRS in secondary region
> - Will survive a DC loss in primary region, as well as primary region going offline
> - You or Microsoft must initiate failover

#### *Read Access in a Secondary Region*

> - Read-Only without Failover
> - Applications can use secondary storage
> - Available in Geo-redundant storage 
>  - Read-Access Geo-Redundant Storage (RA-GRS)
>  - Read-Access Geo-Zone-Redundant Storage (RA-GZRS)
> - Append *-secondary* to storage account name (https://"StorageAcctName"-secondary.blob.core.windows.net)


#### **Azure Storage and Durability and Availability Scenarios**

|Outage Scenario      |LRS   |ZRS   |GRS / RA-GRS   |GZRS / RA-GZRS   |
|:-:|:-:|:-:|:-:|:-:|
| DC node becomes unavailable  |YES   |YES   |YES   |YES   |
| Entire DC becomes unavailable  |NO   |YES   |YES   |YES   |
| Primary region-wide outage   |NO   |NO   |YES   |YES   |
| Read access when in secondary region when primary is unavailable   |NO   |NO   |YES (with RS-GRS)   | YES (with RA-GZRS)   |

#### **Storage Account Supported Capabilities**

|    Account Type    | Data Objects                                    | Performance Tiers            | Access Tiers       | Replication Options                                      |
|:------------------:|-------------------------------------------------|------------------------------|--------------------|----------------------------------------------------------|
| General Purpose v2 | Blob, File, Table Disk, Queue & Data Lake gen 2 | Standard Premium (Disk Only) | Hot, Cool, Archive | LRS, GRS, RA-GRS, ZRS, GZRS (preview), RA-GZRS (preview) |
| General Purpose v1 | Blob, File, Queue, Table and Disk               | Standard Premium (Disk Only) | N/A                | LRS, GRS, RA-GRS                                         |
| BlockBlobStorage   | Blob (block blobs and append blobs)             | Premium                      | N/A                | LRS, ZRS                                                 |
| FileStorage        | File Only                                       | Premium                      | N/A                | LRS, ZRS                                                 |
| BlobStorage        | Blob (block blobs and append blobs)             | Standard                     | Hot, Cool, Archive |  LRS, GRS, RA-GRS                                        |

---
## **Data Storage Authorization**


> - Anonymous
>   - Azure blobs only
> - Authenticated
>   - Shared Key Authorization
>   - Shared Access Signatures (SAS)
>  - Azure AD

#### *Authorizing Access to Azure Storage Data*

|                    | Shared Key (Storage Account Key( | Shared Access Signature (SAS) | Azure AD                                       | Anonymous Public Read Access |
|--------------------|----------------------------------|-------------------------------|------------------------------------------------|------------------------------|
| Azure Blobs        | Supported                        | Supported                     | Supported                                      | Supported                    |
| Azure Files (SMB)  | Supported                        | Not Supported                 | *Supported using Azure AD Domain Services Only | Not Supported                |
| Azure Files (REST) | Supported                        | Supported                     | Not Supported                                  | Not Supported                |
| Azure Queues       | Supported                        | Supported                     | Supported                                      | Not Supported                |
| Azure Tables       | Supported                        | Supported                     | Not Supported                                  | Not Supported                |

