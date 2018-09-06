# Errors

> Example of detailed error response:

```json
{
  "message": "Failed", 
  "errors": [
    {
      "resource": "MUS::User", 
      "field": "username", 
      "error": "is already taken"
    }
  ]
}
```

We try to return a usefull HTTP status code, and together with that often a JSON response with details about the error.

Error Code | Meaning
---------- | -------
400 | Bad Request -- Just plain wrong request, could not find a way to handle that.
401 | Unauthorized -- Your API key is wrong.
404 | Not Found -- The requested data could not be found.
422 | Unprocessable entity -- The data you gave us was not valid, please se details in JSON.
500 | Internal Server Error -- Please check that you at least tried to supply company_id or access_token headers.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.
