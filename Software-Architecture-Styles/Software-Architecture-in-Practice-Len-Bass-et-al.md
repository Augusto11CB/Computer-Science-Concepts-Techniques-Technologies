# Notes - Software Architecture in Practice 4th Edition de Len Bass et al.

- [Notes - Software Architecture in Practice 4th Edition de Len Bass et al.](#notes---software-architecture-in-practice-4th-edition-de-len-bass-et-al)
  - [Introduction](#introduction)
  - [Part I - Introduction](#part-i---introduction)
    - [What Is Software Architecture?](#what-is-software-architecture)
      - [Definition of a "Good Architecture" for the Authors](#definition-of-a-good-architecture-for-the-authors)
      - [Architecture and Behavior](#architecture-and-behavior)
      - [System Architecture and Enterprise Architecture](#system-architecture-and-enterprise-architecture)
      - [Three Kinds of Structure](#three-kinds-of-structure)
    - [Why Is Software Architecture Important?](#why-is-software-architecture-important)
      - [1. Inhibiting or Enabling a System’s Quality Attributes](#1-inhibiting-or-enabling-a-systems-quality-attributes)
      - [2. Reasoning about and Managing Change](#2-reasoning-about-and-managing-change)
      - [3. Predicting System Qualities](#3-predicting-system-qualities)
      - [4. Communication among Stakeholders](#4-communication-among-stakeholders)
      - [5. Early Design Decisions](#5-early-design-decisions)
      - [6. Constraints on Implementation](#6-constraints-on-implementation)
      - [7. Influences on organizational Structure](#7-influences-on-organizational-structure)
  - [Part II - Quality Attributes](#part-ii---quality-attributes)
    - [Understanding Quality Attributes](#understanding-quality-attributes)
      - [Discution about Functional Requirements](#discution-about-functional-requirements)
    - [Quality Attribute Considerations](#quality-attribute-considerations)
      - [Three Problems in Discussions of System Quality Attributes](#three-problems-in-discussions-of-system-quality-attributes)
    - [Quality Attribute Scenarios](#quality-attribute-scenarios)
    - [Achieving Quality Attributes through Architectural Patterns and Tactics](#achieving-quality-attributes-through-architectural-patterns-and-tactics)
    - [Analyzing Quality Attribute Design Decisions - Tactics-Based Questionnaires](#analyzing-quality-attribute-design-decisions---tactics-based-questionnaires)
    - [Availability](#availability)
      - [Availability General Scenario](#availability-general-scenario)
      - [Tactics for Availability](#tactics-for-availability)
        - [Detect Faults](#detect-faults)
        - [Recover From Faults](#recover-from-faults)
      - [Tactics-Based Questionnaire for Availability](#tactics-based-questionnaire-for-availability)
      - [Patterns for Availability](#patterns-for-availability)
      - [References for the Chapter Availability](#references-for-the-chapter-availability)
    - [Deployability](#deployability)
      - [Continuous Deployment](#continuous-deployment)
## Introduction
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
        - Accomplished by modifying a single element.
        - Ex: Create/Implement a new bussiness rule.
    - non-local
        - Result in modifications in multiple elements.
        - Leaves the underlying architectural approach intact.
        - Ex: Create/Implement a new bussiness rule + adding new fields to the database  + changes in the interface.
    - architectural
        - Ex: changing a single-threaded system to a multi-threaded.

- In order to determine which change paths have the least risk, when changes are necessary/essential, and what are the consequences of proposed changes all require a deep understandment of the relationships, behaviors and performance of the elements of the system.

#### 3. Predicting System Qualities

> Architecture not only imbues systems with qualities, but does so in a predictable way.
>
> if we know that certain kinds of architectural decisions lead to certain quality attributes in a system, then we can make those decisions and rightly expect to be rewarded with the associated quality attributes. 
> 
> \- BASS, Len et al. Software Architecture in Practice, Addison-Wesley, 2021

#### 4. Communication among Stakeholders
- Architecture is an abstraction that can be used by stakeholders as a basis for creating understandiment, perform negotiation, form consensus and communicating with each other.
    - Each stackeholder has a different concern about the system.
    - Architecture provires common language in which different concerns can be addressed,

#### 5. Early Design Decisions
- Architecture is the manifestation of the earliest design decisions about a system (BASS, Len et al.).
- These decisions have disproportionate weight with the respect to the system's remanining development because they influence and constrain much of what follows.

#### 6. Constraints on Implementation
- implementation must conform to the design decisions prescribed by the architecture
- interaction between elements, fulfillment of responsibilities all of these things can be restricted by architecture and must be implemented according to  its guidelines.

#### 7. Influences on organizational Structure
- Architecture has its effects on the structure of the development project (and somethimes in the structure of the entire organization)
- Work-breakdown structure of a system is manifested in the architecture (work assignment structure)
    - Work-breakdown structure dictates units of planning, scheduling and budget; interteam communication channels etc
    - A side effect of establishing the work-breakdown structure is to freeze some aspects of the software architecture (BASS, Len et al.).
- Conway’s law states that “organizations which design systems . . . are constrained to produce designs which are copies of the communication structures of these organizations.” (Melvin E. Conway. “How Do Committees Invent?”).

## Part II - Quality Attributes
### Understanding Quality Attributes
- (ISO 25010) defines functional suitability as “the capability of the software product to provide functions which meet stated and implied needs when the software is used under specified conditions.”

<br>

#### Discution about Functional Requirements
> Functionality describes what the system does and quality describes how well the system does its function. That is, **qualities are attributes of the system** and **function is the purpose of the system**.
> 
> \- BASS, Len et al. Software Architecture in Practice, Addison-Wesley, 2021

About de above definition, the autors do not complete agree with what were. As an example to explain the disagreement they have with the ISO's definition is a  a software that controls engine behavior. They state "how can the function be correctly implemented without considering timing behavior?"

In order to describe **computations that a system must perform** they coined the term "**responsibility**".
    - “What are the timing constraints on that set of responsibilities?”
    - “What modifications are anticipated with respect to that set of responsibilities?”
    - Above are some questions that make sense and are actionable in terms of "**resposibility**".
    
### Quality Attribute Considerations
- there is two main categories of quality attributes. 
    - The **first category** contains the attributes that describe **properties** of the **system at runtime**.
    - The **secondy category** includes those attributes that describe **properties** of the **development of the system** (e.g. modifiability, testability, or deployability).

- The achievement of a quality attribute can never be done in isolation. There will be always effects on the others attributes - sometimes positve and sometimes negative.
    - Ex: almost every quality attribute negatively affects performance. The authors comment about the attribute portability. To achieve portability system dependencies must be isolated. This introduces overhead into the system's execution, which then reduce performance.

- "Quality attribute requirements are satisfied by the structures and behaviors of the architecture." (BASS, Len et al.) 

#### Three Problems in Discussions of System Quality Attributes
1. The definitions provided for an attribute are not testable
    - A system must be modifiable
        - Systems will be modifiable with the respect to one set of changes and not modifiable with respect to another.
    - A system must be robust

2. Discussion often focuses on which quality a particular issue belongs to.
    - DDoS, which system aspect it belongs?
        - performance, security, or usability? According to the autors, this kind of debate over categorization doesn't help understand and create architectural solutions to actually manage the attributes of concern.

3. Each attribute community has developed its own vocabulary
    - Events == performance communit.
    - Attacks == security community.
    - Faults == availability community.
    - All of these terms may refer to the same thing, but they are described using different terms.

### Quality Attribute Scenarios
- Quality attribute scenarios have six parts:

1. Stimulus: Describe the event that arrives at the system or project.
2. Stimulus source: from where the stimulus came from  (a human, a computer system, or any other actor).
3. Response: resultanting activity that occurs after the arrival of the stimulus.
4. Response measure: response shoud be measurable in some way in order to allow the execution and application of tests.
5. environment: set of circumstances where the scenario takes place (often this refers to a runtime state)
6. artifact: the target of the stimulus

![Image from BASS, Len et al. Software Architecture in Practice, Addison-Wesley, 2021](https://user-images.githubusercontent.com/17462762/138536770-8272ec43-16df-4ff5-8500-0349389b380a.png)
- Image from BASS, Len et al. Software Architecture in Practice, Addison-Wesley, 2021

### Achieving Quality Attributes through Architectural Patterns and Tactics
- **Tatic**: design decision (design techniques) that affects how a quality attribute response is going to be achieved.
    - "Tactics give the architect insight into the properties of the resulting design fragment" (BASS, Len et al.)

> An architectural pattern describes a particular recurring design problem that arises in specific design contexts and presents a well-proven architectural solution for the problem
> 
> \- BASS, Len et al. Software Architecture in Practice, Addison-Wesley, 2021

What we mean by the term "solution" mentioned in the quote above is a description of the roles of the architectural elements, their responsibilities and relationships, and the way they collaborate with each other.

There is no silver bullet, patterns often are a combination of a set of fine tactics, however we must keep in mind that frequently tradeoffs needed to be made among the quality attributes.

As the software ages its architecture often evolve and transform as a result of many small decisions and business force, it can lead to a problem called "death by a thousand cuts". This problem occurs when developers make suboptimal decisions due to several factors such as schedule pressuers, or lack of understanding of the structures of the system. This situation also is called **Architecture debt**.

### Analyzing Quality Attribute Design Decisions - Tactics-Based Questionnaires
> 1. For each tactics question, fill the “Supported” column with “Y” if the tactic is supported in the architecture and with “N” otherwise.
> 
> 2. If the answer in the “Supported” column is “Y,” then in the “Design Decisions and Location” column describe the specific design decisions made to support the tactic and enumerate where these decisions are, or will be, manifested (located) in the architecture. For example, indicate which code modules, frameworks, or packages implement this tactic.
> 
> 3. In the “Risk” column indicate the risk of implementing the tactic using a (H = High, M = Medium, L = Low) scale.
> 
> 4. In the “Rationale” column, describe the rationale for the design decisions made (including a decision to not use this tactic). Briefly explain the implications of this decision. For example, explain the rationale and implications of the decision in terms of the effort on cost, schedule, evolution, and so forth.
> 
> \- BASS, Len et al. Software Architecture in Practice, Addison-Wesley, 2021

### Availability
- reliability == performs according to its specifications
- availability builds on the concept of reliability by adding the notion of recovery
    - it includes the ability of a system to hide (mask) or repair faults so they do not become failures
- failure is the visible deviation of the system of its specification
- a failure's cause is called fault

- **Fault vs Failures**
    - If there is a fault in a code that is executed and this fault araise but the system is able to recover from the fault without any visible deviation from its specification, then it is safe to thai that no failure has occured.

- understand the nature of the failures that can happen during operation is high demanding task while building high-availability fault-tolerant system.

- System downtime refers to periods when a system is unavailable.
- only **unscheduled outages** contribute to **system downtime**.

#### Availability General Scenario
- [Availability General Scenario](https://github.com/AugustoCalado/Books-Repository/blob/main/Books-Highlights/Software-Architecture-in-Practice-Len-Bass-et-al/Availability-General-Scenario.md)

#### Tactics for Availability
- Fault Detection
- Fault Recovery
- Fault Prevention

![Figure 4.3 - BASS, Len et al. Software Architecture in Practice, Addison-Wesley, 2021](https://user-images.githubusercontent.com/17462762/138689218-3a65535f-470a-4e5b-a793-9ed05a36bf4b.png)
- Image from BASS, Len et al. Software Architecture in Practice, Addison-Wesley, 2021

##### Detect Faults
- Monitor
    - The monitor is a component that orchestrates software using other detection faults tactics to identify malfunctioning components.
- Watchdog
    - Watchdog is a specialization of the monitor, in which the detection mecanism employed uses a counter or timer that periodically reset
- Ping/echo
- Heartbeat
- Timestamp
- Condition monitoring
- Sanity Checking
- Voting
    - Replication
    - Functional Redundancy
    - Analytic Redundancy
- Exception detection
    - System exceptions
    - Parameter fence tactic
    - Parameter typing employs
    - timout
- Self-test

##### Recover From Faults
Tactics about recover from faults are categorizes into two types. The first is preparation and repair tactics, and the second is reintroduction tactics.

- **Preparation and repair tactics**
    - Redundant spare
    - Rollback
    - Exception handling
    - Software upgrade
    - Retry
    - Ignore faulty behavior
    - Graceful degradation
    - Reconfiguration
    - **TODO** Create separated README to alocate more info about this topic

- **Reintroduction**
    - Shadow
    - State resynchronization
    - Escalating restart
    - Nonstop forwarding
    - **TODO** Create separated README to alocate more info about this topic

#####**Prevent Faults**
- Removal from service
- Transactions
- Predictive model
- Exception prevention
- Increase competence set
- **TODO** Create separated README to alocate more info about this topic

#### Tactics-Based Questionnaire for Availability
[Tactics-Based Questionnaire for Availability](https://github.com/AugustoCalado/Books-Repository/blob/main/Books-Highlights/Software-Architecture-in-Practice-Len-Bass-et-al/Tactics-Based-Questionnaire-for-Availability.md)

#### Patterns for Availability
- Active Redundancy (hot spare)
- Passive Redundancy (warm spare)
- Cold spare (spare)
- Triple Modular Redundancy (TMR)
- **Circuit Breaker**
- Process pairs
- Forward error recovery

#### References for the Chapter Availability
- HAMMER, Robert. Patterns for Fault Tolerant Software, Wiley Software Patterns Series, 2013
- SCOTT, James and KAZMAN, Rick. Realizing and Refining Architectural Tactics: Availability, 2009
- NYGARD, Michael. Release It!: Design and Deploy Production-Ready Software, 2007
- UTAS, Greg Robust Communications Software: Extreme Availability, Reliability and Scalability for Carrier-Grade Systems, 2005

### Deployability
- In the old days, releases were infrequent, large numbers of changes were bundled into releases and schedules. Each release could contain new features and bug fixes. Due to competitive pressures in many domains there was a need for shorter releases cycles.

#### Continuous Deployment
Deployment can be defined as a process that start with the coding activity and only ends when real users receive and iteract with the system's new version in a production environment.

**Continuous deployment** is when the deployment **process** if fully automated and **do not require human intervention**. Howerver, if some sort of **human interaction is required** to place the system into production (e.g due to regulations or policies), this **process** is called **continuous delivery**

**Deployment pipeline**
