# Events integration API endpoints

## Reference

* [Callbacks](./endpoints/callbacks.md)
* [Listeners](./endpoints/listeners.md)
* [Subscriptions](./endpoints/listener-subscriptions.md)
* [Profiles](./endpoints/profiles.md)
* [Overview](./endpoints/overview.md)

## Extension-level aliases

Events integration API endpoints are also available on extension level. For example instead of 

```
GET https://api.phone.com/v4/accounts/VOIP_ID//integrations/events/callbacks
```

you should call

```
GET https://api.phone.com/v4/accounts/VOIP_ID/extensions/EXTENSION_ID/integrations/events/callbacks
```
