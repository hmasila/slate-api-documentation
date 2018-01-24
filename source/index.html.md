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

## send single sms

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
  "to": "25409907990",
  "message_id": 134,
  "status": "Successful",
  "message_price": "0.56"
}
```

This endpoint enables you to send messages.

### HTTP Request

<aside class="success">
GET http://app-domain.com/api/messages
</aside>

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
to | true | Phone number of the recipient.
from | true | Phone number of the sender.
text | true | Message to be sent.

Sanitized phone numbers must begin with the international country code (ex: 254722000000), and should be <= 14 long

## Bulk messaging

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

```PHP
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
  "message_id": 128,
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
GET http://app-domain.com/api/bulk-messages
</aside>

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
to | true | Phone numbers of the recipients separated by commas.
from | true | Phone number of the sender.
text | true | Message to be sent.

# Send Voice Messages

## send single voice message

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
  "to": "25409907990",
  "voice_message_id": 124,
  "status": "Successful",
  "voice_message_price": "1.13",
  "voice": "female",
  "language": "en-gb"
}
```

This endpoint enables you to send voice messages.

### HTTP Request

<aside class="success">
GET http://app-domain.com/api/voice-messages
</aside>

### Query Parameters

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
    "voice_message_id": 128,
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
GET http://app-domain.com/api/bulk-voice-messages
</aside>

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
to | true | Phone numbers of the recipients separated by commas.
from | true | Phone number of the sender.
text | true | Voice message to be sent.
voice | false | The voice in which the messages needs to be read to the recipient. Possible values are: male, female.
Default: female
language | false | The language in which the message needs to be read to the recipient. Possible values are: <> Default: en-gb
