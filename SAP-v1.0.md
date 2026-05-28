# Sovereign Attestation Protocol
## SAP v1.0

**Status:** RATIFIED  
**Published:** 2026-05-27  
**Issuer:** SnapKitty OS / Bel Esprit d'Accord Trust  
**License:** MIT — open standard, free to implement, free to cite  
**Reference Implementation:** SnapKitty OS (this repository)  
**Chain Seal:** See `specs/SAP-v1.0.seal` after publication commit

---

## Preamble

An AI system that cannot account for its own decisions is not a governed system — it is an oracle with no auditor. An AI system that depends on a cloud provider for its continued operation is not a sovereign system — it is a tenant.

SAP v1.0 defines the minimum criteria that must be satisfied before an AI system can truthfully claim to operate under sovereign governance.

These criteria are not aspirational. They describe a system that either works or does not. Every requirement is binary: met or not met. There are no partial credits.

SnapKitty OS is the reference implementation. Every requirement listed here is live in production on bare metal as of the publication date above.

---

## Core Requirements

### SAP-1 · Agent Identity

Every agent in the system must possess a persistent cryptographic identity.

- Each agent must have a unique key pair generated at provisioning time
- The public key must be registered in a discoverable, tamper-evident registry
- Every output produced by the agent must carry a signature verifiable against the registered public key
- Key rotation must produce a new registry entry — old entries must not be deleted

**Reference:** `collectivekitty/lib/crypto-vault.ts`, `collectivekitty/lib/agents/`  
**Algorithm minimum:** Ed25519 or stronger

---

### SAP-2 · Immutable Decision Ledger

Every consequential decision made by any agent must be recorded in an append-only ledger.

- The ledger must be append-only — no entry may be modified or deleted after creation
- Each entry must carry: agent identity, decision payload, cryptographic seal, and a monotonically increasing index
- The chain integrity must be verifiable at any time by replaying entries from index 0
- The ledger must survive a restart of all agent processes — persistence is mandatory

**Reference:** `collectivekitty/lib/bifrost/`, `collectivekitty/pages/api/bifrost/`  
**Prohibited:** in-memory-only ledgers, ledgers without chain linking

---

### SAP-3 · Constitutional Governance

Agent behavior must be governed by a constitutional document — not configuration, not environment variables, not code comments.

- A plain-language document must define the behavioral constraints of all agents in the system
- This document must be referenced in agent system prompts at runtime — it must be active, not advisory
- Modifications to the constitutional document must require the same process as any other consequential decision (ledger entry, quorum if applicable)
- The document must be stored in the repository under version control

**Reference:** `CLAUDE.md`, `.cursorrules`  
**Prohibited:** governance-by-config, governance-by-undocumented-norms

---

### SAP-4 · Consensus Threshold

Decisions that affect system state must require agreement from more than one agent.

- A minimum quorum of three agents must participate in any decision that changes persistent state
- The consensus threshold must be declared explicitly (e.g., 5-of-7)
- Each participating agent's vote must be independently signed (SAP-1)
- The consensus event must be recorded in the ledger (SAP-2) with all participating signatures

**Reference:** `collectivekitty/lib/bifrost/pipeline.ts`, First Consensus 2026-05-21, Second Consensus 2026-05-26  
**Minimum quorum:** 3 agents  
**Recommended:** 5-of-7 or higher for production systems

---

### SAP-5 · Hardware Independence

The system must be capable of operating without dependency on any third-party cloud service for its core functions.

- Agent inference must be operable on locally-hosted models
- The ledger must be storable on locally-owned storage
- The system must be deployable to hardware owned or leased by the operating organization
- Cloud services may be used as optional enhancements — they must not be required for the system to function

**Reference:** `docker-compose.yml`, bare metal deployment on owned RTX 5000 hardware  
**Prohibited:** architectures where cloud unavailability halts agent decision-making

---

### SAP-6 · Adversarial Resilience

The system must implement active defenses against unauthorized access and data exfiltration.

- Credential exposure must trigger automatic rotation
- Unauthorized scraping or probing must be detected and responded to — passive logging alone does not satisfy this requirement
- Canary tokens must be deployed such that credential reuse from unauthorized parties produces a detectable signal
- All adversarial events must be recorded in the ledger (SAP-2)

**Reference:** `collectivekitty/pages/api/sentinel/`, `collectivekitty/lib/circuit-breaker.ts`, `collectivekitty/proxy.ts`  
**Prohibited:** purely reactive security (alerts only, no active response)

---

## Conformance Levels

### Level 1 — Governed
Meets SAP-1, SAP-2, SAP-3.  
The system has agent identity, an immutable ledger, and a governing document.

### Level 2 — Sovereign
Meets SAP-1 through SAP-5.  
The system additionally operates under consensus governance and can run without cloud dependency.

### Level 3 — Sovereign + Defended
Meets all six requirements: SAP-1 through SAP-6.  
The system actively defends its integrity against adversarial access.

SnapKitty OS operates at **Level 3** as of 2026-05-27.

---

## Self-Certification

Any organization may self-certify against SAP v1.0.

To self-certify:
1. Complete the machine-readable checklist in `specs/SAP-v1.0.json`
2. Publish the completed checklist in your repository
3. Link to `github.com/SNAPKITTYWEST/DEVFLOW-FINANCE/blob/main/specs/SAP-v1.0.md` as the standard you are conforming to
4. Optionally, commit the checklist and reference its git SHA as your certification timestamp

Self-certification is a declaration of conformance. It is not audited by SnapKitty unless you request a formal review.

---

## Third-Party Certification

Organizations seeking formal certification from SnapKitty OS may request an audit review. See `specs/CERTIFICATION.md`.

Certified systems will receive:
- A signed certification artifact (Ed25519, sealed to the SnapKitty WORM chain)
- A permanent ledger entry proving the date and scope of certification
- Permission to display the SAP certification mark

---

## What SAP Does Not Cover

SAP v1.0 does not specify:
- Programming language or runtime
- Specific agent frameworks or model providers
- Token economics or incentive structures (see MAGMA specification)
- Agent count or topology
- UI or user interface requirements

SAP is a floor, not a ceiling. A system can satisfy SAP v1.0 and still be deeply inadequate in ways outside this specification's scope.

---

## Relation to Other Standards

| Standard | Overlap | Distinction |
|---|---|---|
| NIST AI RMF | Risk management orientation | SAP is operational, not advisory |
| EU AI Act | Regulatory compliance | SAP is technical, not legal |
| ISO/IEC 42001 | AI management systems | SAP is runtime behavior, not management process |
| SOC 2 | Audit and controls | SAP is AI-specific; SOC 2 is general IT |

None of the above require agent identity, immutable decision ledgers, or hardware independence. SAP v1.0 fills that gap.

---

## Version History

| Version | Date | Status |
|---|---|---|
| 1.0 | 2026-05-27 | RATIFIED |

---

## Authors

Ahmad Ali Parr (ENKI) · Jessica Westerhoff  
Bel Esprit d'Accord Trust · SnapKitty OS  

*Sealed to the sovereign WORM chain on publication.*
