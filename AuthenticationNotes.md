authentication methods != authorisation framework
jwt is not an authentication method, jwt is a token structure
oauth 2 is auth framework

before making api requests, authorisation must be done
identity not confirmed - 401

basic auth methods
basic, digest, api keys and session

basic - verification on server side after credentials are provided
id and password encoded in base64
this is reversible, only secure on https

digest - md5 hashing
similar to basic only
better than basic but raerly used

api key - generate unique key
use unique key to get requests
keys per user, api key matched with what the request is sending what the actual api key mapped to the user is
if this key leaks its kinad over, theres no expiration

session based -
user logs in 
store data in session storage
session id generated and session cookie is set
requests made with cookies, lookup session happens
after this maybe it passes or fails
this type of auth is stateful, does not scale well
once server crashes its over
can use redis to support this or sql type db

token based auth
bearer and jwt tokens, access and refresh tokens

this is what is commonly used
bearer token means whoever has the token gets access, most common type of bearer token is jwt
validate credentials on server side, this is stateless
jwt tokens are stateless and dont depend on anyone else
simplified authentication process

requests made with token are verified locally, can pass or fail

access token - short lived and used for api calls to the server
refresh tokens - get new access token whenever access token expires

oauth2 and oidc
open id connect

oauth2 - authorisation framework
redirect to consent screen with permission requests
allowing this gives an auth code
exchange code for token
return the access token
access token just allows for the access and all, does not identify user

oidc -
credentials and consent, returns auth code
exchange auth code for token
u get access token and id token
id token is your gmail id
identify using id token, once identity confirmed session is created
u login after this
this scales well also

sso - single sign on
this a user experience not an authenitcation
login once and access multiple services
think google, u login and can access gmail, drive, youtube etc.

global session is stored in session storage
this uses identity protocols

saml idp and oidc idp
xml based protocol
 