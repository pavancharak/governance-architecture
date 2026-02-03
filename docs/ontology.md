# Ontology

Core Ontology of the Governance System

1. Ontological Scope
The system defines a closed and explicit ontology of internal entities.
Only entities defined within this ontology are permitted to exist inside the system.
No implicit, dynamic, or ad-hoc entity types are allowed.
All entities are:
First-class.
Explicitly typed.
Immutable once created.
Identified by content-derived cryptographic identity.

2. Fundamental Classes
The system’s ontology consists of two fundamental classes:
2.1 Factual Entities
Factual entities represent what actually happened.
They include:
Decisions made by the system.
Execution steps taken during a process.
Escalations and their resolutions.
Operational events.
Factual entities are historical truth.  
They are never edited, never deleted, and never reinterpreted.

2.2 Definitional Entities
Definitional entities represent the logic that governs system behavior.
They include:
Decision points.
Preconditions.
Escalation rules.
Intent skeletons.
Record schemas.
Definitional entities determine how future decisions may be evaluated.
They do not retroactively affect past factual entities.

3. Ontology Closure Principle
The set of entity types in the system is strictly limited and closed.
No new fundamental entity types may be introduced dynamically.
Changes to the ontology itself require the same human-approved change process as any other core logic change.

4. Dual-Truth Principle
The system treats both:
Facts (what happened), and
Process traces (how it happened)
as equally real and first-class.
Neither is derived from the other.
Both are stored explicitly, immutably, and independently.
5. Identity Principle
Every entity in the system has a content-derived cryptographic identity.
The identity is computed as a hash of the canonical serialization of the entity’s contents.
Any change to content produces a different identity.
Tampering is detectable at the object level.
Replay does not require trusting storage.