# <API Name>

This document describes the **external and internal API surface** exposed by the system.

---

## Purpose

Explain:

- who consumes this API
- what capability it exposes
- whether it is public or internal

---

## API Style

Describe the API style.

- REST / GraphQL / RPC / Event-based
- Synchronous or asynchronous
- Versioning approach

---

## Authentication and Authorization

Describe:

- how callers are authenticated
- how access is authorized

(No secrets or credentials.)

---

## Endpoints / Operations

Describe available operations at a high level.

### <Operation Name>

- **Description**: <What this operation does>
- **Inputs**: <Conceptual inputs>
- **Outputs**: <Conceptual outputs>
- **Errors**: <High-level error cases>

No full request/response schemas here unless necessary.

---

## Data Contracts

Describe shared data shapes conceptually.

- What data is exchanged
- Stability guarantees
- Backward compatibility rules

---

## Rate Limits and Constraints

If applicable:

- Limits
- Timeouts
- Payload size constraints

---

## Non-Goals

What this API explicitly does not support.
