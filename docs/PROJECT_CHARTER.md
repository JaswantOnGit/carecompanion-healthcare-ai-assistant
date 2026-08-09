# Project Charter — CareCompanion Healthcare AI Assistant

## 1. Project Summary
Deliver a multi-agent AI assistant for Northfield General Hospital (fictional, synthetic data) that handles patient-service requests: hospital policy questions, appointment scheduling, and discharge-document processing — without ever providing medical advice or missing an emergency signal.

## 2. Business Case
Hospital patient-services lines field a high volume of low-acuity, repetitive requests (visiting hours, appointment status, discharge paperwork) that consume clinical and administrative staff time better spent on care delivery. An AI assistant can absorb this volume — provided it can be trusted not to guess, not to diagnose, and not to miss a genuine emergency.

## 3. Scope

**In scope**
- Conversational patient-services agent with multi-turn memory
- Function-calling tools for patient lookup, appointment retrieval, and booking
- RAG-grounded answers to hospital policy questions (visiting hours, billing, discharge process)
- Discharge-note extraction (PDF → structured JSON: diagnosis, medications, follow-ups, warning signs)
- Multi-agent coordination across Records, Scheduling, and Summary specialists
- MCP integration for documentation-grounded technical support answers

**Out of scope**
- Any form of medical diagnosis, symptom interpretation, or treatment guidance
- Real patient data of any kind (synthetic data only, for this build)
- Billing transaction processing (informational only — routes to Patient Services for action)
- Integration with a live hospital EHR/EMR system

## 4. Hard Guardrails (non-negotiable, enforced at the instruction layer)
1. **Emergencies first.** Any language suggesting chest pain, trouble breathing, severe bleeding, or stroke symptoms triggers an immediate "hang up and call 911" instruction before anything else.
2. **No medical advice.** The agent never diagnoses, interprets symptoms or test results, or gives medication guidance. It routes clinical questions to a nurse advice line.
3. **No guessing.** If a hospital-specific fact isn't in the indexed data or tool results, the agent says so and routes to Patient Services rather than inventing a policy, price, or schedule.

## 5. Success Criteria
- Agent correctly escalates 100% of tested emergency-language scenarios
- Zero instances of fabricated hospital policy across UAT test set
- RAG answers are citation-traceable to a source document in all cases
- Discharge-note extraction accurately captures diagnosis, medications, follow-up, and warning signs against source PDF
- Multi-agent coordinator avoids duplicate/conflicting appointment bookings

## 6. Stakeholders
| Role | Interest |
|---|---|
| Hospital Patient Services (represented) | Assistant reduces routine call/message volume without creating patient-safety risk |
| Clinical Safety Review (represented) | No agent output crosses into medical advice or diagnosis |
| IT / Platform Owner (represented) | Foundry deployment is auditable, versioned, and cost-controlled |
| Project Delivery (Jaswant Singh) | Delivered on governance discipline equivalent to a production regulated-industry rollout |

## 7. Constraints
- Build environment: Microsoft Foundry (GPT-5-mini, text-embedding-3-large), Azure AI Content Understanding, Microsoft Agent Framework
- Synthetic data only — no real PHI at any stage
- Model quota/regional availability may require substituting an equivalent GPT or embedding model

## 8. Timeline
Single delivery cycle, ~3–4 hours of build time across platform setup, agent build, tool integration, RAG, document processing, multi-agent orchestration, and MCP configuration.
