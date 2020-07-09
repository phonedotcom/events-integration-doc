# Listeners

Listener is an entity that associates subscriptions with callbacks.

## Get list of listeners

Returns list of listeners created on account (or an extension)

```
GET https://api.phone.com/v4/accounts/VOIP_ID/integrations/events/listeners
```

### Optional query parameters

* `limit` - limits the number of items in the API response (default is 25)
* `offset` - list offset (default is 0)
* `filters[callback_id]` - filters listeners based on a given callback ID

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

Returns a listener

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

Creates a listener

```
POST https://api.phone.com/v4/accounts/VOIP_ID/integrations/events/listeners/LISTENER_ID
```

### Request

A JSON with at least all mandatory parameters:

#### Mandatory

* `callback_id` - `integer`, callback ID

#### Optional

* `version` - `string`, events format (default is `2.0.0`)
* `expires_at` - `integer` or `null`, defines an expiration time for a listener

#### Example

```json
{
  "callback_id": 1776
}
```

### Response

Similar to the response from "Get listener".


## Update listener

Updates one or more properties of the listener.

```
PATCH https://api.phone.com/v4/accounts/VOIP_ID/integrations/events/listeners/LISTENER_ID
```

### Request

JSON with all the required parameters neded for the "Create listener" API.

### Response

Similar to the response from "Get listener".

## Delete listener

Deletes a listener. 

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
