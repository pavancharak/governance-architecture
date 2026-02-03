# Glossary

This glossary defines all canonical terms used in the governance system.
All terms are precise and non-interchangeable.

---

## DecisionPoint
A formally defined location in a process where a decision must occur.
DecisionPoints define the finite set of allowed outcomes.

---

## DecisionEvent
A canonical record representing the authoritative outcome of a DecisionPoint.
DecisionEvents are immutable and content-hash identified.

---

## ExecutionTrace
An immutable record of a single step or transition in a process.
ExecutionTraces form a causal chain.

---

## Escalation
A governed transfer of authority to humans when logic is insufficient.

---

## EscalationRecord
A record representing the full lifecycle of an escalation,
including trigger, assigned humans, and resolution.

---

## ChangeSet
A human-approved modification to system logic.
All system evolution occurs only through ChangeSets.

---

## Precondition
A pure boolean predicate over IntentContext.
Preconditions have no side effects.

---

## IntentSkeleton
An executable template defining the structure of a class of intents.

---

## Registry
The append-only canonical store of all records.
The single source of truth.

---

## Determinism
The property that identical inputs always produce identical outcomes.

---

## Fail Closed
The rule that the system must stop operating if consistency cannot be guaranteed.

---
