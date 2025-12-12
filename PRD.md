# Product Requirements Document: Email Newsletter Service

## Overview

**Project:** zero2prod  
**Type:** Cloud-native backend API  
**Language:** Rust 2024

A minimal email newsletter backend service that enables blog visitors to subscribe to updates and allows the blog author to send email notifications to all subscribers when new content is published.

---

## User Stories

### Story 1: Newsletter Subscription
**As a** blog visitor,  
**I want to** subscribe to the newsletter,  
**So that** I can receive email updates when new content is published on the blog.

**Acceptance Criteria:**
- Visitor can submit their email address to subscribe
- Email address is validated before storing
- Duplicate subscriptions are handled gracefully
- Subscriber receives confirmation that subscription was successful

### Story 2: Send Newsletter
**As the** blog author,  
**I want to** send an email to all my subscribers,  
**So that** I can notify them when new content is published.

**Acceptance Criteria:**
- Author can compose and send a newsletter with subject and body
- Newsletter is delivered to all confirmed subscribers
- System handles delivery failures gracefully
- Author receives feedback on send status

---

## Non-Goals (Out of Scope)

The following features are explicitly **NOT** included in this version:

- Unsubscribe functionality
- Managing multiple newsletters
- Subscriber segmentation/multiple audiences
- Email open/click rate tracking
- Rich HTML email templates
- Scheduled/delayed sending
- Subscriber management UI

---

## Technical Requirements

### API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/subscriptions` | Subscribe a new email address |
| `POST` | `/newsletters` | Send newsletter to all subscribers |
| `GET`  | `/health_check` | Service health check endpoint |

### Data Model

#### Subscriber
| Field | Type | Constraints |
|-------|------|-------------|
| `id` | UUID | Primary key |
| `email` | String | Unique, valid email format |
| `name` | String | Subscriber's name |
| `subscribed_at` | Timestamp | When subscription was created |
| `status` | Enum | `pending_confirmation`, `confirmed` |

#### Newsletter (Request)
| Field | Type | Description |
|-------|------|-------------|
| `title` | String | Email subject line |
| `content` | Object | `{ text: String, html: String }` |

### Non-Functional Requirements

- **Performance:** Handle concurrent subscription requests
- **Reliability:** Idempotent subscription handling
- **Security:** Input validation, rate limiting
- **Observability:** Structured logging, health checks
- **Cloud-Native:** 
  - Containerized (Docker)
  - 12-factor app principles
  - Environment-based configuration
  - Graceful shutdown handling

### Technology Stack

- **Runtime:** Rust 2024
- **Web Framework:** actix-web (async, performant)
- **Database:** PostgreSQL
- **Email Delivery:** Third-party SMTP service (e.g., Postmark, SendGrid)
- **Configuration:** Environment variables
- **Deployment:** Docker container

---

## Success Criteria

1. A visitor can successfully subscribe with a valid email
2. Author can send a newsletter that reaches all subscribers
3. Service passes health checks
4. All clippy warnings resolved (`-D warnings`)
5. Test coverage for critical paths
6. Service runs in a container

---

## Milestones

1. **M1:** Project setup, health check endpoint, CI pipeline
2. **M2:** Subscription endpoint with database persistence
3. **M3:** Email confirmation flow
4. **M4:** Newsletter sending endpoint
5. **M5:** Production deployment configuration
