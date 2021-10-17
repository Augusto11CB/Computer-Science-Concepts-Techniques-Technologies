# Notes - Software Architecture in Practice 4th Edition de Len Bass et al.

The basic principle of software architecture is every software system is constructed to satisfy an organization’s business goals, and that the architecture of a system **is a bridge between those (often abstract) business goals and the final (concrete) resulting system**.

<br>

- **Topics**: the design, analysis, documentation of architectures ad examine the influences, principally in the form of business goals that lead to quality attribute requirements, that inform these activities.

## Part I -

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

- **Enterprise Architecture**


### Why Is Software Architecture Important?

### Understanding Quality Attributes
