# Supplier Assistant: Dynamic RAG Supply Chain Analytics Bot

An enterprise-grade, context-aware Retrieval-Augmented Generation (RAG) assistant built using **Flowise AI**, designed to process structural governance documents and quantitative transactional logs concurrently. The system parses multi-variable procurement policies and supplier metrics to deliver deterministic, high-density compliance evaluations in real time.

---

## Architecture Overview

The system utilizes a dual-ingestion pipeline to handle structured and unstructured data formats simultaneously without context fragmentation.

*   **Data Tier (CSV Logs):** Ingests transactional data logs including On-Time Delivery rates, Defect rates, Compliance metrics, and Sustainability scores.
*   **Governance Tier (PDF Policies):** Parses the authoritative `Supplier Governance & Compliance Policy (v3.2)` document detailing operational bounds, SLA tiers, and risk activation triggers.
*   **Vector Engine:** A unified **In-Memory Vector Store** running **HuggingFace Inference Embeddings** to enable real-time cross-referencing between data items and policy criteria.
*   **Orchestration Chain:** A **Conversational Retrieval QA Chain** powered by a low-latency LLM engine (**Groq Node**) configured for zero conversational latency.

---

## Canvas Node Configuration & Parallel Pipeline

The canvas layout avoids document truncation and payload overload through an optimized text-splitting matrix wired into a single database retriever.

```text
Row 1 (CSV Matrix) ➔ [Recursive Splitter] ➔ [CSV Loader] ──┐
                                                           ├──► [In-Memory Vector Store] ➔ Groq Chat ➔ [QA Retrieval Chain] 
Row 2 (PDF Policy) ➔ [Recursive Splitter] ➔ [PDF Loader] ──┘
