---
title: API Documentation

language_tabs: # must be one of https://git.io/vQNgJ
  - curl
  - ruby
  - python
  - javascript

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
    '0800900900',
    '0800990990',
    'Hi, Lets meet for coffee'
  )
  puts response
```

```python
import app_name

api = app_name.authorize('Thequickbrownfoxjumpsoverthelazydog')
response = api.messages.create(
    from='from_number',
    to='to_number',
    text='Hi, Lets meet for coffee', )
print(response)
```

```shell
curl "http://app-domain.com/api/messages"
    -H "Content-Type: application/json" \
    -H "Authorization: Thequickbrownfoxjumpsoverthelazydog"
    -d '{"from": "07111111111","to": "14156667777", "text": "Hi, Lets meet for coffee"}' \

```

```javascript
const app_name = require('app_name');

let api = app_name.authorize('Thequickbrownfoxjumpsoverthelazydog');
let text = "Let's meet for coffee"
let response = api.messages.create(
      "14153336666", // from
      "14156667777", // to
      "Test Message", // text
  );
  console.log(response);
```

> The above command returns JSON structured like this:

```json
{
  "to": "14156667777",
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

Provide a list of recipient numbers separated with commas. (e.g. 254756667547<254758778318<254758809799).



```ruby
require 'app_name'

api = AppName::APIClient.authorize!('Thequickbrownfoxjumpsoverthelazydog')
api.kittens.get(2)
```

```python
import app_name

api = app_name.authorize('Thequickbrownfoxjumpsoverthelazydog')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: Thequickbrownfoxjumpsoverthelazydog"
```

```javascript
const app_name = require('app_name');

let api = app_name.authorize('Thequickbrownfoxjumpsoverthelazydog');
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
require 'app_name'

api = AppName::APIClient.authorize!('Thequickbrownfoxjumpsoverthelazydog')
api.kittens.delete(2)
```

```python
import app_name

api = app_name.authorize('Thequickbrownfoxjumpsoverthelazydog')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: Thequickbrownfoxjumpsoverthelazydog"
```

```javascript
const app_name = require('app_name');

let api = app_name.authorize('Thequickbrownfoxjumpsoverthelazydog');
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
