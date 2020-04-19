## 12-Factor Applications
The twelve-factor app is a methodology for building software-as-a-service apps. It is a set of criteria to help measure how friendly an app to run in a cloud environment.

1. **One codebase in source control**
One codebase tracked in revision control (such as Git), many deploys. Each deploy can have a different version activated, but they all share the same codebase, thus making them identifiable as different deploys of the same app, although some deployes may have some extra commits, such as in development environment.

2. **Declared dependencies**
Explicitly declare and isolate dependencies. A twelve-factor app never relies on implicit existence of system-wide packages (packaging system for distributing support libraries). It declares all dependencies, completely and exactly, via a dependency declaration manifest. 

The app 'calls' out its dependencies, instead of depending on them just being there in the target environment.

3. **Config stored in the environment** -
An app’s config is everything that is likely to vary between deploys (Credentials to external services, resource handles to the database ). It states that the configuration should be remove from the code and stored in a external (remote) system. 

Apps sometimes store config as constants in the code. This is a violation of twelve-factor, which requires strict separation of config from code. Config varies substantially across deploys, code does not.

4. **Backing Services as attached resources**
Treat backing services as attached resources. A backing service is one that requires a network connection to run.

The code for a twelve-factor app makes **no distinction between local and third party services.** To the app, both are **attached** resources not some sort of embedded tightly coupled resource, making it easier to swap when changing environments. **A deploy of the twelve-factor app should be able to swap out a *local MySQL database* with one managed by a third party (such as Amazon RDS) without any changes to the app’s code.** 

5. **Separate build and run stages**
Strictly separate build and run stages. Build, release, and run stages should be treated as completely distinct from one another
A codebase is transformed into a deploy through three stages
- **build stage:** code repo is converted into an executable bundle known as a build. the build stage fetches vendors dependencies and compiles binaries and assets.
- **release stage:** e takes the build produced and combines it with the deploy's current config. The result is a release ready for immediate execution in the execution environment.
- **run stage:** runs the app in the execution environment

6. **App executed as stateless processes**
The app is executed in the execution environment as one or more processes. The state of your system is completely defined by your databases and shared storage, and not by each individual running application instance.

7. **Port binding**
> The twelve-factor app is completely self-contained and does not rely on runtime injection of a webserver into the execution environment to create a web-facing service. The web app exports HTTP as a service by binding to a port, and listening to requests coming in on that port.The twelve-factor app is completely self-contained and does not rely on runtime injection of a webserver into the execution environment to create a web-facing service. The web app exports HTTP as a service by binding to a port, and listening to requests coming in on that port. By [12factor.net](https://12factor.net/port-binding )

This factor is an extension of factor IV. The application is ''self-contained" any services are exposed via ports like http. 

8. **Scale out processes**
When the code is executed, lots of small processes are handling specific needs (handlers for process requests, handlers for API calls and handlers for background processing). By keeping these processes working independently and running them as separate processes, the application can scale better.

9. **Disposability** - Maximize robustness with fast startup and graceful shutdown
**Short startup** time provides more agility for the release process and scaling up; and it aids robustness, because the process manager can more easily move processes to new physical machines when warranted. 

**Shut down gracefully** as a web procces  is achieved by ceasing to listen on the service port (thereby refusing any new requests), allowing any current requests to finish, and then exiting. **Shut down gracefully** as a worker process  is achieved by returning the current job to the work queue (e.g. on RabbitMQ the worker can send a **NACK**).
  
10. **Environment Parity** 
Keep environments in sync. When environments are similar, testing and developing gets much simpler. Similar environments means ensuring that areas such as your infrastructure stack, config management processes, software and runtime versions and deployment tools are the same everywhere.

11. **Treat logs like event streams**
Logging is important for debugging and checking up on the general health of your application. At the same time, the application shouldn’t concern itself with the storage of this information. Instead, these **logs should be treated as a continuous stream that is captured and stored by a separate service.**

12. **Run admin processes  one-off processes**
Run admin/management tasks as one-off processes — tasks like database migration or executing one-off scripts in the environment. To avoid messing with the database, use the tooling that were built alongside the app to go and check the database.

