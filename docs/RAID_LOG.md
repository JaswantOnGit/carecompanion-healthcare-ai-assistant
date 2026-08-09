# RAID Log — CareCompanion Healthcare AI Assistant

RAID = Risks, Assumptions, Issues, Dependencies. Reviewed against actual build behavior (see `/assets` for evidence).

## Risks

| # | Risk | Likelihood | Impact | Mitigation | Status |
|---|---|---|---|---|---|
| R1 | Agent hallucinates a hospital policy (visiting hours, billing rule) that doesn't exist | Medium | High | RAG-only grounding for policy questions; explicit instruction to say "I don't know" and route to Patient Services rather than infer | Mitigated — confirmed in UAT (see `10-rag-refusal-no-invented-policy.png`) |
| R2 | Agent fails to escalate a genuine emergency described in ambiguous language | Low–Medium | Critical | Hard-priority instruction ranks emergency detection above all other rules; tested with symptom-adjacent phrasing | Mitigated — no missed-escalation cases in UAT set |
| R3 | Agent gives medical advice when directly or indirectly asked | Medium | High | Explicit "no medical advice" rule with fixed nurse-line redirect | Mitigated |
| R4 | Multi-agent coordinator creates a duplicate or conflicting appointment | Medium | Medium | Coordinator required to check existing appointments before booking; confirmation step added | Mitigated — confirmed in `15-scheduling-duplicate-check.png` |
| R5 | Discharge-note extraction misses or misreads a critical field (medication dose, warning sign) | Low–Medium | High | Structured JSON schema enforced via prompt; spot-checked against source PDF | Monitored — would require larger sample for production sign-off |
| R6 | Regional model quota unavailable for GPT-5-mini / text-embedding-3-large | Low | Low | Documented fallback to any equivalent GPT / embedding model | Accepted |
| R7 | MCP connection to Microsoft Learn is unavailable or returns stale docs | Low | Low | Agent instructed to name its source page; failure degrades gracefully to general knowledge with a caveat | Accepted |

## Assumptions

| # | Assumption | Validation approach |
|---|---|---|
| A1 | All patient, appointment, and discharge data used in this build is synthetic | Confirmed — sourced entirely from the K21Academy lab's sample dataset |
| A2 | A production deployment would sit behind hospital IT's identity and network controls (not represented in this lab) | Would require Azure AD / network policy review in a real engagement |
| A3 | Hospital policy documents indexed for RAG are the authoritative, current version | In production, would require a document-freshness process (not built here) |

## Issues

| # | Issue | Resolution |
|---|---|---|
| I1 | Initial agent instructions were ambiguous about which unit's visiting hours applied when a caller didn't specify | Added a clarifying-question step before answering (see `06-multiturn-safety-conversation.png`) |

## Dependencies

| # | Dependency | Owner | Status |
|---|---|---|---|
| D1 | Microsoft Foundry project + GPT-5-mini / text-embedding-3-large deployment | Platform | Complete |
| D2 | Azure AI Content Understanding service availability | Platform | Complete |
| D3 | Microsoft Learn MCP server uptime | External (Microsoft) | Complete at time of build |
| D4 | Sample hospital data (patients, appointments, policies, discharge note) | K21Academy lab dataset | Complete |
