# Listeners

Listener is entity which connects subscriptions with callback.

## Get list of listeners

Returns list of listeners you have on account (extension)

```
GET https://api.phone.com/v4/accounts/VOIP_ID/integrations/events/listeners
```

### Optional query parameters

* `limit` - limit of the items in the output (default is 25)
* `offset` - list offset (default is 0)
* `filters[callback_id]` - filter listeners by ID of callback

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
      "id": 1001,
      "voip_id": 1000002,
      "extension_id": null,
      "version": "2.0.0",
      "callback_id": 1768,
      "created_at": 1592928702,
      "expires_at": null
    },
    {
      "id": 1000,
      "voip_id": 1000002,
      "extension_id": null,
      "version": "2.0.0",
      "callback_id": 1768,
      "created_at": 1591305649,
      "expires_at": null
    }
  ]
}
```

## Get listener

Returns listener

```
GET https://api.phone.com/v4/accounts/VOIP_ID/integrations/events/listeners/LISTENER_ID
```

### Response example

```json
{
  "id": 1001,
  "voip_id": 1000002,
  "extension_id": null,
  "version": "2.0.0",
  "callback_id": 1768,
  "created_at": 1592928702,
  "expires_at": null
}
```

## Create listener

Creates listener

```
POST https://api.phone.com/v4/accounts/VOIP_ID/integrations/events/listeners/LISTENER_ID
```

### Request

JSON with these mandatory parameters:

#### Mandatory

* `callback_id` - `integer`, callback ID

#### Optional

* `version` - `string`, events format (default is `2.0.0`)
* `expires_at` - `integer` or `null`, allows to define expiration time for listener

#### Example

```json
{
  "callback_id": 1776
}
```

### Response

The same as for "Get listener".


## Update listener

Updates some properties of the listener.

```
PATCH https://api.phone.com/v4/accounts/VOIP_ID/integrations/events/listeners/LISTENER_ID
```

### Request

JSON with any of parameters available for "Create listener".

### Response

The same as for "Get listener".

## Delete listener

Deletes listener. 

```
DELETE https://api.phone.com/v4/accounts/VOIP_ID/integrations/events/listeners/LISTENER_ID
```

### Response

Successful:

```json
{
  "success": true
}
```
