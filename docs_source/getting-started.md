This chapter provides all information you need to know in order to start your integration right away. 
 
## Authentication and Security

First of all, you need to have Wirecard ePOS API credentials (username & password) in order to successfully authenticate with Wirecard ePOS API. At the moment, only **basic access authentication** is supported.

!!! Tip
    
    Please contact your Wirecard representative to obtain your personal credentials. If you don't know your Wirecard representative, please contact us at retail.mpos@wirecard.com

!!! Note
    
    In the context of an HTTP transaction, **basic access authentication** is a method for an HTTP user agent (e.g. a web browser) to provide a username and password when making a request. In basic HTTP authentication, a request contains a header field of the form Authorization: Basic <credentials>, where credentials is the base64 encoding of id and password joined by a colon.
     
     HTTP Basic authentication (BA) implementation is the simplest technique for enforcing access controls to web resources because it does not require cookies, session identifiers, or login pages; rather, HTTP Basic authentication uses standard fields in the HTTP header, removing the need for handshakes.
     
     The BA mechanism provides no confidentiality protection for the transmitted credentials. They are merely encoded with Base64 in transit, but not encrypted or hashed in any way. Therefore, Basic Authentication is typically used in conjunction with HTTPS to provide confidentiality.
    
    When the user agent wants to send authentication credentials to the server, it may use the Authorization field. The Authorization field is constructed as follows:
    
    - The username and password are combined with a single colon (:). This means that the username itself cannot contain a colon. 
    - The resulting string is encoded into an octet sequence. The character set to use for this encoding is by default unspecified, as long as it is compatible with US-ASCII, but the server may suggest use of UTF-8 by sending the charset parameter. 
    - The resulting string is encoded using a variant of Base64.
    - The authorization method and a space (e.g. "Basic ") is then prepended to the encoded string. 

    For example, if the browser uses Aladdin as the username and OpenSesame as the password, then the field's value is the base64-encoding of Aladdin:OpenSesame, or QWxhZGRpbjpPcGVuU2VzYW1l. Then the Authorization header will appear as: “Authorization: Basic QWxhZGRpbjpPcGVuU2VzYW1l”
    
    See [Wikipedia](https://en.wikipedia.org/wiki/Basic_access_authentication) for more details.

## Testing Environment

**Wirecard ePOS TEST environment** is provided to API integrators for their development purposes. In case your credentials are valid for ePOS TEST environment, please refer to the following URL:
       
    https://switch-test.wirecard.com/mswitch-server/

!!! Tip
    
    - You have received user account credentials to TEST environment.
    - You can check the received credentials - type them instead of {YourUsername} and {YourPassword} - with following CURL request: 
        
        >curl -X GET "https://switch-test.wirecard.com/mswitch-server/v1/info/version" -H "accept: text/plain" -u {YourUsername}:{YourPassword}
    
        Upon successful authentication, system responds with its version.
        
## Production Environment

**Wirecard ePOS PROD environment** is available on the following URL:

    https://switch.wirecard.com/mswitch-server/