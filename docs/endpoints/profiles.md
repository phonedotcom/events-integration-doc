# Profiles

A Profile allows to specify a notifications email for a callback. Notifications are emitted  when there is a need to notify the callback owner of some issues like timeouts, or de-registration of the callback.

## Get list of profiles

Returns list of profiles created on the account (or extension)

```
GET https://api.phone.com/v4/accounts/VOIP_ID/integrations/events/profiles
```

### Optional query parameters

* `limit` - limits the number of items in the output (the default is 25)
* `offset` - list offset (the default is 0)

### Response example

```json
{
  "filters": {},
  "sort": {
    "id": "desc"
  },
  "limit": 25,
  "offset": 0,
  "items": [
    {
      "id": 389,
      "voip_id": 1000002,
      "extension_id": null,
      "name": "My special profile",
      "support_email": "support@example.org",
      "created_at": 1591869178
    },
    {
      "id": 383,
      "voip_id": 1000002,
      "extension_id": null,
      "name": "Profile which uses default account's email",
      "support_email": null,
      "created_at": 1588015093
    }
  ]
}
```

## Get profile

Returns a profile

```
GET https://api.phone.com/v4/accounts/VOIP_ID/integrations/events/profiles/PROFILE_ID
```

### Response example

```json
{
  "id": 389,
  "voip_id": 1000002,
  "extension_id": null,
  "name": "My special profile",
  "support_email": "support@example.org",
  "created_at": 1591869178
}
```

_Pay attention that if config has headers with names like `Authorization` or `X-Api-Key` value in the output will be replaced with `true`._ 

## Create profile

Creates profile

```
POST https://api.phone.com/v4/accounts/VOIP_ID/integrations/events/profiles/PROFILE_ID
```

### Request

JSON with the following mandatory parameters:

* `name` - `string`, the profile name
* `support_email` - `string`, notification email in case of no-responsive callback.

#### Example

```json
{
    "name": "My profile",
    "support_email": "test@example.org"
}
```

### Response

Similar to the "Get profile" response.


## Update profile

Updates one or more properties of a profile

```
PATCH https://api.phone.com/v4/accounts/VOIP_ID/integrations/events/profiles/PROFILE_ID
```

### Request

JSON with any of the parameters needed for the "Create profile" API.

### Response

Similar to the "Get profile" response.

## Delete profile

Deletes profile. Pay attention, that API will not allow you to delete profile which is associated to a callback. 

```
DELETE https://api.phone.com/v4/accounts/VOIP_ID/integrations/events/profiles/PROFILE_ID
```

### Response

Successful:

```json
{
  "success": true
}
```
