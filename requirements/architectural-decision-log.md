# Architectural Decision Log: Monolith vs. Microservices

This document records the decision-making process regarding the high-level architecture for this project.

## 1. Context and Initial Considerations

The project requirements identify two primary domains of functionality:

1.  **Public API (`items-list`):** A public-facing service responsible for providing a filtered, paginated list of products. It also handles the soft-deletion of items.
2.  **ETL & Analytics:** A private, background service responsible for periodically ingesting product data from the Contentful API, persisting it, and generating reports based on the entire dataset (e.g., percentage of deleted items).

Two primary architectural approaches were considered:

-   **Microservices Architecture:** This would involve creating separate, independently deployable services for each domain. Communication between them would likely require a message broker (e.g., Kafka) and an API Gateway, with each service managing its own data.
-   **Monolithic Architecture:** This would involve building a single application containing both domains as distinct modules. They would share a common database and infrastructure, with communication handled in-process.

## 2. Decision

After careful consideration of the project's scale, constraints, and guiding principles, the decision has been made to adopt a **well-structured Monolithic Architecture**.

## 3. Rationale for the Decision

This choice is based on the following key factors:

### a. Pragmatism and Reduced Complexity
For a project of this limited scope, a microservices architecture introduces substantial operational and cognitive overhead (e.g., managing brokers, gateways, distributed data, complex deployments) that is not justified. A monolith provides the most direct and pragmatic path to fulfilling the requirements.

### b. Data Integrity and Consistency
The reporting module requires transactional access to the data managed by the public API module. A shared database within a monolith guarantees strong, immediate consistency for calculating reports without the complexity of data synchronization and eventual consistency inherent in distributed systems.

### c. Alignment with Prescribed Architectural Style
The project's coding style guide mandates a **Vertical Slice Architecture**. This pattern is perfectly suited for a modular monolith, allowing us to achieve the primary organizational benefits of microservices (strong domain boundaries, high cohesion, low coupling) without the operational costs. We can build distinct, self-contained modules for `products` and `reports` within a single, deployable application.

### d. Development Velocity
A monolithic approach enables faster development, testing, and deployment cycles, which is critical in the context of this developer test. It allows the focus to remain on implementing business logic and clean code rather than on managing distributed system infrastructure.

### e. Future Extensibility
A monolith built on Clean Architecture and Vertical Slices is not a dead end. Should the application's requirements grow, the clear boundaries established by the vertical slices would make it significantly easier to extract a module into a separate microservice in the future if needed.

---

**Conclusion:** The monolithic approach is the most robust, efficient, and professional choice, directly aligning with the project's requirements and demonstrating a mature understanding of architectural trade-offs.
