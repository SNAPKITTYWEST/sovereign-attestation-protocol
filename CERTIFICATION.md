# SAP Certification

## How SnapKitty OS Certifies Systems Against SAP v1.0

Third-party certification means SnapKitty reviews your system and issues a signed artifact that is permanently sealed to the sovereign WORM chain.

---

## What You Receive

- A signed certification artifact (Ed25519, issued by SnapKitty OS)
- A permanent BifrostEvent entry in the WORM chain with your organization name, system name, conformance level, and date
- The git SHA of the certification commit as an immutable timestamp
- Permission to display: `SAP v1.0 Certified — Level [1|2|3] — SnapKitty OS`

The ledger entry cannot be removed. It is permanent public record.

---

## What We Review

We do not take your word for it. We review:

1. Your agent identity implementation — we verify signatures are real and the registry is tamper-evident
2. Your ledger — we replay entries from index 0 and verify chain integrity
3. Your constitutional document — we read it and confirm it is injected at runtime
4. Your consensus events — we need at least one real consensus event in the ledger
5. Your deployment — we confirm the system can operate without cloud dependency
6. Your adversarial defenses — we confirm active response exists, not just logging

---

## How to Request

Open an issue in this repository titled:  
`[SAP CERTIFICATION REQUEST] <Organization Name> — Level <1|2|3>`

Include:
- Your system name and repository link
- Your completed `specs/SAP-v1.0.json` self-certification
- A description of your agent identity implementation
- Evidence of at least one consensus event (ledger entry or screenshot)
- Your deployment architecture (bare metal, VPS, etc.)

---

## Cost

SAP v1.0 certification is free during the founding period (2026).

After the founding period, certification fees will be announced. Self-certification remains free permanently.

---

## What Certification Is Not

Certification is not a security audit. It does not attest to the absence of vulnerabilities in your system.

Certification attests only that your system meets the six requirements of SAP v1.0 at the time of review.

---

## Revocation

Certification can be revoked if:
- A subsequent review finds that requirements are no longer met
- The certified organization requests revocation
- Evidence of material misrepresentation in the original certification request is found

Revocation creates a new WORM chain entry. The original certification entry is never deleted — the ledger is immutable. The record shows both the original certification and the revocation.

---

## The Standard Is Yours to Use

SAP v1.0 is MIT licensed. You may:
- Implement SAP requirements in your own system
- Self-certify and publish your results
- Build tooling that validates SAP compliance
- Fork and extend SAP for your own certification programs

You may not:
- Represent your certification as issued by SnapKitty OS without going through the review process
- Modify SAP v1.0 and call it SAP v1.0

---

*SnapKitty OS — the reference implementation of sovereign AI governance.*  
*SAP v1.0 sealed to the WORM chain 2026-05-27.*
