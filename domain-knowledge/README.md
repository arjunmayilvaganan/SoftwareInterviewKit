# Domain Knowledge Interview Topics

## Overview

Domain knowledge interviews assess your technical expertise in specific technologies, programming languages, or industry domains relevant to the role. These questions help employers evaluate your depth of understanding and ability to apply technical knowledge to real-world problems.

## Common Technology Areas

### Frontend Development

#### Core Concepts
- **JavaScript/TypeScript Fundamentals**
  - Closures, prototypes, this binding, promises, async/await
  - Type systems, generics, interfaces, utility types
- **DOM Manipulation and Browser APIs**
  - Event propagation, virtual DOM, Web APIs
  - Performance optimization, layout thrashing, repaints/reflows

#### Frameworks and Libraries
- **React**
  - Component lifecycle, hooks, context, state management
  - Rendering optimization, memoization, code splitting
- **Vue**
  - Reactivity system, composition API, directives
  - Vuex, routing, single-file components
- **Angular**
  - Dependency injection, modules, services, observables
  - Change detection, zones, Angular Universal

#### Common Interview Questions
- Explain the virtual DOM and its benefits
- How would you debug a performance issue in a React application?
- Describe how you would implement state management in a large application
- Compare different ways to manage side effects in React (useEffect vs useReducer vs Redux)

