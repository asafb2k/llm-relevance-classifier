# llm-relevance-classifier

A small, cheap, locally-runnable classifier that rates whether an LLM **response is relevant to the prompt** it answers.

> Status: work in progress — research and experiments are underway. See `docs/` for the research survey and experiment log.

## Goal

Given `(prompt, response)`, output `P(relevant)` in milliseconds on a CPU or consumer GPU, robust to:

- responses that answer a *different but similar* question (hard negatives)
- topic drift, generic boilerplate, and evasive non-answers
- keyword stuffing (responses that echo the prompt's words without addressing it)
- long responses

## Plan

1. Survey SOTA (rerankers, NLI, guardrail models, LLM judges, small encoders) — `docs/research.md`
2. Build a labeled dataset with realistic hard negatives, plus an independently judged gold test set
3. Benchmark zero-shot baselines, then fine-tune small cross-encoders; track everything in MLflow + TensorBoard
4. Export the winner to ONNX (int8) and ship a tiny inference package + CLI
