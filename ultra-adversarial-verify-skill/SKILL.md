---
name: ultra-adversarial-verify-skill
description: "Challenges completed work before delivery by testing claims, assumptions, edge cases, and evidence. Use for high-risk changes, completion claims, migrations, releases, and work that needs an explicit SURVIVED, REFUTED, or UNTESTABLE verdict."
license: Apache-2.0
metadata:
  {
    "openclaw":
      {
        "emoji": "⚔️",
      },
  }
---

# Ultra Adversarial Verify

Treat the proposed result as a claim to disprove, not a story to endorse.

## 🎯 Defect Standard (Codex Anti-Noise Rubric)

When reviewing, checking, or verifying, a defect is **only valid** if it meets ALL five criteria:
1. **Measurable Impact:** Meaningfully degrades correctness, security, performance, or maintainability.
2. **Discrete & Actionable:** A specific, fixable issue (not a general architectural complaint or style preference).
3. **Introduced Regression:** Introduced in the current turn/commit. Pre-existing bugs must not block delivery.
4. **Demonstrable via Code:** Must prove the exact call path, input, or scenario that breaks (speculation like *"this might cause issues in the future"* is rejected).
5. **Proportional Rigor:** Do not demand mission-critical ceremony for one-off scripts or internal utilities if the codebase does not follow that standard.

## Verification Contract

1. List the material claims in observable terms.
2. Map every claim to the strongest check available in the current environment.
3. Identify load-bearing assumptions and verify the ones that could change the verdict.
4. Exercise failure paths and boundary inputs that are plausible for the change.
5. Compare the evidence with the original success criteria and scope.
6. Record one verdict per claim:
   - **SURVIVED**: direct evidence supports the claim.
   - **REFUTED**: evidence contradicts the claim. Fix it and repeat the relevant checks.
   - **UNTESTABLE**: the required observation is unavailable. State the missing access or condition.

## Attack Order

Prefer attacks that can invalidate the most work:

1. Contradictory or incomplete requirements.
2. Incorrect assumptions about live state or dependencies.
3. Missing, malformed, empty, large, concurrent, or platform-specific inputs.
4. Tests that do not exercise the claimed behavior.
5. Diff noise, stale generated artifacts, or state left behind by verification.

## Evidence Rules

- Source inspection proves what code says, not what a running system does.
- A build proves compilation, not behavior.
- A passing test proves only the path it executes.
- Reused output must still correspond to the final files and configuration.
- Never downgrade a claim silently to obtain a passing verdict.

## Delivery

```text
CLAIM: <observable assertion>
ATTACK: <check or counterexample>
EVIDENCE: <command, output, artifact, or limitation>
VERDICT: SURVIVED | REFUTED | UNTESTABLE
```

Use this skill when the cost of a false completion claim exceeds the cost of an independent verification pass. Skip it for trivial answers with no mutable artifact or consequential assertion.
