---
title: "Content API Overview"
description: "Describes the Content API, what it does, and who should use it."
author: "swhite-msft"
manager: "ehansen"

ms.service: "shopping-content-api"
ms.topic: "article"
ms.author: "scottwhi"
---
# Content API Overview
Bing Ads Content API is a RESTful API that allows advertisers to programmatically 
manage their [Bing Merchant Center](http://help.bingads.microsoft.com/#apex/3/en/51083/1) catalogs. The Content API is an alternative to managing your catalog using the Bing Merchant Center web page or by using FTP. The Content API has the following advantages:

-   Provides the ability to update product offers incrementally rather than uploading the entire data feed. Being able to update  a subset of your products is more efficient than having to upload the entire feed by using FTP.

-   Provides the ability to make changes to product pricing and availability to reflect close to real-time market conditions. For example, if your product goes out of stock, you can quickly update its Availability field using the Content API.

-   Provides the ability to batch together large numbers of items to process in a single request. A batch operation can include inserts, deletes, and updates. Using batch operations is a more efficient use of resources than using single operation calls (for example, a single insert operation).

-   Provides the ability to download catalog status reports.

-   Provides the ability to manage your catalogs programmatically.


## Who Should Use the API?
You should consider using the Content API if:

-   You are currently using the Google Content API. 

-   Your feed includes a large number of products.

-   You are able to integrate the Content API with the rest of your inventory management systems.

If your catalog is small, or you have a limited ability to integrate with your inventory systems, you may be better off using one of the other methods for uploading your catalog (see [Submit your feed file](http://help.bingads.microsoft.com/#apex/3/en/51086/1)).

# Get Started with the Content API

To quickly get started making calls to the Content API, see [Bing Ads Content API Quickstart](./quickstart.md) 

## <a name="credentials"/> Do you have your Bing Ads credentials and developer token?
To use the Content API, you must have a Bing Ads account and credentials. New users to Bing Ads must use a Microsoft account to access Bing Ads. Current users that haven't transitioned to a Microsoft account may use their Bing Ads user name. 

To get a Bing Ads account, go to [http://bingads.microsoft.com](http://bingads.microsoft.com). If you're not signed in to your Microsoft account, you'll be redirected to sign in to your Microsoft account or sign up for a Microsoft account. After signing in, you'll have the option to **Sign up for a new Bing Ads account**. Select the sign up option and **Continue** with the sign up process.

Next, you'll need a developer token. To get a token to use in the production environment, see [Bing Ads Developer Portal](https://developers.bingads.microsoft.com/account). Click **Request Token** and provide the requested information. If you will be using the API to manage your own account, you'll receive your token immediately; however, if you'll be managing accounts for others, it may take up to five business days to get a token.

## <a name="authentication"/> Authenticating your credentials

Content API uses the same authentication schemes as Bing Ads API. If you use legacy credentials (i.e., username, password) with Bing Ads API, you may continue using them with Content API; however, customers are being asked to transition their legacy credentials to Microsoft account credentials. 

For details about authenticating Microsoft account credentials with OAuth, see [Managing User Authentication with OAuth](~/guides/authentication-oauth.md). You *can* use the [Bing Ads SDK](~/guides/client-libraries.md) for .NET, Java, or Python to authenticate both legacy and Microsoft account credentials (but only for authentication; the Bing Ads SDK does not provide interfaces for the Content API).

For an example that shows how to use OAuth to authenticate Microsoft account credentials, see [Authenticating Microsoft Account Credentials in C#](../shopping-content/code-example-authentication-oauth.md).

## Where to use your credentials and developer tokens?

All calls must specify the DeveloperToken header, and set it to the developer token that you were given.

All calls may specify either the AuthenticationToken header, if you use OAuth to authenticate your Microsoft account, or the UserName and Password headers, if you use legacy credentials.

If you manage catalogs on behalf of other customers, you must set the `CustomerId` header to the customer ID of the customer whose store you're managing, and the `CustomerAccountId` header to the account ID of any of the customer's accounts that you manage (it doesn't matter which managed account). 

For information about these and other headers that the request and response may contain, see [Headers](../shopping-content/products-resource.md#headers). 

## <a name="configurebmc"/> Configuring Bing Merchant Center to use the API

For an overview of Bing Merchant Center, see [What is Bing Merchant Center?](http://help.bingads.microsoft.com/#apex/3/en/51083/1) The topic includes links to all of the Merchant Center topics and related videos.

You must complete the following steps if you haven't already done so.

1. [Verify and claim your Website's URL](http://help.bingads.microsoft.com/#apex/3/en/50888/1)
  To get the webmaster tools mentioned in Verify and claim your Website's URL, see [Bing Webmaster Tools](http://www.bing.com/toolbox/webmaster). Sign in with the same Microsoft account that you use for Bing Ads. For more information about using the tool, see [Verify Ownership of Your Website](http://www.bing.com/webmaster/help/how-to-verify-ownership-of-your-site-afcfefc6). 
2. [Create a Bing Merchant Center store](http://help.bingads.microsoft.com/#apex/3/en/51085/1)
3. [Add a catalog](http://help.bingads.microsoft.com/#apex/3/en/51105/1)

When you create a BMC store, the process creates a default catalog for you. The store and all catalogs that you create are automatically enabled for API management. The store contains a default catalog that all product gets, inserts, updates, and deletes apply to unless you specify the [bmc-catalog-id](../shopping-content/products-resource.md#bmccatalogid) query parameter in the resource URL. 

The **Store Setting** tab contains the Tenant URL, which you use as the base URI of your resource URL.

As an alternative to adding and enabling catalogs using the BMC web application, you may use the [Catalogs](../shopping-content/catalogs-resource.md) resource. For more information, see [Managing your Catalogs](../shopping-content/manage-catalogs.md).

> [!NOTE] 
> You may be able to use the API with FTP in certain circumstances to update a catalog feed. For information about using the API with FTP, see [Can I Use the API and FTP?](../shopping-content/can-use-api-ftp.md). 


### In This Section

|Topic|Description|
|---------|---------------|
|[Release Notes](../shopping-content/release-notes.md)|Describes changes to the Bing Ads Content API for each release.|
|[Get Started](../shopping-content/get-started.md)|Provides the steps for getting started using the Bing Ads Content API.|
|[Testing your Code in Sandbox](../shopping-content/test-code-sandbox.md)|Provides options for testing your app before releasing it into production.|
|[API Best Practices](../shopping-content/api-best-practices.md)|Provides best practices for using the Bing Ads Content API.|
|[Managing your Products](../shopping-content/manage-products.md)|Provides details for how to use the [Products](../shopping-content/products-resource.md) resource to add, get, update, and delete product offers.|
|[Managing your Catalogs](../shopping-content/manage-catalogs.md)|Provides details for how to use the [Catalogs](../shopping-content/catalogs-resource.md) resource to add, get, update, and delete API enabled catalogs.|
|[How Do I Get the Status of Product Offers?](../shopping-content/how-get-status-product-offers.md)|Provides details for how to use the [Status](../shopping-content/catalogs-resource.md) resource to get the status of product offers in a catalog.|
|[Code Examples](../shopping-content/code-examples.md)|Provides C# code examples that show how to use Bing Ads Content API resources.|
|[Content API Reference](../shopping-content/reference.md)|Provides details about the programming elements of the Bing Ads Content API.|
