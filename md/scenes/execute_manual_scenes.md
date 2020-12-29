# Execute manual scenes

```http
POST /v1.0/scenes/{sceneId}/execute
```

## Description

Sends a request to execute a manual scene.

## Path parameters

| Name    | Type   | Required | Description |
| ------- | ------ | -------- | ----------- |
| sceneId | String | Yes      | scene ID    |

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
| 190                         | Device internal error due to device states not synchronized with server |

## Sample

### Execute a scene

Request

```http
POST https://api.switch-bot.com/v1.0/scenes/T02-202009221414-48924101/execute
```

Response

```js
{
    "statusCode": 100,
    "body": {},
    "message": "success"
}
```
