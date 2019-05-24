This chapter describes how can merchant manage its own users. User account is required for any interaction with Wirecard ePOS API.

## Create a new user

    POST https://switch.wirecard.com/mswitch-server/v1/users

        {
            "username": "john.doe",
            "email": "john.doe@example.com",
            "firstName": "John",
            "lastName": "Doe",
            "merchant": {
                "id": "{{YourMerchantId}}"
                },
            "password": "Password123!",
            "roles": [
                "MERCHANT_ADMIN"
            ],
            "status": "ENABLED",
            "timeZone": "Europe/Berlin"
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

## List all users

    GET https://switch.wirecard.com/mswitch-server/v1/users

## Get a specific user

    GET https://switch.wirecard.com/mswitch-server/v1/users/{userId}
