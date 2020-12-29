# Standard HTTP Error Codes

The following table lists the most common HTTP error response,

| Code | Name                   | Description                                                  |
| :--- | :--------------------- | :----------------------------------------------------------- |
| 400  | Bad Request            | The client has issued an invalid request. This is commonly used to specify validation errors in a request payload. |
| 401  | Unauthorized           | Authorization for the API is required, but the request has not been authenticated. |
| 403  | Forbidden              | The request has been authenticated but does not have appropriate permissions, or a requested resource is not found. |
| 404  | Not Found              | Specifies the requested path does not exist.                 |
| 406  | Not Acceptable         | The client has requested a MIME type via the Accept header for a value not supported by the server. |
| 415  | Unsupported Media Type | The client has defined a contentType header that is not supported by the server. |
| 422  | Unprocessable Entity   | The client has made a valid request, but the server cannot process it. This is often used for APIs for which certain limits have been exceeded. |
| 429  | Too Many Requests      | The client has exceeded the number of requests allowed for a given time window. |
| 500  | Internal Server Error  | An unexpected error on the SmartThings servers has occurred. These errors should be rare. |
