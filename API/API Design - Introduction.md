
# API Design

## Consideration
The content written in this material are the main points explained in the article An Introduction to APIs  by Brian Cooksey.


## Nomenclature
• SOAP: API architecture known for standardized message formats
• REST: API architecture that centers around manipulating  resources   
• Resource: API term for a business noun like customer or order  
• Endpoint: A URL that makes up part of an API. In REST, each  resource gets its own endpoints  
• Query String: A portion of the URL that is used to pass data to the  server  
• Query Parameters: A key-value pair found in the query string  (topping=cheese)   · Pagination: P

## URL Pattern
In a  typical REST API, a resource will have two URL patterns assigned to it.  The ﬁrst is the plural of the resource name, like /orders. The second is  the plural of the resource name plus a unique identiﬁer to specify a  single resource, like /orders/<order_id>,

## Query string.
REST APIs use the query string to deﬁne details of a search.
Another use of the query string is to limit the amount of data returned  in each request.

## Real time communication
Real time communication will be splited  into two broad categories 1.  The ﬁrst we call "client-driven," where a person interacts with the client  and wants the server's data to update. The other we call "serverdriven", where a person does something on the server and needs the  client to be aware of the change.

### Client-driven integration
when a user interacts with the client, the  client knows exactly when data changes, so it can call the API  immediately to let the server know. There's no delay (hence it's realtime) and the process is eﬃcient because only one request is made for each action taken by a person.

### Server Driven integration
The data is changing  on the server and the client needs to know about it. Yet, if server can't  make requests, since it

**Polling**
When the client is the only one who can make requests, the simplest  solution to keep it up-to-date with the server is for the client to simply  ask the server for updates. This can be accomplished by repeatedly  requesting the same resource

It is ineﬃcient. Most of the requests the client makes are wasted because  nothing has changed. Worse, to get updates sooner, the polling interval  has to be shortened, causing the client to make more requests and  become even more ineﬃcient. This solution does not scale well.

**Long polling**
Long  polling uses the same idea of the client repeatedly asking the server for  updates, but with a twist: the server does not respond immediately.  Instead, the server waits until something changes, then responds with  the update.

**Long polling concerns**
There are concerns like how many requests  can the server hold on to at a time, or how to recover if the client or  server loses its connection.

**Webhooks**
webhooks is a technique where the client both makes requests and listens for them,  allowing the server to easily push updates to it.

webhooks  requires the client to provide a Callback URL where it can receive  events, and the server to have a place for a person to enter that  Callback URL. From a  technical perspective the client became a service too, by listening for requests, enabling two-way  communication.

Webhook subscription
Is a process dynamic that not require  a person to manually enter a Callback URL on the server. Examples: HTTP Subscriptions Speciﬁcation, Restful Webhooks,  REST Hooks, and PubSubHubbub.
