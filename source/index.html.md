---
title: Tranxactor API v2.0.0
language_tabs:
  - http--request
  - http--response
toc_footers:
  - '2017 Tranxactor Group - All rights reserved'
includes: []
search: true
highlight_theme: darkula
---

# Transactor API -- Kupid Report v1.0.0

> Scroll down for code samples, example requests and responses. Select a language for code samples from the tabs above or the mobile navigation menu.

This API is designed for KUPID Point of Sales system administrator module. It provides all meta data for the client side building dashboard report and daily sales report.

<aside class="notice">
    All API sevice need authentication token to use, You need replese 'username', 'password', 'moduleCode' to get your auth token code. 
    You must replace `api_token` with your personal API auth token code for the rest services. 
</aside>

Base URL on Test Server= <a href="https://tr4ns2.tr4ns.com/TransactorAPI-SpringBoot/api/2/">https://tr4ns2.tr4ns.com/TransactorAPI-SpringBoot/api/2/</a>

# Authentication

> Authentication Example

````http--request
POST https://tr4ns2.tr4ns.com/TransactorAPI-SpringBoot/api/2/tokens HTTP/1.1
Host: tr4ns2.tr4ns.com
Content-Type: application/json
ModuleCode: <Your_ModuleCode>
Accept: application/json    

Body:
{
	"username":<Your_Username>,
	"password":<Your_Password>
}
````
````http--response
Body:
{
  "_links": {
    "member": {
      "href": "https://tr4ns2.tr4ns.com/TransactorAPI-SpringBoot/api/2/members/me"
    }
  },
  "token": "<API_Token>",
  "masterToken": "<Master_Token>",
  "expiration": "2017-05-05T00:34:25.285Z",
  "userId": "1",
  "userName": "<Your_Username>",
  "userType": "6",
  "module": "Your_ModuleCode"
}

````

- Client authentication. 
    - Flow: implicit
    - Authorization URL = [/tokens](https://tr4ns2.tr4ns.com/TransactorAPI-SpringBoot/api/2/tokens)

### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
moduleCode|head|String|true|Your Project API moduleCode|
username|body|String|true|Your API Client username|
password|body|String|true|Your Password|

### Response

Parameter|In|Type|Description
---|---|---|---|---|
token|body|String|Your Project API Auth Token code|

<aside class="notice">
    This auth token code is required for all other service in this package. 
</aside>

# KPUID Report [/kupid]

This package includes all kupid reporting related services.


## Get POS Totals Report
API PATH = [/posTotals](https://tr4ns2.tr4ns.com/TransactorAPI-SpringBoot/api/2/kupid/posTotals)

> GET POS Totals Report
````http--request
POST https://tr4ns2.tr4ns.com/TransactorAPI-SpringBoot/api/2/kupid/posTotals HTTP/1.1
Host: tr4ns2.tr4ns.com
Content-Type: application/json
ModuleCode: <Your_ModuleCode>
Authorization: <Your_Token>
Accept: application/json    

Body:
{
	"programId":"262",
	"startDate":"2017-04-02 12:00",
	"endDate":"2017-05-04 12:00",
	"deviceIds":[37951],
	"programUserId":"",
	"flGroupByDevice":"0",
	"flShowTax":"1"
}

````

````http--response
Body:
{
  "_links": {
    "self": {
      "href": "https://tr4ns2.tr4ns.com/TransactorAPI-SpringBoot/api/2/kupid/hourlyTotals"
    }
  },
  "_embedded": {
    "data": [
      {
        "number_of_transactions": "3",
        "discounts_amount": "0",
        "gross_sales_amount": "339.96",
        "net_sales_amount": "339.96",
        "loyalty_value_amount": "0",
        "credit_value_amount": "0",
        "tax_amount": "31.3018"
      }
    ]
  }
}

````
### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
programId|body|Nmuber|true|Your Program Id.
startDate|body|Date|true|The start date for your query. format="yyyy-MM-dd HH:mm"
endDate|body|Date|true|The end date for your query. format="yyyy-MM-dd HH:mm"
deviceIds|body|ARRAY|false|The devices which include in this query. If null, then all devices would be included.
programUserId|body|Number|false|Pet object that needs to be added to the store
flGroupByDevice|body|Number|false|group by device, default is 0.
flShowTax|body|Number|false|Show Tax amount, defalut is 1.



### Response

<aside class="success">
    If the flGroupByDevice parameter in request is 0, then store_id, store_name, device_id and device_name will be hiden in response message.
</aside>

Parameter|In|Type|Description
---|---|---|---|---|
number_of_transactions|body|String|The amount of transactions
discounts_amount|body|String|The amount of discounts
gross_sales_amount|body|String|The gross sales amount
net_sales_amount|body|String|The net sales amount
loyalty_value_amount|body|String|The loyalty value amount
credit_value_amount|body|String|The credit value amount
tax_amount|body|String|The tax amount
store_id|body|String|Store ID
store_name|body|String|Store Name
device_id|body|String|Device ID
device_name|body|String|Device Name


## Get Hourly Totals Report
API PATH = [/hourlyTotals](https://tr4ns2.tr4ns.com/TransactorAPI-SpringBoot/api/2/kupid/hourlyTotals)

> GET Hourly Totals Report
````http--request
POST https://tr4ns2.tr4ns.com/TransactorAPI-SpringBoot/api/2/kupid/hourlyTotals HTTP/1.1
Host: tr4ns2.tr4ns.com
Content-Type: application/json
ModuleCode: <Your_ModuleCode>
Authorization: <Your_Token>
Accept: application/json    

Body:
{
	"programId":"262",
	"startDate":"2017-04-02 12:00",
	"endDate":"2017-05-04 12:00",
	"deviceIds":[37951],
	"programUserId":"",
	"flGroupByDevice":"0",
	"flShowTax":"1"
}

````

````http--response
Body:
{
  "_links": {
    "self": {
      "href": "https://tr4ns2.tr4ns.com/TransactorAPI-SpringBoot/api/2/kupid/hourlyTotals"
    }
  },
  "_embedded": {
    "data": [
      {
        "number_of_transactions": "3"
      }
    ]
  }
}

````
### Parameters

Parameter|In|Type|Required|Description
---|---|---|---|---|
programId|body|Nmuber|true|Your Program Id.
startDate|body|Date|true|The start date for your query. format="yyyy-MM-dd HH:mm"
endDate|body|Date|true|The end date for your query. format="yyyy-MM-dd HH:mm"
deviceIds|body|ARRAY|false|The devices which include in this query. If null, then all devices would be included.
programUserId|body|Number|false|Pet object that needs to be added to the store
flGroupByDevice|body|Number|false|group by device, default is 0.
flShowTax|body|Number|false|Show Tax amount, defalut is 1.



### Response

<aside class="success">
    If the flGroupByDevice parameter in request is 0, then store_id, store_name, device_id and device_name will be hiden in response message.
</aside>

Parameter|In|Type|Description
---|---|---|---|---|
number_of_transactions|body|String|The amount of transactions
discounts_amount|body|String|The amount of discounts
gross_sales_amount|body|String|The gross sales amount
net_sales_amount|body|String|The net sales amount
loyalty_value_amount|body|String|The loyalty value amount
credit_value_amount|body|String|The credit value amount
tax_amount|body|String|The tax amount
store_id|body|String|Store ID
store_name|body|String|Store Name
device_id|body|String|Device ID
device_name|body|String|Device Name


