---
title: API Reference

language_tabs: # must be one of https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers
  - plaintext

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Prodigy API
---

# Prodigy API Documentation

//START of section - Do NOT copy this section to CMS//
This is Work in Progress documentation for the Prodigy API suite. The current structure of this document is a mix of competitive and first party content. The overall structure and content will change significantly.

Customers will use our API to post and get information. There will be multiple APIs to document. A customer may use one or more of these APIs to complete tasks within our system.

<b> APIs to be documented </b>

API | Description
--------- |------------
FIX |   FIX (Financial Information eXchange) API is a messaging protocol that is commonly used in the electronic trading industry to enter orders, submit cancel requests, and receive fills. This is intended to be used in conjunction with the FIX 4.4 Protocol Specification.
Websocket |The WebSocket API makes it possible to open a two-way interactive communication session between the user's browser and a server. With this API, you can send messages to a server and receive event-driven responses without having to poll the server for a reply. 
stunnel | Stunnel is a proxy designed to add TLS encryption functionality to existing clients and servers without any changes in the programs' code. Stunnel uses the OpenSSL library for cryptography, so it supports whatever cryptographic algorithms are compiled into the library.       

<b>Style</b>  
The final documentation should adhere to the following conventions:
Minimal prose. Keep the prose simple and functional. APIs are typically used by subject matter experts, thus the syntax and code are most important and should not be buried within or after long prose explanations.
San-serif font for prose, serif for code.
Precise coding examples that can be copied for ease of use. Code must be properly indented.
If there are multiple steps in a process, provide an overview of each step before the detailed example for each.
Clear mathematical formulae where applicable. (Mathematical formulae will more likely appear in our application documentation.)

//END of section//

# <b>Table of Contents</b>

Overview 
Websocket API 
  Currently Supported Instruments
  Connectivity (alpha)
  Authorization
  Depth of Market Subscription (depth)
  Price Info Subscription (price_info)
  Websocket Availability
  Websocket FAQ
stunnel Connectivity
  Setup a client-side stunnel to connect to Prodigy’s CLOB
FIX API
  Logon <A>
    Anatomy of a Logon Message
  Logout <5>
    Anatomy of a Logout Message
  NewOrderSingle <D>
    Anatomy of a NewOrderSingle Message
  OrderCancelRequest <F>
    Anatomy of a OrderCancelRequest Message
  OrderMassStatus <AF>
    Anatomy of a OrderMassStatus Message
  TradeCaptureReportRequest <AD>
    Anatomy of a TradeCaptureReportRequest Message




# <b> Overview </b>

This document describes the API for the Prodigy decentralized exchange.

By using any API provided by Prodigy, you agree to its Terms of Use and Privacy Policy.

## Currently Supported Instruments
BTC-USD: Bitcoin/USD spot price

# Depth of Market Subscription (depth)

Gets depth data for a market.
## Subscribe Message
Gets depth data for a market.

```plaintext
{
'user': 'g',
'action': 'subscribe',
'type': 'depth',
'value': ['BTC-USD'],
"token":"<provided by Prodigy>"
};

```
## Response
The initial depth data response returns information about the market and its current buy and sell levels with data that describes the depth at each level.

Data | Definition
--------- |------------
Denominator | Factor to divide <Price> by for USD value      
available | true       


```plaintext
{
  "data": {
"Denominator":"100",
"DisplaySymbol":"BTC-USD",
"SecurityID":"1000000189",
"Symbol":"BTC-USD",
"buy_levels": [...
{
"NumOfOrders": "10",
"Price": "2037600",
"Qty": "4660000",
},
...],
"sell_levels": [...
{
"NumOfOrders": "7",
"Price": "2056150",
"Qty": "6370000",
},
...],
},
  "Type":3
}


```

Use the `Logon <A>` message to authenticate a user establishing a connection to a remote system. The `Logon <A>` message must be the first message sent by the application requesting to initiate a FIX session.



## Setup a client-side stunnel to connect to Prodigy’s CLOB

<b>Important environment variables:</b>

`export CLOB_HOST=clob-alpha.prodigy`

`export STUNNEL_PORT=[THE_LOCAL_PORT_TO_OPEN]`


# Kittens

## Get All Kittens

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens" \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2" \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2" \
  -X DELETE \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

