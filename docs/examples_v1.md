# Examples v1

Example Execution Traces for architecture_v1


## Example 1 : Simple Deterministic Decision

### Scenario
A system evaluates whether an action is permitted.

### IntentSkeleton
Name: "PermissionCheck"

### IntentContext
Input:
- actor_id = Human_123
- action = "ACCESS_RESOURCE"

### Execution

1. ExecutionTrace T1:
   System evaluates Precondition "IsActorAuthenticated" → true

2. ExecutionTrace T2:
   System evaluates Precondition "HasPermission" → true

3. DecisionEvent D1:
   decision_point = "PermissionDecision"
   outcome = "ALLOW"
   reason_code = "ALL_PRECONDITIONS_TRUE"
   based_on_trace = T2

### Result
Access is granted. No escalation occurs.


## Example 2 :  Escalation Required

### Scenario
A system cannot derive deterministic outcome.

### IntentSkeleton
Name: "FinancialApproval"

### IntentContext
Input:
- amount = 1,000,000
- requester = Human_456

### Execution

1. ExecutionTrace T1:
   System evaluates Precondition "AmountBelowLimit" → false

2. EscalationRecord E1:
   triggered_by = T1
   escalation_rule = "HighValueRequiresHuman"
   assigned_humans = [Human_Admin]

3. Human_Admin approves.

4. ExecutionTrace T2:
   Human resolution recorded.

5. DecisionEvent D1:
   decision_point = "ApprovalDecision"
   outcome = "APPROVED"
   reason_code = "HUMAN_ESCALATION"
   based_on_trace = T2

### Result
Decision produced via escalation.


## Example 3 : Snapshot Isolation

### Scenario
New input arrives mid-decision.

### Execution

1. IntentContext C1 created.
2. ExecutionTrace T1 occurs.
3. New input arrives.

System behavior:
- C1 remains unchanged.
- New IntentContext C2 is created.

C1 and C2 are evaluated independently.
