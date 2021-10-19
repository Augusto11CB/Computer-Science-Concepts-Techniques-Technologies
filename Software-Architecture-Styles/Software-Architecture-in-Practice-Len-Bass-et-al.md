# Notes - Software Architecture in Practice 4th Edition de Len Bass et al.

The basic principle of software architecture is every software system is constructed to satisfy an organization’s business goals, and that the architecture of a system **is a bridge between those (often abstract) business goals and the final (concrete) resulting system**.

<br>

- **Topics**: the design, analysis, documentation of architectures ad examine the influences, principally in the form of business goals that lead to quality attribute requirements, that inform these activities.

## Part I - Introduction

### What Is Software Architecture?
- Architecture is about reasoning-enabling structures.

    > The software architecture of a system is the set of structures needed to reason about the system. These structures comprise software elements, relations among them, and properties of both.
    >
    > \- BASS, Len et al. Software Architecture in Practice, Addison-Wesley, 2021

- A structure is a set of elements held together by a relation.

- Architectural structures can be organized into **three useful categorie**:
    - 1. Component-and-connector structures
    - 2. Module structures
    - 3. Allocation structures

- A structure is architectural if it supports reasoning about the system and the system’s properties.
- The reasoning should be about an attribute of the system that is important to some stakeholder(s).
    - These attributes are: 
        > properties such as the functionality achieved by the system, the system’s ability to keep operating usefully in the face of faults or attempts to take it down, the ease or difficulty of making specific changes to the system, the system’s responsiveness to user requests, and many others
        >
        > \- BASS, Len et al. Software Architecture in Practice, Addison-Wesley, 2021

> Thus the set of architectural structures is neither fixed nor limited. What is architectural depends on what is useful to reason about in your context for your system.
> 
> \- BASS, Len et al. Software Architecture in Practice, Addison-Wesley, 2021

- **Architecture is an abstraction**
    - Architecture consists of structures, structures consiste of elements and relations, meaning that an architecture embraces software elements and how those elements relate to each other. **Therefore an architecture is an abstraction of a system exposes certain details and hides others**.

- **Every software system has a software architecture**, because every ystem has elements and relations.

#### Definition of a "Good Architecture" for the Authors
They decided not to define architecture of a system by being good or bad, instead they said:

> An architecture may either support or hinder achieving the important requirements for a system.
> 
> \- BASS, Len et al. Software Architecture in Practice, Addison-Wesley, 2021

#### Architecture and Behavior
> Architecture includes behavior, the behavior of each element is part of the architecture insofar as that behavior can help you reason about the system.
> 
> \- BASS, Len et al. Software Architecture in Practice, Addison-Wesley, 2021

#### System Architecture and Enterprise Architecture
- **System architecture** is the portrayal of a system in which occurs the mapping of functionalities onto hw and sw components + human interaction with those componentes.
    - Software architecture onto Hardware Architecture;
    - Concern for the human interaction.

<br>

- **Enterprise Architecture** is a description of the structure and behavior of an organization’s processes, information flow, personnel, and organizational subunits. A modern enterprise architecture is concerned with how software systems support the enterprise’s business processes and goals

#### Three Kinds of Structure

1. Component-and-Connector (C&C)

C&C focus on the fashion the elements interact with each other at **runtime** to carry out the system's functions.
- Runtime behavior == components
    - Components are the principal units of computation
- interactions == connectors
    - Connectors are the communication vehicles among components

> C&C structures help answer questions such as the following:
> 
>   - What are the major executing components and how do they interact at runtime?
> 
>   - What are the major shared data stores?
> 
>   - Which parts of the system are replicated?
> 
>   - How does data progress through the system?
> 
>   - Which parts of the system can run in parallel?
> 
>   - Can the system’s structure change as it executes and, if so, how?
>
> \- BASS, Len et al. Software Architecture in Practice, Addison-Wesley, 2021


2. Module Structures

Module structures show how a system is structured as a set of code or data units that have to be constructed or procured. Those modules are assigned with specific responsibilities.

The elements that make up the module are: perhaps classes, packages, layers, or merely divisions of functionality, all of which are units of implementation.

Modules represent a static way of considering the system.

> Module structures allow us to answer questions such as the following:
> 
>   - What is the primary functional responsibility assigned to each module?
> 
>   - What other software elements is a module allowed to use?
> 
>   - What other software does it actually use and depend on?
> 
>   - What modules are related to other modules by generalization or specialization (i.e., inheritance) relationships?
>
> \- BASS, Len et al. Software Architecture in Practice, Addison-Wesley, 2021

3. Allocation structures 

### Why Is Software Architecture Important?

Reasos to motivate the creation of a new architecture, or the analysis and evolution of an existing one

#### 1. Inhibiting or Enabling a System’s Quality Attributes 
- The architecture of a system plays a big role to allow the system to meet its desired quality attributes.

- Some quality attributes:
    - High performance
    - Highly secure
    - Developer incremental subsets of the system
    - Reusable

- The strategies to achieve this qualitiy attribute and others are architectural. However, architecture alone will not guarantee their achievement. The design and implementation decisions can undermine an adequate architecture design.

> quality is not completely a function of an architectural design. But that’s where it starts.
> 
> \- BASS, Len et al. Software Architecture in Practice, Addison-Wesley, 2021

#### 2. Reasoning about and Managing Change
- Modifiability is the quality of "how easy changes can be made to a system".

- 80 percent of a typical software system’s total cost occurs after initial deployment (BASS, Len et al).

- The changes can be splited in 3 categories
    - local
        - Accomplished by modifying a single element
        - Ex: Create/Implement a new bussiness rule
    - non-local
        - Result in modifications in multiple elements
        - Leaves the underlying architectural approach intact
        - Ex: Create/Implement a new bussiness rule + adding new fields to the database  + changes in the interface
    - architectural
        - Ex: changing a single-threaded system to a multi-threaded

- In order to determine which change paths have the least risk, when changes are necessary/essential, and what are the consequences of proposed changes all require a deep understandment of the relationships, behaviors and performance of the elements of the system.

#### 3. Predicting System Qualities

> Architecture not only imbues systems with qualities, but does so in a predictable way.
>
> if we know that certain kinds of architectural decisions lead to certain quality attributes in a system, then we can make those decisions and rightly expect to be rewarded with the associated quality attributes. A
> 
> \- Booch, G. et al. Object-Oriented Analysis and Design with Applications

### Understanding Quality Attributes
