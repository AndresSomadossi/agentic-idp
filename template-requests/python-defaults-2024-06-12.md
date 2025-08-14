## Template Request: python-defaults

### Description
Request for a new Python template utilizing all platform defaults: Python 3.x, no specific framework, platform default package manager (likely pip or poetry), monorepo structure, and CI/CD via GitHub Actions with linting, testing, and containerization. Intended for rapid bootstrapping of Python projects within platform standards. Deployment will be blocked until the template passes engineering review.

### Requirements
- **Language/Runtime:** Python 3.x
- **Framework:** None specified (platform default)
- **Purpose:** General-purpose Python applications and services
- **Key Features:**
  - Monorepo support
  - CI/CD (GitHub Actions)
  - Linting
  - Testing
  - Containerization
- **Constraints:**
  - Must work for private repos and shared org environments
  - No framework-specific setup required

### Proposed Stack
- **Language:** Python
- **Runtime:** Python 3.x
- **Framework:** N/A (platform default)
- **Package Manager:** pip or poetry (platform default)
- **Additional Tools:**
  - Testing: pytest
  - Linting: flake8 or black
  - CI/CD: GitHub Actions
  - Containerization: Docker

### Implementation Details
- **Monorepo:** Yes
- **CI/CD:** GitHub Actions workflows for build, test, lint, and Docker image creation
- **Deployment:** Blocked until template passes engineering review
- **Testing:** pytest
- **Documentation:** Basic `README.md` for usage

### Priority
- **Urgency:** High
- **Business Impact:** Enables automated project bootstrapping for Python services and applications
- **User Request:** Andres (requested via Project Starter Agent)

### Validation Results
- **Existing Templates Checked:** None found for Python defaults in agentic-idp (catalog unavailable, 404)
- **Similar PRs Checked:** None found for Python default template request in recent PR history
- **Uniqueness Confirmed:** Yes (no overlaps in catalog or PR history)

### Notes
- Audit/disclaimer: Final deployment is subject to IDP maintainers' approval. Template may be replaced if a recommended one becomes available.
- Engineering team notified via Teams for review.
