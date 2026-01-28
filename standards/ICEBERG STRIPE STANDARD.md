❄️ ICEBERG STRIPE STANDARD
Framework Edition — Enterprise v1.0
Universal Payment Architecture Standard for All Iceberg Products

Table of Contents
Purpose

Scope

Terminology

Architectural Principles

Stripe Integration Philosophy

High‑Level Architecture

Directory Structure

Module Boundaries

Payment Lifecycle

Checkout Layer Standard

Webhook Layer Standard

Internal Job Layer Standard

Event Routing Standard

Idempotency Standard

Signature Verification Standard

Security Requirements

Error Model

Error Code Registry

Logging & Observability

Retry Semantics

Failure Recovery

Testing Requirements

Naming Conventions

Allowed Patterns

Forbidden Patterns (Non‑Negotiable)

Multi‑Product Compatibility Rules

AI‑Safe Constraints

Versioning Strategy

Deployment Requirements

Mental Model

Glossary

Change Log

1. Purpose
The ICEBERG STRIPE STANDARD defines the universal, deterministic, enterprise‑grade rules for integrating Stripe into any Iceberg Framework product.

This standard ensures:

predictable payment flows

strict separation of concerns

secure webhook handling

deterministic AI‑generated backend

zero improvisation

zero ambiguity

zero hidden state

This is a framework‑level document.

2. Scope
This standard applies to:

all Iceberg products (Audit, SEO, Memory, future tools)

all backend implementations (Next.js, Node, Nest, Go, etc.)

all payment flows (one‑time, subscription, usage‑based)

all webhook handlers

all checkout session creators

all internal job triggers

It does not describe product‑specific logic.

3. Terminology
Checkout Layer — endpoint that creates a Stripe Checkout Session.

Webhook Layer — endpoint that receives Stripe events.

Internal Job Layer — asynchronous job triggered after webhook validation.

Product Logic — business logic executed after payment confirmation.

Idempotency — guarantee that repeated events do not duplicate work.

4. Architectural Principles
Stripe is isolated  
Payment logic MUST live in a dedicated module.

Webhooks are authoritative  
No product logic runs until Stripe confirms payment.

Checkout is stateless  
Checkout endpoints MUST NOT contain business logic.

Webhooks are pure  
Webhooks MUST NOT execute product logic directly.

Idempotency is mandatory  
Every payment flow MUST be idempotent.

Security first  
Signature verification is required for every webhook.

AI‑safe design  
Payment logic MUST be deterministic and predictable.

5. Stripe Integration Philosophy
Stripe is treated as:

a payment oracle

a state machine

a source of truth

The backend MUST NOT:

trust frontend payment status

trust client‑side events

trust redirect URLs

Only Stripe webhook events define payment state.

6. High‑Level Architecture
Frontend
  ↓
Checkout Layer
  ↓
Stripe Checkout
  ↓
Stripe Webhook
  ↓
Webhook Layer
  ↓
Event Router
  ↓
Internal Job Layer
  ↓
Product Logic
7. Directory Structure
Framework‑level canonical structure:
src/
  modules/
    payments/
      services/
        stripe.service.ts
      handlers/
        webhook-handler.ts
      router/
        event-router.ts
      jobs/
        payment-jobs.ts
      utils/
        signature.ts
        idempotency.ts
      types/
        stripe.types.ts
8. Module Boundaries
Payments module MAY depend on:
core/errors

core/logging

core/config

core/validation

Payments module MUST NOT depend on:
product modules

AI modules

storage modules

API routes

9. Payment Lifecycle
9.1. Checkout
Creates a Stripe Checkout Session

Returns only the session URL

No business logic

9.2. Stripe
Processes payment

Sends webhook event

9.3. Webhook
Verifies signature

Parses event

Routes event

MUST NOT run product logic

9.4. Internal Job
Executes product logic

MUST be idempotent

