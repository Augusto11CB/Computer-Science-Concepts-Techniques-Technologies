# Designing RESTful Web APIs

REST is an acronym for **RE**presentational **S**tate **T**ransfer. REST is an **architectural style** for distributed hypermedia systems. It was first presented by Roy Fielding in 2000 in his famous dissertation.

Like other architectural styles, REST has its own guiding principles and constraints. **These principles must be satisfied if a service interface needs to be referred to as RESTful.**

REST architectural style, data and functionality are considered **resources** and are accessed using **Uniform Resource Identifiers** (URIs).

## Architectural Constraints
REST defines 6 architectural constraints which make any web service – a truly RESTful API.

1. Uniform interface
2. Client–server
3. Stateless
4. Cacheable
5. Layered system
6. Code on demand (optional)

### 1. Uniform interface
- Identification of resources – The interface must be able to uniquely identify each individual resource involved in the interaction between the client and the server.
- Manipulation of resources through representations – The resources should have uniform representations in the server response. These representations should be used to modify the resources state in the server.
- Self-descriptive messages – Each resource representation should carry enough information to describe how to process the message. It should also provide information of the additional actions that can be performed on the resource.
- Hypermedia as the engine of application state – The client should have only the initial URI of the application. All other resources and interactions should be driven dynamically by the client application with the use of hyperlinks (HATEOAS).
- Resource representations across the system should follow specific guidelines such as naming conventions, link formats, or data format (XML or/and JSON).

### Client-server
- Client applications and server applications MUST be able to evolve separately without any dependency on each other. A client should know only resource URIs, and that’s all. 
- The client-server design pattern **enforces the principle of separation of concerns** which helps the client and server components to evolve independently.

> Servers and clients may also be replaced and developed independently, as long as the interface between them is not altered.

### Stateless
-  The server will not store anything about the latest HTTP request the client made. It will treat every request as new.
-  If the client application needs to be a stateful application for the end-user, where the user logs in once and does other authorized operations after that, then each request from the client should contain all the information necessary to service the request – including authentication and authorization details.


> No client context shall be stored on the server between requests. The client is responsible for managing the state of the application.

### Cacheable
- The cache constraint requires that the data within a response should be implicitly or explicitly labeled as cacheable or non-cacheable.

- If the response is cacheable then the client application is given the right to reuse the response data later, for equivalent requests and for a specified time period.

> Well-managed caching partially or completely eliminates some client-server interactions, further improving scalability and performance.

### Layered system
- REST allows you to use a layered system architecture where you deploy the APIs on server A, and store data on server B and authenticate requests in Server C, for example. A client cannot ordinarily tell whether it is connected directly to the end server or an intermediary along the way.

### Code on demand (optional)
REST also allows client functionality to be extended by downloading and executing code in the form of applets or scripts.

This simplifies clients by reducing the number of features required to be pre-implemented. Servers can provide part of features delivered to the client in form of code and the client only needs to execute the code.

