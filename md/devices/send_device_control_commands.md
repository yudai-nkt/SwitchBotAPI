# Send device control commands

```http
POST /v1.0/devices/{deviceId}/commands
```

## Description

Send control commands to physical devices and virtual infrared remote devices.

## Command set for physical devices

The table below describes all the available commands for phsyical devices,

| deviceType     | commandType     | Command     |  command parameter    |  Description    |
| ---- | ---- | ---- | ---- | ---- |
|  Bot    |  command    | turnOff     | default     | set to OFF state |
| Bot | command | turnOn | default | set to ON state |
| Bot | command | press | default | trigger press |
| Plug     | command | turnOn | default | set to ON state |
| Plug | command | turnOff | default | set to OFF state |
| Curtain     | command |  setPosition    | index0,mode0,postion0<br />e.g. `0,ff,80` |  mode: 0 (Performance Mode), 1 (Silent Mode), ff (default mode) <br />postion: 0~100 (0 means opened, 100 means closed)  |
| Curtain | command |  turnOff    | default | equivalent to set position to 100 |
| Curtain | command |  turnOn    | default | equivalent to set position to 0 |
| Humidifier | command | turnOff | default | set to OFF state                                             |
| Humidifier | command | turnOn | default | set to ON state                                              |
| Humidifier | command |setMode  | `auto`or `101` or<br />  `102` or `103` or `{0~100}` | auto, set to Auto Mode,<br />101, set atomization efficiency to 34%,<br />102, set atomization efficiency to 67%,<br />103, set atomization efficiency to 100% |
| Smart Fan | command |turnOn | default | set to ON state |
| Smart Fan | command |turnOff | default | set to OFF state |
| Smart Fan | command | setAllStatus | power,fanMode,<br />fanSpeed,shakeRange<br/>e.g. `on,1,1,60` | power: off/on,<br />fanMode: 1/2,<br />fanSpeed: 1/2/3/4,<br />shakeRange: 0~120<br/>fanMode: 1 (Standard), 2 (Natural) |

## Command set for virtual infrared remote devices

The table below describes all the available commands for virtual infrared remote devices,

| deviceType                             | commandType | Command                    | command parameter                                            | Description                                                  |
| -------------------------------------- | ----------- | -------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| All home appliance types except Others | ""          | turnOn                     | default                                                      | every home appliance can be turned on by default             |
| All home appliance types except Others | command     | turnOff                    | default                                                      | every home appliance can be turned off by default            |
| Others                                 | `customize` | {user-defined button name} | default                                                      | all user-defined buttons must be configured with commandType=customize |
| Air Conditioner                        | command     | setAll                     | {temperature},{mode},{fan speed},{power state}<br />e.g. `26,1,3,on` | the unit of temperature is in celsius; <br />modes include 1 (auto), 2 (cool), 3 (dry), 4 (fan), 5 (heat); <br />fan speed includes 1 (auto), 2 (low), 3 (medium), 4 (high); <br />power state includes on and off |
| TV, IPTV/Streamer,  Set Top Box         | command     | SetChannel                 | {channel number}, e.g. 15                                | set the TV channel to switch to                              ||                                        | command     | setMute                    | default                                                      | mute/unmute                                                  |
|                                        | command     | volumeAdd                  | default                                                      | volume up                                                    |
|                                        | command     | volumeSub                  | default                                                      | volume down                                                  |
|                                        | command     | channelAdd                 | default                                                      | next channel                                                 |
|                                        | command     | channelSub                 | default                                                      | previous channel                                             |
| DVD, Speaker                           | command     | setMute                    | default                                                      | mute/unmute                                                  |
|                                        | command     | FastForward                | default                                                      | fast forward                                                 |
|                                        | command     | Rewind                     | default                                                      | rewind                                                       |
|                                        | command     | Next                       | default                                                      | next track                                                   |
|                                        | command     | Previous                   | default                                                      | last track                                                   |
|                                        | command     | Pause                      | default                                                      | pause                                                        |
|                                        | command     | Play                       | default                                                      | play/resume                                                  |
|                                        | command     | Stop                       | default                                                      | stop                                                         |
| Speaker                                | command     | volumeAdd                  | default                                                      | volume up                                                    |
|                                        | command     | volumeSub                  | default                                                      | volume down                                                  |
| Fan                                    | command     | swing                      | default                                                      | swing                                                        |
|                                        | command     | timer                      | default                                                      | set timer                                                    |
|                                        | command     | lowSpeed                   | default                                                      | set fan speed to low                                         |
|                                        | command     | middleSpeed                | default                                                      | set fan speed to medium                                      |
|                                        | command     | highSpeed                  | default                                                      | set fan speed to high                                        |
| Light                                  | command     | brightnessUp               | default                                                      | brightness up                                                |
|                                        | command     | brightnessDown             | default                                                      | brightness down                                              |

>  Note: Most of the devices support `turnOn` or `turnOff`, which are case-sensitive. For infrared remote devices, when you have created customized buttons, you must set `commandType` to `customize`, otherwise the command will not work. `command` needs to be set to the name of the customized button.



## Path parameters

| Name     | Type   | Required | Description |
| -------- | ------ | -------- | ----------- |
| deviceId | String | Yes      | device ID   |

## Request body parameters

| Name        | Type   | Required | Description                                                 |
| ----------- | ------ | -------- | ----------------------------------------------------------- |
| command     | String | Yes      | the name of the command                                     |
| parameter   | String | No       | some commands require parameters, such as `SetChannel`      |
| commandType | String | No       | for customized buttons, this needs to be set to `customzie` |

## Response

The response is basically a JSON object, which contains the following properties,

| Key Name   | Value Type   |
| ---------- | ------------ |
| statusCode | Integer      |
| message    | String       |
| body       | Object&lt;body&gt; |

## Errors

| Error code/message          | Description                                                  |
| --------------------------- | ------------------------------------------------------------ |
| {"message": "Unauthorized"} | Http 401 Error. User permission is denied due to invalid token. |
| 151                         | device type error                                            |
| 152                         | device not found                                             |
| 160                         | command is not supported                                     |
| 161                         | device offline                                               |
| 171                         | hub device is offline                                        |
| 190                         | Device internal error due to device states not synchronized with server. Or command fomrat is invalid. |

## Sample

### Bot example

Turn a Bot on

Request

```http
POST https://api.switch-bot.com/v1.0/devices/210/commands
```

```js
{
    "command": "turnOn",
    "parameter": "default",
    "commandType": "command"
}
```

Response

```js
{
    "statusCode": 100,
    "body": {},
    "message": "success"
}
```



### Infrared remote device example

Set an Air Conditioner

Request

```http
POST https://api.switch-bot.com/v1.0/devices/02-202007201626-70/commands
```

```js
{
    "command": "setAll",
    "parameter": "26,1,3,on",
    "commandType": "command"
}
```

Response

```js
{
    "statusCode": 100,
    "body": {},
    "message": "success"
}
```



Trigger a customized button

Request

```http
POST https://api.switch-bot.com/v1.0/devices/02-202007201626-10/commands
```

```js
{
    "command": "ボタン", // the name of the customized button
    "parameter": "default",
    "commandType": "customize"
}
```

Response

```js
{
    "statusCode": 100,
    "body": {},
    "message": "success"
}
```
