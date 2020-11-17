# Events integration API endpoints

## Reference

* [Callbacks](./endpoints/callbacks.md)
* [Listeners](./endpoints/listeners.md)
* [Subscriptions](./endpoints/listener-subscriptions.md)
* [Profiles](./endpoints/profiles.md)
* [Overview](./endpoints/overview.md)

## Extension-level aliases

Events integration API endpoints are also available on an extension level. For example, instead of this URL:

```
GET https://api.phone.com/v4/accounts/VOIP_ID/integrations/events/callbacks
```

you should use the following URL when you need or can only use extension level APIs:

```
GET https://api.phone.com/v4/accounts/VOIP_ID/extensions/EXTENSION_ID/integrations/events/callbacks
```
