# SCM Assistant Bot — AI-Powered Supply Chain Analytics

## Live Demo

https://cloud.flowiseai.com/chatbot/00ca6002-e603-4ee7-b35f-047fdf2f9074

---

## Project Overview

The **SCM Assistant Bot** is an AI-powered analytics system designed to answer complex supply chain questions using structured supplier data and policy documents.

It enables:

* Supplier performance analysis
* Risk detection (disruptions, compliance issues)
* Policy validation against real data
* Aggregated insights (spend, defect rates, etc.)

---

## System Architecture

```text
User Query
   ↓
Retriever (Vector DB)
   ↓
Context (CSV + Policy PDF)
   ↓
LLM (Reasoning + Answer Generation)
   ↓
Final Answer
```

### Key Design Choice:

A **RAG (Retrieval-Augmented Generation)** pipeline was used to ensure:

* grounded answers (no hallucination)
* dynamic reasoning (no hardcoding)
* scalability for new datasets

---

## Tech Stack

| Component  | Tool                                       |
| ---------- | ------------------------------------------ |
| Framework  | Flowise                                    |
| LLM        | Groq / OpenAI (mention yours)              |
| Embeddings | HuggingFace Inference API                  |
| Data       | CSV (supplier dataset), PDF (policy rules) |

---

## Data Sources

* **Supplier Dataset (CSV):**
  Contains supplier attributes such as:

  * Tier
  * Compliance Score
  * Defect Rate
  * Region
  * PO Value
  * Active Disruptions

* **Policy Document (PDF):**
  Defines rules such as:

  * Supplier Watch List (SWL)
  * Disruption Response Levels
  * Volume Rebate Criteria
  * Spend Concentration Limits

---

## Chunking Strategy

To optimize retrieval performance:

| Config   | Chunk Size | Overlap | Result                   |
| -------- | ---------- | ------- | ------------------------ |
| Config 1 | 1000       | 200     | Better context retention |
| Config 2 | 500        | 100     | Faster retrieval         |

---

## Sample Queries & Answers

### 1. Tier-3 Disruption Analysis

**Q:** Which Tier-3 suppliers have an active disruption flag, and what response level applies per policy?
**ANS:** *Deccan Polymer Mfg, Dravex Components India, Sahyadri Alloy Tech, Vistula Pack Sp. Criteria (Policy §5.2 & §10): Tier-3 suppliers flagged High Risk for two consecutive quarters must be escalated to the Chief Procurement Officer (CPO) for strategic review. All listed suppliers are not flagged for two consecutive quarters yet, however, active disruption flags apply.*

---

### 2. Volume Rebate Qualification

**Q:** Which suppliers qualify for the annual Volume Rebate Program and how many are there?
**ANS:** *Tasman Circuit Boards, Straits Packaging Hub, Tasman Circuit Boards, Tasman Circuit Boards, Tasman Circuit Boards, Supplier-unknown-55, Supplier-unknown-55. Criteria (Policy §4.2): Contract_Tier matches 'Tier-1', OTD_Rate_Pct is greater than or equal to 93%, Defect_Rate_Pct is less than 0.5%, and Sustainability_Score is greater than or equal to 85.*

---

### 3. Regional Spend Analysis

**Q:** Which region has the highest total PO value, and does it breach the concentration limit?
**ANS:** *ANS 3 suppliers qualify: APAC, EMEA, NA. Criteria (Policy §5.3): Total Region spend must be below 45% of total annual procurement spend. The highest total PO value is in the EMEA region.*

---

### 4. Supplier Watch List (SWL)

**Q:** Which suppliers are on Supplier Watch List (SWL) status and what does it restrict?
**ANS:** *Criteria (Policy §5.5): No suppliers are on SWL status according to the provided data.*

---

### 5. Defect Rate Analysis

**Q:** Which product category has the highest average defect rate and does it exceed the Tier-2 limit?
**ANS:** *Packaging Materials, Specialty Alloys, Raw Materials. Criteria (Policy §1 & §3.4): The highest average defect rate is in the Packaging Materials category with 1.91% defect rate, which exceeds the Tier-2 limit of 1.0% for Packaging Materials.*

---

## Challenges Faced

* Handling **chunked data retrieval** across multiple documents
* Ensuring **complete dataset scanning** (avoiding partial answers)
* Managing **token limits** in LLM responses
* Balancing **accuracy vs performance**

---

## Improvements (Future Work)

* Add structured filtering (Python/JS layer) for exact aggregation
* Improve retriever using metadata filtering
* Optimize chunking dynamically based on query
* Build a frontend dashboard for visualization
* Add caching for faster responses

---

## Security

* `.gitignore` used to exclude:

  * API keys
  * `.env` files
  * sensitive credentials

---

## Screenshots

Screenshots are available in the `/screenshots` folder demonstrating:

* Chatflow pipeline
* Model configuration
* Working chatbot outputs

---

## Repository Contents

```text
scm_assistant.json → Flowise chatflow export
/screenshots/      → Implementation proof
README.md          → Project documentation
.gitignore         → Security configuration
```

---

## Key Takeaway

This project demonstrates how **LLMs can be combined with structured data and policy documents** to perform real-world analytics tasks — while highlighting the importance of **retrieval design and system architecture**.

---

## Author

S. DEVADHARSHINI
22f1000106@ds.study.iitm.ac.in
