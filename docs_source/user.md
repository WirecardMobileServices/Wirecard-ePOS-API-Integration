# User management

Purpose of this chapter is to describe how can merchant manage its own users. User account is required as the whole communication with ePOS system is done via particular user account.

ePOS backend API calls used for managing user accounts are described below:

##### 1. Create a new user
POST /v1/users

with the example body: 
~~~~
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
~~~~

User role defines what operations (API calls) are available to a particular user account. Wirecard ePOS backend provides following user roles:
- Merchant Admin - see all merchant sales and can create new user accounts 
- Merchant Advanced User - see all merchant sales
- Merchant User - see only own sales

##### 2. List all user accounts
GET /v1/users
##### 3. Get a specific user account
GET /v1/users/{userId}

