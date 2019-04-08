# Authentication and security

To contact ePOS backend, first you need to properly authenticate against
the system. To do that, you need to have first account created by your
Wirecard representative. If you don't have representative, please
contact us at retail.mpos@wirecard.com

In ePOS we use basic authentication, when making a request. In the
context of an HTTP transaction, basic access authentication is a method
for an HTTP user agent (e.g. a web browser, curl, ...) to provide a user
name and password when making a request. In basic HTTP authentication, a
request contains a header field of the form Authorization: Basic
<credentials>, where credentials is the base64 encoding of id and
password joined by a colon. HTTP Basic authentication (BA)
implementation is the simplest technique for enforcing access controls
to web resources because it does not require cookies, session
identifiers, or login pages; rather, HTTP Basic authentication uses
standard fields in the HTTP header, removing the need for handshakes.
The BA mechanism provides no confidentiality protection for the
transmitted credentials. They are merely encoded with Base64 in transit,
but not encrypted or hashed in any way. Therefore, Basic Authentication
is typically used in conjunction with HTTPS to provide confidentiality.
When the user agent wants to send authentication credentials to the
server, it may use the Authorization field. The Authorization field is
constructed as follows: 
- The username and password are combined with a single colon (:). This
  means that the username itself cannot contain a colon. 
  
- The resulting string is encoded into an octet sequence. The character
  set to use for this encoding is by default unspecified, as long as it
  is compatible with US-ASCII, but the server may suggest use of UTF-8
  by sending the charset parameter. 
  
- The resulting string is encoded
  using a variant of Base64. 
  
- The authorization method and a space (e.g. "Basic ") is then prepended to the encoded string. 

For example, if the browser uses Aladdin as the username and OpenSesame
as the password, then the field's value is the base64-encoding of
Aladdin:OpenSesame, or QWxhZGRpbjpPcGVuU2VzYW1l. Then the Authorization
header will appear as: “Authorization: Basic QWxhZGRpbjpPcGVuU2VzYW1l”

Example of CURL request: 
- curl -X GET
"https://switch.wirecard.com/mswitch-server/v1/info/version" -H "accept:
application/json" -H "Authorization: Basic QWxhZGRpbjpPcGVuU2VzYW1l" 
- curl -X GET "https://switch.wirecard.com/mswitch-server/v1/info/version" -H
"accept: application/json" -u Aladdin:OpenSesame

## Test Environment

Wirecard ePOS backend TEST environment is provided to API integrators for their development purposes. In case your credentials are valid for ePOS backend TEST environment, please refer to https://switch-test.wirecard.com/mswitch-server/ 

One can test the validity of credentials by calling:

GET https://switch-test.wirecard.com/mswitch-server/v1/info/version

