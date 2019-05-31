This chapter provides information in order to start integration straight away.

## Production Environment

**Wirecard ePOS Production environment** is available on the following URL:

    https://switch.wirecard.com/mswitch-server/
    
## Test Environment

**Wirecard ePOS Test environment** is provided to integrators for their development purposes. It is available on the following URL:
       
    https://switch-test.wirecard.com/mswitch-server/
    
!!! Tip

    Wirecard ePOS API is available via [**Swagger UI**](https://swagger.io/tools/swagger-ui/) on the following URL:

        https://switch-test.wirecard.com/mswitch-server/swagger-ui.html
        
    Wirecard ePOS credentials for Test environment are needed in order to access and interact with [Swagger UI](https://swagger.io/tools/swagger-ui/).
       
## Authentication

At the moment, only [basic authentication](https://en.wikipedia.org/wiki/Basic_access_authentication) is supported.

You will receive Wirecard ePOS credentials (username & password) after [contacting Wirecard](https://www.wirecard.com/contact). 

!!! Tip
    
    You can check your credentials with the following CURL request:
    
        curl -X GET "https://switch.wirecard.com/mswitch-server/v1/info/version" -H "accept: text/plain" -u {YourUsername}:{YourPassword}
        
    Upon successful authentication, response includes current system version.