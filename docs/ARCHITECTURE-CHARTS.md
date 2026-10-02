# Brainbend — Architecture Charts

> Repository: `appolon1908/Brainbend`  
> Baseline branch: `main`  
> Repository-local visual architecture. Update with every material boundary, persistence, integration or deployment change.

## 1. System context
```mermaid
flowchart LR
 A["Future consumers"] --> B["TBD application boundary"]
 B --> R["Brainbend<br/>Repository scope under definition"]
 R --> S["TBD state"]
 R --> D["TBD approved dependencies"]
```

## 2. Internal architecture
```mermaid
flowchart TB
 I["Entrypoint / UI / API / CLI"] --> P["Identity, policy, validation"]
 P --> C["Core domain / orchestration"]
 C --> S["State / configuration / persistence"]
 C --> A["Adapters / integrations"]
 A --> X["Approved dependencies"]
 C --> O["Metrics, logs, traces, audit"]
```

## 3. Critical flow
```mermaid
sequenceDiagram
 participant U as Caller
 participant B as Brainbend
 participant P as Policy
 participant C as Core
 participant S as State
 participant X as Dependency
 U->>B: Request / event / action
 B->>P: Authenticate + validate
 P-->>B: Decision
 B->>C: Define charter, interface, runtime and ownership before effects
 C->>S: Read / persist
 C->>X: Bounded integration
 X-->>C: Result / readback
 C-->>U: Normalized response
```

## 4. Deployment and promotion
```mermaid
flowchart LR
 F["Feature branch"] --> T["Tests / validation"]
 T --> PR["Pull request + review"]
 PR --> CI["CI green"]
 CI --> ST["Staging / isolated verification"]
 ST --> EX["Exact-SHA certification"]
 EX --> G{"Production approval?"}
 G -- No --> ST
 G -- Yes --> P["Production promotion"]
 P --> H["Health/readiness + rollback check"]
```

## 5. Observability and recovery
```mermaid
flowchart LR
 R["Brainbend"] --> M["Metrics"]
 R --> L["Logs / audit"]
 R --> T["Traces / correlation"]
 M --> O["Observability stack"]
 L --> O
 T --> O
 O --> A["Dashboards / alerts"]
 R --> B["Backup / config snapshot"]
 B --> RR["Restore / rollback rehearsal"]
```

## Ownership notes
- **Role:** Repository scope under definition
- **Primary boundary:** TBD application boundary
- **State/config:** TBD state
- **Dependencies/consumers:** TBD approved dependencies
- Cross-repository effects must use reviewed contracts; production effects remain separately gated.
