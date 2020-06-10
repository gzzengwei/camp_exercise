
# Week 01

## What should Architect know about
- documentation
- distributed System
- CAP
- performance testing
- DDD

## requirements
- coding
- product
- performace optimization/troubleshooting
- modeling and documentation
- business logic/ functional/ non-funtional
- communication/leadership

## architect
- is a role, not a position

## Modeling

### 4 + 1
- logic view (object models)
- process view (concurrency/sync/async)
- physical view (deployment)
- development view (static stucture)
- scenario (use cases )

### logic view
- stakeholders: customers, users, development lead
- view: functional , interface, responsibility, interaction
- elements: system/sub system/ module/ sub-module, interface
- dev team, cost/progress estimation

### development view
- stakeholders: dev, tester
- view: system implementation
- elements: system components, partitions, framework, business/general services and interfaces
- system design / implementation

### physical view
- stakeholders: intergration dev, ops
- view: logic components to physicial deployment
- phycial nodes and communication between them


### process view
- stakeholders: performance optimization dev
- view: status of system process/thread
- elements: system process/thread, MQ

### scenario view
- stakeholders: users, designers, devs
- view: main/critical scenariosm, non-functional requirements

## UML Modeling

### concept

business domain --analysing-> Concept modeling --extract-> Business Requirement --design-> Solutions

### UML types

Static types:
- Use case
- Object
- Class
- Component
- Package
- Deployment

Dynamic types:
- Collaboration
- Sequence
- Activity
- State

### modeling element

- class
- object
- node
- package
- componment

relations:
- association
- dependency
- aggregation
- inheritance

### Messaging
- simple
- synchronous
- asynchoronous