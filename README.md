# Phone.com events v. 2 integration guide

Phone.com provides support for webhooks (HTTPS callbacks) and some other types of integration for different [events](./docs/events-format.md) associated with Phone.com accounts.

## Getting started

There are endpoints in the API that allow you to configure callbacks and subscribe only to the events you need.

You need to have an access token to use the Phone.com API. Contact support by email at api@phone.com to discuss your integration and get a key.

Full documentation of all endpoints can be found [here](./docs/api-endpoints.md); this section of the document discusses only the minimal set-up you need to start receiving events.

### Create callback

First, you will need to define a callback:

```
curl -L -X POST 'https://api.phone.com/v4/accounts/VOIP_ID/integrations/events/callbacks' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer YOUR_ACCESS_TOKEN' \
  --data-raw '{"config": {"url": "http://example.org"}}'
```

_Pay attention that the `url` you use in the `config` should return 200 or 201 HTTP code to a POST request with a JSON body `{"test": 1}`, else the API will not allow you to create a callback._

You may use one callback for multiple different listeners.

In the response you will receive a JSON object.  In the next step you will need the `id` provided in the callback JSON object.

### Create listener

The next step is creating the listener:

```
curl -L -X POST 'https://api.phone.com/v4/accounts/VOIP_ID/integrations/events/listeners' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer YOUR_ACCESS_TOKEN' \
  --data-raw '{"callback_id": CALLBACK_ID}'
```

In the response you will receive a JSON object. Like before, you will need the `id` from that JSON object for the next step.

### Create subscription

Now you need to have your listener to subscribe to some events. In the subscription, you should define the `:tags` of the events you want to receive.

```
curl -L -X POST 'https://api.phone.com/v4/accounts/VOIP_ID/integrations/events/listeners/LISTENER_ID/subscriptions' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer YOUR_ACCESS_TOKEN' \
  --data-raw '{":tags": ["call"]}'
```

Find out more about [tags](./docs/tags.md).

Note: Due to caching it may take up to 5 minutes for your new listener to be activated.

### Create filter

There is a way to filter events. For example, by phone number:

```
curl -L -X POST 'https://api.phone.com/v4/accounts/VOIP_ID/integrations/events/listeners/LISTENER_ID/filters' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer YOUR_ACCESS_TOKEN' \
  --data-raw '{"filter_type": "number", "filter_value": { "eq": "+15551234567" }}'
```

## Technical support

Email: api@phone.com
