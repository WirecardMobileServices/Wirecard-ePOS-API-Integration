This chapter provides information in order to start integration straight away.

## Production Environment

**Wirecard ePOS PROD environment** is available on the following URL:

    https://switch.wirecard.com/mswitch-server/
    
## Test Environment

**Wirecard ePOS TEST environment** is provided to integrators for their testing purposes. It is available on the following URL:
       
    https://switch-test.wirecard.com/mswitch-server/
 
## Authentication

At the moment, only [basic authentication](https://en.wikipedia.org/wiki/Basic_access_authentication) is supported.

You will receive Wirecard ePOS credentials (username & password) after [contacting Wirecard](https://www.wirecard.com/contact). 

!!! Tip
    
    You can check your credentials with the following CURL request:
    
        curl -X GET "https://switch.wirecard.com/mswitch-server/v1/info/version" -H "accept: text/plain" -u {YourUsername}:{YourPassword}
        
    Upon successful authentication, response includes current system version.