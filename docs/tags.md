# Tags

Tags are being used for configuring subscriptions. They are also being provided in events' payload.

## Tags logic in subscriptions

Tags implementing `AND` logic, for example, you want to receive events about inbound calls and outbound SMS. To achieve that you need to create two subscriptions:

1. With tags: `call` and `inbound`
2. With tags: `message` and `outbound`

If you want to receive events related to inbound calls and all sms:

1. With tags: `call` and `inbound`
2. With tag: `message`

For all inbound activity, create just one subscription with tag `inbound`.

If you create one subscription with tags `call` and `message` you will receive nothing, because there are now events which are related to call and SMS at the same time.

## List of tags

### Common

* __inbound__ - inbound activity (applies for calls and messages)
* __outbound__ - outbound activity (applies for calls and messages)

### Calls

* __call__ - event is related to call
* __new-call__ - call (if not first leg, than call's leg) is completed
* __connecting-call__ - call (call's leg) is in "connecting" state
* __connected-call__  - call (call's leg) is connected (answered)
* __completed-call__ - call (if not first leg, than call's leg) is completed
* __first-leg__ - event is related to the main (first) leg of the call
* __not-first-leg__ - event is not related to the main (first) leg of the call
* __to-did__ - call (call's leg) is calling phone number
* __from-did__ - call (call's leg) initiated from phone number
* __to-extension__ - call (call's leg) is calling Phone.com extension (device)
* __from-extension__ - call (call's leg) initiated from Phone.com extension (device)  

### Messages

* __message__ - event is related to message
* __sms-message__ - message is SMS
* __mms-message__ - message is MMS
* __*ms-message__ - message is SMS or MMS

### Misc

* __call-log__ - call log record is available or updated (see [https://apidocs.phone.com/docs/get-account-call-log]())
* __recording__ - some recording is available
* __call-recording__ - call recording is available

### Planned, unstable or deprecated

* __received-message__ - message received
* __sent-message__ - message sent
* __delivered-message__ - message delivered
* __fax__ - event is related to fax
* __voicemail__ - voicemail received
* __voicemail-transcript__ - voicemail transcription is ready
* __listener-callback__
* __deactivated-listener-callback__
* __deleted-listener-callback__