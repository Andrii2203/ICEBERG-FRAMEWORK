# API Interaction Standard  
(Iceberg Framework — Enterprise Edition, v0.1)

This standard defines the **official, deterministic, secure, and scalable way** that all Iceberg‑based Next.js applications interact with APIs.

It covers:

- architecture  
- adapters  
- error handling  
- caching  
- RSC integration  
- server actions  
- security  
- observability  
- testing  
- multi‑tenancy  
- performance  
- resilience  
- governance  

This is an enterprise‑grade document with **35 sections**.

---

# 1. Core Principles

## 1.1. Server‑Driven API Interaction
All API calls must be executed **on the server**, never in the client.

## 1.2. Adapter‑Based Architecture
DTOs must never reach UI.  
Adapters convert API → Domain.

## 1.3. Deterministic Error Handling
All errors follow a single normalized format.

## 1.4. Predictable Caching
Caching is server‑controlled, never client‑controlled.

## 1.5. Strict Separation of Concerns
API layer contains no UI, no business logic, no state.

---

# 2. API Layer Structure

```
src/shared/api/
  http/
  adapters/
  endpoints/
  errors/
  types/
  utils/
```

---

# 3. HTTP Client Architecture

## 3.1. Single HTTP Client
One client for all requests.

## 3.2. Required Features
- base URL  
- interceptors  
- timeouts  
- retries  
- logging  
- error normalization  

## 3.3. Forbidden
- multiple clients  
- inline fetch logic  
- duplicated headers  

---

# 4. Request Lifecycle

## 4.1. Steps
1. Build request  
2. Attach auth/session  
3. Validate input  
4. Execute request  
5. Normalize error  
6. Adapt response  
7. Return domain model  

## 4.2. Forbidden
- skipping validation  
- returning raw DTO  

---

# 5. Adapter Architecture

## 5.1. Purpose
Convert:

```
DTO → Domain Model
```

## 5.2. Rules
- pure functions  
- deterministic  
- no side effects  
- no API calls  

## 5.3. Forbidden
- DTO in UI  
- adapters in components  
- mixing DTO and domain  

---

# 6. DTO Architecture

## 6.1. DTO Rules
- reflect API exactly  
- never modified  
- never extended  

## 6.2. Forbidden
- using DTO as domain model  
- mutating DTO  

---

# 7. Domain Model Architecture

## 7.1. Domain Models
- stable  
- typed  
- UI‑safe  

## 7.2. Forbidden
- leaking DTO fields  
- exposing API internals  

---

# 8. Error Handling Architecture

## 8.1. Unified Error Format

```ts
type ApiError = {
  code: string;
  message: string;
  status: number;
  details?: unknown;
};
```

## 8.2. Error Categories
- transport  
- HTTP  
- business  
- unexpected  

## 8.3. Forbidden
- throwing raw errors  
- leaking backend stack traces  

---

# 9. Retry Architecture

## 9.1. Retry Rules
- exponential backoff  
- max retry count  
- retry only idempotent requests  

## 9.2. Forbidden
- retrying POST  
- infinite retries  

---

# 10. Timeout Architecture

## 10.1. Rules
- strict timeouts  
- per‑endpoint configuration  

## 10.2. Forbidden
- unlimited timeouts  

---

# 11. Authentication Architecture

## 11.1. Rules
- server‑side session  
- cookies only  
- no tokens in client  

## 11.2. Forbidden
- localStorage tokens  
- query param tokens  

---

# 12. Authorization Architecture

## 12.1. Rules
- enforced server‑side  
- enforced before API call  

## 12.2. Forbidden
- client‑side permission checks  

---

# 13. Input Validation Architecture

## 13.1. Rules
- validate before sending  
- validate server actions  
- validate forms  

## 13.2. Forbidden
- trusting client input  

---

# 14. Output Validation Architecture

## 14.1. Rules
- validate DTO shape  
- validate required fields  

## 14.2. Forbidden
- trusting API blindly  

---

# 15. Caching Architecture

## 15.1. Public Data
`force-cache`

## 15.2. Private Data
`no-store`

## 15.3. Revalidation
`next: { revalidate: X }`

## 15.4. Forbidden
- caching private data  
- caching mutations  

---

# 16. Tag‑Based Revalidation

## 16.1. Rules
- use tags for lists  
- use tags for dashboards  

## 16.2. Forbidden
- revalidate everything  

---

# 17. RSC Integration

## 17.1. Rules
- API calls only in RSC  
- no client fetch  

## 17.2. Forbidden
- API in useEffect  
- API in client hooks  

---

# 18. Server Actions Integration

## 18.1. Rules
- all mutations via server actions  
- validate input  
- return domain models  

## 18.2. Forbidden
- POST from client  

---

# 19. Route Handler Integration

## 19.1. Rules
- only for streaming  
- only for uploads  
- only for webhooks  

## 19.2. Forbidden
- business logic  

---

# 20. Multi‑Tenancy Architecture

## 20.1. Rules
- tenantId required  
- tenant isolation enforced  

## 20.2. Forbidden
- trusting client tenantId  

---

# 21. Observability Architecture

## 21.1. Logs
- URL  
- status  
- latency  
- userId  
- tenantId  

## 21.2. Metrics
- p95 latency  
- error rate  
- throughput  

---

# 22. Tracing Architecture

## 22.1. Rules
- correlationId required  
- trace per request  

---

# 23. Rate Limiting Architecture

## 23.1. Rules
- per user  
- per tenant  
- per IP  

---

# 24. Throttling Architecture

## 24.1. Rules
- protect backend  
- protect RSC  

---

# 25. Circuit Breaker Architecture

## 25.1. Rules
- open on repeated failures  
- fallback to cached data  

---

# 26. Bulk Request Architecture

## 26.1. Rules
- batch requests  
- reduce API load  

---

# 27. Pagination Architecture

## 27.1. Rules
- cursor‑based  
- deterministic  

---

# 28. Sorting Architecture

## 28.1. Rules
- server‑side  
- validated  

---

# 29. Filtering Architecture

## 29.1. Rules
- server‑side  
- validated  

---

# 30. Search Architecture

## 30.1. Rules
- server‑side  
- debounced client input  

---

# 31. File Upload Architecture

## 31.1. Rules
- streaming  
- server‑side validation  

---

# 32. Webhook Architecture

## 32.1. Rules
- signature validation  
- idempotency  

---

# 33. Performance Architecture

## 33.1. Rules
- avoid overfetching  
- avoid underfetching  
- use aggregation endpoints  

---

# 34. Resilience Architecture

## 34.1. Rules
- retries  
- fallbacks  
- circuit breakers  

---

# 35. Anti‑Patterns (Forbidden)

❌ API in client components  
❌ useEffect fetch  
❌ DTO in UI  
❌ caching private data  
❌ POST from client  
❌ tokens in localStorage  
❌ trusting client tenantId  
❌ business logic in API layer  
❌ adapters in components  
❌ multiple HTTP clients  

---

# Summary

The API Interaction Standard ensures:

- **deterministic API behavior**  
- **secure server‑driven architecture**  
- **clean adapter‑based data flow**  
- **predictable error handling**  
- **correct caching**  
- **RSC‑first design**  
- **enterprise‑grade resilience**  
- **multi‑tenant safety**  
- **observability and governance**  

