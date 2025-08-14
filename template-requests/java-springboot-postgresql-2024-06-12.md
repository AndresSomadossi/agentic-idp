## Template Request: Java Spring Boot PostgreSQL Backend

### Description
A new backend template for enterprise Java services using Spring Boot and PostgreSQL. This template should match conventional enterprise backend standards, provide standard integrations for testing, CI/CD, and containerization, and use modern defaults (Gradle or Maven as build tool).

### Requirements
- **Language/Runtime:** Java
- **Framework:** Spring Boot
- **Purpose:** Enterprise backend service
- **Key Features:**
  - Spring Boot application structure
  - PostgreSQL integration
  - Standard build tool (Gradle/Maven)
  - Default testing (JUnit, Mock frameworks)
  - CI/CD pipeline (GitHub Actions)
  - Containerization (Docker)
- **Constraints:**
  - Use standard and modern defaults for all integrations
  - No special deployment constraints

### Proposed Stack
- **Language:** Java
- **Runtime:** JVM
- **Framework:** Spring Boot
- **Package Manager:** Gradle or Maven (default to Gradle)
- **Additional Tools:** JUnit, Mockito, GitHub Actions, Docker

### Implementation Details
- **Monorepo:** No
- **CI/CD:** GitHub Actions
- **Deployment:** Standard (Docker-ready)
- **Testing:** JUnit, Mockito
- **Documentation:** Standard README, API docs

### Priority
- **Urgency:** Medium
- **Business Impact:** Enables standardized backend development for enterprise Java services
- **User Request:** Andres (requested via Project Starter Agent)

### Validation Results
- **Existing Templates Checked:** None found for Java + Spring Boot + PostgreSQL in agentic-idp
- **Similar PRs Checked:** None found for Java + Spring Boot + PostgreSQL template request
- **Uniqueness Confirmed:** Yes (no overlaps in catalog or PR history)

### Notes
- Audit/disclaimer: Final deployment is subject to IDP maintainers' approval. Template may be replaced if a recommended one becomes available.
- Engineering team notified via Slack for review.
