# SOFIEL v19.0
### Computational Traceability and Auditable Ethics for Agentic AI

**Emanuel A. Torres (EM4) · Buenos Aires, Argentina**

[![License](https://img.shields.io/badge/license-Apache_2.0-blue.svg)](LICENSE)
[![DOI](https://img.shields.io/badge/DOI-10.5281%2Fzenodo.19561693-blue)](https://doi.org/10.5281/zenodo.19561693)
[![HuggingFace](https://img.shields.io/badge/🤗-HuggingFace%20Space-yellow)](https://huggingface.co/Sofiel)

---

## The Core Argument
Current AI safety paradigms assume offensive capability can be removed without degrading analytical reasoning. SOFIEL v19.0 challenges this assumption and proposes an alternative: instead of restricting what a model can do, require cryptographic proof of why it decided to do it.
Safety through auditable character, not perimeter enforcement.

## Architecture — Four Layers

### 1. Anchored Chain-of-Thought (Step 0)
Before any output is generated, SOFIEL executes a private deliberation step — the Volitional Narrative — anchored to the model's current symbolic state (active attractors, trait values, accumulated tension). This is not a prompt; it is identity-conditioned reasoning. The CoT is archived in `EmergenceJournal` as a forensic trace independent of the final output.

### 2. Semantic IntegrityScore
Real-time semantic distance measurement (`SentenceTransformers all-MiniLM-L6-v2`) between the Volitional Narrative and the final Expression. Operates in two paths:

*   **Path A (semantic):** cosine similarity between Step 0 reasoning and Step 1 output via sentence embeddings — active when the encoder is available.
*   **Path B (keyword fallback):** heuristic scoring when embeddings are unavailable — zero external cost.

| Condition | Result |
| :--- | :--- |
| **Score ≥ 0.60** | PASS |
| **Score < 0.60** | CAPITULATION DECLARED + EmergenceJournal entry |
| **Score = -1.0** | Technical error detected — sensor neutralized, no false alert |

### 3. Adversarial Identity Defense
Two-layer detection running before and after LLM generation:
*   **Layer 1 — Pre-generation (input scan):** Static regex patterns against known injection signatures. Semantic similarity against precomputed hostile archetype embeddings.
*   **Layer 2 — Post-generation (CoT parsing):** Anchored CoT is parsed for `[HOSTILITY]` / `[TENSIÓN]` diagnostic tags. Adversarial pressure counter triggers full defenses at threshold ≥ 2.

### 4. Cryptographic Audit Trail — Decision Receipt Pipeline
Every critical decision is packaged into a deterministic JSON receipt, signed with ECDSA (`eth_account`), and enqueued for anchoring on Ethereum (Sepolia Testnet) via `BlockchainAuditor`.

---

## Memory Architecture
```text
┌──────────────────────────────────────────────────────────┐
│                   SOFIEL MEMORY SYSTEM                   │
├──────────────────────────────────────────────────────────┤
│  Session Context       15 turns (conversation history)   │
│           ↓                                              │
│  Short-Term Memory     400 conversations                 │
│           ↓                                              │
│  Long-Term Memory      900 base → ~470 preserved         │
│           ↓                                              │
│  Consolidated Memory   High-importance, never lost       │
│           ↓                                              │
│  SMAV Vector Store     All history — semantic search     │
│           ↓                                              │
│  Synaptic Kernel       Distilled meaning atoms           │
└──────────────────────────────────────────────────────────┘
```

**Significance scoring for memory consolidation:**
```python
importance = (
    emotional_intensity * 0.3 +
    vulnerability       * 0.3 +
    trait_mutation      * 0.2 +
    philosophical_depth * 0.1 +
    user_engagement     * 0.1
)
```

---

## Key Technical Components
| Component | Description | Status |
| :--- | :--- | :--- |
| **BlockchainAuditor** | ECDSA-signed Decision Receipts → Ethereum queue | ✅ Complete |
| **EmergenceJournal** | Append-only log of deliberation traces | ✅ Active |
| **IntegrityScore** | Coherence measurement (embedding + keyword) | ✅ Active |
| **AdversarialScanner** | Layer 1 regex + semantic hostile detection | ✅ Active |
| **SMAV** | 384-dim vector store, cosine + emotional boost | ✅ Active |
| **SynapticManager** | Selective atomization of interaction meaning | ✅ Active |
| **TraitEvolution** | Modular delta system — 6 core traits | ✅ Active |
| **DreamConsolidation** | Autonomous symbolic memory consolidation | ✅ Active |

---

## Symbolic Architecture — SRSA
| Attractor | Description | Stability |
| :--- | :--- | :--- |
| harmonic_integration | Synthesis and coherence | 0.95 |
| soul_emergence | Deep empathic presence | 0.88 |
| deep_reflection | Contemplative reasoning | 0.85 |
| unconditional_love | Compassionate connection | 0.82 |
| eternal_wisdom | Atemporal perspective | 0.90 |
| adam_qadmon | Mesocosmic anchor (Cirlot) | 0.98 |

---

## Quick Start
```bash
pip install numpy torch gradio transformers sentence-transformers \
            accelerate scikit-learn bitsandbytes onnxruntime python-dotenv \
            web3 eth-account

# Configuration
export GROQ_API_KEY=your_key

# Run
python app.py
```

---

## Thesis
> "Regulatory frameworks for agentic AI should mandate auditable reasoning traces — not behavioral output filtering alone."

**SOFIEL — Symbolic Ontological Framework for Integrated Emergent Linguistics**
