# Get device status
```http
GET /v1.0/devices/{deviceId}/status
```

## Description
Get the status of a physical device that has been added to the current user's account.

Physical devices refer to the following SwitchBot products,

 -  Bot
 -  Plug
 -  Curtain
 -  Meter
 -  Humidifier
 -  Smart Fan

## Path parameters

| Name     | Type   | Required | Description |
| -------- | ------ | -------- | ----------- |
| deviceId | String | Yes      | device ID   |

## Responses
The response is basically a JSON object, which contains the following properties,

| Key Name   | Value Type   |
| ---------- | ------------ |
| statusCode | Integer      |
| message    | String       |
| body       | Object&lt;body&gt; |

body object contains the following properties,

| Key                    | Value Type | Description                                                  |
| ---------------------- | ---------- | ------------------------------------------------------------ |
| deviceId               | String     | device ID                                                    |
| deviceType             | String     | device type                                                  |
| hubDeviceId            | String     | device's parent Hub ID                                       |
| power                  | String     | only available for Bot/Plug/Humidifier devices. ON/OFF state |
| humidity               | Integer    | only available for Meter/Humidifier devices. humidity percentage |
| temperature            | Float      | only available for Meter/Humidifier devices. temperature in celsius |
| nebulizationEfficiency | Integer    | only available for Humidifier devices. atomization efficiency % |
| auto                   | Boolean    | only available for Humidifier devices. determines if a Humidifier is in Auto Mode or not |
| childLock              | Boolean    | only available for Humidifier devices. determines if a Humidifier's safety lock is on or not |
| sound                  | Boolean    | only available for Humidifier devices. determines if a Humidifier is muted or not |
| calibrate              | Boolean    | only available for Curtain devices. determines if a Curtain has been calibrated or not |
| group                  | Boolean    | only available for Curtain devices. determines if a Curtain is paired with or grouped with another Curtain or not |
| moving                 | Boolean    | only available for Curtain devices. determines if a Curtain is moving or not |
| slidePosition          | Integer    | only available for Curtain devices. the percentage of the distance between the calibrated open position and close position that a Curtain has moved to |
| mode                   | Integer    | only available for Smart Fan devices. the fan mode           |
| speed                  | Intger     | only available for Smart Fan devices. the fan speed          |
| shaking                | Boolean    | only available for Smart Fan devices. determines if the fan is swinging or not |
| shakeCenter            | Intger     | only available for Smart Fan devices. the fan's swing direciton |
| shakeRange             | Intger     | only available for Smart Fan devices. the fan's swing range, 0~120° |

The reponses may contain the following codes and message,

| Status Code | Body Content       | Message      | Description |
| ----------- | ------------------ | ------------ | ----------- |
| 100         | Device list object | success      | Returns an object that contains two device lists |
| n/a       | n/a | Unauthorized | Http 401 Error. User permission is denied due to invalid token. |
| 190         | n/a | System error | Device internal error due to device states not synchronized with server |

## Sample

### SwitchBot Meter example

Request the status of a SwitchBot Thermometer and Hygrometer

Request

```http
GET https://api.switch-bot.com/v1.0/devices/C271111EC0AB/status
```

Response


```js
{
    "statusCode": 100,
    "body": {
        "deviceId": "C271111EC0AB",
        "deviceType": "Meter",
        "hubDeviceId": "FA7310762361",
        "humidity": 52,
        "temperature": 26.1
    },
    "message": "success"
}
```

### SwitchBot Curtain example

Request the status of a SwitchBot Curtain

Request

```http
GET https://api.switch-bot.com/v1.0/devices/E2F6032048AB/status
```

Response


```js
{
    "statusCode": 100,
    "body": {
        "deviceId": "E2F6032048AB",
        "deviceType": "Curtain",
        "hubDeviceId": "FA7310762361",
        "calibrate": true,
        "group": false,
        "moving": false,
        "slidePosition": 0
    },
    "message": "success"
}
```
