# Callbacks

Callbacks represent URLs on your side which will be called by our system when event occurs.

## Get list of callbacks

Returns the list of instantiated callbacks on the account (or extension)

```
GET https://api.phone.com/v4/accounts/VOIP_ID/integrations/events/callbacks
```

### Optional query parameters

* `limit` - limit the number of items in the output (default is 25)
* `offset` - list offset (default is 0)
* `filters[name]` - filter callbacks by name
* `filters[profile_id]` - filter callbacks by the ID of the profile
* `filters[fallback_callback_id]` - filter by the ID of the fallback-callback profile

### Response example

```json
{
  "filters": {},
  "sort": {
    "id": "desc"
  },
  "limit": 25,
  "offset": 0,
  "items": [
    {
      "id": 1776,
      "voip_id": 1000002,
      "extension_id": null,
      "fallback_callback_id": null,
      "name": "My callback",
      "profile_id": 383,
      "enabled": true,
      "mode": "HTTPS",
      "config": {
        "url": "https://example.org",
        "method": "POST"
      }
    },
    {
      "id": 1775,
      "voip_id": 1000002,
      "extension_id": null,
      "fallback_callback_id": null,
      "name": "Another callback",
      "profile_id": null,
      "enabled": true,
      "mode": "HTTPS",
      "config": {
        "url": "https://example.com",
        "method": "POST"
      }
    }
  ]
}
```

## Get callback

Returns callback

```
GET https://api.phone.com/v4/accounts/VOIP_ID/integrations/events/callbacks/CALLBACK_ID
```

### Response example

```json
{
  "id": 1776,
  "voip_id": 1000002,
  "extension_id": null,
  "fallback_callback_id": null,
  "name": "My callback",
  "profile_id": 383,
  "enabled": true,
  "mode": "HTTPS",
  "config": {
    "url": "https://example.org",
    "method": "POST"
  }
}
```

_Pay attention that if config has headers with names like `Authorization` or `X-Api-Key` value in the output will be replaced with `true`._ 

## Create callback

Creates callback

```
POST https://api.phone.com/v4/accounts/VOIP_ID/integrations/events/callbacks/CALLBACK_ID
```

### Request

JSON with these parameters:

#### Mandatory

* `config` - `object`, configuration of the callback. Depends on the `mode`.

##### Config for HTTPS and HTTP modes

* `url` - `string`, __required__, URL of the callback
* `method` - `string`, callback HTTP method POST/GET (default is `POST`)
* `headers` - `array` or `null`, __required__, callback HTTP Headers, (default is `null`). Array items:
    * `name` - header name
    * `value` - header value
* `timeout` - `integer` or `null`, Callback timeout (default is `null`, system timeout will be used)  

#### Optional

* `name` - `string` or `null`, the callback name (default is `null`)
* `fallback_callback_id` - `integer` or `null`, ID of the callback to be the fallback for the main callback (default is `null`)   
* `profile_id` - `integer` or `null`, ID of the [profile](./profiles.md) (default is `null`)
* `enabled` - `boolean`, enable or disable callback (default is `true`)
* `mode` - `string`, callback type HTTP/HTTPS (default is `HTTPS`)

#### Example

```json
{
    "name": "my callback",
    "config": {
        "method": "POST",
        "url": "https://example.org",
        "headers": [
            {
                "name": "X-Api-Key",
                "value": "XXXXXXXXXXXXXXXXXXXX"
            }
        ]
    },
    "profile_id": 20000
}
```

### Response

Similar to the "Get callback" response.


## Update callback

Updates some properties of the callback

```
PATCH https://api.phone.com/v4/accounts/VOIP_ID/integrations/events/callbacks/CALLBACK_ID
```

### Request

JSON with the parameters needed for "Create callback".

### Response

Similar to the "Get callback" response.

## Delete callback

Deletes a callback. Pay attention, the API will not allow the deletion of a callback which is used as a fallback for another callback. 

```
DELETE https://api.phone.com/v4/accounts/VOIP_ID/integrations/events/callbacks/CALLBACK_ID
```

### Response

Successful:

```json
{
  "success": true
}
```

Error:

```json
{
  "@error": {
    "@message": "Error: Callback is in use. Look for listeners using it.",
    "@httpStatusCode": 409,
    "@time": "2020-06-25T17:09:39.323Z"
  }
}
```