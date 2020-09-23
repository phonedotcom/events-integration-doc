# Tags

Tags are used as part of the subscriptions configuration. The Tags are passed to the events' payload.

## Tags logic in subscriptions

Tags can be used to reduce the amount and pinpoint the type of events sent by the event hub to the application. The events apply `AND` logic. For example, if you want to receive events only about inbound calls and also only about outbound SMS (messages), you will need to create two subscriptions:

1. With the tags: `call` and `inbound`
2. With the tags: `message` and `outbound`

If you want to receive events related to inbound calls plus all events sms events you will create two subscriptions:

1. With the tags: `call` and `inbound`
2. With the tag: `message`

To create a listener for all inbound activity, create just one subscription with tag `inbound`.

If you create one subscription with the tags `call` and `message`, you will receive nothing, since there are no events that are both a call and an SMS message.

## List of tags

### Common

* __inbound__ - inbound activity (applies to calls and messages)
* __outbound__ - outbound activity (applies to calls and messages)

### Calls

* __call__ - event related to call
* __new-call__ - a call (or call leg) is starting a call
* __connecting-call__ - a call (or call leg) is in "connecting" state (ringing)
* __connected-call__  - call (or call leg) got connected (answered)
* __completed-call__ - the call (if not first leg, than call's leg) completed a call (ended)
* __first-leg__ - event related to the main (first) leg of a call
* __not-first-leg__ - event is not related to the main (first) leg of the call
* __to-did__ - a call (or call's leg) is calling to this phone number
* __from-did__ - a call (or call's leg) initiated from this phone number
* __to-extension__ - a call (or call's leg) is calling a Phone.com extension (device)
* __from-extension__ - a call (or call's leg) is initiated from Phone.com extension (device)  

### Messages

* __message__ - the event is related to a message
* __sms-message__ - message is of type SMS
* __mms-message__ - message is of type MMS
* __*ms-message__ - message is of type SMS or MMS

### API Errors

_Account level only_

* __api-error__ - request to API returned error
* __api-error-trusted__ - request to API returned error (excluding unauthorized requests)

### Misc

* __call-log__ - call log record is available or just got updated (see [https://apidocs.phone.com/docs/get-account-call-log]())
* __recording__ - some recording is available
* __call-recording__ - call recording is available

### Planned, unstable or deprecated

* __received-message__ - message received
* __sent-message__ - message sent
* __delivered-message__ - message delivered
* __fax__ - fax related event
* __voicemail-recording__ - voicemail received
* __voicemail-transcript__ - voicemail transcription is ready
* __listener-callback__
* __deactivated-listener-callback__
* __deleted-listener-callback__
