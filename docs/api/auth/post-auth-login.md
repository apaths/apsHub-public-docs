# POST/ /api/v1/auth/login


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

You must be authenticated and send a unique user token to access API
routes. To successfully retreive a token you must be a registered
user, and submit a matching password. If you are need to register
as a user [See Registration](../../registration/README.md) for
instructions.


## Request construction

### Body parameters

Pass parameters in the request body. All fields are
optional unless marked with `REQUIRED`.

> **TBA: FOR METACLINIC** to match the current request schema.

| Parameter                  | Type        | Required | Description                        |
|----------------------------|-------------| :------: |------------------------------------|
| email                      | String      | REQUIRED | Email used for account             |
| password                   | String      | REQUIRED | Password for the account           |

### Example request

```GET /api/v1/metaclinic/claims```


## Success responses

#### `200 OK`

**Condition** \
User is authenticated, authorized, and the `eligibility` object was retreived
successfully.

**Returns** \
An object with the schema shown below.

> **TBA: FOR METACLINIC** to match the current request schema.

**Example return**
``` Javascript
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6I",
  "user": {
    "id": 278,
    "name": "Hugh Janis",
    "roles": [
      "Basic"
    ]
  }
}
```


## Client error responses

#### `400 BAD REQUEST`

**Condition** \
Invalid input was supplied.

**Returns** \
Status code and list of invalid parameters and messages.

**Example request**
```GET /api/v1/metaclinic/eligibility```

> **TBA FOR METACLINIC** need the request inputs to complete.

**Example return**
``` Javascript
[
  {
    location: "body",
    param: "email",
    value: "notavalidenv,
    msg: "Must be a valid email"
  },
  {
    location: "body",
    param: "password",
    value: "",
    msg: "Must include a password"
  }
]
```

#### `401 UNAUTHORIZED`
**Condition** \
User does not have the proper role for the requesed operation.

**Returns** \
A one-element array like the example below.

**Example return**
``` Javascript
[
  {
    "param": "account",
    "location": "body",
    "msg": "Unknown email or username"
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
