# Engineering Practices Interview Topics

## Overview

Engineering practices questions assess your understanding of software development principles, methodologies, and best practices beyond coding algorithms. These questions help employers evaluate your approach to building maintainable, scalable, and reliable software.

## Key Topics

### Software Development Methodologies

#### Agile Practices
- **Scrum**: Sprint planning, daily stand-ups, retrospectives, velocity tracking
- **Kanban**: Continuous flow, work-in-progress limits, pull-based systems
- **User Stories**: Writing effective stories, acceptance criteria, estimation techniques

**Interview Questions:**
- How do you handle scope changes during a sprint?
- Describe how you've implemented agile practices in previous roles.
- How do you estimate user story complexity and time requirements?

#### Continuous Integration/Delivery
- **CI Pipelines**: Build automation, test automation, deployment gates
- **CD Strategies**: Blue/green deployments, canary releases, feature flags
- **DevOps Integration**: Cross-functional responsibilities, SRE principles

**Interview Questions:**
- Describe your experience setting up or improving a CI/CD pipeline.
- How do you ensure safe production deployments?
- What monitoring do you implement for newly deployed features?

### Code Quality

#### Testing Strategies
- **Unit Testing**: Coverage goals, mocking strategies, test-driven development
- **Integration Testing**: Service integration, API contracts, test environments
- **End-to-End Testing**: User workflows, performance testing, security testing

**Interview Questions:**
- How do you determine appropriate test coverage for your code?
- Explain your approach to test-driven development.
- How would you test a distributed system?

#### Code Reviews
- **Review Process**: Pull request workflows, approval policies
- **Review Focus**: Code style, security issues, performance concerns, design patterns
- **Automated Reviews**: Static analysis tools, linters, security scanners

**Interview Questions:**
- What do you look for when reviewing others' code?
- How do you handle disagreements during code reviews?
- What tools do you use to automate parts of the code review process?

### Architecture and Design Patterns

#### SOLID Principles
- **Single Responsibility**: One reason to change
- **Open/Closed**: Open for extension, closed for modification
- **Liskov Substitution**: Subclasses should be substitutable for base classes
- **Interface Segregation**: Clients shouldn't depend on methods they don't use
- **Dependency Inversion**: Depend on abstractions, not implementations

**Interview Questions:**
- How have you applied SOLID principles in your work?
- Give an example of refactoring code to better follow single responsibility.
- How do you handle dependencies in large codebases?

#### Design Patterns
- **Creational Patterns**: Factory, Singleton, Builder
- **Structural Patterns**: Adapter, Decorator, Composite
- **Behavioral Patterns**: Observer, Strategy, Command

**Interview Questions:**
- Which design patterns do you use most frequently and why?
- When would you choose composition over inheritance?
- Describe a situation where you implemented the observer pattern.

#### Architecture Styles
- **Microservices**: Service boundaries, communication, data consistency
- **Monolithic**: Modular monoliths, deployment strategies
- **Serverless**: Function design, state management, cold starts

**Interview Questions:**
- How do you determine appropriate service boundaries in microservices?
- What challenges have you faced with distributed systems?
- How do you handle data consistency across microservices?

### DevOps and Infrastructure

#### Infrastructure as Code
- **Configuration Management**: Ansible, Chef, Puppet
- **Infrastructure Provisioning**: Terraform, CloudFormation, Pulumi
- **Container Orchestration**: Kubernetes, Docker Swarm

**Interview Questions:**
- How do you manage infrastructure configurations across environments?
- Describe your experience with container orchestration platforms.
- How do you ensure infrastructure changes are reliable and testable?

#### Monitoring and Observability
- **Metrics Collection**: Key performance indicators, SLIs, SLOs
- **Logging Strategies**: Structured logging, log aggregation
- **Distributed Tracing**: Request tracking across services

**Interview Questions:**
- How do you approach debugging in distributed systems?
- What observability tools have you worked with?
- How do you determine what metrics to collect for a service?

### Team Collaboration

#### Version Control Strategies
- **Branching Models**: Git flow, trunk-based development
- **Commit Practices**: Atomic commits, meaningful messages
- **Collaboration Workflows**: Pull/merge requests, reviews, integrations

**Interview Questions:**
- Describe your preferred Git workflow and why you prefer it.
- How do you handle merge conflicts in a team setting?
- What do you include in a good commit message?

#### Technical Debt Management
- **Identification**: Code smells, complexity metrics
- **Prioritization**: Impact assessment, refactoring ROI
- **Incremental Improvement**: Boy Scout rule, refactoring strategies

**Interview Questions:**
- How do you identify technical debt in a codebase?
- How do you make the case for addressing technical debt to stakeholders?
- Describe a successful technical debt reduction initiative you led.

## Case Study Topics

1. **Production Incident Response**
   - On-call rotations and escalation policies
   - Incident management and communication
   - Post-mortem processes and blameless culture

2. **Legacy System Modernization**
   - Strangler pattern implementation
   - Incremental migration strategies
   - Maintaining functionality during transitions

3. **Cross-functional Collaboration**
   - Working with product managers and designers
   - Translating business requirements to technical solutions
   - Managing competing priorities

## Resources

### Books
- [Clean Code](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882) by Robert C. Martin
- [The Pragmatic Programmer](https://pragprog.com/titles/tpp20/the-pragmatic-programmer-20th-anniversary-edition/) by Dave Thomas and Andy Hunt
- [Building Microservices](https://www.oreilly.com/library/view/building-microservices-2nd/9781492034018/) by Sam Newman
- [Site Reliability Engineering](https://sre.google/books/) by Google

### Online Resources
- [Martin Fowler's Blog](https://martinfowler.com/) - Patterns and practices
- [The Twelve-Factor App](https://12factor.net/) - Methodology for building software-as-a-service apps
- [ThoughtWorks Technology Radar](https://www.thoughtworks.com/radar) - Emerging techniques and technologies
- [Developer to Architect](https://developertoarchitect.com/) - Architectural thinking resources

### Podcasts
- [Software Engineering Daily](https://softwareengineeringdaily.com/)
- [The Changelog](https://changelog.com/podcast)
- [Architecture Weekly](https://github.com/oskardudycz/ArchitectureWeekly)

### Learning Platforms
- [Pluralsight](https://www.pluralsight.com/) - Software practices and architecture courses
- [A Cloud Guru](https://acloud.guru/) - Cloud and DevOps training