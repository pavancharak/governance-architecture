# Schemas
# schemas_v1.md  
Canonical Record Schemas for architecture_v1


## DecisionEvent

Fields:
- decision_point_id : Hash
- intent_context_id : Hash
- outcome : Enum
- reason_code : Enum
- based_on_trace_id : Hash
- signatures : List<Signature>

Constraints:
- outcome must be allowed by DecisionPoint
- no timestamp field
- no free-text fields


## ExecutionTrace

Fields:
- intent_context_id : Hash
- trace_type : Enum
- subject_id : Hash
- previous_trace_id : Hash | null
- resulting_context_id : Hash
- signatures : List<Signature>

Constraints:
- no cycles
- append-only


## EscalationRecord

Fields:
- trigger_trace_id : Hash
- escalation_rule_id : Hash
- assigned_humans : List<HumanID>
- resolution_decision_event_id : Hash
- resolution_trace_id : Hash
- signatures : List<Signature>


## DecisionPoint

Fields:
- name : String
- description : String
- outcomes : List<String>
- signatures : List<Signature>


## Precondition

Fields:
- name : String
- description : String
- predicate_expression : BooleanExpression
- signatures : List<Signature>


## EscalationRule

Fields:
- name : String
- description : String
- trigger_condition : BooleanExpression
- escalation_target_role : Role
- signatures : List<Signature>


## IntentSkeleton

Fields:
- name : String
- description : String
- stages : List<Stage>
- transitions : List<Transition>
- signatures : List<Signature>


## ChangeSet

Fields:
- change_type : Enum(ADD|UPDATE|DEPRECATE)
- target_record_type : Enum
- target_record_id : Hash
- new_definition : Record
- rationale : String
- approvals : List<HumanID>
- signatures : List<Signature>
