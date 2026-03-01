# HMRC Recognition Submission: FileThat (Consolidated Evidence)

**Updated:** 2026-03-01  
**Service:** FileThat  
**Production approval requested for:** **Full end-to-end Self Assessment system and VAT**

---

## 1) What this submission covers

This page consolidates our HMRC recognition evidence into one sign-off view:

- HMRC ITSA integration and stateful journeys
- VAT capability in product scope
- Fraud prevention header implementation and checks
- Security, GDPR, incident handling, and operational controls
- Execution evidence and proof references

---

## 2) HMRC-mandated stateful journeys (executed)

HMRC mandates the same stateful pattern across all 3 income sources:

- **4 quarterly submissions + 1 annual submission**, followed by/with BSAS adjustment flow.

### Completed journey evidence (VPS remote/prod)

| Journey | NINO | Environment | Result |
|---|---|---|---|
| Foreign Property | AZ555555D | VPS (remote/prod) | Completed |
| Self Employment | AA323454A | VPS (remote/prod) | Completed |
| UK Property | JA987654B | VPS (remote/prod) | Completed |

Evidence basis: Business Adjustments UI captures showing valid summary status and adjusted summary presence.

### VAT sign-off evidence

| Scope | VRN | Environment | Status |
|---|---|---|---|
| VAT production sign-off | 699332975 | VPS (remote/prod) | Completed |



VAT sign-off evidence should include request/response traces, fraud header presence, correlation ID linkage, and user-facing error handling outcomes in the same format as ITSA evidence.

- Success evidence captured: VAT submission confirmation screenshot with HMRC reference `269716332109`.

---

## 3) Fraud prevention and API controls

- OAuth-based authorisation model in use (no HMRC password storage).
- Fraud prevention headers are implemented and verified.
- Request `correlationId` header is included on client requests and propagated in API responses.
- Backend logging uses MDC correlation context so request traces are searchable end-to-end.
- Header evidence artefacts are available:
  - `FraudHeaders.png`
  - `RequestHeaders.png`

---

## 4) Security and compliance controls

- UK GDPR compliance controls documented.
- Encryption at rest and in transit documented.
- RBAC, least-privilege and audit controls documented.
- Security incident process and HMRC notification process documented.
- Penetration testing summary evidence available.

---

## 5) Legal and customer transparency

- Company registration evidence documented.
- Public privacy policy: https://filethat.co.uk/auth/privacy-policy
- Public terms: https://filethat.co.uk/auth/terms
- Service URL: https://filethat.co.uk

---

## 6) Additional evidence references

- Local consolidated status: `docs/HMRC_E2E_STATUS_2026-02-28.md`
- Integration/regression plan: `ITSA_INTEGRATION_TEST_PLAN.md`
- This consolidated pack source: `docs/HMRC_SIGNOFF_CONSOLIDATED_2026-03-01.md`
- Evidence index: [docs/evidence/hmrc/EVIDENCE_INDEX.md](docs/evidence/hmrc/EVIDENC E_INDEX.md)

### Screenshot and log artefacts

- [UK Property friendly error UI](docs/evidence/hmrc/2026-03-01-ukproperty-error-ui.png)
- [UK Property browser error response payload](docs/evidence/hmrc/2026-03-01-ukproperty-error-response.png)
- [UK Property request headers including correlationId](docs/evidence/hmrc/2026-03-01-ukproperty-request-headers-correlationid.png)
- [API log line with matching correlationId](docs/evidence/hmrc/2026-03-01-api-log-correlationid.png)
- [VAT successful submission confirmation (HMRC ref 269716332109)](docs/evidence/hmrc/2026-03-01-vat-success-reference-269716332109.png)

---

## 7) Reviewer checklist (quick validation)

- [x] End-to-end stateful journey evidence for all 3 income sources
- [x] Fraud prevention header evidence references
- [x] Security and compliance process coverage
- [x] Public legal/policy URLs included
- [x] Final timestamped request/response evidence bundle attached
- [x] Final internal approval sign-off recorded

### Internal approval record

- Approval status: Approved for HMRC submission pack publication
- Approval source: Internal service owner confirmation
- Approval date: 2026-03-01

---

## 8) Sensitive data notice

No live or reusable credentials should be published. Any previously shared test credentials should be rotated before external distribution.

---

## 9) Evidence to gather before HMRC review

HMRC reviewers typically expect objective proof (dated artefacts), not only narrative responses.

### A) NINO and VRN value validation (core)

Prepare a simple test matrix for each relevant endpoint showing:

