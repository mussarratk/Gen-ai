Below is a complete, production-ready `README.md` optimized to showcase high-level enterprise architecture, robust Engineering practices, and deep expertise in Azure AI services for tech recruiters and hiring managers.

Copy and paste the raw Markdown block directly into your project's `README.md` file on GitHub.

```markdown
# Enterprise Multi-Modal RAG with Azure AI & GPT-4o

[![Python 3.10+](https://img.shields.io/badge/python-3.10%2B-blue.svg)](https://www.python.org/downloads/)
[![Azure AI Foundry](https://img.shields.io/badge/Azure%20AI-Foundry-0078D4.svg)](https://azure.microsoft.com/en-us/products/ai-foundry)
[![Azure AI Search](https://img.shields.io/badge/Azure%20AI-Search-0078D4.svg)](https://azure.microsoft.com/en-us/products/ai-services/ai-search)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

An production-grade Retrieval-Augmented Generation (RAG) architecture engineered to process, index, and query unstructured, heterogeneous multi-modal data streams (Video, Audio, Visuals, and PDF documents) using **Azure AI Content Understanding**, **Azure AI Search**, and **Azure OpenAI (GPT-4o)**.

---

## 🎯 Architecture & Pipeline Overview

This solution unifies unstructured, multi-modal content into a high-dimensional vector space, applying automated feature extraction, semantic chunking, and multimodal retrieval to enable cross-modal reasoning without data loss.


```

┌──────────────────────────────────────────────────────────────────────────────────┐
│                             Multi-Modal RAG Pipeline                             │
├──────────────────────────────────────────────────────────────────────────────────┤
│                                                                                  │
│  ┌──────────────┐   ┌──────────────────────────┐   ┌──────────────────────────┐  │
│  │ Data Sources │   │ Azure Content            │   │ Azure AI Search          │  │
│  │ ──────────── │   │ Understanding            │   │ ──────────────────────── │  │
│  │ • PDF        │──▶│ ──────────────────────── │──▶│ • HNSW Vector Index      │  │
│  │ • Video MP4  │   │ • OCR / Layout Extraction│   │ • Hybrid Search          │  │
│  │ • Audio MP3  │   │ • Whisper Speech-to-Text │   │ • Semantic Ranker (L2)   │  │
│  │ • Visuals    │   │ • Image Verbalization    │   └────────────┬─────────────┘  │
│  └──────────────┘   └──────────────────────────┘                │                │
│                                                                 │ (Relevant      │
│                                                                 │  Context)      │
│                                                                 ▼                │
│  ┌──────────────┐   ┌──────────────────────────┐   ┌──────────────────────────┐  │
│  │ User / CLI   │   │ Azure OpenAI Service     │   │ RAG Agent Engine         │  │
│  │ ──────────── │   │ ──────────────────────── │   │ ──────────────────────── │  │
│  │ Query Request│──▶│ • GPT-4o (Reasoning)     │◀──│ • Identity Authentication│  │
│  │ & Stream     │   │ • text-embedding-3-large │   │ • Context Injection      │  │
│  └──────────────┘   └──────────────────────────┘   └──────────────────────────┘  │
│                                                                                  │
└──────────────────────────────────────────────────────────────────────────────────┘

```

---

## 💡 Key Features & Engineering Highlights

* **Cross-Modal Content Processing:** Automated extraction pipelines convert raw video (visual frame descriptions + audio track), MP3s, PDFs, and high-resolution images into structured, embeddable semantic chunks.
* **Hybrid Search Strategy:** Combines Keyword (BM25) search with high-dimensional Vector Search (`text-embedding-3-large`, 3072 dimensions) using **HNSW (Hierarchical Navigable Small World)** indexing and Reciprocal Rank Fusion (RRF).
* **Enterprise Security & Identity:** Fully implemented with **Azure Entra ID (MSAL/Azure Identity)** using Role-Based Access Control (RBAC) and zero hardcoded secrets.
* **Dual Deployment Paradigms:** Exposes both a local, async Python CLI/REST API server and cloud-native deployment scripts for **Azure AI Foundry Agents**.

---

## 📊 Modality Matrix

| Modality | Ingestion Processing Pipeline | Vector Representation |
| :--- | :--- | :--- |
| **📄 PDF Documents** | Layout-aware text extraction + structural chunking | 3072-dim embeddings (`text-embedding-3-large`) |
| **🎥 Video (`.mp4`)** | Video frame sampling + audio transcript synthesis | Multi-stream combined semantic vectors |
| **🎵 Audio (`.mp3`)** | Azure Speech / Whisper transcription + time-stamping | Chronological text segment embeddings |
| **🖼️ Images** | Dense image verbalization, visual feature description | Text-projected visual embedding space |

---

## 📂 Repository Structure


```

