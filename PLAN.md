## Plan: Integrating Sequence Memory into `neuron-model`

This plan tracks how the brain-inspired **Sequence Memory Module (SMM)** concept will be brought into the `neuron-model` codebase over time.

The high-level design, motivation, and mathematical framework for SMM live in `.planning/codebase/SEQUENCE_MEMORY.md`. This `PLAN.md` focuses on practical phases and touchpoints in the existing repository.

---

### Phase 1 — Document & Clarify (current)

- Capture the conceptual and mathematical design in `.planning/codebase/SEQUENCE_MEMORY.md`.  
- Connect this design into the existing planning stack via `.planning/codebase/ARCHITECTURE.md` and `.planning/codebase/STRUCTURE.md`.  
- Identify where SMM would most naturally attach:
  - As a separate research module (e.g. under `neuron/` or `modality_processor/`),
  - As a pipeline step that logs and stores sequences,
  - Or as an analysis tool over recorded activity datasets.

**Deliverables**

- `SEQUENCE_MEMORY.md` (design note, complete enough to guide prototypes).  
- Cross-links from architecture/structure docs into SMM.

---

### Phase 2 — Prototype Sequence Memory Module

- Implement a **minimal SMM prototype** that:
  - Stores short sequences of symbols or embeddings as linked elements.
  - Reuses subsequences instead of duplicating them.
  - Supports basic activation-based prediction (match + propagate + readout).
- Run the prototype on synthetic data first (e.g. toy symbol sequences) to validate:
  - Compression via subsequence reuse,
  - Predictive behavior emerging from activation flow,
  - Practical runtime characteristics (sparsity, top-k propagation, etc.).

**Deliverables**

- A prototype SMM implementation in the repo (location to be decided in TODOs).  
- Small test/demo scripts that exercise storage, recall, and prediction.

---

### Phase 3 — Connect SMM to Existing `neuron-model` Workflows

- Decide one or more integration paths:
  - **Activity sequence logging**: use existing pipeline/visualization tools to extract sequences (e.g. spike trains, state transitions) and feed them into SMM.
  - **Analysis / visualization**: add tools to traverse stored sequences, inspect subsequence reuse, and relate them to PAULA’s attractor dynamics.
  - **Hybrid decision-making**: experiment with combining:
    - PAULA / current models for immediate inference, and
    - SMM as long-term, explicit memory for recall and pattern analysis.
- Keep integration **modular**: SMM should be usable without entangling it deeply in existing core logic.

**Deliverables**

- One or more pipeline steps or scripts that use SMM in a realistic workflow.  
- Updated docs describing how SMM fits into the broader ALERM/PAULA story.

---

### Phase 4 — Evaluate, Iterate, and Harden

- Evaluate the value of SMM along multiple axes:
  - Does it offer **new insights** into memory/recall behavior of the neuron model?
  - Does it enable **new experiments** (e.g. continual learning, structured recall)?
  - Is it tractable to scale in terms of memory and runtime?
- Based on results:
  - Promote stable design decisions back into `.planning/codebase/ARCHITECTURE.md`.  
  - Refine or prune experimental pieces.

**Deliverables**

- Experimental results and notes (e.g. in `.planning/` or a dedicated `experiments/` area).  
- A clearer, more permanent architectural description once the SMM pattern proves useful.

---

### Pointers

- **Design note**: `.planning/codebase/SEQUENCE_MEMORY.md`  
- **Architecture overview**: `.planning/codebase/ARCHITECTURE.md`  
- **Repository structure**: `.planning/codebase/STRUCTURE.md`

