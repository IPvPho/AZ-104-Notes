[//] <> (AZ-104 Notes | Michael Bender | Pluralsight)

# <ins>***Configure Azure Files and Blob Storage***</ins>
---

### <ins>*Azure File Share*</ins>

> - Cloud-based SMB or NFS file share
> - Accessible from Windows, MacOS, and Linux
> - Clients use Port 445 (check prior that it's open)
>   - 445 is a known attack vector, not recommended to use file share for public protection resources, use Site-to-Site VPN or ExpressRoute
> - Supported in GPv1, GPv2, and FileStorage accounts
> - Replication available depending on storage account


### <ins>*Azure File Share Requirements:*</ins>

> 1. Performance
> 2. Sizing
> 3. Redundancy

#### <ins>*Azure File Share Options*</ins>


|            | Max Size of File Share                   | Performance Tiers | Access Tiers                     | Replication Options                |
|:----------:|------------------------------------------|-------------------|----------------------------------|------------------------------------|
| GPv2       | 5 TB default Up to 100 TiB upon request | Standard          | Hot, Cool, Archive,  Transaction Optimized | LRS, GRS, ZRS, GZRS                |
| GPv1       | 5 TB default Up to 100 TiB upon request | Standard          | N/A                              | LRS, GRS                           |
| FieStorage | 100 TB default                          | Premium           | N/A                              | LRS, ZRS (small subset of regions) |


#### <ins>*Creating Azure File Share with Azure CLI*</ins>

```Bash
> az storage share create \
> --account-name <storageAccountName> \
> --account-key <storageAccountKey> \ or --sas-key <SharedAccessSignatureKey>
> --name <shareName> \
> --quota <SizeInGB>
```
#### <ins>*Creating a Directory within the File Share in Azure CLI*</ins>

```Bash
> az storage directory create \
> --account-name <storageAccountName> \
> --account-key <storageAccountKey> \ or --sas-key <SharedAccessSignatureKey>
> --share-name <FileShareName> \
> --name "<DirectoryName>"
```

#### <ins>*Uploading a file to the File Share with Azure CLI*</ins>

```Bash
> az storage file upload \
> --account-name <storageAccountName> \
> --account-key <storageAccountKey> \ or --sas-key <SharedAccessSignatureKey>
> --share-name <FileShareName> \
> --source "<SourceFile>" \
> --path "<DirectoryName>/<FileName>"
```


### <ins>*Azure Files Access Tiers*</ins>
---

> 1. **Hot:**
>       - Storage optimized for general file share purposes (organizational and Azure file sync)
>       - Storage cost is higher
>       - Access cost is lower
> 2. **Cool:**
>       - Cost efficient storage optimized for online archive storage scenarios
>       - Lower cost of storage
>       - Access cost is higher as it is intended not to be accessed as often as Hot tier
> 3. **Transaction Optimized:**
>       - Transaction heavy workloads that do not need lower-latency
>       - Highest storage-at-rest cost
>       - Lowest access cost per transaction compared to above
>       - Great for applications requiring file shares or backend storage

### <ins>*Authentication*</ins>

> - AAD Domain Services and AD Domain Services
>   - Provides identity-based access for hybrid environments
>   - Allows granular share-level and file-level permissions
> - Storage Account Keys or Shared Access Signatures
>   - Less granular control
>  - **Secure the keys** (best for limited access)

#### <ins>*Azure File Sync*</ins>

> - Provides an on-premises caching solution on Windows Server
> - Replicates data between on-premises DCs and Azure
> - Integrates with Azure File Shares
> - Seamless integration into file share infrastructure


#### <ins>*Azure File Sync Management Components*</ins>

> - **Cloud Endpoint:** 
>  - Azure File Share being synced
> - **Server Endpoint:**
>  - Local server with windows file system path being synced with Azure File Sync and Azure File Share
>  - Define local system path within your sync group 
> - **Sync Group:**
>  - Defines relationship between Cloud endpoint and Server endpoint
>  - Only one cloud endpoint allowed
>  - Multiple server endpoints allowed

![File Sync in Action](https://user-images.githubusercontent.com/3911650/49400286-0a9eb000-f701-11e8-95f9-4ff38170319c.png)

#### <ins>*Deploying Azure FIle Sync*</ins>

> 1. Deploy the Storage Sync Service
> 2. Create a sync group and cloud endpoint
> 3. Install the azure File Sync agent on Windows Server(s)
> 4. Register Windows Server with the Storage Sync Service
> 5. Create a server endpoint and wait for sync