---
title: API Reference

language_tabs:
  - curl
  - ruby
  - php
  - python

toc_footers:
  - <a href='https://www.travelpayouts.com/'>Sign Up for a Developer Token</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Data Access API

Travelpayouts Data API – the way to get travel insights for your site or blog. You can get flight price trends and find popular destinations for your customers.

Dear partners! Attention, the data is transferred from the cache, so it is recommended to use them to generate static pages. 

To access the API you must pass your token in the X-Access-Token header or in the token parameter. To obtain a token for the Data Access API, go to http://www.travelpayouts.com/developers/api.

Dates are accepted in the formats YYYY-MM and YYYY-MM-DD.

The server response is always sent in json format with the following structure:

  - **success** – true for successful request, false in case of errors;
  - **data** – result of the request; in case of an error is equal to null;
  - **error** – short description of the error that prevented request completion; for successful request is equal to null.

Dates and times are given in UTC, formatted according to [ISO 8601](https://ru.wikipedia.org/wiki/ISO_8601). Prices are given in rubles as of when the ticket is put in the search results. It is not recommended to use expired prices (the approximate expiration date is given in the value of the expires_at parameter).

**Important**. We strongly urge receiving data in compressed GZIP format, which saves a significant amount of time in receiving the response. To get data in compressed form, send the header Accept-Encoding: gzip, deflate.

To obtain access to the API for searching for plane tickets and hotels, [send a request](https://support.travelpayouts.com/hc/en-us/requests/new).

## Flight price history

Brings back the list of prices found by our users during the most recent 48 hours according to the filters used.

### HTTP Request

`GET http://api.travelpayouts.com/v2/prices/latest?currency=usd&period_type=year&page=1&limit=30&show_to_affiliates=true&sorting=price&trip_class=0&token=PutHereYourToken`

### Request parameters

> Example of code:

```curl
curl --include --header "X-Access-Token: YOUR_API_TOKEN_HERE" "http://api.travelpayouts.com/v2/prices/latest?currency=rub&period_type=year&page=1&limit=30&show_to_affiliates=true&sorting=price&trip_class=0"
```

```ruby
require 'rubygems' if RUBY_VERSION < '1.9'
require 'rest_client'
headers  = {:x_access_token => "YOUR_API_TOKEN_HERE"}
response = RestClient.get "http://api.travelpayouts.com/v2/prices/latest?currency=rub&period_type=year&page=1&limit=30&show_to_affiliates=true&sorting=price&trip_class=0", headers
puts response
```

```php
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, "http://api.travelpayouts.com/v2/prices/latest?currency=rub&period_type=year&page=1&limit=30&show_to_affiliates=true&sorting=price&trip_class=0");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, TRUE);
curl_setopt($ch, CURLOPT_HEADER, FALSE);
curl_setopt($ch, CURLOPT_HTTPHEADER, array("X-Access-Token: YOUR_API_TOKEN_HERE"));
$response = curl_exec($ch);
curl_close($ch);
var_dump($response);
```

```python
from urllib2 import Request, urlopen
headers = {"X-Access-Token": "YOUR_API_TOKEN_HERE"}
request = Request("http://api.travelpayouts.com/v2/prices/latest?currency=rub&period_type=year&page=1&limit=30&show_to_affiliates=true&sorting=price&trip_class=0", headers=headers)
response_body = urlopen(request).read()
print response_body
```

Note! If the point of departure and the point of destination are not specified, the API shall bring back 30 of the cheapest tickets that have been found during the most recent 48 hours.

Parameter | Default | Description
--------- | ------- | -----------
currency | RUB | The airline ticket’s currency.
origin | - | The point of departure. The IATA city code or the country code. The length - from 2 to 3 symbols.
destination | - | The point of destination. The IATA city code or the country code. The length - from 2 to 3 symbols.
beginning_of_period | - | The beginning of the period, within which the dates of departure fall (in the YYYY-MM-DD format, for example, 2016-05-01). Must be specified if **period_type** is equal to month.
period_type | - | The period for which the tickets have been found (the required parameter): **year** — for the whole time, **month** — for a month.
one_way | false | **true** - one way, **false** - back-to-back.
page | 1 | A page number.
limit | 30 | The total number of records on a page. The maximum value - 1000e.
show_to_affiliates | true | **false** - all the prices, **true** - just the prices, found using the partner marker (recommended).
sorting | price | The assorting of prices: **price** — by the price. For the directions, only **city - city** assorting by the price is possible; **route** — by the popularity of a route; **distance_unit_price** — by the price for 1 km.
trip_class | 0 | The flight class: **0** — Economy class; **1** — Business class; **2** — First.
trip_duration | 1 | A page number.
token | - | Individual affiliate token.


Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

> To authorize, use this code:

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
```

> Make sure to replace `meowmeowmeow` with your API key.

Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

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
curl "http://example.com/api/kittens"
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
curl "http://example.com/api/kittens/2"
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

