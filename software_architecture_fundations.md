# Software Architecture Foundations
Course: https://www.linkedin.com/learning/software-architecture-foundations/

## Thinking Architecturally

Conway's law:
- The structure of the software must reflect the structure of the organization developing the software
  - N-Tier software structure === N-Tier organization structure
    - UI layer === Frontend dev team
    - Backend layer === Backend dev team
    - DB Layer === Database management team
  - Micro-service software structure === Small feature team
    - Feature A (UI, Backend, DB) === Feature A team
    - Feature B (UI, Backend, DB) === Feature B team

Incremental vs Big Up-front Design:
- Big up front design (get things right the first time)
  - Waterfall
    - bottom up (DB first -> Business Logic -> User Interface)
- Incremental design (create 1 story at a time)
  - Designed to be built incrementally
    - top down design (Customer first -> Stories -> Technology)
    - build something useful quickly
    - defer technology decisions till the last available moment

Bottom up design (**domain driven design**)
- Structure of the code directly match the domain, not the implementation technology. E.g. Accounting software uses accounting structure
  - Driven by stories
      Domain          | Software Subsystem
      ----------------|-----------------
      Storefront      | Invoicing
      Warehouse       | Payment
  - Different subsystems can have different technologies
- **Bounded context** (models naturally the problems we are solving)
  - context:
    - store context 
    - warehouse content
  - stores send order to warehouse, people between contexts don't talk all the time
  - Ubiquitous context
    - In each context the definition of an item (e.g. order) can mean different things. (E.g. in a shop, an order is a book, where as in a warehouse, an order is a shelf location, weight, shipping label.
    - create smaller objects, easier to build
  - Allow changes to a system (which typically happen in a particular context), by a single development group
  - Software directly model the communication structure of the domain. 
    - E.g. 
      - Real life: when store front team talks to the warehouse team via an intermediary
      - Software: context are small, run indecently, and communicate via networks
  - **Agent** (each micro-service is a self contained agent)
    - properties:
      - Business logic
      - UI framework
      - Cache
      - Web-server
    - actions:
      - messaging: simplify communication
      - caching: store data locally in memory instead in a slower and harder to access database
      - logging: track what your program does as it works
      - monitoring: observe how your program uses system resources as it works
    - interactions:
      - think about how agents communicate (XML, Json, DB, etc.)

research by talking to people to find the best architecture
- try to not get locked into a vendor (e.g. only Microsoft etc.)
