# Express create

This endpoint allows to create listener, callback (profile) and subscriptions with one API call.

```
POST https://api.phone.com/v4/accounts/VOIP_ID/integrations/events/overview
```

### Request

A JSON with at least all mandatory parameters:

#### Mandatory

Callback should be defined as ID or payload:

* `callback_id` - `integer`, callback ID
* `:callback` - `object`, see "Create callback" in [Callbacks](./callbacks.md#create-callback)

At least one subscription is required:

* `subscriptions` - `array` of Subscriptions, see "Create subscription" in [Listener Subscriptions](./listener-subscriptions.md#create-subscription)

#### Optional

See "Create listener" in [Listeners](./listeners.md#create-listener)

#### Example 

```json
{
    ":callback": {
        "config": {
            "url": "https://example.org"
        }
    },
    ":subscriptions": [
        {
            ":tags": [
                "call-log"
            ]
        }
    ]
}
```

### Response

Similar to the item from "Overview" response.