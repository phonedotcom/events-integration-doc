# Listener subscriptions

Defines what kind of events should generate a callback.

## Get list of subscriptions

Returns the list of subscriptions for a given listener.

```
GET https://api.phone.com/v4/accounts/VOIP_ID/integrations/events/listeners/LISTENER_ID/subscriptions
```

### Optional query parameters

* `limit` - limits the number of items in the output (default is 25)
* `offset` - list offset (default is 0)

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
      "id": 3030,
      ":tags": [
        "recording"
      ]
    },
    {
      "id": 3029,
      ":tags": [
        "call-log"
      ]
    }
  ]
}
```

## Get subscription

Returns a subscription

```
GET https://api.phone.com/v4/accounts/VOIP_ID/integrations/events/listeners/LISTENER_ID/subscriptions
```

### Response example

```json
{
  "id": 3029,
  ":tags": [
    "call-log"
  ]
}
```

## Create subscription

Creates a subscription

```
POST https://api.phone.com/v4/accounts/VOIP_ID/integrations/events/listeners/LISTENER_ID/subscriptions
```

### Request

JSON with these mandatory parameters:

* `:tags` - `string[]`, array of `string`. See [tags](./../tags.md).

#### Example

```json
{
  ":tags": ["call", "inbound"]
}
```

### Response

Similar to the "Get subscription" response.

## Delete subscription

Deletes a subscription. 

```
DELETE https://api.phone.com/v4/accounts/VOIP_ID/integrations/events/listeners/LISTENER_ID/subscriptions/SUBSCRIPTION_ID
```

### Response

Successful:

```json
{
  "success": true
}
```
