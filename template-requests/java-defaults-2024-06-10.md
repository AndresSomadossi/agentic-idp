## Template Request: java-defaults

### Description
Request for a new Java template utilizing all defaults: Java 17 (JDK), Maven package manager, no specific framework, standard CI/CD (GitHub Actions), linting, testing, and containerization. Intended for private repositories within org `my-org`. Deployment will be blocked until the template passes engineering review.

### Requirements
- **Language/Runtime:** Java (JDK 17)
- **Framework:** None specified
- **Purpose:** General-purpose Java applications
- **Key Features:**
  - Monorepo support
  - CI/CD (GitHub Actions)
  - Linting
  - Testing
  - Containerization
- **Constraints:**
  - Must work for private repos within `my-org`
  - No framework-specific setup required

### Proposed Stack
- **Language:** Java
- **Runtime:** JDK 17
- **Framework:** N/A
- **Package Manager:** Maven
- **Additional Tools:**
  - Testing: JUnit
  - Linting: Checkstyle or SpotBugs
  - CI/CD: GitHub Actions
  - Containerization: Docker

### Implementation Details
- **Monorepo:** Yes
- **CI/CD:** GitHub Actions workflows for build, test, lint, and Docker image creation
- **Deployment:** Blocked until template passes engineering review
- **Testing:** JUnit
- **Documentation:** Basic `README.md` for usage

### Priority
- **Urgency:** High
- **Business Impact:** Enables automated project bootstrapping for Java services in org `my-org`
- **User Request:** Andres (requested via Project Starter Agent)

### Notes
- Notifications to be sent via Slack channel #devops-notifications
- Repo visibility: private
- Please audit the setup for best practices and compliance.
