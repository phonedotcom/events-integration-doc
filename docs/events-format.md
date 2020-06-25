# Events format

## Common

* `uuid` - unique identifier of the event
* `version` - version of event's format 
* `listener_id` - ID of the listener 
* `context` - Context of the event (contains information about account or extension associated with the listener)
* `timestamp` - UNIX timestamp (seconds)
* `timestamp_ns` - UNIX timestamp (nanoseconds)
* `tags` - list of event's [tags](./tags.md)
* `data_type` - type of the object in `data`
* `data_object_uuid` - unique identifier of the data object
* `data` - will be different for different values of the field `data_type`.

## Data per object type

### Call

* `uuid` - unique identifier of the call
* `direction` - unique identifier of the call
* `event_leg` - information about current event's leg _(see "Call's leg object")_
* `first_leg` - information about first (main) leg of the call _(see "Call's leg object")_. `null` if `event_leg` is the first leg.

_Also see [call events explanation](./call-events-explanation.md)_


#### Call's leg object

* `uuid` - unique identifier of the call's leg (the same as call's UUID for the first leg) 
* `from` - leg's caller _(see "Call's participant object")_
* `to` - leg's callee  _(see "Call's participant object")_
* `is_first` - boolean value which shows is leg first (main) or not
* `state` - leg's state. Possible values: `new`, `connecting`, `connected`, `completed`.
* `completion_status` - leg's completion state. Possible values: `success` - leg was answered, `cancelled` - leg was not answered, `busy` - device was busy, `failed` - error occurred.

#### Call's participant object

* `type` - type of the call's participant entity. Possible values: `device`, `extension`, `did` (phone number)
* `id` - ID of the object. For `type=did` it will be phone number
* `line` - device line; applicable for `type=device` only
* `domain` - SIP domain; applicable for `type=device` only
* `extension_id` - ID of extension; applicable for `type=device` and `type=extension`
* `extension` - extension number; applicable for `type=device` and `type=extension`

### Message

* `uuid` - unique identifier of the message
* `direction` - `inbound` or `outbound`
* `state` - message delivery status: `received`, `sent`, etc.
* `inbox` - information about inbox message belongs to
    * `id` - ID of the message in the inbox
    * `extension_id` - ID of the extension
    * `did` - customer's number associated with the message
* `from` - sender of the message _(see "Call's participant object" with `type=did`)_
* `to` - recipients of the message _(array of "Call's participant object" with `type=did`)_
* `type` - `sms` or `mms`
* `message` - message text
* `media` - message attachments (for `mms`). Array of object:
    * `url` - URL of the attachment
    * `type` - MIME type of the attachment
    * `size` - size of the attachment in bytes
    * `filename` - name of the attachment
    * `thumbnail` - URL of thumbnail if exists

### Call log

`uuid` - uuid of the call (call log)

### Recording

`uuid` - uuid of the recording
`type` - type of object; possible value: `call`
`size` - size of the recording in bytes
`duration` - recording duration in seconds

## Example

This is example of call event. You can find more examples in [this directory](./../events-examples)

```json
{
  "uuid": "00000000-0000-0000-0000-000000000000",
  "version": "2.0.0",
  "listener_id": 1000,
  "context": {
    "type": "account",
    "id": 1000002,
    "voip_id": 1000002
  },
  "timestamp": 1593029665,
  "timestamp_ns": 1593029665343497000,
  "tags": [
    "call",
    "completed-call",
    "not-first-leg",
    "inbound",
    "from-did",
    "to-extension"
  ],
  "data_type": "call",
  "data_object_uuid": "11111111-1111-1111-1111-111111111111",
  "data": {
    "uuid": "1111-1111-1111-1111-111111111111",
    "direction": "inbound",
    "event_leg": {
      "uuid": "22222222-2222-2222-2222-222222222222",
      "from": {
        "type": "did",
        "id": "+15550000001"
      },
      "to": {
        "type": "device",
        "id": 777777,
        "line": 1,
        "domain": "sip.phone.com",
        "extension_id": 555555,
        "extension": 500
      },
      "is_first": false,
      "state": "completed",
      "completion_status": "cancelled"
    },
    "first_leg": {
      "uuid": "1111-1111-1111-1111-111111111111",
      "from": {
        "type": "did",
        "id": "+15550000001"
      },
      "to": {
        "type": "did",
        "id": "+15550000002"
      },
      "is_first": true,
      "state": null,
      "completion_status": null
    }
  }
}
```