

# Microservices Architecture

Microservices, aka Microservice Architecture, is an architectural style that structures an application as a collection of small autonomous services, modeled around a business domain.

## Microservices Feature
Decoupling – Services within a system are largely decoupled. So the application as a whole can be easily built, altered, and scaled

Componentization – Microservices are treated as independent components that can be easily replaced and upgraded

Business Capabilities – Microservices are very simple and focus on a single capability

Autonomy – Developers and teams can work independently of each other, thus increasing speed

Continous Delivery – Allows frequent releases of software, through systematic automation of software creation, testing, and approval

Responsibility – Microservices do not focus on applications as projects. Instead, they treat applications as products for which they are responsible

Decentralized Governance – The focus is on using the right tool for the right job. That means there is no standardized pattern or any technology pattern. Developers have the freedom to choose the best useful tools to solve their problems

Agility – Microservices support agile development. Any new feature can be quickly developed and discarded again

## Microservices Architecture -  Benefits
A very common microservices interview question which you should be ready for! There are plenty of pros that are offered by Microservices architecture. Here are a few of them:

- Microservices can adapt easily to other frameworks or technologies. 
- Different languages and technologies can be used to build different services of the same application
- Failure of a single process does not affect the entire system.
- Provides support to big enterprises as well as small teams.
- Can be deployed independently and in relatively less time.
- _**Independent Development**_ - All microservices can be easily developed based on their individual functionality
- _**Granular Scaling**_ - Individual components can scale as per need, there is no need to scale all components together

## Microservices Architecture -  Cons
* Increases troubleshooting challenges
* **Increases delay due to remote calls**
* Increased efforts for configuration and other operations
* **Difficult to maintain transaction safety**
* Tough to track data across various boundaries
* Difficult to code between services
 
## Microservices Architecture - Challenges
* **Automate the Components**: Difficult to automate because there are a number of smaller components. So for each component, we have to follow the stages of Build, Deploy and, Monitor.
* **Perceptibility**: Maintaining a large number of components together becomes difficult to deploy, maintain, monitor and **identify problems**. It requires great perceptibility around all the components.
* **Configuration Management**: Maintaining the configurations for the components across the various environments becomes tough sometimes.
* **Debugging**: Difficult to find out each and every service for an error. It is essential to maintain centralized logging and dashboards to debug problems.

## The Fundamentals Of Microservices Design
// TODO [9 Successful Microservice Design](https://www.lambdatest.com/blog/9-fundamentals-to-a-successful-microservice-design/)
-   Define a scope
-   **Combine loose coupling with high cohesion**
-   Create a unique service which will act as an identifying source, much like a unique key in a database table
-   Creating the correct API and take special care during integration.
-   Restrict access to data and limit it to the required level
-   Maintain a smooth flow between requests and response
-   Automate most processes to reduce time complexity
-   Keep the number of tables to a minimum level to reduce space complexity
-   Monitor the architecture constantly and fix any flaw when detected.
-   Data stores should be separated for each microservices.
-   For each microservices, there should be an isolated build.
-   Deploy microservices into containers.
-   Servers should be treated as stateless.

## How Does Microservice Architecture Work?
// TODO Colocar Image
-   **Clients** – Different users from various devices send requests.
-   **Identity Providers** – Authenticates user or clients identities and issues security tokens.
-   **API Gateway** – Handles client requests.
-   **Static Content** – Houses all the content of the system.
-   **Management** – Balances services on nodes and identifies failures.
-   **Service Discovery** – A guide to find the route of communication between microservices.
-   **Content Delivery Networks** – Distributed network of proxy servers and their data centers.
-   **Remote Service** – Enables the remote access information that resides on a network of IT devices.

## Why Would You Need Reports & Dashboards In Microservices?
Reports and dashboards are mainly used to monitor and upkeep microservices. There are multiple tools that help to serve this purpose.  Reports and dashboards can be used to:

-   find out which microservices expose what resources.
-   find out the services which are impacted whenever changes in a component occur.
-   provide an easy point which can be accessed whenever documentation is required.
-   Versions of the components which are deployed.
-   To obtain a sense of maturity and compliance from the components.

## Coupling and Cohesion?
The **coupling** can be considered to be the **measurement of strength between the dependencies of a component.** A good Microservices application design always consists of **low coupling** and **high cohesion**.

**Cohesion** is also another measurement unit. More like a degree to which the elements inside a module remain bonded together, or **the degree to which the elements inside a module belong together is said to be cohesion.**

The key to d**esign microservices is a composition of low coupling along with high cohesion**. **When loosely coupled, a service knows very little about other**. This keeps the services intact. **In high cohesion, it becomes possible to keep all the related logic in a service**. Otherwise, the services will try to communicate with each other, impacting the overall performance.

## REST/RESTful and Microservices
**Representational state transfer (REST) is a software architectural style that _defines a set of constraints_ to be used for creating Web services**. **Web services that _conform to the REST architectural style_, called RESTful Web services**, provide interoperability between computer systems on the Internet. **RESTful Web services allow the requesting systems to access and manipulate textual representations of Web resources by using a uniform and predefined set of _stateless operations_**. 

Microservices can be implemented with or without RESTful APIs, but it’s always easier to build loosely coupled microservices using RESTful APIs.