- Reference: [restfulapi.net](https://restfulapi.net/rest-architectural-constraints/)

## REST

### What is a Resource?
- The key abstraction of information in REST is a resource. Any information that can be named can be a resource. For example, a REST resource can be a document or image, a temporal service, a collection of other resources, a non-virtual object (e.g. a person), and so on.

<br>

- The state of the resource, at any particular time, is known as the resource representation.

<br>

- The resource representations are consist of:
    - the data
    - the metadata describing the data
    - and the hypermedia links that can help the clients in transition to the next desired state.

<br>

- The resources are acted upon by using a set of simple, well-defined operations. Also, the resources have to be decoupled from their representation so that their content can be accessed in a variety of formats, such as HTML, XML, plain text, PDF, JPEG, JSON, and others.

### Identifiers
- **Resource Identifiers** are used by REST to identify each and every **resource** involved in an interaction between client and the server components

### Hypermedia
- The **data format** of a representation is known as a **media type**. The media type identifies a specification that defines how a representation is to be processed.
- A truly RESTful API looks like hypertext. Every addressable unit of information carries an address, either explicitly (e.g., link and id attributes) or implicitly (e.g., derived from the media type definition and representation structure).

<br>

> Hypertext (or hypermedia) means the simultaneous presentation of information and controls such that the information becomes the affordance through which the user (or automaton) obtains choices and selects actions.
> 
> \- Roy Fielding

### Resource Methods
- Resource methods are used to perform the desired transition between two states of any resource.

<br>

> A large number of people wrongly relate resource methods to HTTP methods (i.e. GET/PUT/POST/DELETE). Roy Fielding has never mentioned any recommendation around which method to be used in which condition. All he emphasizes is that it should be a uniform interface.
>
> For example, if we decide that HTTP POST will be used for updating a resource – rather than most people recommend HTTP PUT – it’s alright. Still, the application interface will be RESTful.
>
> \-  [restfulapi](https://restfulapi.net/)

### REST and HTTP are not the same
- Roy fielding, in his dissertation, has nowhere mentioned any implementation direction – including any protocol preference or even HTTP.

## REST Resource Naming Guide
> The key abstraction of information in REST is a resource. Any information that can be named can be a resource: a document or image, a temporal service (e.g. “today’s weather in Los Angeles”), a collection of other resources, a non-virtual object (e.g., a person), and so on.
>
> In other words, any concept that might be the target of an author’s hypertext reference must fit within the definition of a resource.
>
> A resource is a conceptual mapping to a set of entities, not the entity that corresponds to the mapping at any particular point in time.
>
> \- [Roy Fielding’s dissertation](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm#sec_5_2_1_1)


### URI
- REST APIs use Uniform Resource Identifiers (URIs) to address resources. REST API designers should create URIs that convey a REST API’s resource model to its potential client developers.

### Singleton and Collection Resources
- A resource can be a singleton or a collection.

- For example, “customers” is a collection resource and “customer” is a singleton resource (in a banking domain).

- “customers” collection resource can be identified using the URI “/customers”. We can identify a single “customer” resource using the URI “/customers/{customerId}”.

### Collection and Sub-collection Resources
- A resource may contain sub-collection resources also
- For example:
    - sub-collection resource "accounts" of a particular "customer" can be identified using the URI 
        - `/customers/{customerId}/accounts` (baking domain)
    - resource "account" inside the sub-collection resource "accounts"
        - ` /customers/{customerId}/accounts/{accountId}`

## Best Practices
The reference for this section is [restfulapi - resource naming](https://restfulapi.net/resource-naming/).

### Use Nouns to Represent Resources
Restful URI should refer to a resource that is a "thing" (noun) instead of referring to an action (verb) because nouns have properties that verbs do not have.

- **Examples**
    - users of the system
        - `api.example.com/user-management/users/`
    - users accounts
    - network devices
        - `api.example.com/device-management/managed-devices`
<br>

- **Resources Archetypes**
    - Document
    - Collection
    - Store
    - Controller

#### Document
- document ~ object instance **or** document ~ database record
- in REST it is a single resource inside a resource collection
- the **state representation** of a document includes both fields with values and links to other related resources
- use **singular** name to denote document resource archetype

#### Collection
- Collection resource is a server-managed directory of resources
- Clients may propose new resources to be added to a collection. However, it is up to the collection to choose to create a new resource or not.
- A collection resource chooses what it wants to contain and also decides the URIs of each contained resource.
- Use the **plural** name to denote the collection resource archetype.

#### Store
- Client-managed resource repository
    - store resource lets an API client put resources in, get, remove.
- A store never generates new URIs. Instead, each stored resource has a URI. The URI was chosen by a client when it was initially put into the store.
- Use **plural** name to denote store resource archetype.

#### Controller
- Controller resources are like **executable functions** with parameters and return values; inputs, and outputs;
- Use **verb** to denote controller archetype

<br>

**Example**
```
api.example.com/cart-management/users/{id}/cart/checkout
api.example.com/song-management/users/{id}/playlist/play
```

### Use forward slash (/) to indicate hierarchical relationships
- The forward-slash (/) character is used in the path portion of the URI to indicate a hierarchical relationship between resources. e.g.

```
api.example.com/device-management
aapi.example.com/device-management/managed-devices
aapi.example.com/device-management/managed-devices/{id}
aapi.example.com/device-management/managed-devices/{id}/scripts
```

#### Do not use trailing forward slash (/) in URIs
- As the last character within a URI’s path, a forward slash (/) adds no semantic value and may cause confusion. It’s better to drop them completely.

<br>

- Good example: api.example.com/device-management/managed-devices 
- Bad example: api.example.com/device-management/managed-devices/  

### Use hyphens (-) to improve the readability of URIs
- To make your URIs easy for people to scan and interpret, use the hyphen (-) character to improve the readability of names in long path segments.

<br>

- Good example: api.example.com/devicemanagement/manageddevices 
- Bad example: api.example.com/device-management/managed-devices

###  Do not use underscores (`_`)
-  Depending on the application’s font, it’s possible that the underscore (_) character can either get partially obscured or completely hidden in some browsers or screens.

### Use lowercase letters in URIs
- When convenient, lowercase letters should be consistently preferred in URI paths.

### Do not use file extentions
- File extensions look bad and do not add any advantage. Removing them decreases the length of URIs as well. No reason to keep them.
- If the _media type_ of API have to be highlight using file extension then you should rely on the media type, as communicated through the Content-Type header, to determine how to process the body’s content.

### Never use CRUD function names in URIs
- URIs should not be used to indicate that a CRUD function is performed. 
- HTTP request methods should be used to indicate which CRUD function is performed.

### Use query component to filter URI collection
Enable sorting, filtering, and pagination capabilities in resource collection API and pass the input parameters as query parameters. e.g.

```
http://api.example.com/device-management/managed-devices
http://api.example.com/device-management/managed-devices?region=USA
http://api.example.com/device-management/managed-devices?region=USA&brand=XYZ
http://api.example.com/device-management/managed-devices?region=USA&brand=XYZ&sort=installation-date
```

