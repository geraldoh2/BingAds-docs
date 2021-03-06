---
title: Predicate Data Object - Customer Management
ms.service: bing-ads-customer-management-service
ms.topic: article
author: eric-urban
ms.author: eur
description: Defines a predicate for the list of entities requested using one of the search operations, for example SearchAccounts, [SearchClientLinks](../customer-management-service/searchclientlinks.md), or [SearchCustomers](../customer-management-service/searchcustomers.md).
---
# Predicate Data Object - Customer Management
Defines a predicate for the list of entities requested using one of the search operations, for example [SearchAccounts](../customer-management-service/searchaccounts.md), [SearchClientLinks](../customer-management-service/searchclientlinks.md), or [SearchCustomers](../customer-management-service/searchcustomers.md).

## Syntax
```xml
<xs:complexType name="Predicate" xmlns:xs="http://www.w3.org/2001/XMLSchema">
  <xs:sequence>
    <xs:element minOccurs="0" name="Field" nillable="true" type="xs:string" />
    <xs:element minOccurs="0" name="Operator" type="tns:PredicateOperator" />
    <xs:element minOccurs="0" name="Value" nillable="true" type="xs:string" />
  </xs:sequence>
</xs:complexType>
```

## <a name="elements"></a>Elements

|Element|Description|Data Type|
|-----------|---------------|-------------|
|<a name="field"></a>Field|The name of the element for  the object you are searching.<br /><br />For possible values, see the Predicates element of one of the search operations, for example [SearchAccounts](../customer-management-service/searchaccounts.md), [SearchClientLinks](../customer-management-service/searchclientlinks.md), or [SearchCustomers](../customer-management-service/searchcustomers.md).|**string**|
|<a name="operator"></a>Operator|Defines the relationship between the field and the value.|[PredicateOperator](predicateoperator.md)|
|<a name="value"></a>Value|The string to search in the specified field.<br /><br /> The length of this string must be four or greater, unless the field is set to MarketCountry or MarketLanguage.|**string**|

## Requirements
Service: [CustomerManagementService.svc v11](https://clientcenter.api.bingads.microsoft.com/Api/CustomerManagement/v11/CustomerManagementService.svc)  
Namespace: https\://bingads.microsoft.com/Customer/v11/Entities  

## Used By
[SearchAccounts](searchaccounts.md)  
[SearchClientLinks](searchclientlinks.md)  
[SearchCustomers](searchcustomers.md)  
[SearchUserInvitations](searchuserinvitations.md)  
