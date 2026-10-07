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
 

some more pointers:
1. For JWT (access + refresh token) strategy you should never store the access token in cookie or storage (localstorage, session storage, etc.). Doing so allows JS to be able to access it, so in case a third-party JS is injected, they'll have access to it. Thus, you always keep the access token in memory, meaning the app memory, like a state in your react app.

2. Usually you also keep copy of the refresh token in your DB so that you can maintain the user's session. When the refresh token passed you (may) compare it. And like that by storing multiple refresh tokens from the same user (via different browsers/devices) you can provide multiple sessions for the same user. This allows you to give the security option 'log out from all devices'. If the user selects that, then you delete the refresh token values stored in the server and also using the response wipe out the tokens from the client. Now after this if the user visits the url (website/web app) from any other device where session was previously ongoing, now since the refresh token provided by the client doesn't match with the one in the server (since server ain't got any), the client gets 401 response and gets kicked out, being redirected to login and their cookies getting deleted.

3. In case you're supporting for older browsers you also need CSRF token (not 100% sure about this). You pass the CSRF token both in normal cookie and header ("Double Submit Cookie" pattern), and then check whether their values are the same in the server. If they're not, then there was a CSRF attack and you give a bad response (maybe 401 or 400, not sure).

1. The strategy mentioned in Point 1 (memory + header) provides the highest security but it's more difficult to implement. So instead many (like Next.js) instead pass/set both tokens as httpOnly on the client, and also provide a CSRF token. However they don't use the "double submit cookie" pattern, but rather some other new pattern called as "synchronizer" pattern. In this pattern for the CSRF token the server generates a random string (token), and both stores it in itself (DB) as well as passing it to the user. Then the user passes this CSRF token when making a request (access and refresh tokens are now httpOnly so they get passed on by default) as header. The server gets the CSRF token and it compares it with the one in the server, and if they match then it's okay. Note that since the CSRF token is manually injected via JS, an attacker attempting to perform a CSRF attack wouldn't be able to add the header since they don't have access to your JS, and due to SOP (Same-Origin-Policy), unless you've allowed the attacker's domain using CORS.

The difference between the "double submit cookie" pattern and the "synchronizer" pattern is that the former is stateless and doesn't need DB storage, while the latter needs the server to remember.

2. Building on point 1, the difference between the "memory + header" approach and the "both tokens in httpOnly cookie" approach is that in the former while there's more security, the client logic is messy and you might see a flash of login screen if not handled properly.

