---
title: API Documentation

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby
  - python
  - javascript
  - php

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the <app_name> API! You can use our API to access <app_name> API endpoints, which can get information on mobile messaging services - SMS and VOICE

You can view code examples in the dark area to the right. You can switch the programming language of the examples with the tabs in the top right.

# Authentication

> To authorize, use this code:

```ruby
require 'app_name'

api = AppName::APIClient.authorize!('Thequickbrownfoxjumpsoverthelazydog')
```

```python
import app_name

api = app_name.authorize('Thequickbrownfoxjumpsoverthelazydog')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: Thequickbrownfoxjumpsoverthelazydog"
```

```javascript
const app_name = require('app_name');

let api = app_name.authorize('Thequickbrownfoxjumpsoverthelazydog');
```

```php
<?
require 'app_name';
use AppName\APIClient;

$api = APIClient::authorize('Thequickbrownfoxjumpsoverthelazydog');
?>
```
> Make sure to replace `Thequickbrownfoxjumpsoverthelazydog` with your API key.

AppName uses API keys to allow access to the API. You can register a new AppName API key at our [developer portal](http://app-domain.com/developers).

AppName expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: Thequickbrownfoxjumpsoverthelazydog`

<aside class="notice">
You must replace <code>Thequickbrownfoxjumpsoverthelazydog</code> with your personal API key.
</aside>

# Send SMS

## Single SMS Messaging

```ruby
require 'app_name'

api = AppName::APIClient.authorize!('Thequickbrownfoxjumpsoverthelazydog')
response = api.messages.create(
    '25409907990',
    '25429907390',
    'Hi, Lets meet for coffee'
  )
  puts response
```

```python
import app_name

api = app_name.authorize('Thequickbrownfoxjumpsoverthelazydog')
response = api.messages.create(
    from='25409907990',
    to='25429907390',
    text='Hi, Lets meet for coffee')
print(response)
```

```shell
curl "http://app-domain.com/api/messages"
    -H "Content-Type: application/json" \
    -H "Authorization: Thequickbrownfoxjumpsoverthelazydog"
    -d '{"from": "25429907390","to": "25409907990", "text": "Hi, Lets meet for coffee"}'

```

```javascript
const app_name = require('app_name');

let api = app_name.authorize('Thequickbrownfoxjumpsoverthelazydog');
let response = api.messages.create(
      "25429907390", // from
      "25409907990", // to
      "Hi, Lets meet for coffee", // text
  );
  console.log(response);
```

```php
<?
require 'app_name';
use AppName\APIClient;

$api = AppClient::authorize('Thequickbrownfoxjumpsoverthelazydog');
$response = $api->messages->create(
      "25429907390", // from
      "25409907990", // to
      "Hi, Lets meet for coffee", // text
  );
  print_r($response);
?>
```
> The above command returns JSON structured like this:

```json
{
  "id": 134,
  "to": "25409907990",
  "status": "Successful",
  "message_price": "0.56"
}
```

This endpoint enables you to send messages.

### HTTP Request

<aside class="success">
POST http://app-domain.com/api/messages
</aside>

### Body Parameters

Parameter | Required | Description
--------- | ------- | -----------
to | true | Phone number of the recipient.
from | true | Phone number of the sender.
text | true | Message to be sent.

Sanitized phone numbers must begin with the international country code (ex: 254722000000), and should be <= 14 long

## Bulk SMS Messaging

It is possible to send one message to multiple recipients via a single API request.

Provide a list of recipient numbers separated with commas. (e.g. 254756667547, 254758778318, 254758809799).



```ruby
require 'app_name'

api = AppName::APIClient.authorize!('Thequickbrownfoxjumpsoverthelazydog')
response = api.messages.create(
    '254700900900',
    '25409907990, 25429907390, 25419907590, 25407907960',
    'Hi, the meeting has been moved to 4pm'
  )
  puts response
```

```python
import app_name

api = app_name.authorize('Thequickbrownfoxjumpsoverthelazydog')
response = api.messages.create(
    from='254700900900',
    to='25409907990, 25429907390, 25419907590, 25407907960',
    text='Hi, the meeting has been moved to 4pm')
print(response)
```

```shell
curl "http://app-domain.com/api/messages"
    -H "Content-Type: application/json" \
    -H "Authorization: Thequickbrownfoxjumpsoverthelazydog"
    -d '{"from": "254700900900","to": "25409907990, 25429907390, 25419907590, 25407907960", "text": "Hi, the meeting has been moved to 4pm"}' \

```

```javascript
const app_name = require('app_name');

let api = app_name.authorize('Thequickbrownfoxjumpsoverthelazydog');
let response = api.messages.create(
      "254700900900", // from
      "25409907990, 25429907390, 25419907590, 25407907960", // to
      "Hi, the meeting has been moved to 4pm", // text
  );
  console.log(response);
```

```php
<?
require 'app_name';
use AppName\AppClient;

$api = AppClient::authorize('Thequickbrownfoxjumpsoverthelazydog');
$response = api->messages->create(
      "254700900900", // from
      "25409907990, 25429907390, 25419907590, 25407907960", // to
      "Hi, the meeting has been moved to 4pm", // text
  );
  print_r($response);
?>
```

> The above command returns JSON structured like this:

```json
{
  "id": 128,
  "message_price": "1.31",
  "recipients": [
    {
      "msisdn": "25429907690",
      "status": "Successful"
    },
    {
      "msisdn": "25459907390",
      "status": "Failed"
    },
    {
      "msisdn": "25427907390",
      "status": "Successful"
    },
    {
      "msisdn": "25427807390",
      "status": "Successful"
    }
  ]
}
```

This endpoint enables you to send bulk messages.

### HTTP Request

<aside class="success">
POST http://app-domain.com/api/bulk-messages
</aside>

### Body Parameters

Parameter | Required | Description
--------- | ------- | -----------
to | true | Phone numbers of the recipients separated by commas.
from | true | Phone number of the sender.
text | true | Message to be sent.

# Send Voice Messages

## Single Voice Messaging

```ruby
require 'app_name'

api = AppName::APIClient.authorize!('Thequickbrownfoxjumpsoverthelazydog')
response = api.voice_messages.create(
    '25409907990',
    '25429907390',
    'Hi, Lets meet for coffee'
  )
  puts response
```

```python
import app_name

api = app_name.authorize('Thequickbrownfoxjumpsoverthelazydog')
response = api.voice_messages.create(
    from='25409907990',
    to='25429907390',
    text='Hi, Lets meet for coffee')
print(response)
```

```shell
curl "http://app-domain.com/api/voice-messages"
    -H "Content-Type: application/json" \
    -H "Authorization: Thequickbrownfoxjumpsoverthelazydog"
    -d '{"from": "25429907390","to": "25409907990", "text": "Hi, Lets meet for coffee"}'

```

```javascript
const app_name = require('app_name');

let api = app_name.authorize('Thequickbrownfoxjumpsoverthelazydog');
let response = api.voiceMessages.create(
      "25429907390", // from
      "25409907990", // to
      "Hi, Lets meet for coffee", // text
  );
  console.log(response);
```

```php
<?
require 'app_name';
use AppName\APIClient;

$api = AppClient::authorize('Thequickbrownfoxjumpsoverthelazydog');
$response = $api->voiceMessages->create(
      "25429907390", // from
      "25409907990", // to
      "Hi, Lets meet for coffee", // text
  );
  print_r($response);
?>
```
> The above command returns JSON structured like this:

```json
{
  "id": 124,
  "to": "25409907990",
  "status": "Successful",
  "voice_message_price": "1.13",
  "voice": "female",
  "language": "en-gb"
}
```

This endpoint enables you to send voice messages.

### HTTP Request

<aside class="success">
POST http://app-domain.com/api/voice-messages
</aside>

### Body Parameters

Parameter | Required | Description
--------- | ------- | -----------
to | true | Phone number of the recipient.
from | true | Phone number of the sender.
text | true | Voice message to be sent.
voice | false | The voice in which the messages needs to be read to the recipient. Possible values are: male, female.
Default: female
language | false | The language in which the message needs to be read to the recipient. Possible values are: <> Default: en-gb


Sanitized phone numbers must begin with the international country code (ex: 254722000000), and should be <= 14 long

## Bulk Voice Messaging

It is possible to send one voice message to multiple recipients via a single API request.

Provide a list of recipient numbers separated with commas. (e.g. 254756667547, 254758778318, 254758809799).



```ruby
require 'app_name'

api = AppName::APIClient.authorize!('Thequickbrownfoxjumpsoverthelazydog')
response = api.bulk_voice_messages.create(
    '254700900900',
    '25409907990, 25429907390, 25419907590, 25407907960',
    'Hi, the meeting has been moved to 4pm'
  )
  puts response
```

```python
import app_name

api = app_name.authorize('Thequickbrownfoxjumpsoverthelazydog')
response = api.bulk_voice_messages.create(
    from='254700900900',
    to='25409907990, 25429907390, 25419907590, 25407907960',
    text='Hi, the meeting has been moved to 4pm')
print(response)
```

```shell
curl "http://app-domain.com/api/bulk-voice-messages"
    -H "Content-Type: application/json" \
    -H "Authorization: Thequickbrownfoxjumpsoverthelazydog"
    -d '{"from": "254700900900","to": "25409907990, 25429907390, 25419907590, 25407907960' \
    ', "text": "Hi, the meeting has been moved to 4pm"}' \

```

```javascript
const app_name = require('app_name');

let api = app_name.authorize('Thequickbrownfoxjumpsoverthelazydog');
let response = api.bulkVoiceMessages.create(
      "254700900900", // from
      "25409907990, 25429907390, 25419907590, 25407907960", // to
      "Hi, the meeting has been moved to 4pm", // text
  );
  console.log(response);
```

```php
<?
require 'app_name';
use AppName\AppClient;

$api = AppClient::authorize('Thequickbrownfoxjumpsoverthelazydog');
$response = api->bulkVoiceMessages->create(
      "254700900900", // from
      "25409907990, 25429907390, 25419907590, 25407907960", // to
      "Hi, the meeting has been moved to 4pm", // text
  );
  print_r($response);
?>
```

> The above command returns JSON structured like this:

```json
  {
    "id": 128,
    "voice_message_price": "1.31",
    "voice": "female",
    "language": "en-gb",
    "recipients": [
      {
        "msisdn": "25429907690",
        "status": "Successful"
      },
      {
        "msisdn": "25459907390",
        "status": "Failed"
      },
      {
        "msisdn": "25427907390",
        "status": "Successful"
      },
      {
        "msisdn": "25427807390",
        "status": "Successful"
      }
    ]
  }
```

This endpoint enables you to send bulk voice messages.

### HTTP Request

<aside class="success">
POST http://app-domain.com/api/bulk-voice-messages
</aside>

### Body Parameters

Parameter | Required | Description
--------- | ------- | -----------
to | true | Phone numbers of the recipients separated by commas.
from | true | Phone number of the sender.
text | true | Voice message to be sent.
voice | false | The voice in which the messages needs to be read to the recipient. Possible values are: male, female.
Default: female
language | false | The language in which the message needs to be read to the recipient. Possible values are: <> Default: en-gb

# HLR Lookup
An HLR allows you to view details of a mobile number (MSISDN).

## Single HLR Lookup

```ruby
require 'app_name'

api = AppName::APIClient.authorize!('Thequickbrownfoxjumpsoverthelazydog')
response = api.hlr_lookup.search('25409907990')
puts response
```

```python
import app_name

api = app_name.authorize('Thequickbrownfoxjumpsoverthelazydog')
response = api.hlr_lookup.search(msisdn='25409907990')
print(response)
```

```shell
curl "http://app-domain.com/api/hlr-lookup?msisdn=25429907390"
    -H "Content-Type: application/json" \
    -H "Authorization: Thequickbrownfoxjumpsoverthelazydog"

```

```javascript
const app_name = require('app_name');

let api = app_name.authorize('Thequickbrownfoxjumpsoverthelazydog');
let response = api.hlrLookup.search("25429907390");
console.log(response);
```

```php
<?
require 'app_name';
use AppName\APIClient;

$api = AppClient::authorize('Thequickbrownfoxjumpsoverthelazydog');
$response = $api->hlrLookup->search("25429907390");
print_r($response);
?>
```
> The above command returns JSON structured like this:

```json
{
  "id": 1245,
  "msisdn": 25429907390,
  "status": "Active",
  "country_iso": "KE",
  "country_name": "Kenya"
}
```

This endpoint enables you search for phone number details.

### HTTP Request

<aside class="success">
GET http://app-domain.com/api/hlr-lookup?msisdn=xyz
</aside>

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
msisdn | true | Phone number you want to look up.

Sanitized phone numbers must begin with the international country code (ex: 254722000000), and should be <= 14 long

## Bulk HLR Lookup

```ruby
require 'app_name'

api = AppName::APIClient.authorize!('Thequickbrownfoxjumpsoverthelazydog')
response = api.bulk_hlr_lookup.search('25429907390, 25622307390, 15417242018')
puts response
```

```python
import app_name

api = app_name.authorize('Thequickbrownfoxjumpsoverthelazydog')
response = api.bulk_hlr_lookup.search(msisdns='25429907390, 25622307390, 15417242018')
print(response)
```

```shell
curl -G -v "http://app-domain.com/api/bulk-hlr-lookup"
    -H "Content-Type: application/json" \
    -H "Authorization: Thequickbrownfoxjumpsoverthelazydog"
    --data-urlencode "msisdns=25429907390, 25622307390, 15417242018"

```

```javascript
const app_name = require('app_name');

let api = app_name.authorize('Thequickbrownfoxjumpsoverthelazydog');
let response = api.bulkHlLookup.search("25429907390,25622307390,15417242018");
console.log(response);
```

```php
<?
require 'app_name';
use AppName\APIClient;

$api = AppClient::authorize('Thequickbrownfoxjumpsoverthelazydog');
$response = $api->bulkHlrLookup->search("25429907390, 25622307390, 15417242018");
print_r($response);
?>
```
> The above command returns JSON structured like this:

```json
[
  {
    "id": 1245,
    "msisdn": 25429907390,
    "status": "Active",
    "country_iso": "KE",
    "country_name": "Kenya"
  },
  {
    "id": 8245,
    "msisdn": 25622307390,
    "status": "Active",
    "country_iso": "UG",
    "country_name": "Uganda"
  },
  {
    "id": 1245,
    "msisdn": 15417242018,
    "status": "Unknown",
    "country_iso": "US",
    "country_name": "United States of America"
  }
]
```

This endpoint enables you to send messages.

### HTTP Request

<aside class="success">
GET http://app-domain.com/api/bulk-hlr-lookup?msisdns=xyz%5C%2Ctrw
</aside>

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
msisdns | true | Phone numbers you want to look up separated by commas.

Sanitized phone numbers must begin with the international country code (ex: 254722000000), and should be <= 14 long

# Balances
Returns your balance if the request was successful.

## Check Balance

```ruby
require 'app_name'

api = AppName::APIClient.authorize!('Thequickbrownfoxjumpsoverthelazydog')
response = api.balance
puts response
```

```python
import app_name

api = app_name.authorize('Thequickbrownfoxjumpsoverthelazydog')
response = api.balance()
print(response)
```

```shell
curl "http://app-domain.com/api/balance"
    -H "Content-Type: application/json" \
    -H "Authorization: Thequickbrownfoxjumpsoverthelazydog"

```

```javascript
const app_name = require('app_name');

let api = app_name.authorize('Thequickbrownfoxjumpsoverthelazydog');
let response = api.balance();
console.log(response);
```

```php
<?
require 'app_name';
use AppName\APIClient;

$api = AppClient::authorize('Thequickbrownfoxjumpsoverthelazydog');
$response = $api->balance();
print_r($response);
?>
```
> The above command returns JSON structured like this:

```json
{
  "id": 16245,
  "account_type": "prepaid",
  "currency": "USD",
  "amount": "57"
}
```

This endpoint allows you to query your balance.

### HTTP Request

<aside class="success">
GET http://app-domain.com/api/balance
</aside>

### Query Parameters
No query parameters

# PriceList
Returns the pricelist of the country queried.

## Check PriceList

```ruby
require 'app_name'

api = AppName::APIClient.authorize!('Thequickbrownfoxjumpsoverthelazydog')
response = api.pricelist.search("NL"
puts response
```

```python
import app_name

api = app_name.authorize('Thequickbrownfoxjumpsoverthelazydog')
response = api.pricelist("NL")
print(response)
```

```shell
curl "http://app-domain.com/api/pricelist?country_code=NL"
    -H "Content-Type: application/json" \
    -H "Authorization: Thequickbrownfoxjumpsoverthelazydog"

```

```javascript
const app_name = require('app_name');

let api = app_name.authorize('Thequickbrownfoxjumpsoverthelazydog');
let response = api.pricelist("NL");
console.log(response);
```

```php
<?
require 'app_name';
use AppName\APIClient;

$api = AppClient::authorize('Thequickbrownfoxjumpsoverthelazydog');
$response = $api->pricelist("NL");
print_r($response);
?>
```
> The above command returns JSON structured like this:

```json
{
  "country": "NL",
  "name": "Netherlands",
  "prefix": "31",
  "currency": "EURO",
  "networks": [
    {
      "network": "KPN",
      "sms_price": "0.13",
      "voice_message_price": "0.25"
    },
    {
      "network": "Lyca Mobile",
      "sms_price": "0.09",
      "voice_message_price": "0.15"
    },
    {
      "network": "Aldi Talk",
      "sms_price": "0.13",
      "voice_message_price": "0.29"
    },
    {
      "network": "Telfort",
      "sms_price": "N/A",
      "voice_message_price": "N/A"
    },
    ... //the list is longer
  ]
}
```

This endpoint allows you to query pricelists per country.

### HTTP Request

<aside class="success">
GET http://app-domain.com/api/pricelist?country_code=NL
</aside>

### Query Parameters
Parameter | Required | Description
--------- | ------- | -----------
country_code | true | Country code to search pricing.

# Delivery status
Returns the delivery status of a message.

## Check Delivery Status

```ruby
require 'app_name'

api = AppName::APIClient.authorize!('Thequickbrownfoxjumpsoverthelazydog')
response = api.messages.check_delivery("145")
puts response
```

```python
import app_name

api = app_name.authorize('Thequickbrownfoxjumpsoverthelazydog')
response = api.messages.check_delivery("145")
print(response)
```

```shell
curl "http://app-domain.com/api/messages/145"
    -H "Content-Type: application/json" \
    -H "Authorization: Thequickbrownfoxjumpsoverthelazydog"

```

```javascript
const app_name = require('app_name');

let api = app_name.authorize('Thequickbrownfoxjumpsoverthelazydog');
let response = api.messages.checkDelivery("145");
console.log(response);
```

```php
<?
require 'app_name';
use AppName\APIClient;

$api = AppClient::authorize('Thequickbrownfoxjumpsoverthelazydog');
$response = $api->messages.checkDelivery("145");
print_r($response);
?>
```
> The above command returns JSON structured like this:

```json
{
  "id": 145,
  "date_sent": "2018-01-01 12:00:00",
  "date_delivered": "2018-01-01 12:01:24",
  "delivery_status": "DELIVERED"
}
```

This endpoint allows you to query your message delivery status.

### HTTP Request

<aside class="success">
GET http://app-domain.com/api/messages/:id
</aside>

### Query Parameters
Parameter | Required | Description
--------- | ------- | -----------
id | true | Message ID to be queried
