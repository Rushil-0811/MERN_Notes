most apps have this thing called client server architecture

client - mobile app
server - db
request - store/modify

server has IP address, send request to the correct ip address

domain name system (DNS) - maps domain names to ip addresses
proxy server acts as middleman bw device and server
proxy server hides your ip address, reverse proxy hides the server Ip address?

delay happens due to physical distance b/w user adn the actual physical data center, data has to travel from the user to the data center and then return to the user
round trip delay is called latency
to reduce latency deploy multiple servers across multiple servers

client and servers communicate using a set of rules called http/https
https - secure
https encrypts the request and response
https dont define the actual request and responses tho, that is done by APIs or application programming interfaces

two most popular api stylkes - REST and Graphql

I mean u know what rest is right buddy, no need to make notes on that

rest api sometimes shares lot more info than needed
graphql helps get the precise data and only the required stuff
graphql takes mroe time tho and isnt easy to cache, rest on the other hand is easy to cache.
You store this data in a database (duh)
mainly two types of databases - sql and nosql
sql - tables, predefined schema, strong consistency
nosql- scalability and performance
modern apps use sql and nosql together4

as users grow, requests and all will also grow,
so u gotta increasae tne server size and all, this is called vertical scaling
vertical scaling has limitaions as u cant keep increasing this, theres just one point of failure for the entire system
its not a long scale solution

adding more servers is called horizontal scaling
this distributes the load
if one goes down, the other server can pick this up.

A load balancer is somewhat of a trafffic manager, distributing requests across mulitple servers
uses load balancing algorithms to decide which server to send data to

now as users increase, the data will also increase, for db also u can do vertical scaling.

effective way to speed up db read queries is indexing
indexing is an efficient lookup table that helps db locate the data without going through all the data
index are created on keys such as primary keys or foreign keys
index the most frequently used columns

another db scaling method is replication
create copies of dbs across multiple servers
primary replica - write operations
read replica - read operations
if primary replica fails, read can take over

split db into smaller pieces and distribute them across multiple servers
this technique is called sharding
data is distributed on basis of sharding key, this can be user id or anything else
sharding is also called horizontal partitioning

can split db by columns - this is called vertical partitioning
can split dbs by rows or columns basically
can make queries faster as each request will only scan the split db instead of the entire long table

retrieving data from disk is slower than retrieving it from memory
storing frequently accessed data in memory is called caching
cache aside pattern- first checks cache if a request is made
get from db, store it in cache for faster requests
to prevent outdated data to be given in response via cache, time-to-live (ttl) is used

normalisation - break data into separate tables
to get combined data, join operations are used
join can slow down query speed

denormalisation- reduces number of joins by combining related data into a single table
this leads to increased storage tho and more complicated update operations

distributed systems
cap theorem - no dsitributed system can achieve consistency, availabilit and partition tolerance at the same time.

apps need to handle pictures, videos, pdfs apart form the usual text
traditional dbs are not built for this
we use blob storage for this scenario
blobs- individual files stored in buckets on the cloud
blob storage is amazon s3
blob storage can be directly sent to the user, but again this will lead to buffering if difference b/w the user and the actual server is pretty large.
for this a content delivery network (cdn) is used, delivers content faster based on the user location

most apps use http
http works for static web pages, but slow for live chat apps
for htpp polling can be used to be quick, but it is insufficient
web sockets allow for continuous two way communication b/w clioent and server
eliminates need for polling if web sockets are used
what if a server needs to update another server via websockets?
to solve this webhooks are used, allows htpp request to be sent to different servers
monolithic architecture was used in tradiitonal systems, its basically a big large code base containing everything required by the app, this becomes hard to manage tho
solution is to break down services into smaller parts called microservices, having its own independent logic for an ooperation, has own db and all, making it easier for scaling independently
can communicate with other servcices using apis
message queues - allows services to be communicated asynchronously
can prevent overload for public apis by using rate limiting, requests number of requests a client can send in a certain time
various rate limiting algos include - fixed window, sliding window and token bucket
API gateway - centralised system that handles authentication, rate limiting , requesting routing, etc.
idempotency ensures that repeated requests give the same result
request gets a unique id, if a request stops and gets sent to another server, a check is made if the id exists or not to avoid duplicating the request