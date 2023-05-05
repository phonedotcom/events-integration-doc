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

## Create filter

Creates a filter

```
POST https://api.phone.com/v4/accounts/VOIP_ID/integrations/events/listeners/LISTENER_ID/filters
```

### Request

JSON with these parameters:

* `filter_type` - `string`. Mandatory. Filter's fype. Supported values: `number`, `schedule`
* `filter_value` - `object`. Mandatory. Configuration of the filter (different for different filter types)
* `not_logic` - `boolean`. Options (`false` by default). `true` value inverts logic of the filter so events satistying filter's criterea will NOT be emitted.

#### `filter_value` per type

##### `filter_type=number`

Provde one of parameters

* `eq` - `string`. Phone number (`+` followed by digits).
* `in` - `string[]`. List of numbers.
* `match` - `string`. Pattern for number (use `%` as wildcard)

##### `filter_type=schedule`

* `id` - `integer`. ID of schedule

Schedules are being updated asyncronously and it may take some time. We recommend to call `PATCH` endpoint to resync it immediately.

#### Example

```json
{
  "filter_type": "number",
  "filter_value": {
    "eq": "+15555551234"
  }
}
```

### Response

Similar to the "Get filter" response.

## Update filter

Updates a filter. 

```
PATCH https://api.phone.com/v4/accounts/VOIP_ID/integrations/events/listeners/LISTENER_ID/filters/SUBSCRIPTION_ID
```

### Request

Similar to the "Create filter" request.

### Response

Similar to the "Get filter" response.

## Delete filter

Deletes a filter. 

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
