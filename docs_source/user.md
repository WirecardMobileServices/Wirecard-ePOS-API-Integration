Purpose of this chapter is to describe how can merchant manage its own users. User account is required for any interaction with Wirecard ePOS API.

## Create a new user

    POST https://switch.wirecard.com/mswitch-server/v1/users
    
        {
           "username": "john.doe",
           "email": "john.doe@example.com",
           "firstName": "John",
           "lastName": "Doe",
           "merchant": {
             "id": "e5869bc0303b4dabbf1e593d619146dc"
           },
           "password": "Password123!",
           "roles": [
             "MERCHANT_ADMIN"
           ],
           "status": "ENABLED",
           "timeZone": "Europe/Berlin"
        }


User role defines permissions available to a particular user account. Wirecard ePOS provides following merchant-related roles:

- Merchant Admin - see all merchant sales and can create new user accounts 
- Merchant Advanced User - see all merchant sales
- Merchant User - see only own sales

## List all user accounts

    GET https://switch.wirecard.com/mswitch-server/v1/users

## Get a specific user account

    GET https://switch.wirecard.com/mswitch-server/v1/users/{userId}

