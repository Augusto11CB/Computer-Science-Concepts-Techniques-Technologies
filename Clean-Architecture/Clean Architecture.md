-   Entities: encapsulate enterprise wide business rules. An entity is a set of data structures and functions.
-   Use Cases: the software in this layer contains application specific business rules. It encapsulates and implements all of the use cases of the system.
-   Web: the software in this layer is a set of adapters that convert data from the format most convenient for the use cases and entities, to the format most convenient for some external agency such as the Database or the Web
-   Framework & Driver: this layer is generally composed of frameworks and tools such as the Database, the Web Framework, etc.

## Entity Module

## UseCases Module
The UseCases module contains the business rules that are essential for our application. The only dependency of this module is to **entity**. In this module, **"gateways"** for the repositories are being defined. Each **use case** defines the interface of the gateway that is required following the ISP. These gateways, operate on the domain entities defined in entity.

Also, in the UseCase Module is used:
1.  a  _mapper function_  that converts the  `RequestDto`  to a  `RequestEntity`object (the input of the use case)
2.  a  _mapper function_  that converts the  `ResponseEntity`  object (the output of the use case) of the  `UseCase`  execution to a  `ResponseDto`

## Repository Module(s)
This module contains the implementation of the **"gateways"** defined in the **usecases** module. This module depends on the framework that facilitates the data access. Also, This layer is responsible for providing the data required by the usecase. Repository Modulues should be designed such data it can be re-used by any application without modification in their presentation logic.

The entities in this module, are normally DB entities or entities specific of the framework that has been used, so mapper functions are required to make the translation between these entities and domain entities.

## Web Module
This module contains all the details of the delivery mechanism that is used.
