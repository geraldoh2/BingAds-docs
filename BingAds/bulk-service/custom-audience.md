---
title: "Custom Audience Record - Bulk"
ms.service: bing-ads-bulk-service
ms.topic: "article"
author: "eric-urban"
ms.author: "eur"
description: Describes the Custom Audience fields in a Bulk file.
dev_langs:
  - csharp
---
# Custom Audience Record - Bulk
Defines a custom audience that can be downloaded and uploaded in a bulk file. 

> [!NOTE]
> Only update of the *Description* is supported for upload. You cannot add or delete a custom audience using the Bing Ads API.

> [!NOTE]
> Not everyone has this feature yet. If you don’t, don’t worry. It’s coming soon.

## <a name="entitydata"></a>Attribute Fields in the Bulk File
For a *Custom Audience* record, the following attribute fields are available in the [Bulk File Schema](../bulk-service/bulk-file-schema.md). 

- [Audience](#audience)
- [Client Id](#clientid)
- [Description](#description)
- [Id](#id)
- [Membership Duration](#membershipduration)
- [Modified Time](#modifiedtime)
- [Parent Id](#parentid)
- [Scope](#scope)
- [Status](#status)

You can download all fields of the *Custom Audience* record by including the [DownloadEntity](../bulk-service/downloadentity.md) value of *CustomAudiences* in the [DownloadCampaignsByAccountIds](../bulk-service/downloadcampaignsbyaccountids.md) or [DownloadCampaignsByCampaignIds](../bulk-service/downloadcampaignsbycampaignids.md) service request. Additionally the download request must include the [DataScope](../bulk-service/datascope.md) value of *EntityData*. For more information, see [Bulk Download and Upload](~/guides/bulk-download-upload.md).

The following Bulk CSV example would update the description and membership duration of a custom audience. 

```csv
Type,Status,Id,Parent Id,Client Id,Modified Time,Name,Description,Membership Duration,Scope,Audience,Remarketing Targeting Setting,
Format Version,,,,,,5,,,,,
Custom Audience,Active,IdHere,ParentIdHere,ClientIdGoesHere,,,Updated Custom Audience Description,30,Account,Custom Audience,,
```

If you are using the [Bing Ads SDKs](~/guides/client-libraries.md) for .NET, Java, or Python, you can save time using the *BulkServiceManager* to upload and download the *BulkCustomAudience* class, instead of calling the service operations directly and writing custom code to parse each field in the bulk file. 


```csharp
var uploadEntities = new List<BulkEntity>();

// Map properties in the Bulk file to the BulkCustomAudience
var bulkCustomAudience = new BulkCustomAudience
{
    // 'Client Id' column header in the Bulk file
    ClientId = "ClientIdGoesHere",

    // Map properties in the Bulk file to the 
    // CustomAudience object of the Campaign Management service.
    CustomAudience = new CustomAudience
    {
        // 'Description' column header in the Bulk file
        Description = "Updated Custom Audience Description",
        // 'Id' column header in the Bulk file
        Id = customAudienceIdKey,
        // 'Membership Duration' column header in the Bulk file
        MembershipDuration = null,
        // 'Audience' column header in the Bulk file
        Name = null,
        // 'Parent Id' column header in the Bulk file
        ParentId = accountIdKey,
        // 'Scope' column header in the Bulk file
        Scope = null,
    },
                
    // 'Status' column header in the Bulk file
    Status = Status.Active
};

uploadEntities.Add(bulkCustomAudience);

var entityUploadParameters = new EntityUploadParameters
{
    Entities = uploadEntities,
    ResponseMode = ResponseMode.ErrorsAndResults,
    ResultFileDirectory = FileDirectory,
    ResultFileName = DownloadFileName,
    OverwriteResultFile = true,
};

var uploadResultEntities = (await BulkService.UploadEntitiesAsync(entityUploadParameters)).ToList();
```

### <a name="audience"></a>Audience
The name of the custom audience.

The name can contain a maximum of 128 characters

**Add:** Not supported  
**Update:** Read-only    
**Delete:** Not supported  

### <a name="clientid"></a>Client Id
Used to associate records in the bulk upload file with records in the results file. The value of this field is not used or stored by the server; it is simply copied from the uploaded record to the corresponding result record. It may be any valid string to up 100 in length.

**Add:** Not supported  
**Update:** Optional    
**Delete:** Not supported  

### <a name="description"></a>Description
The description of the custom audience. Use a description to help you remember what audience you are targeting with this custom audience.

The description can contain a maximum of 1,024 characters.

**Add:** Not supported  
**Update:** Optional    
**Delete:** Not supported  

### <a name="id"></a>Id
The system generated identifier of the custom audience.

**Add:** Not supported  
**Update:** Required  
**Delete:** Not supported  

### <a name="membershipduration"></a>Membership Duration
The membership duration determines how far back in time Bing Ads should look for actions that match your custom audience definition in order to add people to your list. For a custom audience the membership duration is not set in the Bing Ads web application, and Bing Ads defers to your custom audience provider settings.

When you request the custom audience via Bing Ads API, the returned membership duration will be null.

**Add:** Not supported  
**Update:** Not supported  
**Delete:** Not supported  

### <a name="modifiedtime"></a>Modified Time
The date and time that the entity was last updated. The value is in Coordinated Universal Time (UTC).

> [!NOTE]
> The date and time value reflects the date and time at the server, not the client. For information about the format of the date and time, see the dateTime entry in [Primitive XML Data Types](https://go.microsoft.com/fwlink/?linkid=859198).

**Add:** Not supported  
**Update:** Read-only  
**Delete:** Not supported  

### <a name="parentid"></a>Parent Id
The system generated identifier of the account or customer. If the *Scope* is set to *Account*, this is the account ID, and otherwise it is the customer ID.

**Add:** Not supported  
**Update:** Required  
**Delete:** Not supported  

### <a name="scope"></a>Scope
Scope defines what accounts can use this custom audience. If scope is set to *Account*, the custom audience can only be associated with ad groups within one specified account (*Parent Id*). If scope is set to *Customer*, the custom audience can be associated with any ad groups across all of the customer's accounts.

**Add:** Not supported  
**Update:** Read-only    
**Delete:** Not supported  

### <a name="status"></a>Status
The custom audience status.

Possible values are *Active* or *Deleted*. 

**Add:** Not supported  
**Update:** Read-only    
**Delete:** Not supported

