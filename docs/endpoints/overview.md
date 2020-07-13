# Overview

Returns list of listeners with callbacks, profiles and subscriptions.

```
GET https://api.phone.com/v4/accounts/VOIP_ID/integrations/events/overview
```

### Optional query parameters

* `limit` - limits the number of items in the output (the default is 25)
* `offset` - list offset (the default is 0)

### Response example

```json
{
  "filters": {},
  "sort": {
    "id": "desc"
  },
  "total": 43,
  "limit": 2,
  "offset": 0,
  "items": [
    {
      "id": 9591,
      "voip_id": 1000002,
      "extension_id": null,
      "version": "2.0.0",
      "callback_id": 1776,
      "created_at": 1591305333,
      "expires_at": null,
      ":callback": {
        "id": 1776,
        "voip_id": 1000002,
        "extension_id": null,
        "fallback_callback_id": null,
        "name": "My callback",
        "profile_id": 389,
        "enabled": true,
        "mode": "HTTPS",
        "config": {
          "url": "https://example.org",
          "method": "POST"
        },
        ":profile": {
          "id": 389,
          "voip_id": 1000002,
          "extension_id": null,
          "name": "My special profile",
          "support_email": "support@example.org",
          "created_at": 1591869178
        },
        ":fallback": null
      },
      ":subscriptions": [
        {
          "id": 4980,
          ":tags": [
            "call"
          ]
        },
        {
          "id": 4989,
          ":tags": [
            "message"
          ]
        },
        {
          "id": 4990,
          ":tags": [
            "call-log"
          ]
        },
        {
          "id": 4991,
          ":tags": [
            "recording"
          ]
        }
      ]
    }
  ]
}
```