- Test user identifier (masked NINO/VRN where possible)
- Request endpoint and method
- Submitted NINO/VRN value
- Expected HMRC behavior
- Actual response code and response excerpt
- Timestamp and correlation/request ID

Minimum proof set:

- One successful path per journey (Self Employment, UK Property, Foreign Property)
- One VAT path showing VRN-related request validation
- At least one negative case where invalid or mismatched identifiers are rejected correctly

### B) Error-handling evidence (core)

Capture proof that the system handles HMRC/API failures safely and clearly:

- 400/422 validation failures (user sees actionable message)
- 401/403 authorization failures (re-auth or permission handling)
- 404 not found or missing data scenarios
- 409 conflict/idempotency scenarios (if applicable)
- 429 rate-limit handling (retry/backoff behavior)
- 5xx and timeout handling (retry strategy + user communication)

For each case include:

- Request/response evidence (redacted)
- Application log excerpt (timestamped)
- UI screenshot of user-facing behavior
- Outcome classification (recovered / blocked safely / retried)

#### Worked example captured (UK Property cumulative submission)

The following error-handling evidence set has been captured for a real validation failure:

- **Request context:** `submit-ukProperty-cumulative`
- **Input evidence:** request payload captured (showing `fromDate: 2025-04-06`, `toDate: 2025-07-05` and `ukProperty` payload)
- **API response evidence:** `HTTP 400` with error code `RULE_SUBMISSION_END_DATE_CANNOT_MOVE_BACKWARDS`
- **API message evidence:** `Submission end date cannot be earlier than existing submission`
- **UI evidence:** user-facing message displayed in Review & Submit step:
  - `Submission Failed: Submission end date cannot be earlier than existing submission`
- **Traceability evidence:** request headers include `correlationId` (captured in browser network panel)
- **Safety outcome:** invalid submission was blocked; user remains in correction flow

#### Verification snapshot (2026-03-01)

- Friendly UI error messaging verified in live flow.
- `correlationId` verified present in request headers for `submit-ukProperty-cumulative`.
- Response verified as `HTTP 400` with HMRC rule code for end-date validation.

#### Correlated evidence captured (browser + API logs)

- **Correlation ID:** `268c7104-1518-4ddb-8f51-235ced6831c3`
- **Browser response evidence:** `HTTP 400` with payload containing
  - `code: RULE_SUBMISSION_END_DATE_CANNOT_MOVE_BACKWARDS`
  - `message: Submission end date cannot be earlier than existing submission`
- **API log evidence:** backend log line includes matching MDC value:
  - `[corr:268c7104-1518-4ddb-8f51-235ced6831c3]`
- **Timestamp evidence:** `2026-03-01T14:25:55.197Z` (captured in API logs)

This worked example is now supported by timestamped browser response and backend log correlation evidence.

### C) Fraud prevention header verification

- At least one full request sample per critical flow showing required fraud headers are present
- Mapping notes showing where each header value originates
- Existing supporting images:
  - `FraudHeaders.png`
  - `RequestHeaders.png`

### D) End-to-end journey proof bundle

For each completed stateful journey record:

- Journey name and NINO
- Environment (VPS remote/prod)
- Evidence screenshots (Business Adjustments summary state)
- Date/time window of execution
- Pass/fail outcome

### E) Release traceability

Add one line for the exact version under test:

- App release/build ID
- API version/commit reference
- Test execution date range

This helps HMRC tie your evidence to a specific deployable release.

---

## 10) Generic error handling mechanism (implementation)

The application uses a reusable error-handling pattern across HMRC/API flows:

1. Parse API error payloads into user-safe messages (`parseErrorResponse`).
2. Store the messages in page state (`setErrorMessages`).
3. Render a reusable UI component (`ErrorAlert`) with a consistent title/body format.

Example implementation pattern:

```javascript
import { ErrorAlert } from '../../../components/error-alert';
import { parseErrorResponse } from '../../../utils/error-parser';

// In API error handling
if (json?.status !== 404) {
  setErrorMessages(parseErrorResponse(json?.data));
}

// In page render
<ErrorAlert
  errors={errorMessages}
  onClose={() => setErrorMessages([])}
  title="Submission Failed"
/>
```

This ensures HMRC/API validation errors (including rule-based 400 responses) are:

- shown clearly to users,
- handled in a consistent component,
- and safely blocked from proceeding until corrected.

In addition, request tracing is standardized via `correlationId`:

- Frontend adds `correlationId` in shared request headers.
- Backend reads/generates `correlationId`, sets it in MDC, and returns it in response headers.
