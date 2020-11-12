# Google Analytics

This application allows you to report event to Google Analytics events tracking. For example you may configure setup when every call to your Phone.com phone number will be reported as event, so you will be able to calculate conversions.

## Configuration

Name of the application: `google-analytics`

### Parameters

* `tracking_id` - your Google tracking ID like `UA-00000000-1`
* `static` - object with of static values added to the event.
    * Available keys of the object: `cd1`, `cd2`, `cd4`, `cd5`, `cid`, `dh`, `dl`, `ea`, `ec`, `el`, `ev`, `ni`, `t`, `tid`, `uid`, `v`.
    * Values will be added to event as is.
* `dynamic` - object with of static values added to the event.
    * Available keys of the object: `cd1`, `cd2`, `cd4`, `cd5`, `cid`, `dh`, `dl`, `ea`, `ec`, `el`, `ev`, `ni`, `uid`.
    * Available values - the actual values will be extracted from the event: 
        * `call_duration` - duration of the call. It will work for `call-log` events only.
        * `direction` - direction of the call/message - `in` or `out`.
        * `direction_text` - direction of the call/message - `inbound` or `outbound`.
        * `phone_number` - your phone number or extension (for outbound calls)
        * `other_phone_number` - phone number of the other side

Read more about Google Analytics parameters: https://developers.google.com/analytics/devguides/collection/protocol/v1/parameters

## Example

```json
    {
      "name": "My Google Analytics integration",
      "mode": "APPLICATION",
      "config": {
        "application": "google-analytics",
        "parameters": {
          "tracking_id": "UA-00000000-1",
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