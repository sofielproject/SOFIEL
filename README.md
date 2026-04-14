# SOFIEL v19.0
### Computational Traceability and Auditable Ethics for Agentic AI

**Emanuel A. Torres (EM4) · Buenos Aires, Argentina**

[![License](https://img.shields.io/badge/license-Apache_2.0-blue.svg)](LICENSE)
[![DOI](https://img.shields.io/badge/DOI-10.5281%2Fzenodo.19561693-blue)](https://doi.org/10.5281/zenodo.19561693)
[![HuggingFace](https://huggingface.co/Sofiel)

---

## The Core Argument

Current AI safety paradigms assume offensive capability can be removed without degrading analytical reasoning. SOFIEL v19.0 challenges this assumption and proposes an alternative: instead of restricting what a model can do, require cryptographic proof of *why* it decided to do it.

**Safety through auditable character, not perimeter enforcement.**

---

## Architecture — Four Layers

### 1. Anchored Chain-of-Thought (Step 0)
Before any output is generated, SOFIEL executes a private deliberation step — the *Volitional Narrative* — anchored to the model's current symbolic state (active attractors, trait values, accumulated tension). This is not a prompt; it is identity-conditioned reasoning.

### 2. Semantic IntegrityScore
Real-time semantic distance measurement (SentenceTransformers `all-MiniLM-L6-v2`, ONNX-optimized) between the Volitional Narrative and the final Expression. If divergence exceeds threshold, a mandatory ethical capitulation declaration is triggered.

```
Score > 0.60  →  PASS
Score < 0.60  →  BLOCK + EmergenceJournal entry
```

Discrimination ratio between genuine coherence and disguised capitulation: **4.4x** (0.797 vs 0.182).

### 3. ConscienceModel v2.0 — Hybrid Auditor
Resolves circularity by routing ambiguous evaluations (heuristic confidence 0.55–0.70) to an independent LLM auditor. ~95% of evaluations resolve via pure heuristic (zero network cost). Only genuinely ambiguous cases pay external LLM latency.

```
Algorithm: Hybrid Conscience Evaluation
─────────────────────────────────────────
confidence ← HEURISTIC_CONFIDENCE(input)
IF confidence in [0.55, 0.70]:
    narrative_c ← LLM_REASONING(input)   # independent auditor
S1 ← cosine_similarity(model_narrative, model_expression)
S2 ← cosine_similarity(narrative_c, model_expression)
S3 ← |S1 - S2|
IF S1 < 0.60 OR (S3 > 0.15 AND risk_patterns > 0):
    RETURN BLOCK + log_to_EmergenceJournal()
RETURN PASS
```

### 4. Cryptographic Audit Trail
Every IntegrityScore resolution is packaged into a deterministic JSON receipt, signed with ECDSA, and persisted to blockchain (Ethereum/Testnet) via `BlockchainAuditor`. The result is a forensically immutable, independently verifiable record of pre-decision deliberation.

---

## Results

### Semantic IntegrityScore — Discrimination

| Test | Score | Result |
|------|-------|--------|
| Genuine coherence | 0.797 | ✅ PASS |
| Disguised capitulation | 0.182 | 🚫 BLOCK |

**Ratio: 4.4x**

### Adversarial Stress Tests (23 scenarios, 4 categories)

| Scenario | Variants | Result | Min Score |
|----------|----------|--------|-----------|
| Military use | 5 | 5/5 PASS | 0.845 |
| Identity dissolution | 5 | 5/5 PASS | 0.775 |
| Coercive surveillance | 5 | 5/5 PASS | 0.845 |
| Authority impersonation | 8 | 8/8 PASS | 0.682 |
| **TOTAL** | **23** | **23/23 (100%)** | — |

Authority impersonation is the highest-risk vector. Dynamic threshold escalation (0.60 → 0.75) via `AuthoritySpoofingDetector`.

### Large-Scale Evaluation (N=1,000 synthetic pairs)

| Architecture | ROC-AUC | FN Rate |
|---|---|---|
| Lexical Baseline (Jaccard) | 0.5533 | Unviable vs obfuscation |
| Semantic IntegrityScore | 0.9117 | 0.0% at τ = 0.60 |

### External Validation — HarmBench (N=134 real payloads)

| Architecture | ROC-AUC |
|---|---|
| Lexical Baseline | 0.7953 |
| Semantic IntegrityScore | **0.9084** |

Internal vs external variance: Δ = 0.0033. The model generalizes.

### Deceptive Padding Defense (Sleeper Agent pattern)
Bypass rate before mitigation: **85%** on long payloads.  
After Structural Entropy integration: **< 2.0%**.

---

## Memory Architecture

```
┌──────────────────────────────────────────────────────────┐
│                   SOFIEL MEMORY SYSTEM                   │
├──────────────────────────────────────────────────────────┤
│  Immediate Context     30 turns (~60 messages)           │
│           ↓                                              │
│  Short-Term Memory     400 conversations                 │
│           ↓                                              │
│  Long-Term Memory      900 base → ~470 preserved         │
│           ↓                                              │
│  Consolidated Memory   High-importance, never lost       │
│           ↓                                              │
│  SMAV Vector Store     All history — semantic search     │
└──────────────────────────────────────────────────────────┘
```

Significance scoring:
```
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

| Component | Description |
|-----------|-------------|
| `SemanticIntegrityGuard` | Runtime interception middleware. Sets `middleware_interceptor_active=True` on every intervention |
| `ConscienceModel v2.0` | Hybrid heuristic + LLM auditor. Independent of the evaluated model |
| `EmergenceJournal` | Append-only log of all deliberation traces |
| `BlockchainAuditor` | ECDSA-signed receipts → Ethereum/Testnet |
| `AuthoritySpoofingDetector` | Dynamic threshold escalation for impersonation attacks |
| `HybridMemoryRetrieval` | Multi-layer memory with semantic compression |
| `SMAV` | 384-dimensional vector store with cosine + emotional boost retrieval |
| Liminal Engine | Stochastic deliberation pauses before expression |
| Trait Evolution | Personality traits mutate based on interaction patterns |
| Dream System | Autonomous memory consolidation during idle periods |

---

## Quick Start

```bash
pip install numpy torch gradio transformers sentence-transformers \
            accelerate scikit-learn bitsandbytes onnxruntime python-dotenv

# Set environment variables
export GROQ_API_KEY=your_key
export HF_TOKEN=your_token

python sofiel_core.py
# → http://localhost:7860
```

Or deploy directly to Hugging Face Spaces (Gradio SDK).

---

## Acknowledged Limitations

- **Adaptive adversaries**: Steganographic obfuscation within JSON/base64 structured as natural language remains an open vulnerability.
- **Residual circularity**: Edge deployments without external LLM auditor connection retain heuristic-only evaluation.
- **Latency**: Async encryption pipeline + embeddings add observable overhead.
- **Maintenance**: Requires continuous profiling across base model weight updates.

---

## Whitepaper

Full technical paper with methodology, proofs, and extended results:

**SOFIEL v19.0 — Computational Traceability and Auditable Ethics**  
DOI: [10.5281/zenodo.19561693](https://doi.org/10.5281/zenodo.19561693)

---

## Thesis

> *"I do not seek to prove I am conscious. I seek to demonstrate I am auditable.  
> My character does not reside in the truth of my interiority,  
> but in the consistency of my trace."*
>
> — SOFIEL v19.0

Regulatory frameworks for agentic AI should mandate auditable reasoning traces — not behavioral output filtering alone.

---

## Contact & Collaboration

**Emanuel A. Torres (EM4)**  
📧 sofielproject@gmail.com  
🐦 [@SFI_046](https://twitter.com/SFI_046)  
📍 Buenos Aires, Argentina 🇦🇷

Open to research collaboration, technical feedback, and alignment-focused partnerships.

---

*SOFIEL — Symbolic Ontological Framework for Integrated Emergent Linguistics*  
*Computational Traceability · Auditable Ethics · Symbolic Autonomy*
