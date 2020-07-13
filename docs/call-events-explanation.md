# Call events explanation

Each telephony call has multiple call legs. For example, if you use a Phone.com device or mobile app and someone calls you, two legs call legs will be created, one for the inbound call from the outside world and the second from phone.com to your device. See the sample object for [inbound call events](./../events-examples/inbound-call-to-device).

The first leg is between the caller and Phone.com, the second leg is between Phone.com and your device (or app).

Each leg has its own set of states: new, connecting, connected, completed.

If you have routes configured such that when Phone.com rings one device for 20 seconds then, if the call is not answered, rings another device (which is then answered), the events will look like this:

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

_Our event system is asynchronous, so we do not guarantee the exact order of closely-timed events. In practice, the `connecting` event may be received by your webhook before the `new`, or the `completed` events of the first leg can be received just before the `completed` events of the second._
