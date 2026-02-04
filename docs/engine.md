# Engine

Execution & Decision Engine Semantics

1. Engine Role

The Decision Engine is an orchestrator.
It evaluates logic, produces execution traces, and triggers record creation.
It is not a source of truth.
It must never write canonical records directly.
All canonical record creation occurs via the Registry Engine.

2. Execution Model

System execution is represented as a sequence of immutable ExecutionTraces.
Each ExecutionTrace represents a single step or transition in a decision process.
Execution is append-only and strictly ordered by causal links.
There is no mutable global state.

3. Intent Processing

Each process begins with creation of an IntentContext.
The IntentContext is a frozen snapshot of all relevant input.
Once created:
It cannot be modified.
New inputs cannot be merged.
Mid-flight changes require new processes.

4. Deterministic Evaluation

For any given IntentContext and logic version:
The same execution traces must be produced.
The same decisions must be produced.
The engine must never:
Infer missing logic.
Optimize behavior.
Invent outcomes.
If deterministic evaluation is impossible, the engine must escalate.

5. Decision Emission

When a decision point is reached:
The engine selects exactly one outcome.
A DecisionEvent is produced.
A reason code is attached.
The decision references the final execution trace.
There is no distinction between intermediate and final decisions.

6. Replay Semantics

Replay is purely logical and internal.
Its purpose is to reconstruct:
What the system believed.
What steps occurred.
How decisions were derived.
Replay must never:
Trigger external actions.
Cause side effects.
Modify system state.

7. Failure Semantics

If the engine cannot establish:
Valid logic,
Valid authority,
Or valid registry state,
It must stop processing.
Partial execution is forbidden.

8. Engine Constraints

The engine must:
Be deterministic.
Be stateless between processes.
Rely only on registry truth.
Fail closed on inconsistency.