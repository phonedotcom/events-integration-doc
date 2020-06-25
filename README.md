# Phone.com events v. 2 integration guide

Phone.com provides support of the webhooks (HTTPS callbacks) for different [events](./docs/events-format.md) associated with Phone.com accounts.

## Getting started

Phone.com has some endpoints in the API which allow you to configure callbacks and subscribe for the only events you need.

To use Phone.com API you need to have access token. Contact Phone.com support by email api@phone.com to discuss your integration and get one.

Full endpoints documentation can be found [here](./docs/api-endpoints.md), but this section of the document represents the minimal set-up you need to start receiving events.

### Create callback

First of all you will need to define callback:

```
curl -L -X POST 'https://api.phone.com/v4/accounts/VOIP_ID/integrations/events/callbacks' \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer YOUR_ACCESS_TOKEN' \
--data-raw '{"config": {"url": "http://example.org"}}'
```

_Pay attention, that `url` you use in the `config` should return 200 or 201 HTTP code for POST request with json body `{"test": 1}`, in other case API will not allow you to create callback._

You may use one callback for different listeners.

In the response you will receive JSON object.  In the next step you will need `id` from it.

### Create listener

Next step is creating listener. 

```
curl -L -X POST 'https://api.phone.com/v4/accounts/VOIP_ID/integrations/events/listeners' \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer YOUR_ACCESS_TOKEN' \
--data-raw '{"callback_id": CALLBACK_ID}'
```

In the response you will receive JSON object. In the next step you will need `id` from it.

### Create subscription

Now you need to subscribe your listener to some events. In the subscription you should define `:tags` of events you want receive.

```
curl -L -X POST 'https://api.phone.com/v4/accounts/VOIP_ID/integrations/events/listeners/LISTENER_ID/subscriptions' \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer YOUR_ACCESS_TOKEN' \
--data-raw '{":tags": ["call"]}'
```

More about [tags](./docs/tags.md).

It may take up to 5 minutes for your new listener to start send you events.

## Technical support

Email: api@phone.com