# Authentication

## Overview

- [Introduction](#introduction)
- [Request a token](#request-a-token)
  - [Responses](#responses)
- [Include a token in API requests](include-a-token-in-api-requests)


## Introduction

You need a token to access API routes. You must be a
[registered user](../../registration/readme.md) and have been verified by an APS
adminstrator to successfully [request a token](#request-a-token).


## Request a token

If you're a [registered user](../../registration/readme.md) you can request a token
with by submitting your email and password to the [`api/v1/auth/login`](./post-auth-login.md)
endpoint. Call the route as follows:

**Method:** `POST/` \
**Route:** `/api/v1/auth/login`

Pass the following parameters in the body.

| Parameter        | Type         | Required | Description
|------------------|--------------| :------: |----------------------------------|
| email            | String       | REQUIRED | Email used for you account       |
| password         | String       | REQUIRED | Password for your account        |

### Responses

`200 SUCCESSFUL`
Body will include an object with a token.

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

See the [POST/ `api/v1/auth/login`](./post-auth-login.md) document for
complete error and response information.


## Include a token in API requests

You need to include the access token in an `Authorization` request header, as a
`Bearer` token.

For example in Postman, you can submit your token as a header with the following:

**Key**: Authorization
**Value**: "Bearer eyJhbGciOiJIUzI1NiIsInR5..."

