## 1. Technology Stack and Service Architecture

TALA will be implemented using a cloud-first web application stack with managed backend services and external integrations.

The system will follow a modular monolith approach: one main application will contain the SIS workflows, while external services will provide hosting, authentication, database, storage, payment processing, email delivery, and scheduling computation.

### 1.1 Application Stack

| Layer                | Selected Technology |
| -------------------- | ------------------- |
| Web Framework        | Next.js             |
| Programming Language | TypeScript          |
| Frontend Library     | React               |
| UI Components        | shadcn/ui           |
| UI Base              | Radix UI            |
| Styling              | Tailwind CSS        |
| Icons                | Lucide React        |
| Forms                | React Hook Form     |
| Validation           | Zod                 |
| Tables               | TanStack Table      |
| Date Utilities       | date-fns            |

### 1.2 Backend and Data Services

| Service Area      | Selected Service                          |
| ----------------- | ----------------------------------------- |
| Authentication    | Supabase Auth                             |
| Database          | Supabase PostgreSQL                       |
| File Storage      | Supabase Storage                          |
| Server-Side Logic | Next.js Server Actions and API Routes     |
| Hosting           | Vercel                                    |
| Deployment        | Vercel Preview and Production Deployments |

### 1.3 External Product Integrations

| Integration Area       | Selected Service                                               |
| ---------------------- | -------------------------------------------------------------- |
| Scheduling Computation | Existing Google Cloud Run CP-SAT service using Google OR-Tools |
| Online Payment Gateway | PayMongo                                                       |
| Email Notifications    | Resend                                                         |

### 1.4 Development and AI Tooling

| Tooling Area            | Selected Tool / Service                                      |
| ----------------------- | ------------------------------------------------------------ |
| Repository Hosting      | GitHub                                                       |
| Package Manager         | pnpm                                                         |
| Code Editor             | Antigravity or Cursor                                            |
| AI Development Support  | MCP-enabled tools where available                            |
| UI Component MCP        | shadcn MCP                                                   |
| Database/Backend MCP    | Supabase MCP                                                 |
| Deployment MCP          | Vercel MCP                                                   |
| Repository MCP          | GitHub MCP                                                   |
| Framework Debugging MCP | Next.js DevTools MCP                                         |
| Email MCP               | Resend MCP, when email work begins                           |
| Cloud Run MCP           | Google Cloud Run MCP, optional for CP-SAT service inspection |

PayMongo has no confirmed official MCP server. PayMongo integration will use the official PayMongo dashboard, API documentation, API keys, test mode, and webhook logs.

### 1.5 Service Responsibility Boundaries

TALA remains the source of truth for official SIS records.

Supabase provides authentication, database, and private file storage, but TALA owns the meaning of roles, permissions, workflows, student records, admissions, enrollment, finance evidence, grades, CORs, and audit records.

Vercel provides hosting, deployment, and public webhook accessibility, but TALA owns application behavior and official workflow decisions.

PayMongo provides online payment processing and payment event evidence, but TALA owns payment verification, finance clearance, ledger posting, balance, SOA, and payment acknowledgement.

The Google Cloud Run CP-SAT service provides scheduling computation only. TALA owns scheduling inputs, candidate review, validation, publication, enrollment binding, and COR schedule reference.

Resend provides email delivery only. TALA owns notification triggers, recipient rules, templates, and notification history.

### 1.6 Architecture Style

The selected architecture is:

**Cloud-first modular monolith with external service adapters**

This means:

1. TALA is one main web application.
2. SIS workflows are implemented inside the main application.
3. External systems are connected through service adapters.
4. The system avoids premature microservices.
5. Official academic, enrollment, finance, grade, and artifact records remain inside TALA.
6. External services support infrastructure, payment, email, and scheduling computation.

### 1.7 Environment Strategy

TALA will use separate environments:

| Environment       | Purpose                                           |
| ----------------- | ------------------------------------------------- |
| Development       | Local app connected to development cloud services |
| Preview / Staging | Vercel preview deployment for testing and UAT     |
| Production        | Final deployed system for live institutional use  |

Development should use test or development credentials for Supabase, PayMongo, Resend, and CP-SAT.

Production credentials must not be used during ordinary development or testing.


---