### The Constraints
As constraints possuem como objetivo determinar a forma na qual padrões como HTTP e URI deveriam ser modelados, aproveitando de fato todos os recursos oferecidos pelos mesmos.

- #1 Cliente-Servidor
  - Separar as responsabilidades de diferentes partes de um sistema (ex: separação entre backend e fronted)

- #2 Stateless
  - Cada requisição ao servidor não deve ter ligação com requisisções anteriores ou futuras, ou seja, cada requisição deve conter todas as informações necessárias para que ela seja tratada com sucesso pelo servidor.

- #3 Cache
  - Para uma melhor performace, um sistema REST deve permitir que suas respostas sejam passíveis de cache.


- #4 Interface Uniforme
  - Recurso
  - Mensagens auto-descritivas
  - Hypermedia (ter o poder de navegar usando retorno de chamadas)
 
- #5 Sistemas em Camadas
  - Para permitir a escalabilidade necessária para grandes sistemas distribuídos, um sistema REST deve ter a capacidade de adicionar elementos intermediários e que sejam totalmente transparentes para seus clientes
  - Ex: Versionamentos de endpoints


### Resource
- Definição: São elementos de informação, que através de um identificador global podem ser manipulados.
- Regra: A nomeação de um recurso sempre é formada por um **substantivo**, nunca um verbo!

### URI
- Tradução: Uniform Resource Identifier
- Definição: Uma cadeia de caracteres compacta usada para identificar ou denominar um recurso na internet
- Exemplo: 
  - Recurso: Usuário
  - URI: `www.talk.com/user`

### URL
- Tradução: Uniform Resource Locator
- Definição: É o endereço de um recurso disponível em uma rede
- Exemplo:
  - Recurso: Usuário
  - URL: http://www.talk.com/user

### Modelo de Maturidade Richardson
- Níveis de maturidade que uma aplicação pode atingir ao incorporar rest
 - #0 POX
 - #1 Recursos
 - #2 Verbos HTTP
 - #3 HATEOS

### HTTP Status Code
![image](https://user-images.githubusercontent.com/17462762/131224878-c23f3deb-759c-45f9-899e-1da4e93a0a4e.png)


### Role of Web, RESTful APIs in Microservices
A microservice architecture is based on a concept wherein all its services should be able to interact with each other to build a business functionality. So, to achieve this, each microservice must have an interface. This makes the web API a very important enabler of microservices. Being based on the open networking principles of the Web, RESTful APIs provide the most logical model for building interfaces between the various components of a microservice architecture.

## Containers and Microservices
To manage a microservice based application, containers are a great alternative. **It helps the user to individually deploy and develop.** You can also use Docker to encapsulate the microservice in the image of a container. 

##  Perform Security Testing of Microservices
Microservices cannot be tested as a whole. You will need to test the pieces independently.There are 3 common procedures

* Code scanning – To ensure that any line of code is bug-free and can be replicated.
* Flexibility – The security solution should be flexible so that it can be adjusted as per the requirements of the system.
* Adaptability – The security protocols should be flexible and updated to cope up with the new threats by hackers or security breaches.

### Types of Tests for Microservices
-   At the  **bottom level**, we have  **technology-facing tests**  like- unit tests and performance tests. These are completely automated.
-   At the  **middle level**, we have tests for  **exploratory testing**  like the stress tests and usability tests.
-   At the  **top level,** we have **acceptance tests**  that are few in number. These acceptance tests help stakeholders in understanding and verifying software features.

## Testing Challenges related to Microservice Architecture
// TODO [testing-challenges-related-to-microservice-architecture](https://www.lambdatest.com/blog/testing-challenges-related-to-microservice-architecture/)

## Best practices to design Microservices
1. Separate data store for each Microservice
2. Deploy into Containers
3. Separate Build for each Microservice
4. Treat Servers as Stateless


## Microservice Vs SOA Vs Monolithic
* Monolithic Architecture is similar to a big container wherein all the software components of an application are assembled together and tightly packaged.
* A Service-Oriented Architecture is a collection of services which communicate with each other. The communication can involve either simple data passing or it could involve two or more services coordinating some activity.
* Microservice Architecture is an architectural style that structures an application as a collection of small autonomous services, modeled around a business domain.

### Microservice Vs SOA - Details
//TODO Colar Image

##  Law Stated By Melvin Conway
>“Any organization that designs a system (defined broadly) will produce a design whose structure is a copy of the organization’s communication structure.” – Mel Conway

This law basically tries to convey the fact that, in order for a software module to function, the complete team should communicate well. Therefore the structure of a system reflects the social boundaries of the organization(s) that produced it.

### DRY in Microservices Architecture
**DRY** stands for **Don’t Repeat Yourself**. It basically promotes the concept of reusing the code. This results in developing and sharing the libraries which in turn result in tight coupling.


## References
[lambdatest - top-29-microservices-interview-questions-for-2019](https://www.lambdatest.com/blog/top-29-microservices-interview-questions-for-2019/)
[Edureka - microservices-interview-questions/](https://www.edureka.co/blog/interview-questions/microservices-interview-questions/)
[Java Code Geeks - microservices-interview-questions-and-answers](https://www.javacodegeeks.com/2019/04/microservices-interview-questions-and-answers.html)
[https://dzone.com/articles/top-29-microservices-interview-questions-for-2019](https://dzone.com/articles/top-29-microservices-interview-questions-for-2019)
