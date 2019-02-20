# Authentication

<aside class="notice">
The API access token is created by our support team at info@musskema.dk.
</aside>

## JWT (JSON web token)

> Example of authentication with JWT:

```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json'
 -H 'JWT: eyJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1NTA1NjI2OTcsIm5iZiI6MTU1MDU2MjY5MiwiY29tcGFueV9pZCI6IjEwMDAwMSJ9.FvEyb9ZAKPVsI2OUd91UzlYlrnecuhQqCd-_dVRK79w'
 -X GET 'https://api.secure2.musskema.dk/v3/core/departments'
```

We have choosen [JWT](https://jwt.io) for authentication. There are lots of open source libraries for many languages, so it should be fairly easy to implement.
With JWT we do not expose the pre-shared API access token in a header, and we get expiration on request tokens thus reducing the risk of replay attacks.

> Example of JWT payload:

```JSON
{
  "exp": 1550562697,
  "nbf": 1550562692,
  "company_id": 100001
}
```

There are a number of features in JWT, we have choosen to use the following:

- Algorithm for signature is `HS256`.
- Both `exp` and `nbf` are required, and there can be no more than 15 seconds between.
- The secret to sign the JWT token is the API access token you got from our support team.

In the JWT payload you should send `company_id` = your company ID on Musskema.dk.

Try to paste the token from the example on [jwt.io](https://jwt.io) and see the contents of the token.

## Old plaintext header authentication

```shell
# With shell, you can just pass the correct header with each request
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json'
 -H 'company_id: 10238497'
 -H 'access_token: 01298347edf923874a'
 -X GET 'https://api.secure2.musskema.dk/v3/core/departments'
```

> Make sure to replace `01298347edf923874a` with your API key and `10238497` with your company id.

Authentication is done by HTTP headers. You must supply both company_id and access_token headers.
This feature is still enabled, for backward compatibility, but it is strongly encouraged to use JWT authentication header.

## IP whitelist

On top of authentication it is possible to lock down the API to a select number of IPv4 adresses. Contact our support team if you wish to enable this feature.
