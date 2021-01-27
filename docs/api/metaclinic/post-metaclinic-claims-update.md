# POST/ /api/v1/metaclinic/claims/update


## Overview

- [Description](#description)
- [Authentication](#authentication)
- [Request construction](#request-construction)
  - [Query fields](#query-fields)
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

When a claim is updated in the Metaclinic LIMS it will trigger a request
on the APS Hub for proxied update to APS' payment processor. . You
need to be authenticated and authorized on the APS Hub application to use
this route. The server will [respond](#success-responses) according to the
results of the supplied [input fields](#body-parameters).

## Authentication

You must be an authenticated user to receive an eligibilty status See [Authentication](../auth/README.md).
Use the [`auth/login`](../auth/post-auth-login.md) endpoint to receive your token.
Supply the token in the Authorization Header as a bearer token.

## Request construction

### Body parameters

Pass parameters in the request body. All fields are
optional unless marked with `REQUIRED`.

> **TBA: FOR METACLINIC** to match the current request schema.

| Parameter                  | Type        | Required | Description                        |
|----------------------------|-------------| :------: |------------------------------------|
|                            |             |          |                                    |

### Example request

```GET /api/v1/metaclinic/claims/create```


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
    param: "env",
    value: "notavalidenv,
    msg: "Must include a valid envrionment name env|hotfix|stagin-api"
  },
  {
    location: "body",
    param: "lab",
    value: "",
    msg: "Must include a valid lab code"
  }
]
```

#### `401 UNAUTHORIZED`
**Condition** \
User does not have the proper role for the requesed operation.

**Returns** \
A string with following message.

**Example return**
``` Javascript
"You do not have the appropriate role"
```

#### `403 FORBIDDEN`
**Condition** \
User has not signed into the appliation. The token is either invalid
or missing.

**Returns** \
The following message as a string

**Example return**
``` Javascript
"You must sign in before you can do that."
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
