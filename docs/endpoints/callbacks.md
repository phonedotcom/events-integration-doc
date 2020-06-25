# Callbacks

Callbacks represent URLs on your side which will be called by our system when event occurs.

## Get list of callbacks

Returns list of callbacks you have on account (extension)

```
GET https://api.phone.com/v4/accounts/VOIP_ID/integrations/events/callbacks
```

### Optional query parameters

* `limit` - limit of the items in the output (default is 25)
* `offset` - list offset (default is 0)
* `filters[name]` - filter callbacks by name
* `filters[profile_id]` - filter callbacks by ID of profile
* `filters[fallback_callback_id]` - filter callbacks by ID of the fallback callback

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
* `method` - `string`, URL of the callback (default is `POST`)
* `headers` - `array` or `null`, __required__, URL of the callback, (default is `null`). Array items:
    * `name` - header name
    * `value` - header value
* `timeout` - `integer` or `null`, Callback timeout (default is `null`, system timeout will be used)  

#### Optional

* `name` - `string` or `null`, name of the callback (default is `null`)
* `fallback_callback_id` - `integer` or `null`, ID of the callback to be the fallback for this callback (default is `null`)   
* `profile_id` - `integer` or `null`, ID of the [profile](./profiles.md) (default is `null`)
* `enabled` - `boolean`, is callback enabled (default is `true`)
* `mode` - `string`, callback type (default is `HTTPS`)

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

The same as for "Get callback".


## Update callback

Updates some properties of the callback

```
PATCH https://api.phone.com/v4/accounts/VOIP_ID/integrations/events/callbacks/CALLBACK_ID
```

### Request

JSON with any of parameters available for "Create callback".

### Response

The same as for "Get callback".

## Delete callback

Deletes callback. Pay attention, that API will not allow you to delete callback which is used for some listener of as fallback for another callback. 

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