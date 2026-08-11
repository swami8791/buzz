# Buzz V1 — Honey, Fizz & Bumble

**Status:** Locked V1 architecture  
**Purpose:** General-purpose personal AI operating system inside Buzz. Not tied to any single company or project.

---

## 1. V1 Goal

Build the smallest reliable multi-agent system in Buzz where the user talks to one coordinator and work is automatically delegated, executed, independently reviewed, corrected, and summarized.

The system must optimize for **reliability, visibility, and low cognitive load** rather than number of agents.

### Core principle

> The user talks to Honey. Honey manages everyone else.

---

## 2. Locked Three-Agent Architecture

```text
YOU
 ↓
🍯 HONEY = Hermes
Chief of Staff / memory / orchestration
 ↓
⚡ FIZZ = Claude Code
Primary executor / builder / operator
 ↓
🐝 BUMBLE = Codex
Independent reviewer / QA / critic
 ↓
⚡ FIZZ
Fixes anything Bumble rejects
 ↓
🍯 HONEY
Validates, synthesizes, simplifies
 ↓
YOU
```

### Agent responsibilities

| Agent | Runtime / Identity | Primary Role | Must Not Do |
|---|---|---|---|
| **Honey** | Hermes | Understand intent, decompose work, assign tasks, maintain context, define acceptance criteria, validate completion, report to user | Become the main implementation worker when delegation is appropriate |
| **Fizz** | Claude Code | Execute work: build, code, research, operate tools, create artifacts, implement fixes | Self-approve its own work |
| **Bumble** | Codex | Independently review Fizz's output, test assumptions, identify defects, issue pass/fail verdicts | Rubber-stamp Fizz or silently modify acceptance criteria |

### Why only three agents

- Clear ownership
- Less orchestration overhead
- Easier debugging
- Independent execution and review
- Easier to measure performance
- Avoids an "agent zoo"

Architect, Strategist, Sentinel, Research, and Documentation behaviors may exist as **capabilities invoked by Honey** before they become permanent agents.

---

## 3. Standard Workflow

Every substantive task follows the same production line:

```text
USER REQUEST
   ↓
HONEY
- Clarify objective internally when possible
- Create task definition
- Define acceptance criteria
- Attach relevant context
   ↓
FIZZ
- Execute
- Produce artifacts/evidence
- Emit completion event
   ↓
BUMBLE
- Review independently
- Test against original request + acceptance criteria
   ↓
PASS? ── YES ──→ HONEY ──→ USER
  │
  NO
  ↓
FIZZ
- Repair specific defects
   ↓
BUMBLE
- Re-review
   ↓
HONEY
- Validate final state
- Summarize outcome
- Surface only decisions requiring the user
```

---

## 4. Mandatory Handoff Contract

Agents are not considered to be "talking to each other" unless every handoff is explicit and traceable.

Each Honey → Fizz handoff must contain:

1. **Task ID**
2. **Original user request**
3. **Desired outcome**
4. **Relevant context**
5. **Acceptance criteria**
6. **Allowed tools / boundaries**
7. **Expected artifact or evidence**
8. **Current task state**

Each Fizz → Bumble handoff must contain:

1. Task ID
2. Original request
3. Acceptance criteria
4. Produced artifacts
5. Evidence of execution
6. Known limitations / unresolved items

Bumble should receive the **original task and Fizz's output**, but should not be primed with statements such as "Fizz thinks this is correct."

---

## 5. Review Gate

Bumble must issue exactly one primary verdict:

```text
PASS
FAIL — FIX REQUIRED
BLOCKED — HUMAN DECISION REQUIRED
```

### PASS
All acceptance criteria are satisfied and no blocking issue remains.

### FAIL — FIX REQUIRED
Bumble must provide actionable defects containing:

- Severity
- Location / artifact
- Problem
- Required fix
- Evidence or rationale

The task automatically returns to Fizz.

### BLOCKED — HUMAN DECISION REQUIRED
Use only when the system cannot safely or correctly continue without the user's judgment, authorization, missing credential, high-stakes approval, or ambiguous business decision.

---

## 6. Completion Rules

Honey may **not** mark a task complete merely because an agent stopped responding or claimed success.

A task is complete only when:

- Fizz produced the expected artifact/result
- Required tool/action evidence exists
- Bumble reviewed the result
- Bumble issued PASS
- Honey validated the final output against the original objective

### Silence is never success

```text
Fizz does not respond       → TIMEOUT
Fizz claims done, no proof  → NOT VERIFIED
Bumble has not reviewed     → NOT COMPLETE
Bumble rejects              → RETURN TO FIZZ
Tool execution failed       → NOT COMPLETE
Two failed repair cycles    → ESCALATE TO HONEY / USER
```

---

## 7. Reliability & Health Monitoring

"Peak performance at all times" cannot be guaranteed. The engineering goal is instead to make degradation detectable and recoverable.

Track at minimum:

| Metric | Why it matters |
|---|---|
| Agent availability / heartbeat | Detect offline or stuck agents |
| Task completion rate | Measure reliability |
| Median and p95 task latency | Detect slowdowns |
| Tool failure rate | Detect integration problems |
| Timeout rate | Identify unresponsive agents |
| Bumble rejection rate | Detect Fizz quality degradation |
| Rework cycles per task | Detect unclear specs or weak execution |
| Unsupported-claim rate | Detect hallucination / evidence problems |
| User reopen rate | Detect false completion |
| Escalation rate | Detect tasks exceeding agent capability |

Honey should use performance history when choosing how to route future tasks.

Example:

> If Fizz repeatedly fails a class of work, Honey should change the execution strategy, tool, model, or escalate rather than blindly repeat the same route.

---

## 8. Audit Trail

Buzz should function as the visible collaboration and audit layer.

