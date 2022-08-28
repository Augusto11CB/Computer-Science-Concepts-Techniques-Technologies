# Continuous Integration vs Continuous Delivery vs Continuous Deployment

## Continuous Integration
> Continuous Integration usually refers to integrating, building, and testing code within the development environment. Continuous Delivery builds on this, dealing with the final stages required for production deployment (FOWLER, 2013).


## Continuous Delivery
Continuous Delivery is a software development discipline where software is built in such a way that the software can be released to production at any time.

Continuous delivery is done when: [1]

- The software is deployable throughout its lifecycle;
- Team prioritizes keeping the software deployable over working on new features;
- It is possible to get fast, automated feedback on the production readiness of the systems any time somebody makes a change to them;
- Push-button deployments of any version of the software to any environment on demand.

Continuous delivery is achieved by continuously integrating the software done by the development team, building executables, and running automated tests on those executables to detect problems. Moreover, executables are pushed into production-like environment to ensure the software will work in production ([DeploymentPipeline](https://martinfowler.com/bliki/DeploymentPipeline.html)).


### Continuous Delivery vs Continous Deployment
> Continuous Delivery is sometimes confused with Continuous Deployment. Continuous Deployment means that every change goes through the pipeline and automatically gets put into production, resulting in many production deployments every day. Continuous Delivery just means that you are able to do frequent deployments but may choose not to do it, usually due to businesses preferring a slower rate of deployment. In order to do Continuous Deployment you must be doing Continuous Delivery (FOWLER, 2013).

### Benefits of Continuous Delivery 
- Reduced Deployment Risk: since smaller changes are being deployed, there's less to go wrong and it's easier to fix should a problem appear.

- Believable Progress: many folks track progress by tracking work done. If "done" means "developers declare it to be done" that's much less believable than if it's deployed into a production (or production-like) environment.

- User Feedback: the biggest risk to any software effort is that something is end up being built that isn't useful. The earlier and more frequently working software is in front of real users, the quicker is the feedback to find out how valuable it really is.


## References
FOWLER, M. Continuous Delivery. Available at https://martinfowler.com/bliki/ContinuousDelivery.html. Accessed on 28 Aug. 2022
