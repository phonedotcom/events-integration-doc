# Applications

Applications provide different event-based functionality.

* [Google Analytics](./applications/google-analytics.md)

Example of the payload for creating callback with `mode` `APPLICATION`:

```json
    {
      "name": "My Google Analytics integration",
      "mode": "APPLICATION",
      "config": {
        "application": "google-analytics",
        "parameters": {
          "tracking_id": "UA-00000000-01",
          "static": {
            "ec": "Phone call"
          },
          "dynamic": {
            "ea": "direction_text",
            "el": "phone_number",
            "cd1": "other_phone_number"
          }
        }
      }
    }
```