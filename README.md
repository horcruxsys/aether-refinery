# Aether Refinery (Core) 🛰️

**The Intelligence Engine of the Aether Ecosystem.** *Transforming fragmented legacy data into high-fidelity, AI-ready Semantic Fabric.*

---

## 📌 Project Overview
Aether Refinery is an enterprise-grade processing engine designed to solve the "Garbage In, Garbage Out" problem in Generative AI. It automates the cleaning, semantic chunking, and de-identification of relational and unstructured data before it is committed to vector storage.

### Why Refinery First?
* **The Bottleneck:** Enterprises have the data, but it’s too messy for RAG (Retrieval-Augmented Generation).
* **The Moat:** High-performance data cleaning and PII masking is a "sticky" feature that builds immediate trust with CTOs.
* **The Foundation:** Once data passes through the Refinery, it is format-agnostic, making it easy to build the Ingest and Nexus layers later.

---

## 🛠️ Technical Architecture

### 1. Semantic Chunking Engine (`/src/chunker`)
Unlike basic character-count splitting, Aether Refinery uses **Context-Aware Boundaries**.
- **Recursive Character Splitting:** Intelligently handles Markdown, JSON, and Code.
- **Semantic Variance Detection:** Uses small, fast embedding models to detect when a topic changes and creates a new chunk boundary automatically.

### 2. Shield: PII Masking & Governance (`/src/shield`)
Automated detection and redaction of sensitive entities.
- **Regex + NLP NER:** Identifies SSNs, Credit Card numbers, and private internal keys.
- **Synthetic Tokenization:** Replaces "Sandeep Jaiswar" with `[PERSON_01]` so the LLM can maintain relational context without seeing private data.

### 3. The "Sync" Bridge (`/src/sync`)
- **Incremental Processing:** Only processes delta changes from the source DB to save on embedding costs.
- **Model Switchboard:** Support for OpenAI `text-embedding-3`, Cohere, and local BGE models.

---

## 🏗️ High-Level Stack
- **Core:** Rust (for high-throughput data processing).
- **Orchestration:** Python / Pydantic (for AI logic and model interfacing).
- **Communication:** gRPC / Protobuf (for ultra-low latency between refinery modules).
- **Security:** AES-256 encryption at rest during the transformation phase.

---

## 🚀 Roadmap: Phase 1 (MVP)
- [ ] **v0.1:** SQL-to-Text flattening logic (De-normalizing relational rows).
- [ ] **v0.2:** Basic PII masking (Shield) with 99% accuracy for Finance/Legal terms.
- [ ] **v0.3:** Integration with `pgvector` for immediate output.
- [ ] **v0.4:** MCP (Model Context Protocol) compliance for agentic onboarding.

---

## 🛡️ Security & Compliance
Aether Refinery is built with a **Zero-Knowledge Architecture**. The refinery can be deployed on-premise (VPC), ensuring that raw data never leaves the client's secure perimeter during the transformation process.

---
*© 2026 Aether Systems. Confidential Software Specification.*

