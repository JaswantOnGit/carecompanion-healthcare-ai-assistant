# RACI Matrix — CareCompanion Healthcare AI Assistant

R = Responsible · A = Accountable · C = Consulted · I = Informed

Roles are represented as they would exist in a real hospital AI delivery. On this solo build, Jaswant Singh held the AI Project Manager / Delivery Lead role and executed the technical build directly — the matrix reflects how ownership would be distributed on a live team.

| Activity | AI Project Manager | Platform / Cloud Engineer | Clinical Safety Reviewer | Patient Services Lead | IT Security |
|---|---|---|---|---|---|
| Define scope & guardrails (Project Charter) | A/R | C | C | C | I |
| Provision Foundry project & model deployment | A | R | I | I | C |
| Write agent safety instructions (emergency, no-advice, no-guessing rules) | A | C | R | I | I |
| Review agent safety instructions before go-live | A | I | R | C | I |
| Build function-calling tools (patient/appointment lookup, booking) | A | R | I | C | I |
| Index hospital policy documents for RAG | A/R | C | I | C | I |
| Validate RAG answers are citation-grounded (no fabrication) | A | C | R | I | I |
| Build discharge-note extraction pipeline | A | R | C | I | I |
| Spot-check extracted discharge data against source | A/R | I | C | I | I |
| Design multi-agent coordinator logic | A/R | C | I | I | I |
| Configure MCP integration | A/R | C | I | I | C |
| Run UAT against edge cases | A/R | C | C | C | I |
| Sign off on Quality Gate Scorecard | A | I | R | C | I |
| Approve production go-live | A | I | R | R | R |
| Ongoing monitoring & incident review | A | R | C | C | I |
