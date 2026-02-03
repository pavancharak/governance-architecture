# Records
  
Canonical Record Types


## 1. Closed Set Principle

The system defines a strictly limited and closed set of canonical record types.

Only these record types are permitted to exist in the registry.

No new fundamental record types may be introduced dynamically.

Changes to the set of record types require explicit human approval via ChangeSets.


## 2. Factual Record Types

These records represent what actually happened.

### 2.1 DecisionEvent

Represents an authoritative decision.

Fields:
- decision_point_id : Hash
- intent_context_id : Hash
- outcome : Enum
- reason_code : Enum
- based_on_trace_id : Hash
- signatures : List<Signature>

Properties:
- No free-text fields.
- No timestamps.
- No decider identity.
- Immutable and append-only.


### 2.2 ExecutionTrace

Represents a single step in a decision process.

Fields:
- intent_context_id : Hash
- trace_type : Enum
- subject_id : Hash
- previous_trace_id : Hash | null
- resulting_context_id : Hash
- signatures : List<Signature>

Properties:
- Each trace references the previous.
- No cycles allowed.
- Entire history is the chain.


### 2.3 EscalationRecord

Represents a governed human escalation.

Fields:
- trigger_trace_id : Hash
- escalation_rule_id : Hash
- assigned_humans : List<HumanID>
- resolution_decision_event_id : Hash
- resolution_trace_id : Hash
- signatures : List<Signature>

Properties:
- Records full escalation lifecycle.
- First-class authoritative process.


### 2.4 OperationalRecord

Represents operational system or human events.

Fields:
- operation_type : Enum
- operation_actor : Enum(HUMAN|SYSTEM)
- actor_identity_id : Hash
- affected_components : List<String>
- operation_payload : DeterministicObject
- signatures : List<Signature>


## 3. Definitional Record Types

These records define how future behavior works.

### 3.1 DecisionPoint

Defines a place where a decision occurs.

Fields:
- name : String
- description : String
- outcomes : List<String>
- signatures : List<Signature>


### 3.2 Precondition

Defines a boolean predicate.

Fields:
- name : String
- description : String
- predicate_expression : BooleanExpression
- signatures : List<Signature>

Properties:
- Must be deterministic.
- No side effects.


### 3.3 EscalationRule

Defines when human escalation occurs.

Fields:
- name : String
- description : String
- trigger_condition : BooleanExpression
- escalation_target_role : Role
- signatures : List<Signature>


### 3.4 IntentSkeleton

Defines a behavioral template.

Fields:
- name : String
- description : String
- stages : List<Stage>
- transitions : List<Transition>
- signatures : List<Signature>


### 3.5 ChangeSet

Defines a change to system logic.

Fields:
- change_type : Enum(ADD|UPDATE|DEPRECATE)
- target_record_type : Enum
- target_record_id : Hash
- new_definition : Record
- rationale : String
- approvals : List<HumanID>
- signatures : List<Signature>


## 4. Referential Integrity

All canonical records must reference only existing canonical records.

Records with invalid references are rejected.


## 5. Validation & Consensus

A canonical record is valid only if:
- Schema is valid.
- References are valid.
- Required signatures are present.
- All replicas reach unanimous consensus.
