# SMS Autoresponder

This application allows you to configure automatic SMS responce (notification).

## Configuration

Name of the application: `sms-autoresponder`

### Parameters

* `message` - mandatory parameter; text of the message
* `rate-limit` - from 60 to 2592000; default is 300; period in seconds, how often message can be sent from your number to each number from one listener 

## Example

```json
    {
      "name": "My SMS autoresponder",
      "mode": "APPLICATION",
      "config": {
        "application": "sms-autoresponder",
        "parameters": {
          "message": "Please, call us instead of sending SMS"
        }
      }
    }
```
