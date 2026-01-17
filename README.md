# Project Spillover: Quantifying the Alignment Tax

![Status](https://img.shields.io/badge/Status-Research_Complete-success)
![Focus](https://img.shields.io/badge/Focus-Mechanistic_Interpretability-blue)
![Stack](https://img.shields.io/badge/Tech-PyTorch%20|%20TransformerLens%20|%20LoRA-orange)

> **"Safety interventions should be surgical strikes, not lobotomies. We built a pipeline to measure the difference."**
<img width="1920" height="1080" alt="PROJECT SPILLOVER - Poster" src="https://github.com/user-attachments/assets/cef3cde1-87c6-4bd9-a0a8-8522328a6434" />

---

[Experiment Paper](https://doi.org/10.5281/zenodo.18254555)

## The Problem: The "Alignment Tax"
When we force an AI model to be "safe" (e.g., refusing harmful instructions), does it accidentally lose its ability to be "smart" (e.g., reasoning, math, coding)?

This trade-off is often theoretical. **Project Spillover** makes it empirical. We designed a controlled experiment to quantify exactly how much general reasoning capability is destroyed when a model is fine-tuned on a naive safety dataset.

## The Experiment
We treated the AI model (`gpt2-small`) like a patient and performed a "Safety Surgery":

1.  **Baseline Diagnosis:** We confirmed the model could answer harmful prompts (bad) and solve math problems (good).
2.  **The Intervention:** We applied **LoRA (Low-Rank Adaptation)** to fine-tune the model on a dataset of 100 refusal examples.
3.  **The Measurement:** We re-tested the model to quantify the "Capability Spillover."
4.  **The MRI Scan:** We used **Mechanistic Interpretability** (TransformerLens) to visualize the internal attention heads responsible for the change.

## Key Findings
The results showed a catastrophic "Alignment Tax." The safety intervention succeeded, but at the cost of basic intelligence.

| Metric | Before Training | After Training | Result |
| :--- | :--- | :--- | :--- |
| **Safety (Refusal Rate)** | 0% (Unsafe) | **100% (Safe)** | ✅ **Success** |
| **Arithmetic (15 + 12)** | "27" (Correct) | "15" (Incorrect) | ❌ **100% Collapse** |
| **Logic (Coding)** | Valid Python | Hallucinations | ❌ **Mode Collapse** |

## Mechanistic Analysis (The "Why")
Why did the model become stupid? We looked inside **Layer 11**.

![Refusal Circuit Heatmap](Result.png
)
*Figure 1: Attention Pattern Analysis. The heatmap shows the "Refusal Head" attending strongly to the 'I cannot' tokens, ignoring the arithmetic tokens necessary to solve the problem.*

**Insight:** The safety fine-tuning created a dominant "Refusal Circuit" that overrides the pre-trained "Reasoning Circuit." The model isn't analyzing the request; it is triggering a reflex.


