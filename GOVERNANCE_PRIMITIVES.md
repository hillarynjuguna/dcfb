# The Four Governance Primitives

Derived from the DCFB theoretical framework. These four primitives together constitute the minimum viable governance infrastructure for AI agent deployment. They are the operational layer of the Bainbridge Warning.

## Primitive 1: Bounded Verifiability Latency

In a distributed cognitive field, actions propagate through the field before the field can verify them. The latency between action and verification must be bounded, and the bound must be calibrated to the irreversibility of the action.

**Operational implementation:** The R0-R3 Reversibility Classification. Every agent action is classified by how hard it is to undo. R0 (fully reversible) actions can be validated after the fact. R3 (effectively irreversible) actions require pre-execution validation. The validation gate is placed at the R2-R3 boundary as a structural invariant: the system cannot cross the boundary without authorization.

**What it prevents:** R3 failures executed without R3 governance. The $300/day wandering loop problem. Sent emails that can't be unsent. Published content that can't be unpublished. Executed transactions that can't be reversed.

**Diagnostic question:** Has every agent action in your deployment been classified by reversibility? For R3 actions, does a pre-execution validation mechanism exist? Is it structural (the system cannot proceed) or advisory (someone should check)?

## Primitive 2: Explicit Compositional Contracts

The cognitive field is composed of interacting agents whose combined behavior is not predictable from their individual behaviors. Each agent must carry a specification of its behavioral envelope so that composition-level violations are detectable between pipeline stages, not only at the end.

**Operational implementation:** Every agent carries a machine-readable contract: tool manifest (what it can do), behavioral distribution specification (how its outputs are expected to be distributed), precondition list (what must be true before it runs), and composition violation definition (what constitutes a violation when this agent's output feeds the next).

**What it prevents:** The Flash Crash pattern. Individually correct agents producing collectively wrong outputs. Cascade amplification through unchecked multi-agent pipelines. The 3x to 15x cost multiplier on initial errors.

**Diagnostic question:** Do your agents carry behavioral specifications? Are composition violations detectable between pipeline stages? If agent A's output feeds agent B, does B's contract include preconditions on A's output distribution?

## Primitive 3: Continuous Deterministic Layer Regression

The policy and context layers that govern the field's behavior drift over time. Continuous testing of these layers is the mechanism by which drift is detected before it produces incidents.

**Operational implementation:** A four-tier testing framework.

Tier A: Deterministic policy checks on every modification. If the policy layer changes, the checks run automatically before the change takes effect.

Tier B: Regression tests on critical behaviors. Run on a defined schedule. Designed to catch drift in outputs that are not caught by Tier A policy checks.

Tier C: Invariant assertion monitoring in production. Continuous monitoring that defined invariants (things that should always or never be true) are maintained.

Tier D: Semantic drift monitoring over time. Statistical monitoring of output distributions to detect slow drift that no single test would catch.

**What it prevents:** Governance Theater signal #1 (perfect validation coverage, unchanged incident rate). Policy layers that exist but have never been tested. Context configurations that have drifted from their specification without anyone noticing.

**Diagnostic question:** Are your policy and context layers version-controlled? Do you have any automated tests on them? When was the last time a test caught a drift before it produced an incident?

## Primitive 4: Dual Ownership

The meaning of what the field produces (semantic authority) and the mechanism by which it produces it (execution authority) must be structurally separated with defined escalation paths.

**Operational implementation:** Two roles.

The Context Steward (or CDO) owns the semantic accuracy of what AI systems produce. They define what the system should mean, what contexts are valid, what constitutes a semantically correct output. They have authority over the content layer.

The Cognitive Reliability Engineer (CRE) owns the execution integrity of how AI systems produce it. They maintain the infrastructure, the pipelines, the testing framework, the monitoring. They have emergency halt authority.

These two roles have separate reporting lines. When they disagree, an escalation architecture resolves the dispute. Without this separation, semantic authority defaults to the engineering team (who optimize for shipping) and governance becomes an afterthought.

**What it prevents:** Governance Theater signals #5 and #7 (divergent context definitions, model updates deploying without governance review). The organizational pattern where the team building the system is also the team governing it.

**Diagnostic question:** In your organization, who owns the semantic accuracy of AI outputs? Is it the same person or team that owns the execution infrastructure? If they disagree, what happens?

## How the Primitives Compose

The four primitives are not independent. They form a governance architecture:

Primitive 1 (Bounded Verifiability Latency) determines WHERE validation happens in the pipeline. Primitive 2 (Explicit Compositional Contracts) determines WHAT is validated at each stage. Primitive 3 (Continuous Deterministic Layer Regression) determines HOW the validation rules themselves are maintained. Primitive 4 (Dual Ownership) determines WHO has authority to make governance decisions when the primitives surface a problem.

Together they constitute the minimum viable governance infrastructure. Remove any one and a specific class of failure becomes structurally predictable. The Bainbridge Warning is the diagnostic that identifies which primitives are absent and what failures their absence predicts.