multimodal-rag-azure/
├── Data/                        # Multi-modal test datasets (Sample Media & Docs)
│   ├── BMW_circularity.mp4
│   ├── BMW_forwardism.mp3
│   ├── BMW_sustainable_natural_rubber.pdf
│   └── image.png
├── Assets/                      # Architecture diagrams and runtime metrics
│   ├── rag_data_prep.png
│   └── rag_in_action.png
├── RAG_Data_Preparation.ipynb   # Ingestion, parsing, chunking, and index construction
├── RAG_in_Action.ipynb          # End-to-end evaluation & reasoning queries
├── multimodal_rag_agent.py      # Core RAG Agent (CLI & REST API execution modes)
├── create_foundry_agent.py      # IaC deployment script for Azure AI Foundry
├── index.json                   # HNSW Hybrid Vector Search Index Schema
├── requirements.txt             # Locked dependencies
└── .env.sample                  # Environment configuration template

```

---

## 🛠️ Quickstart Guide

### Prerequisites

* **Python 3.10+**
* **Azure Subscription** with active access to:
  * Azure OpenAI Service (`GPT-4o`, `text-embedding-3-large`)
  * Azure AI Search (Basic Tier or higher for Vector Search)
  * Azure AI Content Understanding / Cognitive Services
  * Azure Blob Storage Container

### 1. Installation

```bash
# Clone repository
git clone [https://github.com/arvie993/multimodal-rag-azure.git](https://github.com/arvie993/multimodal-rag-azure.git)
cd multimodal-rag-azure

# Setup virtual environment
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

```

### 2. Configuration & Authentication

1. Copy the sample environment file:
```bash
cp .env.sample .env

```


2. Populate `.env` with your Azure endpoint configurations.
3. Authenticate with Azure CLI via Entra ID:
```bash
az login

```



---

## 🔐 Security & RBAC Configuration

To adhere to enterprise security standards, ensure the following Azure Role-Based Access Control (RBAC) assignments are active:

| Principal | Target Resource | Required Azure Role |
| --- | --- | --- |
| **User / Developer** | Azure OpenAI Service | `Cognitive Services OpenAI User` |
| **User / Developer** | Azure AI Search | `Search Index Data Contributor` |
| **AI Search Identity** | Azure OpenAI Service | `Cognitive Services OpenAI User` |
| **AI Services Identity** | Azure AI Search | `Search Index Data Reader` |

---

## ⚡ Execution Modes

### Ingestion & Index Pipeline

Execute the data preparation notebook to process multi-modal raw content, produce vector embeddings, and construct the search index:

```bash
jupyter notebook RAG_Data_Preparation.ipynb

```

### Running the RAG Agent Locally

**Interactive CLI Mode:**

```bash
python multimodal_rag_agent.py

```

**REST API Mode:**

```bash
python multimodal_rag_agent.py serve --port 8000

```

### Deploying to Azure AI Foundry

Deploy the agent logic natively to Azure AI Foundry for hosted execution:

```bash
python create_foundry_agent.py

```

---

## 🔍 Index Schema Specification

The `index.json` schema configures vector fields with **HNSW cosine similarity** metrics alongside tokenized content fields:

```json
{
  "name": "multimodal-rag-index",
  "fields": [
    { "name": "content_id", "type": "Edm.String", "key": true, "filterable": true },
    { "name": "document_title", "type": "Edm.String", "searchable": true, "filterable": true },
    { "name": "modality", "type": "Edm.String", "filterable": true, "facetable": true },
    { "name": "content_text", "type": "Edm.String", "searchable": true },
    {
      "name": "content_embedding",
      "type": "Collection(Edm.Single)",
      "dimensions": 3072,
      "vectorSearchProfile": "hnsw-cosine-profile"
    }
  ]
}

```

---

## 📄 License

This project is licensed under the **MIT License** - see the `LICENSE` file for details.

```

<FollowUp label="Want me to generate a matching requirements.txt or .env.sample file?" query="Generate a complete requirements.txt and .env.sample file matching this Azure Multi-Modal RAG README."/>

```
