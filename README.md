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

---

## 3) Fraud prevention and API controls

- OAuth-based authorisation model in use (no HMRC password storage).
- Fraud prevention headers are implemented and verified.
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

---

## 7) Reviewer checklist (quick validation)

- [x] End-to-end stateful journey evidence for all 3 income sources
- [x] Fraud prevention header evidence references
- [x] Security and compliance process coverage
- [x] Public legal/policy URLs included
- [ ] Final timestamped request/response evidence bundle attached
- [ ] Final internal approval sign-off recorded

---

## 8) Sensitive data notice

No live or reusable credentials should be published. Any previously shared test credentials should be rotated before external distribution.
