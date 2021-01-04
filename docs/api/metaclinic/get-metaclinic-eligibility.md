# GET/ /api/v1/metaclinic/eligibility


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

Fetch the state of a patient's eligibility with the APS payment processor. You
need to be authenticated and authorized on the APS Hub application to use
this route. The server will [respond](#success-responses) according to the
results of the supplied [input fields](#body-parameters).

## Authentication

You must be an authenticated user to receive an eligibilty status See [Authentication](../auth/README.md).
Use the [`auth/login`](../auth/post-login.md) endpoint to receive your token.
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

```GET /api/v1/metaclinic/eligibility```


## Success responses

#### `200 OK`

**Condition** \
User is authenticated, authorized, and the `eligibility` object was retreived
successfully.

**Returns** \
An object with the schema shown below.

**Example return**
``` Javascript
{
  "patientEligibilityChecks": [
    {
      "ID": 607575,
      "payerID": 701,
      "casePatientID": 547785,
      "payerClearingHouseID": 701,
      "insuranceType": 1,
      "eligibilityCheckDate": "2020-12-30T19:31:25.789Z",
      "eligibilityRequestID": "16093566857895141",
      "eligibilityResult": true,
      "eligibilityResponse": "ELIGIBLE",
      "eligibilityError": "",
      "responseFileStorageLinkID": 4405205,
      "patientData": {
        "payerID": "64157",
        "accessionID": "Y20-01717",
        "insuranceID": "12345",
        "dateOfService": "2020-12-28",
        "insuredGender": "M",
        "patientGender": "M",
        "sequenceNumber": "16093566857895141",
        "insuredLastName": "Cole",
        "patientLastName": "Cole",
        "insuredFirstName": "James",
        "patientFirstName": "James",
        "insuredMiddleName": "T",
        "patientMiddleName": "T",
        "insuredDateOfBirth": "1915-06-13",
        "patientDateOfBirth": "1915-06-13",
        "insuredRelationship": "self",
        "patientSocialSecurityNumber": "444-44-4444"
      }
    }
  ]
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
