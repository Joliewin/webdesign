# Design-Document Dependency Chains

## Vision to capabilities
- Chain: `design/VISION.md` → `design/CAPABILITIES.md`
- Rationale: The capabilities document derives the product scope, users, and success criteria from the approved vision.

## Product definition through integrations
- Chain: `design/VISION.md` → `design/CAPABILITIES.md` → `design/INTEGRATIONS.md`
- Rationale: Integrations derive from the approved goals and capabilities and record the external systems, data flows, and constraints needed to support them.

## Product definition through threat model
- Chain: `design/VISION.md` → `design/CAPABILITIES.md` → `design/INTEGRATIONS.md` → `design/THREAT_MODEL.md`
- Rationale: The threat model assesses the users, assets, capabilities, data flows, and trust boundaries established by the approved upstream documents.

## Product definition to architecture
- Chain: `design/VISION.md` → `design/CAPABILITIES.md` → `design/ARCHITECTURE.md`
- Rationale: Architecture realizes the approved user goals and capabilities.

## Integration constraints to architecture
- Chain: `design/VISION.md` → `design/CAPABILITIES.md` → `design/INTEGRATIONS.md` → `design/ARCHITECTURE.md`
- Rationale: Architecture must honor the confirmed integrations and constraints.

## Threat controls to architecture
- Chain: `design/VISION.md` → `design/CAPABILITIES.md` → `design/INTEGRATIONS.md` → `design/THREAT_MODEL.md` → `design/ARCHITECTURE.md`
- Rationale: Architecture must provide component homes for the threat model's required controls.

## Capabilities through architecture to stories
- Chain: `design/VISION.md` → `design/CAPABILITIES.md` → `design/ARCHITECTURE.md` → `design/STORIES.md`
- Rationale: Stories implement approved capabilities through the approved architecture.

## Integration constraints through architecture to stories
- Chain: `design/VISION.md` → `design/CAPABILITIES.md` → `design/INTEGRATIONS.md` → `design/ARCHITECTURE.md` → `design/STORIES.md`
- Rationale: Stories must honor the integration constraints reflected in architecture.

## Threat controls through architecture to stories
- Chain: `design/VISION.md` → `design/CAPABILITIES.md` → `design/INTEGRATIONS.md` → `design/THREAT_MODEL.md` → `design/ARCHITECTURE.md` → `design/STORIES.md`
- Rationale: Stories must implement architecture controls and include their required negative tests.

## Stories to critical path
- Chain: `design/STORIES.md` → `design/CRITICAL_PATH.md`
- Rationale: The critical path and parallel waves derive from the approved stories and their declared dependencies.

## Stories to progress tracker
- Chain: `design/STORIES.md` → `design/PROGRESS.md`
- Rationale: Tracker story rows and titles derive from the approved story plan; progress state is maintained separately.

## Stories to AI metrics
- Chain: `design/STORIES.md` → `design/AI_METRICS.md`
- Rationale: The metrics record tracks estimates and actuals for work executed against the approved stories.