#### Resources
- [MDN Web Docs](https://developer.mozilla.org/en-US/) - Comprehensive web development documentation
- [React Documentation](https://reactjs.org/docs/getting-started.html)
- [You Don't Know JS](https://github.com/getify/You-Dont-Know-JS) - In-depth JavaScript knowledge
- [Frontend Masters](https://frontendmasters.com/) - Advanced frontend courses

### Backend Development

#### API Design
- **REST**
  - Resource modeling, status codes, idempotency
  - Versioning, pagination, filtering
- **GraphQL**
  - Schema design, resolvers, directives
  - Batching, caching strategies, subscriptions

#### Server Technologies
- **Node.js**
  - Event loop, streams, clustering
  - Error handling, debugging, performance tuning
- **Java/Spring**
  - Dependency injection, AOP, Spring Boot
  - JVM tuning, garbage collection
- **Go**
  - Goroutines, channels, defer/panic/recover
  - Memory management, concurrency patterns
- **Python**
  - Django, Flask, FastAPI frameworks
  - Asyncio, decorators, context managers

#### Common Interview Questions
- How would you design a rate limiter for an API?
- Explain your approach to API versioning
- Describe how you handle authentication and authorization in your APIs
- How would you implement a job queue for background processing?

#### Resources
- [RESTful API Design: Best Practices](https://blog.restcase.com/restful-api-design-best-practices/)
- [The System Design Primer](https://github.com/donnemartin/system-design-primer)
- [Node.js Best Practices](https://github.com/goldbergyoni/nodebestpractices)

### Databases

#### Relational Databases
- **SQL Optimization**
  - Query execution plans, indexing strategies
  - Normalization/denormalization trade-offs
- **Transaction Management**
  - ACID properties, isolation levels
  - Locking strategies, deadlock prevention

#### NoSQL Databases
- **Document Stores** (MongoDB, Firestore)
  - Document modeling, embedding vs. referencing
  - Aggregation pipelines, indexing
- **Key-Value Stores** (Redis, DynamoDB)
  - Data structures, persistence options
  - Partitioning strategies, consistency models
- **Column-Family Stores** (Cassandra, HBase)
  - Wide-column design, consistency levels
  - Read/write paths, compaction strategies

#### Common Interview Questions
- When would you choose a NoSQL database over a relational database?
- How would you design a database schema for a social media application?
- Explain database indexing and when it might hurt performance
- How would you handle database migrations with zero downtime?

#### Resources
- [Database Internals](https://www.databass.dev/) - How databases work internally
- [SQL Performance Explained](https://use-the-index-luke.com/)
- [MongoDB University](https://university.mongodb.com/) - Free MongoDB courses

### Cloud Services

#### Core Concepts
- **Infrastructure as a Service**
  - Virtual machines, networks, storage
  - Regions, availability zones, edge locations
- **Platform as a Service**
  - App hosting, managed databases, integration services
  - Deployment models, scaling policies
- **Serverless Computing**
  - Functions as a service, event-driven architecture
  - Cold starts, state management, execution limits

#### Provider-Specific Knowledge
- **AWS**
  - EC2, S3, Lambda, DynamoDB, SQS/SNS
  - IAM, VPC, CloudFormation, CloudWatch
- **Google Cloud Platform**
  - Compute Engine, Cloud Storage, Cloud Functions
  - BigQuery, Kubernetes Engine, Pub/Sub
- **Microsoft Azure**
  - Virtual Machines, Blob Storage, Functions
  - Azure SQL, Cosmos DB, Azure DevOps

#### Common Interview Questions
- How would you design a highly available system on AWS?
- Explain different strategies for deploying applications to the cloud
- How would you manage secrets and configuration in a cloud environment?
- Describe how you would set up monitoring and alerting for cloud resources

#### Resources
- [AWS Documentation](https://docs.aws.amazon.com/)
- [Google Cloud Documentation](https://cloud.google.com/docs)
- [Azure Documentation](https://docs.microsoft.com/en-us/azure/)
- [A Cloud Guru](https://acloud.guru/) - Cloud certification training

### Mobile Development

#### Native Development
- **iOS/Swift**
  - UIKit, SwiftUI, view controllers
  - Memory management, ARC, performance optimization
- **Android/Kotlin**
  - Activity lifecycle, fragments, intents
  - Jetpack Compose, MVVM architecture

#### Cross-Platform
- **React Native**
  - Bridge architecture, native modules
  - Performance considerations, navigation
- **Flutter**
  - Widget tree, state management, rendering
  - Platform channels, Dart isolates

#### Common Interview Questions
- How do you handle state management in a mobile app?
- Explain strategies for offline functionality in mobile applications
- How would you optimize a mobile app for performance?
- Describe your approach to testing mobile applications

#### Resources
- [Swift Documentation](https://swift.org/documentation/)
- [Android Developers](https://developer.android.com/)
- [React Native Documentation](https://reactnative.dev/docs/getting-started)
- [Flutter Documentation](https://flutter.dev/docs)

## Industry-Specific Knowledge

### Financial Technology (Fintech)

#### Key Concepts
- **Payment Processing**: Card networks, ACH, wire transfers
- **Banking APIs**: Open banking, account aggregation
- **Cryptocurrency**: Blockchain, smart contracts
- **Regulatory Compliance**: KYC, AML, GDPR, PSD2

#### Common Interview Questions
- How would you design a secure payment processing system?
- Explain the challenges of financial data synchronization
- How would you ensure regulatory compliance in a fintech application?

### Healthcare Technology

#### Key Concepts
- **Electronic Health Records (EHR)**: Data standards, interoperability
- **HIPAA Compliance**: PHI security, audit trails
- **Healthcare Interoperability**: HL7, FHIR, ICD codes
- **Telemedicine**: Real-time communication, scheduling systems

#### Common Interview Questions
- How would you design a system for secure patient data exchange?
- Explain the challenges of healthcare data interoperability
- How would you implement HIPAA compliance in a cloud-based healthcare application?

### E-commerce and Retail

#### Key Concepts
- **Inventory Management**: Real-time stock levels, multi-channel integration
- **Payment Processing**: Payment gateways, fraud detection
- **Order Fulfillment**: Warehouse management, shipping integration
- **Personalization**: Recommendation engines, customer segmentation

#### Common Interview Questions
- How would you design a product recommendation system?
- Explain strategies for handling high-volume traffic during sales events
- How would you implement a multi-tenant e-commerce platform?

## Preparation Strategies

### Focus on Job Requirements
- Carefully analyze the job description for specific technologies and skills
- Prioritize preparing for the technologies mentioned most prominently
- Research the company's tech stack through their engineering blog or GitHub

### Fundamental Understanding
- Focus on understanding core principles rather than memorizing syntax
- Be prepared to explain how things work under the hood
- Practice explaining complex concepts in simple terms

### Hands-on Experience
- Create sample projects showcasing relevant technologies
- Contribute to open-source projects in relevant domains
- Solve real-world problems using the target technology stack

### Stay Current
- Follow industry blogs, podcasts, and newsletters
- Participate in relevant communities (Stack Overflow, Reddit, Discord)
- Attend meetups, conferences, and workshops

## Interview Preparation Resources

### Technology-Specific Preparation
- [Frontend Interview Handbook](https://yangshun.github.io/front-end-interview-handbook/)
- [System Design Interview](https://github.com/checkcheckzz/system-design-interview)
- [The Coding Interview Bootcamp](https://www.udemy.com/course/coding-interview-bootcamp-algorithms-and-data-structure/)

### Practice Platforms
- [LeetCode](https://leetcode.com/) - Technical interview preparation
- [HackerRank](https://www.hackerrank.com/) - Coding challenges
- [Pramp](https://www.pramp.com/) - Mock interviews

### Learning Platforms
- [Pluralsight](https://www.pluralsight.com/) - Technology skill development
- [Coursera](https://www.coursera.org/) - University-level courses
- [egghead.io](https://egghead.io/) - Bite-sized coding tutorials