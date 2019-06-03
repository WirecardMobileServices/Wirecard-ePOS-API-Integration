This chapter describes how can merchant manage its own users. User account is required for any interaction with Wirecard ePOS API.

## Create new user

In order to create new user, make a [`POST /v1/users`](https://switch.wirecard.com/mswitch-server/v1/users) call:

### Request
        
    {
        "username": "john.doe",
        "email": "john.doe@example.com",
        "firstName": "John",
        "lastName": "Doe",
        "merchant": {
            "id": "{MerchantId}"
            },
        "password": "{UserPassword}",
        "roles": [
            "MERCHANT_ADMIN"
        ],
        "status": "ENABLED",
        "timeZone": "Europe/Berlin"
        "returnForbidden": "true"
    }

- `"username"` - user's login name
- `"email"` - _optional field_ - if not provided, it is not possible to send reset password link
- `"firstName"` - user's first name
- `"lastName"` - user's last name
- `"merchant"`
    - `"id"` - identifier of merchant assigned by Wirecard ePOS system
- `"password"` - temporary password, it has to be changed upon first use; password is valid maximum 90 days; see also [Security](security.md) chapter
- `"roles"` - role defines permissions provided to a particular user; following merchant-related roles are available:
    - `"MERCHANT_ADMIN"` - see all merchant sales and can create new user accounts 
    - `"MERCHANT_ADVANCED_USER"` - see all merchant sales
    - `"MERCHANT_USER"` - see only own sales
- `"status"` - either `"ENABLED"` or `"DISABLED"`
- `"timeZone"` - user's time zone
- `"returnForbidden"` - _optional field_ - boolean value; applicable only for `"MERCHANT_ADVANCED_USER"` or `"MERCHANT_USER"`
    - `"true"` - user is not able to perform RETURN operation
    - `"false"` - user is able to perform RETURN operation

### Response

In addition to fields echoed from request, response includes following fields:

    {        
        ...
        "id": "58d8a33faceb4ddf85061f2a975e5525",
        "merchant: { ...
        },
        "failedLoginCount": 0,
        "requestPasswordChange": true,
        "returnForbidden": false,
        "accountExpirationReference": "2019-04-08T11:52:00.169Z",
        "lastPasswordChanged": "2019-04-08T11:52:00.169Z"
    }
        
- `"id"` - user identifier assigned by Wirecard ePOS system
- `"merchant"` - entire merchant object; see [Merchant Details](merchant.md)
- `"failedLoginCount"` - counter of failed authentication; it resets on successful login or password change
- `"requestPasswordChange"` - when `"true"`, user is enforced to change his password
- `"accountExpirationReference"` - date-time of latest user interaction with Wirecard ePOS system
- `"lastPasswordChanged"` - date-time of latest user password change

## List all users

In order to list all users, make a `GET /v1/users` call.

## Get a user

In order to get a specific user, make a `GET /v1/users/{id}` call.