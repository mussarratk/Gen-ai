# 🚀 Multi-Modal RAG with Azure AI

> **Production-oriented Retrieval-Augmented Generation (RAG) pipeline for querying heterogeneous enterprise content — PDFs, videos, audio, and images — using Azure AI Content Understanding, Azure AI Search, Azure OpenAI, and Azure AI Foundry.**

![Azure](https://img.shields.io/badge/Azure-AI%20%26%20Data-blue)
![Python](https://img.shields.io/badge/Python-3.10%2B-yellow)
![RAG](https://img.shields.io/badge/GenAI-Multi--Modal%20RAG-purple)
![Azure AI Search](https://img.shields.io/badge/Azure%20AI%20Search-Vector%20Search-orange)
![Azure OpenAI](https://img.shields.io/badge/Azure%20OpenAI-GPT--4o-green)
![License](https://img.shields.io/badge/License-MIT-lightgrey)

---

## 🎯 Project Overview

Traditional RAG systems primarily operate on text documents. Real enterprise knowledge, however, is distributed across **documents, presentations, images, recorded meetings, training videos, podcasts, and other unstructured media**.

This project addresses that problem by building a **multi-modal RAG architecture on Microsoft Azure**.

The pipeline converts heterogeneous content into searchable representations, stores them in **Azure AI Search**, retrieves the most relevant context using vector search, and uses **Azure OpenAI GPT-4o** to generate grounded responses.

### The engineering objective

**Raw enterprise content → Multi-modal understanding → Structured chunks → Vector embeddings → Hybrid/vector retrieval → Grounded generation**

The implementation demonstrates how to build a RAG solution that is:

* 🔎 **Retrieval-grounded**
* 🧠 **Multi-modal**
* ☁️ **Cloud-native**
* 🔐 **Identity-aware**
* 📈 **Scalable**
* ⚡ **Performance-conscious**
* 🧪 **Evaluation-ready**
* 🏭 **Production-oriented**

---

# 🏆 What This Project Demonstrates

This project is intentionally designed to demonstrate skills relevant to **Data Engineering, Azure Data Engineering, Databricks Engineering, GenAI Engineering, and AI/ML Engineering roles**.

| Skill Area          | Implementation                                           |
| ------------------- | -------------------------------------------------------- |
| Python              | Modular RAG agent, Azure SDK integration                 |
| Azure               | Azure AI Services, AI Search, OpenAI, Foundry            |
| Data Engineering    | Ingestion, transformation, chunking, indexing            |
| GenAI               | RAG, embeddings, prompt engineering                      |
| Multi-Modal AI      | PDF, video, audio, image processing                      |
| Vector Search       | Azure AI Search vector index                             |
| Cloud Security      | Microsoft Entra ID / RBAC                                |
| API Development     | Python RAG service                                       |
| AI Agents           | Azure AI Foundry                                         |
| Data Architecture   | Ingestion → Processing → Retrieval → Generation          |
| Performance         | Chunking, vector retrieval, index optimization           |
| Production Thinking | Observability, evaluation, security, scalability         |
| DevOps              | Environment configuration and deployment-ready structure |

---

# 🧩 Business Problem

Enterprise information is often fragmented across different formats.

For example, an organization may have:

```text
PDF
 └── Product documentation

Video
 └── Sustainability presentation

Audio
 └── Executive discussion

Image
 └── Product / sustainability infographic
```

A conventional keyword-based search system cannot effectively understand all of these sources.

This project creates a unified retrieval layer where a user can ask:

> **"What is BMW's approach to circularity and how does it relate to sustainable materials?"**

The system can retrieve information from:

* 📄 PDF documentation
* 🎥 Video transcript / visual information
* 🎵 Audio transcription
* 🖼️ Image descriptions

and provide a single grounded response.

---

# 🏗️ Architecture

```text
                         ┌─────────────────────────┐
                         │     Enterprise Data     │
                         └────────────┬────────────┘
                                      │
                  ┌───────────────────┼───────────────────┐
                  │                   │                   │
                  ▼                   ▼                   ▼
             ┌────────┐          ┌────────┐          ┌────────┐
             │  PDF   │          │ Video  │          │ Audio  │
             └────┬───┘          └────┬───┘          └────┬───┘
                  │                   │                   │
                  └───────────────────┼───────────────────┘
                                      │
                                      ▼
                     ┌──────────────────────────────┐
                     │ Azure AI Content Understanding│
                     │                              │
                     │ • Text extraction            │
                     │ • Speech transcription       │
                     │ • Visual understanding       │
                     │ • Content normalization      │
                     └──────────────┬───────────────┘
                                    │
                                    ▼
                         ┌──────────────────────┐
                         │ Chunking / Cleaning  │
                         │ Metadata Enrichment  │
                         └────────────┬─────────┘
                                      │
                                      ▼
                         ┌──────────────────────┐
                         │ Azure OpenAI         │
                         │ text-embedding-3-large│
                         └────────────┬─────────┘
                                      │
                                      ▼
                   ┌─────────────────────────────────┐
                   │       Azure AI Search           │
                   │                                 │
                   │ • Vector Search                 │
                   │ • Metadata Filtering            │
                   │ • Semantic Retrieval            │
                   │ • Hybrid Search                 │
                   └───────────────┬─────────────────┘
                                   │
                                   │ Top-K Context
                                   ▼
                         ┌──────────────────────┐
                         │    RAG Orchestrator  │
                         │                      │
                         │ Query → Retrieve →   │
                         │ Context → Generate   │
                         └────────────┬─────────┘
                                      │
                                      ▼
                         ┌──────────────────────┐
                         │ Azure OpenAI GPT-4o  │
                         │                      │
                         │ Grounded Generation  │
                         └────────────┬─────────┘
                                      │
                                      ▼
                              ┌──────────────┐
                              │ User Answer  │
                              └──────────────┘
```

---

# 🔄 End-to-End Data Flow

## 1. Ingestion

Multi-modal source files are collected:

```text
PDF
MP4
MP3
PNG / JPG
```

## 2. Content Understanding

Azure AI Content Understanding processes the raw content.

Examples:

| Input | Processing                        |
| ----- | --------------------------------- |
| PDF   | Text extraction                   |
| Video | Speech + visual understanding     |
| Audio | Speech-to-text                    |
| Image | Image description / verbalization |

The goal is to convert heterogeneous content into a **consistent searchable representation**.

---

## 3. Content Normalization

Extracted information is transformed into structured records.

Example:

```json
{
  "content_id": "bmw-circularity-video-001",
  "document_title": "BMW Circularity",
  "content_type": "video",
  "content_text": "BMW's circularity strategy...",
  "source": "BMW_circularity.mp4",
  "metadata": {
    "language": "en",
    "source_type": "video"
  }
}
```

---

## 4. Chunking

Long content is divided into smaller retrieval units.

Conceptually:

```text
Document
   │
   ├── Chunk 001
   ├── Chunk 002
   ├── Chunk 003
   ├── Chunk 004
   └── ...
```

Good chunking improves:

* Retrieval precision
* Context relevance
* Token efficiency
* Generation quality

---

## 5. Embedding Generation

Each chunk is converted into a vector representation using:

```text
text-embedding-3-large
```

The resulting vector captures the semantic meaning of the content.

```text
Text Chunk
    │
    ▼
Embedding Model
    │
    ▼
[0.021, -0.114, 0.391, ...]
```

---

# 🔎 Retrieval Architecture

When the user submits a question:

```text
User Query
    │
    ▼
Query Embedding
    │
    ▼
Azure AI Search
    │
    ├── Vector Similarity
    ├── Metadata Filtering
    └── Semantic Retrieval
    │
    ▼
Top-K Relevant Chunks
    │
    ▼
Prompt Context
    │
    ▼
GPT-4o
    │
    ▼
Grounded Answer
```

### Why vector retrieval?

Keyword search depends heavily on exact terms.

Vector search enables semantic matching.

For example:

```text
Query:
"How does BMW reduce material waste?"

Can retrieve:
"BMW's circular economy strategy focuses on
material reuse and resource efficiency..."
```

even when the exact phrase **"material waste"** does not appear.

---

# 🧠 RAG Design

The RAG agent follows a controlled pipeline:

```text
                 User Question
                       │
                       ▼
              ┌────────────────┐
              │ Query Analysis │
              └───────┬────────┘
                      │
                      ▼
              ┌────────────────┐
              │ Search Index   │
              └───────┬────────┘
                      │
                      ▼
              ┌────────────────┐
              │ Relevant       │
              │ Context        │
              └───────┬────────┘
                      │
                      ▼
              ┌────────────────┐
              │ Prompt Builder │
              └───────┬────────┘
                      │
                      ▼
                 ┌──────────┐
                 │ GPT-4o   │
                 └────┬─────┘
                      │
                      ▼
              Grounded Response
```

The system is designed to minimize unsupported generation by requiring the model to rely on retrieved context.

---

# 📚 Supported Content

| Modality  | Example                        | Processing                       |
| --------- | ------------------------------ | -------------------------------- |
| 📄 PDF    | BMW Sustainable Natural Rubber | Text extraction + chunking       |
| 🎥 Video  | BMW Circularity                | Transcript + visual descriptions |
| 🎵 Audio  | BMW Forwardism                 | Speech-to-text                   |
| 🖼️ Image | BMW Sustainability Journey     | Image understanding              |

---

# 📁 Repository Structure

```text
multimodal-rag-azure/
│
├── 📓 RAG_Data_Preparation.ipynb
│   └── Content processing, chunking and indexing
│
├── 📓 RAG_in_Action.ipynb
│   └── Retrieval and RAG experimentation
│
├── 🐍 multimodal_rag_agent.py
│   └── Standalone RAG application
│
├── 🐍 create_foundry_agent.py
│   └── Azure AI Foundry agent creation
│
├── 📄 requirements.txt
│   └── Python dependencies
│
├── 📄 index.json
│   └── Azure AI Search index definition
│
├── 🔐 .env.sample
│   └── Environment variable template
│
├── 📂 Assets/
│   ├── rag_data_prep.png
│   └── rag_in_action.png
│
└── 📂 Data/
    ├── BMW_circularity.mp4
    ├── BMW_forwardism.mp3
    ├── BMW_sustainable_natural_rubber.pdf
    └── image.png
```

---

# 🚀 Getting Started

## Prerequisites

### Azure

You need access to:

* Azure AI Services
* Azure AI Content Understanding
* Azure OpenAI
* Azure AI Search
* Azure Blob Storage
* Azure AI Foundry

### Local Development

```text
Python 3.10+
Azure CLI
Git
VS Code / Jupyter
```

---

# 1️⃣ Clone Repository

```bash
git clone https://github.com/arvie993/multimodal-rag-azure.git

cd multimodal-rag-azure
```

---

# 2️⃣ Create Virtual Environment

### Windows

```bash
python -m venv .venv

.venv\Scripts\activate
```

### macOS / Linux

```bash
python3 -m venv .venv

source .venv/bin/activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

---

# 3️⃣ Configure Environment Variables

Create `.env` from the template:

```bash
cp .env.sample .env
```

Example:

```env
AZURE_OPENAI_ENDPOINT=
AZURE_OPENAI_API_KEY=
AZURE_OPENAI_API_VERSION=

AZURE_SEARCH_ENDPOINT=
AZURE_SEARCH_KEY=
AZURE_SEARCH_INDEX=

AZURE_STORAGE_ACCOUNT=
AZURE_STORAGE_CONTAINER=

AZURE_AI_ENDPOINT=
```

> ⚠️ Never commit `.env`, API keys, access tokens, certificates, or other secrets to GitHub.

---

# 4️⃣ Azure Authentication

```bash
az login
```

Optionally select a subscription:

```bash
az account set --subscription "YOUR_SUBSCRIPTION_ID"
```

For production workloads, prefer **Microsoft Entra ID / Managed Identity** over long-lived API keys.

---

# 5️⃣ Prepare and Index Data

Run:

```text
RAG_Data_Preparation.ipynb
```

The notebook performs the conceptual workflow:

```text
Raw Files
   ↓
Content Understanding
   ↓
Content Extraction
   ↓
Normalization
   ↓
Chunking
   ↓
Embedding Generation
   ↓
Azure AI Search
```

---

# 6️⃣ Test the RAG Pipeline

Run:

```text
RAG_in_Action.ipynb
```

This notebook demonstrates:

* Query execution
* Vector retrieval
* Retrieved context
* Source inspection
* Generated response
* Retrieval quality analysis

---

# 🤖 Running the RAG Agent

## Option 1 — Interactive CLI

```bash
python multimodal_rag_agent.py
```

The application starts an interactive question-answering workflow.

Example:

```text
You: What is BMW's approach to circularity?

Assistant:
BMW's circularity strategy focuses on...
```

---

## Option 2 — API Mode

```bash
python multimodal_rag_agent.py serve
```

This allows the RAG pipeline to be exposed as an application/API layer.

---

# ☁️ Azure AI Foundry

The project can also be integrated with **Azure AI Foundry** for agent experimentation and deployment.

Run:

```bash
python create_foundry_agent.py
```

Then configure the agent in Azure AI Foundry.

Typical flow:

```text
Azure AI Foundry
       │
       ▼
RAG Agent
       │
       ▼
Azure AI Search Tool
       │
       ▼
Vector Index
       │
       ▼
Enterprise Knowledge
```

This provides a path from local experimentation to managed AI-agent workflows.

---

# 🔐 Security & Identity

Security is an important part of the architecture.

For Azure environments, the preferred authentication model is:

```text
Application
     │
     ▼
Microsoft Entra ID
     │
     ▼
Azure RBAC
     │
     ├── Azure AI Search
     ├── Azure OpenAI
     └── Azure AI Services
```

### Example Role Assignments

| Principal                | Resource          | Role                           |
| ------------------------ | ----------------- | ------------------------------ |
| User / Service Principal | Azure AI Services | Cognitive Services OpenAI User |
| User / Service Principal | Azure AI Search   | Search Index Data Contributor  |
| Application Identity     | Azure AI Search   | Search Index Data Reader       |
| Application Identity     | Azure AI Services | Cognitive Services OpenAI User |

### Security practices

* Use `.env` only for local development
* Keep secrets outside source control
* Use Managed Identity where possible
* Apply least-privilege RBAC
* Separate development and production resources
* Restrict search index access
* Avoid exposing internal documents unnecessarily

---

# 🔎 Azure AI Search Index

The index contains structured metadata and vector representations.

Example fields:

| Field               | Type                     | Purpose                          |
| ------------------- | ------------------------ | -------------------------------- |
| `content_id`        | String / Key             | Unique chunk identifier          |
| `document_title`    | String                   | Source document                  |
| `content_text`      | String                   | Extracted content                |
| `content_embedding` | Vector                   | Semantic representation          |
| `content_type`      | String                   | PDF / video / audio / image      |
| `source`            | String                   | Original source                  |
| `metadata`          | JSON / structured fields | Additional filtering information |

The vector field is designed to support semantic similarity search.

---

# ⚡ Performance & Scalability Considerations

A production RAG implementation requires more than simply connecting an LLM to a vector database.

This project considers several optimization areas.

### 1. Chunking Optimization

Poor chunking:

```text
Large Document
      ↓
Huge Chunk
      ↓
Low Retrieval Precision
```

Better approach:

```text
Document
   ↓
Meaningful Chunks
   ↓
Relevant Retrieval
   ↓
Smaller Prompt
```

---

### 2. Top-K Retrieval

Rather than passing the entire knowledge base to the LLM:

```text
Millions of records
       ↓
Vector Search
       ↓
Top-K chunks
       ↓
LLM
```

This reduces:

* Token consumption
* Latency
* Irrelevant context
* Generation noise

---

### 3. Hybrid Retrieval

For enterprise applications, retrieval can be extended beyond pure vector search:

```text
                Query
                  │
       ┌──────────┴──────────┐
       ▼                     ▼
 Keyword Search        Vector Search
       │                     │
       └──────────┬──────────┘
                  ▼
             Ranking
                  │
                  ▼
           Relevant Context
```

This is particularly useful for:

* Product IDs
* Technical terminology
* Names
* Exact identifiers
* Semantic questions

---

# 🧪 RAG Evaluation Strategy

A production RAG system should not be evaluated only by asking:

> "Does the answer look good?"

A stronger evaluation framework measures:

### Retrieval

* Recall@K
* Precision@K
* MRR
* NDCG

### Generation

* Faithfulness
* Answer relevance
* Context relevance
* Citation/source correctness

### System

* End-to-end latency
* Retrieval latency
* Token usage
* Cost per query
* Error rate

Conceptually:

```text
                 RAG Evaluation
                       │
       ┌───────────────┼────────────────┐
       ▼               ▼                ▼
   Retrieval        Generation       System
       │               │                │
   Recall@K        Faithfulness       Latency
   Precision@K     Relevance          Cost
   MRR             Grounding          Errors
```

---

# 🛡️ Responsible RAG Design

The application should be designed to reduce hallucinations.

Recommended behavior:

```text
Retrieved Context
       │
       ▼
Is sufficient evidence available?
       │
   ┌───┴────┐
  YES       NO
   │         │
   ▼         ▼
Answer     Abstain /
with       request more
context    information
```

The model should not confidently invent information when the retrieved context does not support an answer.

---

# 💬 Example Queries

### Cross-modal query

```text
What is BMW's approach to circularity?
```

Potential sources:

```text
🎥 Video
📄 PDF
```

---

### Document query

```text
Tell me about sustainable natural rubber.
```

Source:

```text
📄 BMW Sustainable Natural Rubber
```

---

### Audio query

```text
What is BMW's Forwardism strategy?
```

Source:

```text
🎵 Audio transcript
```

---

### Multi-source reasoning

```text
How are BMW's circularity initiatives connected
to sustainable material usage?
```

Potential sources:

```text
📄 PDF
🎥 Video
🖼️ Image
```

This demonstrates the key advantage of the architecture: **retrieving knowledge across different content modalities through a unified semantic retrieval layer.**

---

# 🛠️ Technology Stack

## Cloud

* Microsoft Azure
* Azure AI Services
* Azure AI Content Understanding
* Azure AI Search
* Azure OpenAI
* Azure AI Foundry
* Azure Blob Storage

## AI / GenAI

* Retrieval-Augmented Generation
* GPT-4o
* `text-embedding-3-large`
* Vector embeddings
* Semantic search
* Prompt engineering
* AI Agents

## Development

* Python
* Jupyter Notebook
* OpenAI SDK
* Azure Identity
* Azure SDKs
* REST/API concepts
* Git

---

# 🧠 Key Engineering Decisions

### Why Azure AI Search?

It provides an enterprise-oriented search layer capable of supporting:

* Vector search
* Keyword search
* Semantic retrieval
* Metadata filtering
* Scalable indexing

### Why RAG instead of fine-tuning?

RAG allows the system to work with **changing enterprise knowledge without retraining the foundation model**.

```text
New Document
     ↓
Process
     ↓
Embed
     ↓
Index
     ↓
Immediately Available to RAG
```

This makes RAG more suitable for frequently changing knowledge bases.

### Why multi-modal processing?

Enterprise knowledge isn't exclusively text.

A multi-modal pipeline can extract value from:

```text
Documents
Videos
Audio
Images
```

instead of discarding non-text information.

---

# 📈 Production Enhancement Roadmap

The current implementation provides the core architecture. The following enhancements can move it closer to a production-grade enterprise platform.

## Phase 1 — RAG Quality

* [ ] Hybrid search
* [ ] Semantic ranking
* [ ] Query rewriting
* [ ] Metadata filtering
* [ ] Parent-child chunk retrieval
* [ ] Reranking
* [ ] Source citations

## Phase 2 — Data Engineering

* [ ] Azure Data Factory orchestration
* [ ] Azure Blob Storage ingestion
* [ ] Incremental processing
* [ ] Event-driven ingestion
* [ ] Duplicate detection
* [ ] Schema/version management
* [ ] Dead-letter/error handling

## Phase 3 — Production

* [ ] Managed Identity
* [ ] Key Vault integration
* [ ] Application Insights
* [ ] Structured logging
* [ ] Retry policies
* [ ] Rate-limit handling
* [ ] CI/CD with GitHub Actions
* [ ] Infrastructure as Code

## Phase 4 — Advanced GenAI

* [ ] RAG evaluation pipeline
* [ ] Prompt versioning
* [ ] MLflow experiment tracking
* [ ] Guardrails
* [ ] Query classification
* [ ] Agentic retrieval
* [ ] Conversation memory
* [ ] Multi-turn reasoning

---

# 🔮 Future Architecture

A more production-oriented version can evolve into:

```text
                 ┌───────────────────────┐
                 │ Enterprise Sources    │
                 │ PDF / Video / Audio    │
                 │ Images / APIs / DBs    │
                 └───────────┬───────────┘
                             │
                             ▼
                    ┌─────────────────┐
                    │ Azure Data      │
                    │ Factory / Events│
                    └────────┬────────┘
                             │
                             ▼
                    ┌─────────────────┐
                    │ Azure Blob      │
                    │ Storage         │
                    └────────┬────────┘
                             │
                             ▼
              ┌──────────────────────────────┐
              │ Azure AI Content             │
              │ Understanding                │
              └──────────────┬───────────────┘
                             │
                             ▼
                    ┌─────────────────┐
                    │ Chunk + Metadata│
                    └────────┬────────┘
                             │
                             ▼
                    ┌─────────────────┐
                    │ Azure OpenAI    │
                    │ Embeddings      │
                    └────────┬────────┘
                             │
                             ▼
                  ┌──────────────────────┐
                  │ Azure AI Search      │
                  │ Hybrid + Vector      │
                  └──────────┬───────────┘
                             │
                             ▼
                    ┌─────────────────┐
                    │ RAG Orchestrator │
                    └────────┬────────┘
                             │
                             ▼
                    ┌─────────────────┐
                    │ GPT-4o / Agent  │
                    └────────┬────────┘
                             │
                             ▼
                    ┌─────────────────┐
                    │ User / API / UI │
                    └─────────────────┘
```

---

# 🎤 Interview Talking Points

This project can be explained in an interview using the following structure.

### 1. Problem

> "Enterprise knowledge exists across PDFs, videos, audio and images. I wanted to build a unified retrieval system rather than limiting RAG to text documents."

### 2. Architecture

> "I used Azure AI Content Understanding to extract and normalize information from multiple modalities, generated embeddings using Azure OpenAI, and indexed the chunks in Azure AI Search."

### 3. Retrieval

> "At query time, the user's question is embedded and matched against the vector index. The most relevant chunks are passed as context to GPT-4o for grounded generation."

### 4. Engineering

> "I separated ingestion, content processing, indexing and generation so each stage can scale independently."

### 5. Security

> "For production, I would use Microsoft Entra ID, Managed Identity and least-privilege RBAC rather than relying on static credentials."

### 6. Performance

> "Chunking, Top-K retrieval, metadata filtering, hybrid search and reranking can improve retrieval precision while reducing LLM token usage and latency."

### 7. Productionization

> "The next step would be to introduce orchestration, monitoring, evaluation, CI/CD, Key Vault and automated RAG quality measurement."

---

# 💡 Why This Project Is Valuable

This project demonstrates more than simply calling an LLM API.

It combines:

```text
Data Engineering
       +
Cloud Architecture
       +
Search Engineering
       +
Vector Databases
       +
Generative AI
       +
Python
       +
Security
       +
Production Engineering
```

The core engineering pattern is:

> **Ingest → Understand → Transform → Embed → Index → Retrieve → Generate → Evaluate**

This is the foundation of many modern enterprise GenAI applications.

---

# 📸 Project Screenshots

Add screenshots to the `Assets/` directory and reference them here.

### Data Preparation

```text
Assets/rag_data_prep.png
```

### RAG in Action

```text
Assets/rag_in_action.png
```

Example Markdown:

```markdown
![RAG Data Preparation](Assets/rag_data_prep.png)

![RAG in Action](Assets/rag_in_action.png)
```

---

# 📊 Skills Demonstrated

```text
☁️ Azure Cloud
   ├── Azure AI Services
   ├── Azure AI Search
   ├── Azure OpenAI
   ├── Azure AI Foundry
   └── Azure Blob Storage

🧠 Generative AI
   ├── RAG
   ├── Vector Embeddings
   ├── Prompt Engineering
   ├── AI Agents
   └── Multi-Modal AI

🐍 Python
   ├── SDK Integration
   ├── API Development
   ├── Data Processing
   └── Automation

🔎 Search
   ├── Vector Search
   ├── Semantic Search
   ├── Hybrid Search
   └── Metadata Filtering

🏭 Engineering
   ├── ETL / ELT
   ├── Data Pipelines
   ├── Scalability
   ├── Security
   ├── Monitoring
   └── CI/CD
```

---

# 📚 Learning Resources

* Azure AI Content Understanding
* Azure AI Search
* Azure OpenAI
* Azure AI Foundry
* Retrieval-Augmented Generation
* Vector Search
* Microsoft Entra ID
* Azure RBAC

---

# 📄 License

This project is licensed under the **MIT License**.

---

# 👨‍💻 Author

**Mussarrat K**

Data & AI Engineering | Python | SQL | Azure | Databricks | Generative AI

---

## ⭐ If you find this project useful

Consider giving the repository a ⭐ and exploring the implementation.

> **Built to demonstrate how enterprise data engineering and modern Generative AI can be combined into a scalable, secure and retrieval-grounded architecture.**
