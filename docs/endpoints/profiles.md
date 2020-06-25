# Profiles

Profile allows to specify support email for the callback.

## Get list of profiles

Returns list of profiles you have on account (extension)

```
GET https://api.phone.com/v4/accounts/VOIP_ID/integrations/events/profiles
```

### Optional query parameters

* `limit` - limit of the items in the output (default is 25)
* `offset` - list offset (default is 0)

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

Returns profile

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

JSON with these mandatory parameters:

* `name` - `string`, profile name
* `support_email` - `string`, email for callback's support (will be used in case of problems with callback)

#### Example

```json
{
    "name": "My profile",
    "support_email": "test@example.org"
}
```

### Response

The same as for "Get profile".


## Update profile

Updates some properties of the profile

```
PATCH https://api.phone.com/v4/accounts/VOIP_ID/integrations/events/profiles/PROFILE_ID
```

### Request

JSON with any of parameters available for "Create profile".

### Response

The same as for "Get profile".

## Delete profile

Deletes profile. Pay attention, that API will not allow you to delete profile which is used for some callback. 

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
