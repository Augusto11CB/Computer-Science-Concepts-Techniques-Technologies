
# API Design

## Consideration
The content written in this material are the main points explained in the article An Introduction to APIs  by Brian Cooksey.

## What is an API?
A contract/agreement between different software components on how they should work together

## Nomenclature
- SOAP: API architecture known for standardized message formats
- REST: API architecture that centers around manipulating  resources   
- Resource: API term for a business noun like customer or order  
- Endpoint: A URL that makes up part of an API. In REST, each  resource gets its own endpoints  
- Query String: A portion of the URL that is used to pass data to the  server  
- Query Parameters: A key-value pair found in the query string  (topping=cheese)   · Pagination: P

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

**Webhook subscription**
Is a process dynamic that not require  a person to manually enter a Callback URL on the server. Examples: HTTP Subscriptions Speciﬁcation, Restful Webhooks,  REST Hooks, and PubSubHubbub.

## Best Practices For Changing APIs
* Do not change existing public contracts: data classes, signatures
* Exposes the abstraction to the customers and let them add new features on top of the framework
* Identificação dos recursos (http://site.com/cliente/57). **Cuidado** com IDs sequenciais, pois é possível ler toda a bas.
* Utilize URIs legíveis e o **mesmo padrão de URI na identificação dos recursos**
* Utilização dos métodos HTTP para manipulação dos recursos. Não adicionar na URI a operação a ser realizada no recurso (ex: http://site.com/clientes/10/excluir)
* Não adicionar na URI o formato desejado da representação do recurso (ex: http://site.com/clientes/10?formato=json)

## HATEOS (Hypermedia as the Engine of Application State)
- API HATEOS provê informações que permite navegar entre seus endpoints de forma dinânimca visto que inclui links junto às respostas
- Facilita a integração entre as APIs por não precisar ter configurações hardcoded dos endpoints e ações a serem tomadas a partir de um recurso
- Apesar da especificação do HATEOAS dizer para retornar a URL completa, algumas pessoas defendem a idéia de passar apenas a URI, assim diminui o tamanho do payload e evita problemas com ambientes de teste e Sandbox

## API First Design
AP First Design é uma abordagem de desenvolvimento de Software, na qual o design das API's é priorizado. Como isso, é possível gerar ganhos de escalabilidade, flexibilidade, agilidade e performance para o sistema.

As APIs são a forma primária como um produto expõe suas funcionalidades e por isso é tão importante que elas sejam dedsenhadas de forma inteligente.

"Quando estamos focados apenas no domínio, às vezes esquecemos da comunicação deste domínio com o mundo. Porém quando se faz API first, pensamos no nosso domínio focado na integração com o exterior".

### Pros API First Approach
- times de desenvolvimento podem trabalhar paralelamente após a definição do contrato e mocks da API, aumentando assim a velocidade do time-to-market
- A API é amplamente testada durante o desenvolvimento e não somente depois do produto pronto
- Reduz a probabilidade de erros na integração por trocas de payload. APIs desenvolvidas antes do código tendem a serem melhor desenhadas, confiáveis, consistente e fácil de utilizar.

### How to build my API?
1 - Brainstorm para entender o problema que precisa ser resolvido, as característixas do sistema, as regras de negócio que serão tratadas, os casos de uso, o domínio a ser trabalhado e sua interface com outros domínios
2 - Utilizar o conceito de API First e documentação. Assim as outras pessas já vão saber como se integrar
3 - Criar testes de contratos com endpoints, versionamento, Stubs dos requests e resposes e códigos de erros. Não se esqueça de seguir o style guide de governança
4 - Trabalhe com mocks das APIs, isso ajuda a não depender dos serviço estar completo para permitir testes e integrações. (ex: https://designer.mocky.io/)
5 -  Disponibilizar Collections e environments do Postman para import

## Nice to Know
### GraphQL
![image](https://user-images.githubusercontent.com/17462762/131225948-5db00253-3ad6-4533-a4fe-41aefc08b414.png)

### gRPC
![image](https://user-images.githubusercontent.com/17462762/131225971-ba52181c-0683-4a45-b133-fc80236bf10f.png)

### Thrift vs Protobuf vs Avro vs MessagePack
![image](https://user-images.githubusercontent.com/17462762/131226111-32fbc3f9-6971-454c-a262-f8469cc8e441.png)

### Teste de Carga/Stress
![image](https://user-images.githubusercontent.com/17462762/131226516-2c813efd-b117-4ff9-8231-bb8ce6238b17.png)


### Sensedia
![image](https://user-images.githubusercontent.com/17462762/131226186-442d7538-4dbd-4087-873f-8cd71bb755a9.png)

## Security in APIs
- CORS
- Certificate Pinning (aplicações mobile)

### Limitar o Tráfego
APIs podem ser inundadas por requisições falsas ou incompletas, sobrecarregando o servidor. A negação de serviços podem acontecer(DDoS), tornando assim o fornecimento de informações legítimas inviável;

- No desenvolvimento limite o tráfego de requisições em APIs por
    - Limitações por usuário
    - Limitações por serviço
    - Limitações geográficas
- Monitorar as APIs


### API Keys e dados não Confidenciais
- O uso de API Keys torna a validação um processo mais rápido do que usar a senha criptografada em bases de dados
- Uma API Key gera um valor exclusivo para uso por um cliente API. Não se trata exatamente de um método de autenticação, mas pe uma forma de filtrar solicitações por cliente.
- Ao adicionar uma API Key à sua interface de aplicação, você poderá limitar o número de solicitações por cliente registrado.
- Boas práticas
    - Use OAuth 2.0 com fluxos ativados para oferecer suporte de servidor para servidor e autorização de dispositivo.  Assim, você garante segurança ao seu API Cliente e permite uma boa UX
    - Evite autenticação baseada em nome de usuário e senha
    - Evite manter informações de estado em suas chamadas de API
