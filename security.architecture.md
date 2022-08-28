---
id: kubfavp6rxtcrxynus45304
title: Architecture
desc: ''
updated: 1653181038703
created: 1653181030016
---

# Security Architecture Concepts

- [ ] Explain the characteristics of a security architecture.
- [ ] Understand the different types of high-level architectural models and when to use them.
- [ ] Understand how to describe solutions as they are decomposed to identify threats and specify security controls.
- [ ] Discuss how security patterns can help accelerate the development of security for infrastructure and applications.

---
## Characteristics

The foundation of robust security is a clearly communicated with a systematic analysis of the threats and controls.

- Build with a clearly communicated structure.
- As IT systems increase in complexity, they require a standard set of techniques, tools and communication.

Architectural thinking is about creating and communicating good structure and behavior with the intent of avoiding chaos. Architecture needs to be:

- Described before it can be created.
- With different levels of elaboration for communication.
- Include a solution for implementation and operations.
- That is affordable.
- And secure.

Architecture
: A system describes its overall *static structure* and *dynamic behavior*. It models the system's elements (which for IT systems are software, hardware and its human users), the externally manifested properties of those elements, and the static and dynamic relationships among them.

- ISO/IEC 42010: 20071 defines architecture as the "fundamental organization of a system, embodied in its components, their relationships to each other and the environment, and the principles governing its design and evolution".

## High-Level Architectural Models

### General features of building blocks:

- Package of function defined to meet a business need.
- Could be an actor, business service, application or data entity.
- Defined boundary, but can work with other building blocks.
- Interface/boundary loosely coupled from implementation.

### Enterprise Architecture

- Considers the needs of the whole "enterprise" that is within scope.
  - Could be an entire organization or a large single department.
- Maps the main "components" of problem space and solution at a very high level.
- Shows how the main components interrelate with each other and interlink to external organizations.
- Does not describe the internals the main components or how they will be implemented.
  - A model showing generic business processes.
  - A model showing proposed generic IT components that provide high-level business services.

#### Architecture Building Blocks (ABBs)

- Capture and define architecture requirements (function, data, application).
- Product and vendor neutral.
- Guide the development of a Solution Architecture.

##### Examples of ABBs

- Data Security
- Application Security
- Identity and Access management
- Infrastructure and Endpoint security
- Detect and Respond

### Solution

- Describes the main elements of the solution showing their internal architecture, stored data and the use of any reusable or off-the-shelf components/patterns.
- Describes how specific products or technologies are used.
- Adds a content that might describe the different environments.
- Adds some technology perspectives to provide further detail.
- More detailed than the Enterprise architecture.

#### Solution Building Blocks (SBBs)

- Specify technical components to implement a function.
- Add context of the platforms and environments.
- They may be product/vendor aware.

##### Examples of SBBs

- Key Security Manager
- Certificate Authority
- HSM
- Web Application Firewall (WAF)
- Static Application Security Test (SAST)
- Directory
- Privilege Access Manager
- Hardware Token
- Virus Protection
- Application Firewall
- Spam Filter
- Network Intrusion Prevention System
- Incident Workflow Manager


## Solution Architecture

1. Start with a solution architecture with an architecture overview giving an overview of the system being developed.
2. Continue by clearly defining the external context describing the boundary, actors & use cases that process data.
3. Examine the system internally looking at the functional components and examine the threats to the data flows.
4. Finally look at where the function is hosted, the security zones and the specific protection required to protect data.

## Additional Levels of Abstraction

#### Enterprise Architecture (Contextual)

- High-level Building Blocks giving context.
- Does not identify direct connectivity.
- Does not identify technology or products (other than at a high level).

#### Architecture Overview

- Provides Structure at high level.
- Starts to bring environment/platform context.

#### System Context

- Identifies the boundaries of a system.
- Describes the external actors.
- Used to identify use cases and data.

#### Functional/Component Model

- Definition of functional components.
- Includes data flows and dependencies between components within a system.

#### Operational Model

- Definition of physical nodes.
- Includes physical connections between nodes.


*Define what is required and how it will be delivered.*

Who? - Stakeholders include the client, end users of the system, auditors, third parties and regulators.
Where? - Locations for IT applications include access points for end users, connections to any third parties and the data centers.
When? - An IT system may be required to support a new product launch or to an organizational change.
Why? - Understanding the business rationale for an IT system is critical.
What? - Includes words, tables and pictures to describe the functional requirements e.g. a requirements catalogue supported by use-case diagrams and tables of detailed business rules.
How? - Describes the proposed solution in words and pictures, e.g. conceptual and physical models which decompose the solution into components.

## Security Patterns

*The use of security architecture patterns accelerate the creation of a solution architecture.*

Security Architecture Pattern is:

- Reusable solution to a commonly occurring problem.
- A description or template how to solve a problem that can be used in many different situations.
- Not a finished design as it needs context.
- Can be represented in many different formats.
- Vendor specific or agnostic.
- Available at all levels of abstraction.
