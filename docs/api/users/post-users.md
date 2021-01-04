# POST/ /api/v1/users


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

Use the `POST/ api/v1/users` endpoint to create new users. When
you submit a new user [request](#request-construction) the user
will receive a notification email. Accounts require approval by
and APS Admin before they can be used.

After APS Admin verifies your identity and account, you can then
[login](../auth/post-auth-login.md) to your account to obtain
an API token.

## Request construction

### Body parameters

Pass parameters in the request body. All fields are
optional unless marked with `REQUIRED`.

| Parameter                  | Type        | Required | Description                        |
|----------------------------|-------------| :------: |------------------------------------|
| name                       | String      |          | Name of the person                 |
| email                      | String      | REQUIRED | Email for account                  |
| password                   | String      | REQUIRED | Password for the account           |

### Example request

```GET /api/v1/users```


## Success responses

#### `200 OK`

**Condition** \
User is has sent valid request data and the account was created
successfully.

**Returns** \
An object with the schema shown below.

**Example return**
``` Javascript
{
  "id": 278,
  "created_at": "2020-03-23T00:03:00Z"
}
```


## Client error responses

#### `400 BAD REQUEST`

**Condition** \
Invalid input was supplied.

**Returns** \
Status code and list of invalid parameters and messages.

**Example request**
```GET /api/v1/users```

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
