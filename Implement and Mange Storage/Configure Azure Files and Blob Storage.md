[//] <> (AZ-104 Notes | Michael Bender | Pluralsight)

# <ins>***Configure Azure Files and Blob Storage***</ins>
---

### <ins>*Azure File Share*</ins>

> - CLoud-based SMB or NFS file share
> - Accessible from Windows, MacOS, and Linux
> - Clients use Port 445 (check prior that it's open)
>   - 445 is a known attack vector, not recommended to use file share for public protection resources, use Site-to-Site VPN or ExpressRoute
> - Supported in GPv1, GPv2, and FileStorage accounts
> - Replication available depending on storage account


### <ins>*Azure File Share Requirements:*</ins>

1. Performance
2. Sizing
3. Redundancy

#### <ins>*Azure File Share Options*</ins>


|            | Max Size of File Share                   | Performance Tiers | Access Tiers                     | Replication Options                |
|:----------:|------------------------------------------|-------------------|----------------------------------|------------------------------------|
| GPv2       | 5 TiB default Up to 100 TiB upon request | Standard          | Hot, Cool, Archive,  Transaction Optimized | LRS, GRS, ZRS, GZRS                |
| GPv1       | 5 TiB default Up to 100 TiB upon request | Standard          | N/A                              | LRS, GRS                           |
| FieStorage | 100 TiB default                          | Premium           | N/A                              | LRS, ZRS (small subset of regions) |