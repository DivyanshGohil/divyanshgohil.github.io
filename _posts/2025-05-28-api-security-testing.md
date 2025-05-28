---
title: 'API Security Testing'
date: 2025-05-28
permalink: /posts/2025/05/api-security-testing/
tags:
  - VAPT
  - API Testing
---


## Introduction
In today's interconnected world, APIs (Application Programming Interfaces) are the backbone of modern software, enabling seamless communication between systems. However, they also introduce significant security risks if not properly secured. This guide, based on Wesley Thijs's *CAPIE - Certified API Hacking Expert*, provides a deep dive into API security, testing methodologies, and best practices.

---

## Table of Contents
1. [Introduction to APIs](#introduction-to-apis)
2. [SOAP vs. REST](#soap-vs-rest)
3. [API Authentication & Authorization](#api-authentication--authorization)
4. [API Architectures](#api-architectures)
5. [OWASP API Top 10 - 2023](#owasp-api-top-10---2023)
6. [API Pentesting Documentation](#api-pentesting-documentation)
7. [API Firewalls](#api-firewalls)
8. [HTTP Request Methods](#http-request-methods)
9. [CVSS Scoring](#cvss-scoring)

---

## Introduction to APIs
APIs define the rules for how software components interact. They are critical for modular, scalable architectures but can introduce vulnerabilities if not secured properly. Key points:
- **Types of Web APIs**: REST and SOAP.
- **Importance**: Enable third-party integrations, save development time, and improve scalability.

---

## SOAP vs. REST
Two foundational styles of web APIs:

| Aspect          | SOAP                          | REST                          |
|-----------------|-------------------------------|-------------------------------|
| Protocol        | Strict protocol               | Architectural style           |
| State           | Can be stateful               | Typically stateless           |
| Message Format  | XML                           | JSON (commonly)              |
| Error Handling  | Built-in `<soap:Fault>`       | HTTP status codes             |
| Use Cases       | Enterprise, legacy systems    | Modern web/mobile apps       |

---

## API Authentication & Authorization
Controlling access to APIs is critical. Common methods include:
1. **Basic Authentication**: Base64-encoded credentials (insecure without TLS).
2. **API Keys**: Unique identifiers for applications.
3. **OAuth 2.0**: Delegated access framework (e.g., "Sign in with Google").
4. **JWT (JSON Web Tokens)**: Token-based authentication with Header, Payload, and Signature.

---

## API Architectures
APIs fit into broader system architectures:
- **Monolithic vs. Microservices**: Monolithic is simpler but less scalable; microservices improve scalability but add complexity.
- **API Gateway**: Routes requests, handles caching, rate limiting, and logging.
- **GraphQL**: Allows clients to request specific data, but vulnerable to overfetching.

---

## OWASP API Top 10 - 2023

1. **Broken Object Level Authorization (BOLA)**: Failing to properly enforce ownership checks on object access.
2. **Broken Authentication**: Weak or misconfigured login/session management.
3. **Broken Object Property Level Authorization**: Users can change protected fields (mass assignment).
4. **Unrestricted Resource Consumption**: Lack of rate limits, large payloads, or excessive queries.
5. **Broken Function Level Authorization**: Lower-privileged users can invoke sensitive functions.
6. **Unrestricted Access to Sensitive Business Flows**: Lack of checks around critical operations (e.g., bulk deletes).
7. **Server-Side Request Forgery (SSRF)**: APIs making backend HTTP requests based on user input.
8. **Security Misconfiguration**: Debug endpoints, default credentials, verbose errors, etc.
9. **Improper Inventory Management**: Forgotten, outdated, or undocumented API versions.
10. **Unsafe Consumption of APIs**: Trusting or mishandling unverified third-party responses.

---

## API Pentesting Documentation
A structured approach to API security testing:
1. **Test Plan**: Define objectives, scope, and methodology.
2. **Test Report**: Document findings, severity, and remediation steps.
3. **Test Debrief**: Review results with stakeholders and plan fixes.

---

## API Firewalls
A security layer to inspect and block malicious API traffic:
- **Deployment Models**: Reverse proxy, sidecar/service mesh, inline appliance.
- **Configuration**: Schema validation, rate limiting, authentication checks.
- **Bypass Techniques**: Ethical testing to improve defenses (e.g., input evasion, HTTP verb tampering).

---

## HTTP Request Methods
Key methods for RESTful APIs:
- **GET**: Retrieve data (safe, idempotent).
- **POST**: Create data (unsafe, non-idempotent).
- **PUT/PATCH**: Update data (unsafe, idempotent for PUT).
- **DELETE**: Remove data (unsafe, idempotent).

---

## CVSS Scoring
The Common Vulnerability Scoring System (CVSS) quantifies vulnerability severity:
- **Base Metrics**: Exploitability (e.g., attack vector) and impact (confidentiality, integrity, availability).
- **Temporal/Environmental Metrics**: Adjust for exploit maturity and organizational context.
- **Example**: A SQL injection with High impact scores 4.7 (Medium severity).

---

## Conclusion
APIs are powerful but require robust security practices. By understanding vulnerabilities, testing methodologies, and mitigation strategies, you can build and maintain secure APIs. For deeper insights, explore tools like Postman, SOAP UI, and OWASP guidelines. In my next blog, we’ll get hands-on and perform practical API testing using Postman, cURL, and Python.