# JoinTheFuture — Self-Hosted Infrastructure & Email Automation

**DevOps / Backend Engineering / Linux Administration** · [Live website: jointhefuture.pl](https://jointhefuture.pl/)

[Polski opis projektu](README.pl.md)

> **Portfolio case study.** This repository documents my infrastructure and backend-related work for the JoinTheFuture website. It is **not** a copy of the website's source repository or production configuration.

## Project at a glance

I run the JoinTheFuture website on a **self-managed Linux server**. My responsibilities include infrastructure and hosting operations, **Docker-based services and Caddy**, deployment automation, and the backend supporting the website's contact form.

The contact workflow uses a **Python backend** on infrastructure under our control, with **Hostinger SMTP** for transactional email delivery. It does not require a third-party hosted form backend.

| Area | What I work with |
| --- | --- |
| Hosting & operations | Self-managed Linux server, web hosting and service maintenance |
| Containers & routing | Docker, Caddy reverse proxy, HTTPS and TLS certificates |
| Backend | Python-based contact form endpoint |
| Email integration | SMTP through Hostinger, server-side handling of email credentials |
| Delivery automation | GitHub Actions, build and validation, SSH-based deployment |
| Reliability | Health checks, basic request protection, deployment backups and recovery procedures |

## Architecture — simplified public view

The diagram shows the **logical components**, not a literal network topology or a production-ready deployment specification. In particular, internal proxy hops and deployment details are intentionally omitted.

~~~mermaid
flowchart TD
    A["Visitor / Web Browser"]
    B["JoinTheFuture Website<br/>Self-hosted Linux server"]
    C["Caddy<br/>HTTPS / reverse proxy"]
    D["Contact form"]
    E["Python contact backend"]
    F["Hostinger SMTP"]
    G["Notification / confirmation email"]

    A -->|"HTTPS"| C
    C --> B
    B --> D
    D -->|"Server-side request"| E
    E -->|"SMTP / TLS"| F
    F --> G
~~~

The **site** is hosted on our own server. **Caddy** handles public HTTPS routing; the **contact backend** processes form submissions before sending emails via Hostinger. Docker is used within the hosted infrastructure. The precise internal arrangement may change as services evolve.

## What I implemented or maintain

### Server administration and self-hosting

- Managing the server-side environment for a real, live website.
- Operating Docker-based services and Caddy routing / HTTPS configuration.
- Keeping public-facing hosting separate from private application configuration.

### Python backend & email automation

- Supporting a self-hosted Python endpoint for contact form submissions.
- Relaying form messages and email confirmations through Hostinger SMTP.
- Keeping SMTP credentials on the server rather than exposing them in frontend code.
- Working with request validation and safeguards such as size limits, anti-spam measures and rate limiting.

### Deployment workflow

The website's repository uses **GitHub Actions** to build, check URL consistency and deploy site artifacts to the self-managed server. The workflow also distributes the contact backend files and can activate a server-side deployment hook.

~~~mermaid
flowchart LR
    A["Changes merged to main"]
    B["GitHub Actions"]
    C["Build & checks"]
    D["Server deployment"]
    E["Live website"]

    A --> B --> C --> D --> E
~~~

The underlying source repository and deployment credentials remain private.

## Technology stack

**Linux** · **Docker** · **Caddy** · **Python** · **SMTP (Hostinger)** · **GitHub Actions** · **SSH** · **HTTPS/TLS** · **JavaScript**

## Why this project matters

This is experience maintaining **real-world, self-hosted infrastructure**, not merely running a sample application locally. It demonstrates practical backend integration, web operations, delivery automation, and security-conscious handling of production secrets.

## Verification and confidentiality

- **Live website:** https://jointhefuture.pl/
- **My GitHub:** https://github.com/socir9
- The website's development repository is private; this public case study does not grant access to it.
- No application source code, private server addresses, environment files, credentials, SMTP passwords, customer messages, or internal runbooks are distributed here.
- The documented components describe the project architecture and workflows; they are **not a public infrastructure-as-code deployment package**.

---

**Portfolio owner:** [@socir9](https://github.com/socir9)  
**Focus:** Self-hosting, DevOps practices, Python backend and email automation.
