# POST/ /api/v1/users/password/reset


## Overview

- [Description](#description)
- [Request construction](#request-construction)
  - [Body parameters](#body-parameters)
  - [Example request](#example-request)
- [Success responses](#success-responses)
  - [`200 OK`](#200-ok)
- [Client error responses](#client-error-responses)
  - [`400 BAD REQUEST`](#400-bad-request)
  - [`401 UNAUTHORIZED`](#401-unauthorized)
  - [`403 FORBIDDEN`](#403-forbidden)
  - [`429 TOO MANY REQUESTS`](#429-too-many-requests)
- [Server error responses](#server-error-responses)
  - [`500 SERVER ERROR`](#500-server-error)
  - [`503 SERVICE UNAVAILABLE`](#503-service-unavailable)


## Description

If users forget their password, a reset can be requested with
the `POST/ api/v1/users/password/reset` endpoint. On a successful
[request](#request-construction) the user will recieve an email
with a special reset link.

**THIS IS TBA.**  *For now, the link in the email is non-functional.
You will have to copy the token portion of the link and use it
in the [`PUT/ api/v1/users/password`](./put-users-password.md)
endpoint request using Postman or CURL.*

Note that the token is only good for a few minutes.

## Request construction

### Body parameters

Pass parameters in the request body. All fields are
optional unless marked with `REQUIRED`.

| Parameter                  | Type        | Required | Description                        |
|----------------------------|-------------| :------: |------------------------------------|
| email                      | String      | REQUIRED | Email for account                  |


### Example request

```POST /api/v1/users/password/reset```


## Success responses

#### `200 OK`

**Condition** \
User exists and a password reset workflow was successfully initiated.

**Returns** \
An object with the schema shown below.

**Example return**
``` Javascript
{
  "message": "Check your email!"
}
```


## Client error responses

#### `400 BAD REQUEST`

**Condition** \
Invalid input was supplied.

**Returns** \
Status code and list of invalid parameters and messages.

**Example request**
```POST /api/v1/users/password```

**Example return**
``` Javascript
[
  {
    location: "body",
    param: "email",
    value: "notavalidenv,
    msg: "Must be a valid email"
  }
]
```

#### `429 TOO MANY REQUESTS`
**Condition** \
User has supplied too many operations in too short of a time interval.

**Returns** \
The following message as a string

**Example return**
``` Javascript
"Too many requests. Take a break, man."
```


## Server error responses


#### `500 SERVER ERROR`
**Condition** \
This is a generic, temporary error. The server is having a problem
but should return to service soon. If this error persists--contact support.

**Returns** \
The following message as a string

**Example return**
``` Javascript
"Temporary server error. You may want to try again in a few minutes."
```

#### `503 SERVICE UNAVAILABLE`
**Condition** \
This is an intentional server shut down due to maintenance
(for example) but will return to service (it's not permanent). Unlike
`500 SERVER ERROR` there is no need to contact support if the error is encountered.
