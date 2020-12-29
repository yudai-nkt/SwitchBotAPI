# Get device list

The devices API is used to access the properties and states of SwitchBot devices and to send control commands to those devices.

```http
GET /v1.0/devices
```

## Description
Get a list of devices, which include physical devices and virtual infrared remote devices that have been added to the current user's account.

Physical devices refer to the following SwitchBot products,
 -  Hub
 -  Hub Plus
 -  Hub Mini
 -  Bot (MUST enable Cloud Service first)
 -  Curtain (MUST enable Cloud Service first)
 -  Plug
 -  Meter
 -  Humidifier
 -  Smart Fan

Virtual infrared remote devices refer to virtual devices that are used to simulate infrared signals of a home appliance remote control.
A SwitchBot Hub Plus / Hub Mini is required in order to be able to create these virtual devices within the app. The types of appliances supported include,
 -  Air Conditioner
 -  TV
 -  Light
 -  IPTV/Streamer
 -  Set Top Box
 -  DVD
 -  Fan
 -  Projector
 -  Camera
 -  Air Purifier
 -  Speaker
 -  Water Heater
 -  Vacuum Cleaner
 -  Others

## Responses

The response is basically a JSON object, which contains the following properties,

| Key Name   | Value Type   |
| ---------- | ------------ |
| statusCode | Integer      |
| message    | String       |
| body       | Object&lt;body&gt; |

The body object contains the following properties,

| Key Name           | Value Type            | Description                               |
| ------------------ | --------------------- | ----------------------------------------- |
| deviceList         | Array&lt;device&gt;         | a list of physical devices                |
| infraredRemoteList | Array&lt;infraredRemote&gt; | a list of virtual infrared remote devices |

The deviceList array contains a list of objects with the following key-value attributes,

| Key                | Value Type      | Description                                                  |
| ------------------ | --------------- | ------------------------------------------------------------ |
| deviceId           | String          | device ID                                                    |
| deviceName         | String          | device name                                                  |
| deviceType         | String          | device type                                                  |
| enableCloudService | Boolean         | determines if Cloud Service is enabled or not for the current device |
| hubDeviceId        | String          | device's parent Hub ID                                       |
| curtainDevicesIds  | Array&lt;deviceId&gt; | only available for Curtain devices. a list of Curtain device IDs such that the Curtain devices are being paired or grouped |
| calibrate          | Boolean         | only available for Curtain devices. determines if the open position and the close position of a Curtain have been properly calibrated or not |
| group              | Boolean         | only available for Curtain devices. determines if a Curtain is paired with or grouped with another Curtain or not |
| master             | Boolean         | only available for Curtain devices. determines if a Curtain is the master device or not when paired with or grouped with another Curtain |
| openDirection      | String          | only available for Curtain devices. the opening direction of a Curtain |

The infraredRemoteList array contains a list of objects with the following key-value attributes,

| Key         | Value Type | Description                   |
| ----------- | ---------- | ----------------------------- |
| deviceId    | String     | device ID                     |
| deviceName  | String     | device name                   |
| remoteType  | String     | device type                   |
| hubDeviceId | String     | remote device's parent Hub ID |

The response may contain the following codes and messages,

| Status Code | Body Content       | Message      | Description |
| ----------- | ------------ | ----------- | ----------- |
| 100         | Device list object | success      | Returns an object that contains two device lists |
| n/a       | n/a | Unauthorized | Http 401 Error. User permission is denied due to invalid token. |
| 190         | n/a | System error | Device internal error due to device states not synchronized with server |

## Sample

### Get all devices

Request

```http
GET https://api.switch-bot.com/v1.0/devices
```

Response

```js
{
    "statusCode": 100,
    "body": {
        "deviceList": [
            {
                "deviceId": "500291B269BE",
                "deviceName": "Living Room Humidifier",
                "deviceType": "Humidifier",
                "enableCloudService": true,
                "hubDeviceId": "000000000000"
            }
        ],
        "infraredRemoteList": [
            {
                "deviceId": "02-202008110034-13",
                "deviceName": "Living Room TV",
                "remoteType": "TV",
                "hubDeviceId": "FA7310762361"
            }
        ]
    },
    "message": "success"
}
```
