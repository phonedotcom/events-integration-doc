# Listener filters

There is a way to filter events. If no filters defined, than all events will be processed. If filters defined, events should match all of them.

## Get list of filters

Returns the list of filters for a given listener. 

```
GET https://api.phone.com/v4/accounts/VOIP_ID/integrations/events/listeners/LISTENER_ID/filters
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
  "offset": null,
  "items": [
    {
      "id": 5000,
      "listener_id": 1000,
      "filter_type": "number",
      "filter_value": {
        "in": [
          "+15551234567"
        ]
      }
    }
  ]
}
```

## Get filter

Returns a subscription

```
GET https://api.phone.com/v4/accounts/VOIP_ID/integrations/events/listeners/LISTENER_ID/filters
```

### Response example

```json
{
  "id": 5000,
  "listener_id": 1000,
  "filter_type": "number",
  "filter_value": {
    "in": [
      "+15551234567"
    ]
  }
}
```

## Create subscription

Creates a subscription

```
POST https://api.phone.com/v4/accounts/VOIP_ID/integrations/events/listeners/LISTENER_ID/filters
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
DELETE https://api.phone.com/v4/accounts/VOIP_ID/integrations/events/listeners/LISTENER_ID/filters/SUBSCRIPTION_ID
```

### Response

Successful:

```json
{
  "success": true
}
```
