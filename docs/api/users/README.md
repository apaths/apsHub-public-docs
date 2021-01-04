# Users

- [Introduction](#introduction)
- [API Reference](#api-reference)

## Introduction

The Users service provides methods for managing accounts of people that
use the APS Hub. These routes can also be used by API consumers to
self-serve registration and password management.

## Registration

You can use the [/api/v1/users](./post-users.md) endpoint to register
yourself for APS Hub. You account won't be useable until you are
validated by an APS Administrator. After validtion, you can
get an API token at any time by logging in. Use the
[`/api/v1/auth/login`](../auth/post-auth-login.md) endpoint to
get your api token.

## API Reference

**Create a new user (or register)**\
[`POST /api/v1/users`](./post-users.md)

**Request a password reset**\
[`POST /api/v1/users/password/reset`](./post-users-password-reset.md)

**Set a new password**\
[`PUT /api/v1/users/password`](./put-users-password.md)