10. Checkout Layer Standard
Checkout endpoints MUST:

validate input

create a Stripe session

return session URL

contain no business logic

contain no product logic

contain no AI calls

contain no file generation

Checkout endpoints MUST NOT:

trust frontend payment status

return internal IDs

expose Stripe errors

11. Webhook Layer Standard
Webhook handlers MUST:

verify signature

parse event

route event

return 200 or 400

never throw unhandled exceptions

Webhook handlers MUST NOT:

run product logic

call AI

generate files

return product data

trust frontend

12. Internal Job Layer Standard
Internal jobs MUST:

be idempotent

be asynchronous

be isolated from webhook

run product logic

log execution

handle retries

Internal jobs MUST NOT:

depend on frontend

depend on webhook request body

depend on Stripe payload directly

13. Event Routing Standard
All events MUST be routed through:
PaymentEventRouter.route(event)
Example mapping:
checkout.session.completed → Job: paymentCompleted
invoice.payment_failed → Job: paymentFailed
customer.subscription.deleted → Job: subscriptionCancelled
14. Idempotency Standard
Every payment‑related operation MUST:

check if event was already processed

store event IDs

skip duplicates

ensure product logic runs exactly once

15. Signature Verification Standard
Webhook MUST:

extract signature header

verify using Stripe secret

reject invalid signatures

log verification result

16. Security Requirements
No secrets in logs

No returning Stripe payloads

No exposing internal IDs

No debug endpoints

No bypassing webhook flow

No trusting frontend

17. Error Model
Errors MUST be mapped to:

400 Bad Request
or

500 Internal Server Error
Webhook MUST NOT throw unhandled exceptions.
18. Error Code Registry
stripe-signature-invalid

stripe-event-unknown

stripe-event-duplicate

stripe-event-processing-failed

stripe-checkout-invalid

19. Logging & Observability
Log only:

event type

event ID

processing time

result (success/error)

Do NOT log:

card details

customer data

full Stripe payload

secrets

20. Retry Semantics
Stripe retries webhooks.
System MUST:

handle retries gracefully

skip duplicates

never double‑execute product logic

21. Failure Recovery
If a job fails:

log error

retry with exponential backoff

mark event as failed

never block future events

22. Testing Requirements
MUST include:

unit tests for PaymentService

unit tests for signature verification

integration tests for webhook handler

idempotency tests

event routing tests

23. Naming Conventions
PaymentService

StripeWebhookHandler

PaymentEventRouter

createCheckoutSession

handleStripeEvent

ensureIdempotent

24. Allowed Patterns
pure functions

isolated modules

typed interfaces

deterministic flows

explicit routing

25. Forbidden Patterns (Non‑Negotiable)
Stripe code MUST NOT:

run product logic inside webhook

call AI

generate files

return product data

trust frontend

skip signature verification

skip idempotency

mix payment logic with product logic

expose Stripe errors to users

store Stripe payloads in logs

26. Multi‑Product Compatibility Rules
Stripe Standard MUST support:

one‑time payments

subscriptions

usage‑based billing

multi‑product routing

multi‑tenant routing

27. AI‑Safe Constraints
AI MUST:

follow this standard

never improvise payment flows

never modify lifecycle

never add new events

never skip idempotency

never skip signature verification

never mix layers

28. Versioning Strategy
v1.x — one‑time payments

v2.x — subscriptions

v3.x — usage‑based billing

29. Deployment Requirements
Webhook MUST NOT run on edge runtime

Webhook MUST be deployed on serverless or serverful runtime

Checkout endpoints MAY run on edge

30. Mental Model
Checkout → Stripe → Webhook → Router → Job → Product Logic
31. Glossary
Checkout Session — Stripe payment initiation

Webhook — Stripe event callback

Internal Job — asynchronous product logic executor

Idempotency — guarantee of single execution

32. Change Log
v1.0 — Initial enterprise framework edition.