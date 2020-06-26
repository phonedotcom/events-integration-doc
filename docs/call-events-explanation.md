# Call events explanation

Each call has multiple legs. For example, if you use a Phone.com device or mobile app and somebody calls you, there will be two legs. See the sample object for [inbound call events](./../events-examples/inbound-call-to-device).

The first leg is between the caller and Phone.com, the next leg is between Phone.com and your device (app).

Each leg have its own set of states: new, connecting, connected, completed.

If you have routes configured such that when Phone.com rings one device for 20 seconds then, if the call is not answered, rings another device (which is then answered), the events will be like this:

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

_Our event system is asynchronous, so we do not guarantee the exact order of events. In practice, the `connecting` event may be received by your webhook before the `new`, or the `completed` events of the first leg can be received just before the `completed` events of the second._
