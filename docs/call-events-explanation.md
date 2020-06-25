# Call events explanation

Each call has some legs. For example if you use phone.com device or mobile app and somebody is calling you it will be two legs. See example [inbound call events](./../events-examples/inbound-call-to-device).

The first leg is the leg between caller and Phone.com, another leg is the leg between Phone.com and your device (app).

Each leg have its own set of states: new, connecting, connected, completed.

If you have configuration when Phone.com rings one device for 20 seconds and if call was not answered, rings another device (and it answered) events will be like this:

* 1st leg - new
* 1st leg - connecting
* 2nd leg - new
* 2nd leg - connecting
* 2nd leg - completed (with `completion_state=cancelled`)
* 3rd leg - new
* 3rd leg - connecting
* 3rd leg - connected
* 1st leg - connected
* 3rd leg - completed (with `completion_state=success`)
* 1st leg - completed (with `completion_state=success`)

_Our event system is asynchronous, so we don't guarantee the exact order of events. On practice `connecting` may be received by your webhook a bit earlier than `new` or `completed` of the 1nd leg can be received right before `completed` of the 2nd leg._