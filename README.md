# Member of Technical Staff - Engineering Challenge

>
> This challenge is designed for Senior Staff, Principal, and Team Lead candidates.


| Aspect        | Expectation                                      |
|---------------|--------------------------------------------------|
| **Time**      | 2-4 hours                                        |
| **Format**    | Written document (Markdown Only).                |
| **Code**      | No code changes required (but not prohibited)    |
| **AI Use**    | Permitted                                         |


---

## The Problem Statement

As a Member of Technical Staff on this engineering team, your task is to **evaluate this software** and provide a comprehensive technical assessment covering system design and full stack code. You are expected to be capable of hands-on development of end-to-end of the stack.

### Deliverables

Please provide a written analysis covering SOFTWARE ENGINEERING ASPECTS & OVERALL SYSTEM DESIGN: 

1. **What works well**
   - Identify strengths in the current implementation of the API, Backend, Architecture

2. **What does not work well**
   - Identify issues and areas of concern
   - Classify each by severity: Critical, High, Medium, or Low

3. **Recommended changes**
   - What improvements would you make on the overall system?
   - In what order and why?

4. **Architecture Direction**
   - Given creative powers to drive this technical product ahead, propose a backlog for the next 3 months and 6 months (bullet points only)

5. **Anything and everything else that you would like to mention and deep dive into**

### Guidance

- Spend time exploring the UI, **deep diving into the backend code**, and understanding the overall intent of the system
- Focus on depth over breadth — it's better to thoroughly analyze core areas than to superficially cover everything
- There is no single "right answer" — we're interested in your thinking and prioritization

### Success Metrics & Evaluation Approach

Emphasis on backend, infrastructure, system design, and technical internals over UI and cosmetics.

- **Technical Depth**: Understanding and analysis of complex system interactions
- **Problem Space**: Ability to identify core pillars of the system and issues
- **Strategic Planning**: Quality of change suggestions and decisions
- **Innovation**: Solutions and advanced technical knowledge

---

## The Vision

This product is a PaaS control plane that enables self-service for requesting infrastructure resources. In modern organizations with thousands of developers across hundreds of teams, there is constant demand for various types of infrastructure: AWS services, Kubernetes namespaces, databases, queues, and more.

Various personas will use this portal for their infrastructure needs:
- **Application developers** requesting namespaces and databases for their microservices
- **Data engineers** provisioning storage and compute resources for pipelines
- **Platform teams** managing quotas, policies, and governance across the organization
- **Team leads** tracking resource usage and costs for their teams

Core Objectives:

- **Self-service provisioning** — Developers request what they need without filing tickets
- **Standardization** — Infrastructure is created consistently with best practices baked in
- **Visibility** — Central tracking of all provisioned resources across the organization
- **Governance** — Policies, quotas, and approvals can be enforced programmatically

**This codebase is a prototype** of such a platform, supporting:
- AWS infrastructure provisioning (S3, DynamoDB, Lambda, RDS, SQS)
- Kubernetes namespace provisioning with quotas, limits, and network policies

LocalStack and k3d are used for AWS and Kubernetes locally for development purposes.

---

## Prerequisites

Before starting, ensure you have the following installed:

- **Docker Desktop** (or Docker + Docker Compose)
- **Node.js 18+**
- **kubectl** — Kubernetes CLI
- **mise** — Task runner (installation below)

---

## Getting Started

### 1. Download the codebase

Download the latest release from GitHub:

**https://github.com/intuitivetp/paasport-assessment/releases**

Extract the zip file and open a terminal in the extracted directory.

### 2. Install mise (if not already installed)

```bash
curl https://mise.run | sh
```

Follow the instructions to add mise to your shell profile, then restart your terminal.

### 3. Start the infrastructure stack

```bash
mise run up
```

This will:
- Start PostgreSQL, Gitea (local Git server), and LocalStack via Docker Compose
- Create a k3d Kubernetes cluster
- Install ArgoCD and Headlamp
- Install application dependencies

This takes a few minutes on first run.

### 3. Start the development servers

```bash
mise run dev
```

This starts the API and UI in development mode.

### 4. Access the application

| Service   | URL                          | Credentials       |
|-----------|------------------------------|-------------------|
| UI        | http://localhost:5051        | —                 |
| API       | http://localhost:5050        | —                 |
| ArgoCD    | http://localhost:9080        | admin / admin     |
| Headlamp  | http://localhost:9443        | (token from setup)|
| Gitea     | http://localhost:5055        | paasport / paasport |

---

## Useful Commands

| Command                | Description                              |
|------------------------|------------------------------------------|
| `mise run up`          | Start all infrastructure services        |
| `mise run dev`         | Start API and UI in development mode     |
| `mise run down`        | Stop all services                        |
| `mise run status`      | Check status of running services         |
| `mise run logs`        | View logs from services                  |
| `mise run k3d:k9s`     | Open k9s for Kubernetes exploration      |
| `mise run argocd:ui`   | Open ArgoCD UI in browser                |

---

## Troubleshooting

If you encounter issues:

1. **Docker not running** — Ensure Docker Desktop is started
2. **Port conflicts** — Check if ports 5050, 5051, 5055, 9080, or 9443 are in use
3. **k3d cluster issues** — Try `mise run k3d:down` then `mise run up` to recreate
4. **General reset** — Run `mise run down` followed by `mise run up`

---

### Good luck!
