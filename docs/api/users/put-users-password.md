# `PUT/` api/v1/users/password


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

Users can reset their password with the `PUT/ api/v1/users/password
endpoint if they have a valid reset token and supply a new valid
password. Reset tokes are available from the
[`POST/ api/v1/users/password/reset](./post-users-password-reset.md)
endpoint.

Note that the token is only good for a few minutes.

## Request construction

### Body parameters

Pass parameters in the request body. All fields are
optional unless marked with `REQUIRED`.

| Parameter                  | Type        | Required | Description                        |
|----------------------------|-------------| :------: |------------------------------------|
| password                   | String      | REQUIRED | New password for the account       |
| token                      | String      | REQUIRED } A temporary, encrypted, token used to authenticate the user |


### Example request

```PUT /api/v1/users/password```


## Success responses

#### `200 OK`

**Condition** \
User the token an password are valid and the new password is set
successfully.

**Returns** \
An object with the schema shown below.

**Example return**
``` Javascript
{
  "message": "Password reset. Go login or get a token"
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
    param: "password",
    value: "123,
    msg: "Must be at least 8 characters long"
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
