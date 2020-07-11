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
    - **actions**:
      - messaging: simplify communication
      - caching: store data locally in memory instead in a slower and harder to access database
      - logging: track what your program does as it works
      - monitoring: observe how your program uses system resources as it works
    - **interactions**:
      - think about how agents communicate (XML, Json, DB, etc.)

research by talking to people to find the best architecture
- try to not get locked into a vendor (e.g. only Microsoft etc.)

## Design Process (In parallel)
1. Defining problem - write down a problem statement
   1. Describe user's problem (based on user goals)
2. Developing the user stories
   1. Describe the solution to the problem (user's work, not software implementation) - should be small, fix on a small sticky note
   2. Refine the story
      1. Slicing:
         1. Bad way: horizontal slicing: UI, Logic, DB
         2. Good way: **workflow isolation** - vertical slicing: smaller feature. Done by drawing the flow (activity diagram), and every `if` statement is a choice, and in it, every potential path through the process is a potential narrowing
3. Developing the structure - **event storming** (agents of the system - classes, subsystem, micro-services, and how they talk to each other) - driven by the business people, not the developers
   1. Decide on events (domain level, relevant to business)
      1. e.g. comment submitted, comment added to dashboard, email sent, reply comment, delete comment
   2. Decide on the work that happens when the event is received
      1. e.g. store comment when it is received, send notification when added to dashboard, store reply when reply comment, delete comment when delete comment
   3. Decide on the agent that is doing the work
      1. e.g. storing the comment is done by the commenter, sending the notification is done by the post office, replying to the comment is done by the author, deleting the comment is done by the author
   4. Add the bounded context to each agent:
      1. e.g. submitting the comment is in the `submitting` context, adding to dashboard is in the `displaying` context, replying is in the `submitting` context, and deleting the comment is in the `approving` context

Event map
- start with agents
- use strings to show interactions / communication between agents
- gives big picture view of the design

## Categories of Architecture

Enterprise Architecture (EA)
- structure of business (departmental structure, communication, how things get done)
- similar to bounded context (structure of software must reflect structure the organisation)
- leads to 1 software system modelling the whole organisation, and extremely complex models (e.g. employee which does a large variety of tasks)
- tries to save money through standardisation
- small changes take large amount of time

Patterns discovered, not designed
- Buildings
  - corner office pattern (make people like windows on 2 adjacent walls)
  - cross ventilations pattern
- Programmers (observe patterns when solving similar problems) - give common language
  - Singleton (1 single instance of the object)
  - Utility (provides functions not in the system. E.g. math functions like sin, cosine)
- similar structure, infinite number of implementations


