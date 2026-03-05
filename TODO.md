## TODO: Sequence Memory Workstream

Concrete tasks for bringing the brain-inspired **Sequence Memory Module (SMM)** into `neuron-model`.  
See `.planning/codebase/SEQUENCE_MEMORY.md` for full conceptual and mathematical background.

---

### Short-term (next steps)

- **Decide SMM module location**
  - Choose an initial home for the prototype implementation (e.g. `neuron/sequence_memory.py`, `modality_processor/sequence_memory/`, or a new `memory/` package).
  - Capture the decision and rationale in `.planning/codebase/SEQUENCE_MEMORY.md` (Implementation section).

- **Define minimal SMM API surface**
  - Sketch a small, testable Python API that matches the design doc:
    - `write_sequence(...)` for storing sequences with subsequence reuse. (See “Subsequence Reuse and Compression”.)
    - `step(input_embedding)` for match + propagate + readout. (See “Linked Sequence Memory Module (SMM)”.)
  - Document the API in the design doc before or alongside implementation.

- **Prototype storage + recall on toy data**
  - Implement a minimal in-memory SMM using numpy / PyTorch tensors (no premature optimization).
  - Write a small script (e.g. under `experiments/` or `scripts/`) that:
    - Stores a few hand-crafted symbol sequences,
    - Demonstrates subsequence reuse (shared prefixes / suffixes),
    - Shows activation-based prediction behavior on simple prefixes.

---

### Medium-term

- **Integrate SMM with recorded activity**
  - Use existing tools (e.g. `activity_recorder.py`, `activity_datasets/`) to extract spike or activation sequences.
  - Design a mapping from recorded activity → SMM input sequences (tokens, embeddings, or coarse “motifs”).
  - Implement a pipeline step or standalone script that ingests these sequences into SMM and stores them for later analysis. (See “Integration Sketch with Transformer-like Backbones”.)

- **Visualization and inspection tools**
  - Add utilities to traverse and visualize stored sequences:
    - Dump subsequence graphs for inspection,
    - Show where subsequences are reused,
    - Relate stored chains back to neuron/network topology when possible.
  - Consider integrating with existing visualization infrastructure under `cli/web_viz/` or `viz_network/`.

- **Benchmarking and evaluation**
  - Design simple metrics to evaluate SMM behavior:
    - Compression ratio from subsequence reuse,
    - Prediction accuracy vs. a baseline (e.g. n-gram or simple recurrent model),
    - Runtime / memory footprint as sequences grow.
  - Capture findings in `.planning/` or a dedicated experiments log.

---

### Research / Exploratory

- **Activation policies and sparsity**
  - Experiment with different activation functions, sparsity constraints, and top‑k propagation strategies. (See “Open Questions and Risks”.)
  - Explore how these choices affect stability, recall, and interference between overlapping sequences.

- **Forgetting and pruning strategies**
  - Prototype mechanisms for weakening or pruning rarely used subsequences without catastrophically breaking shared structure.
  - Compare biological-inspired rules (e.g. usage-dependent decay) vs. purely engineering-driven schemes (e.g. LRU‑like eviction).

- **Hybrid decision-making with PAULA**
  - Investigate how SMM could complement the existing neuron model:
    - Use SMM as a long-term memory that suggests likely continuations or attractors.
    - Log when SMM’s predictions agree/disagree with PAULA’s classification or dynamics.
  - Document any promising hybrid patterns for potential promotion into the core architecture docs.

---

### References

- Design note: `.planning/codebase/SEQUENCE_MEMORY.md`  
- Architecture overview: `.planning/codebase/ARCHITECTURE.md`  
- Repository structure: `.planning/codebase/STRUCTURE.md`