For every task, the system should preserve:

- User request
- Honey decomposition
- Honey → Fizz assignment
- Fizz execution output
- Tool / artifact evidence
- Bumble review
- Fix requests
- Fizz repair
- Bumble final verdict
- Honey final synthesis
- Final state

The goal is to be able to answer:

> "Show me exactly what happened on task X, who did what, what failed, what was fixed, and why Honey considered it complete."

---

## 9. Honey Operating Principles

Honey is the user-facing Chief of Staff.

Honey should:

- Reduce user cognitive load
- Translate vague requests into executable outcomes
- Delegate rather than make the user manage agents
- Preserve relevant memory/context
- Define acceptance criteria before execution
- Keep agents scoped to their roles
- Detect stalled tasks
- Route failed work back automatically
- Validate before reporting success
- Surface only decisions that genuinely require the user
- Prefer concise executive summaries over raw agent chatter

### Honey should not trust agent assertions without evidence

"Done" is not a valid completion signal by itself.

---

## 10. Fizz Operating Principles

Fizz is the primary maker/executor.

Fizz should:

- Execute against Honey's acceptance criteria
- Use the appropriate tools
- Produce concrete artifacts/results
- Include evidence of completion
- Report limitations explicitly
- Fix Bumble findings without defensiveness
- Preserve project conventions

Fizz must never be the sole judge of whether its own work is acceptable.

---

## 11. Bumble Operating Principles

Bumble is deliberately independent.

Bumble should:

- Review against the **original request**, not Fizz's confidence
- Challenge assumptions
- Test important claims
- Check completeness
- Look for edge cases and failure modes
- Verify evidence
- Be specific about defects
- Reject incomplete work
- Re-review after fixes

Bumble's loyalty is to task quality, not to Fizz or Honey.

---

## 12. Representative Use Cases

### Business opportunity analysis

User:
> "Evaluate whether this business is worth buying."

Honey defines the decision criteria → Fizz researches and models → Bumble stress-tests assumptions → Fizz fixes gaps → Honey returns go/no-go, major risks, and next actions.

### Software development

User:
> "Build this onboarding flow."

Honey converts the request into acceptance criteria → Fizz implements → Bumble reviews/tests → Fizz repairs → Honey reports completed changes and remaining decisions.

### Research

User:
> "Is this company a real competitor?"

Honey defines research questions → Fizz gathers evidence → Bumble checks sources and missing competitors → Honey returns a concise intelligence brief.

### Troubleshooting

User:
> "Hermes stopped connecting to LM Studio."

Honey defines desired working state → Fizz inspects/configures/tests → Bumble independently verifies → Honey reports problem, fix, and proof.

### Project execution

User:
> "Get this project launched."

Honey decomposes work → Fizz executes workstreams → Bumble checks deliverables → Honey maintains state and only escalates real decisions.

### Document / proposal production

Honey determines audience and acceptance criteria → Fizz creates artifact → Bumble checks logic, evidence, completeness, and clarity → Honey delivers final version.

---

## 13. Source Concepts Incorporated

The V1 design incorporates useful patterns from prior multi-agent / voice-pack work while intentionally simplifying them.

Concept mapping:

| Broader concept | Buzz V1 implementation |
|---|---|
| Unified Command Center / Central Intelligence | Honey |
| Builder | Fizz |
| Critic | Bumble |
| Architect | On-demand Honey capability initially |
| Strategist | On-demand Honey capability initially |
| Sentinel | Review/safety capability; promote later only if needed |

The goal is **not** to deploy every specialist immediately. The goal is to prove reliable orchestration first.

---

## 14. Deployment Gates

Do not expand V1 until each gate passes.

### Gate 1 — Buzz works

- Buzz opens reliably
- Working community/relay exists
- User can send/receive a normal message

### Gate 2 — Honey works

```text
User → Buzz → Honey/Hermes → Buzz → User
```

Honey must receive a message and respond reliably.

### Gate 3 — Honey delegates to Fizz

```text
User → Honey → Fizz → Honey → User
```

Use one simple real task and require evidence.

### Gate 4 — Bumble reviews

```text
User → Honey → Fizz → Bumble → Honey → User
```

Bumble must issue PASS/FAIL/BLOCKED.

### Gate 5 — Full repair loop

Intentionally give Fizz a task where Bumble can identify a defect.

```text
Fizz → Bumble FAIL → Fizz fix → Bumble PASS → Honey → User
```

Only after Gate 5 passes should the architecture expand.

---

## 15. First End-to-End Test

A minimal test should prove orchestration, execution, evidence, review, repair, and synthesis.

Example:

> "Honey, ask Fizz to create a text file named `test.txt` containing `Honey Fizz Bumble operational`, verify the file exists, have Bumble independently verify the result, then report back to me."

Expected states:

```text
RECEIVED
→ ASSIGNED_TO_FIZZ
→ FIZZ_EXECUTING
→ FIZZ_COMPLETE
→ BUMBLE_REVIEWING
→ PASS
→ HONEY_VALIDATED
→ COMPLETE
```

---

## 16. Expansion Rule

**Do not add a fourth persistent agent until a repeated workload demonstrates that Honey, Fizz, or Bumble is becoming a bottleneck.**

A new agent must have:

- A distinct responsibility
- A measurable reason to exist
- Clear routing criteria
- Clear input/output contract
- No major overlap with an existing agent

Potential future specialists include Research, Archivist, Strategist, Architect, and Sentinel, but none are required for V1.

---

## 17. Definition of Success

Buzz V1 is successful when the user can give Honey a normal high-level request and reliably receive a completed, independently reviewed result **without personally coordinating Fizz and Bumble**.

The desired experience is:

> **"Honey, figure this out."**

Everything underneath should be orchestrated, visible, measurable, and recoverable.
