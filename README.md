# Gen-ai

Here is a polished, enterprise-ready `README.md` file designed to showcase production engineering practices to recruiters and hiring managers. It emphasizes system architecture, production-grade patterns (security, performance, hybrid search), and dynamic evaluation metrics.

---

```markdown
# Enterprise Multi-Modal RAG System with Azure AI

[![Azure AI Content Understanding](https://img.shields.io/badge/Azure_AI-Content_Understanding-0078D4?logo=microsoftazure)](https://azure.microsoft.com/)
[![Azure AI Search](https://img.shields.io/badge/Azure_AI-Search_(Vector_&_Hybrid)-0078D4?logo=microsoftazure)](https://azure.microsoft.com/)
[![Azure OpenAI](https://img.shields.io/badge/Azure_OpenAI-GPT--4o_|_Text--Embedding--3--Large-0078D4?logo=openai)](https://azure.microsoft.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.10+](https://img.shields.io/badge/Python-3.10+-3776AB?logo=python&logoColor=white)](https://www.python.org/)

An enterprise-grade Retrieval-Augmented Generation (RAG) architecture built to ingest, vectorize, and query heterogeneous, multi-modal content sources (video, audio, structured/unstructured PDFs, high-resolution imagery) at scale. 

Powered by **Azure AI Content Understanding**, **Azure AI Search** (Hybrid + Semantic Ranker), and **Azure OpenAI (GPT-4o)**, this repository provides both a modular local pipeline and automated provisioning scripts for cloud deployment via **Azure AI Foundry**.

---

## 🎯 Architecture & Design Highlights


```

┌───────────────────────────────────────────────────────────────────────────────────┐
│                          Multi-Modal Ingestion & Query Pipeline                   │
├───────────────────────────────────────────────────────────────────────────────────┤
│                                                                                   │
│  [ Input Sources ]                                                                │
│  ├── PDFs (Text + Chunking)   ──┐                                                 │
│  ├── Videos (Visuals + Audio) ──┼──▶ [ Azure AI Content Understanding ]           │
│  ├── Audio (STT / Speeches)   ──┤     │ (Extraction, Chunking & Multimodal)       │
│  └── Images (Verbalization)   ──┘     │                                           │
│                                       ▼                                           │
│                       [ Azure OpenAI Embedding API ]                              │
│                       │ (text-embedding-3-large: 3072 dim)                        │
│                       │                                                           │
│                       ▼                                                           │
│             ┌─────────────────────────────────────────┐                           │
│             │   Azure AI Search (Vector Index)        │                           │
│             │   - Hybrid Search (HNSW Vector + BM25)  │                           │
│             │   - L2 / Cosine Similarity + Reciprocal │                           │
│             │   - Semantic Re-ranking (L2 Engine)     │                           │
│             └────────────────────┬────────────────────┘                           │
│                                  │                                                │
│  [ User Query ] ─────────────────┼──────────────────────────────┐                 │
│                                  ▼                              ▼                 │
│                       ┌──────────────────────┐      ┌─────────────────────────┐   │
│                       │  Retrieved Context   │─────▶│  Azure OpenAI (GPT-4o)  │   │
│                       └──────────────────────┘      │  (System / RAG Agent)   │   │
│                                                     └───────────┬─────────────┘   │
│                                                                 │                 │
│  [ Formatted Response + Citations ] ◀───────────────────────────┘                 │
│                                                                                   │
└───────────────────────────────────────────────────────────────────────────────────┘

```

### Key Technical Capabilities

* **Unified Multi-Modal Ingestion:** Unifies unstructured assets (video visual descriptions, audio speech-to-text transcripts, PDF text/tables, image verbalizations) into a normalized vector space.
* **Hybrid Search with Semantic Re-ranking:** Blends vector similarity (HNSW algorithm) with classical keyword search (BM25) and applies Azure's L2 Semantic Ranker to mitigate false positives and improve context precision.
* **Identity-First Security:** Zero explicit secrets or hardcoded API keys in code; uses **Microsoft Entra ID (RBAC)** via `DefaultAzureCredential` for identity propagation across Azure resources.
* **Foundry Agent Deployment:** Native deployment script to transform the custom Python agent into an autonomous agent endpoint within **Azure AI Foundry**.

---

## 📦 Ingested Modalities & Normalization Strategy

| Modality | Target Data Type | Feature Extraction Strategy | Chunking / Context Strategy |
| :--- | :--- | :--- | :--- |
| **PDF** | Document (`.pdf`) | Structural layout analysis, OCR, table parsing | Sliding window text chunking with metadata tagging |
| **Video** | Video (`.mp4`) | Audio transcription (Whisper) + visual scene verbalization | Frame-interval & timestamp-bounded scene chunking |
| **Audio** | Audio (`.mp3`) | Speech-to-Text (STT) transcription | Speaker-diarized paragraph segmenting |
| **Image** | Image (`.png`, `.jpg`) | Dense visual description & key entity extraction | Full visual-to-text alignment payload |

---

## 📁 Repository Structure


```

multimodal-rag-azure/
├── Data/                        # Raw sample multi-modal content
│   ├── BMW_circularity.mp4
│   ├── BMW_forwardism.mp3
│   ├── BMW_sustainable_natural_rubber.pdf
│   └── image.png
├── Assets/                      # Diagrams and architecture visuals
├── RAG_Data_Preparation.ipynb   # ETL, Content Understanding analysis, indexing workflow
├── RAG_in_Action.ipynb          # End-to-end evaluation & query sandbox
├── multimodal_rag_agent.py      # Production-grade CLI/REST API agent script
├── create_foundry_agent.py      # Azure AI Foundry SDK deployment script
├── index.json                   # Azure AI Search index declarative schema
├── requirements.txt             # Locked dependencies
└── .env.sample                  # Environment template

```

---

## 🛠️ Tech Stack & Prerequisites

### Infrastructure & Services
* **Azure AI Services:** Content Understanding, Azure OpenAI (`gpt-4o`, `text-embedding-3-large`)
* **Azure AI Search:** Basic Tier or higher (Vector Search & Semantic Ranker enabled)
* **Azure AI Foundry & Storage:** Blob Storage containers for raw document holding

### Local Tooling
* Python **3.10+**
* [Azure CLI](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli)

---

## 🚀 Step-by-Step Setup & Execution

### 1. Repository Setup

```bash
git clone [https://github.com/arvie993/multimodal-rag-azure.git](https://github.com/arvie993/multimodal-rag-azure.git)
cd multimodal-rag-azure

# Create and activate virtual environment
python -m venv .venv

# On Windows:
.venv\Scripts\activate
# On macOS/Linux:
# source .venv/bin/activate

# Install dependencies
pip install -r requirements.txt

```

### 2. Environment Configuration

Copy `.env.sample` to `.env` and supply your Azure service endpoints:

```bash
cp .env.sample .env

```

```env
AZURE_OPENAI_ENDPOINT="https://<your-openai-instance>[.openai.azure.com/](https://.openai.azure.com/)"
AZURE_OPENAI_DEPLOYMENT_NAME="gpt-4o"
AZURE_OPENAI_EMBEDDING_DEPLOYMENT="text-embedding-3-large"
AZURE_SEARCH_SERVICE_ENDPOINT="https://<your-search-instance>.search.windows.net"
AZURE_SEARCH_INDEX_NAME="multimodal-rag-index"
AZURE_CONTENT_UNDERSTANDING_ENDPOINT="https://<your-cu-instance>[.cognitiveservices.azure.com/](https://.cognitiveservices.azure.com/)"

```

### 3. Azure RBAC & Authentication Setup

Run `az login` to establish your active developer token:

```bash
az login
az account set --subscription "YOUR_AZURE_SUBSCRIPTION_ID"

```

Ensure the following Azure Role Assignments are set for your user and identities:

| Identity | Target Resource | Required Role |
| --- | --- | --- |
| **Developer User / Managed Identity** | Azure AI Services | `Cognitive Services OpenAI User` |
| **Developer User / Managed Identity** | Azure AI Search | `Search Index Data Contributor` |
| **Azure AI Search Identity** | Azure AI Services | `Cognitive Services OpenAI User` |

---

## 💻 Execution & Deployment

### Phase 1: Data Preparation & Indexing

Open and run `RAG_Data_Preparation.ipynb`. This notebook:

1. Provisions the vector index based on `index.json`.
2. Processes files inside `/Data` using Azure AI Content Understanding.
3. Generates vector embeddings (`3072` dimensions) using `text-embedding-3-large`.
4. Uploads document chunks into Azure AI Search.

### Phase 2: Interacting with the RAG System

#### Interactive CLI Mode

```bash
python multimodal_rag_agent.py

```

#### API Mode

```bash
python multimodal_rag_agent.py serve --port 8000

```

#### Deploy to Azure AI Foundry

To register the tool definitions, vector index connector, and orchestrator directly inside Azure AI Foundry:

```bash
python create_foundry_agent.py

```

---

## 📈 Evaluation & Benchmark Sample

| Natural Language Query | Vector/Hybrid Target Modalities | Expected Ground Truth Source |
| --- | --- | --- |
| *"What is BMW's overall approach to circularity?"* | Video (Scene + Speech) & PDF | `BMW_circularity.mp4`, `BMW_sustainable_natural_rubber.pdf` |
| *"Detail the specific strategy behind sustainable natural rubber."* | PDF Text & Tables | `BMW_sustainable_natural_rubber.pdf` (p. 1-2) |
| *"What key themes are outlined in the Forwardism audio transcript?"* | Audio (Diarized STT) | `BMW_forwardism.mp3` |

---

## 🔒 Security & Best Practices

* **Keyless Architecture:** Configured to work natively with `azure-identity` (`DefaultAzureCredential`), eliminating hardcoded API keys.
* **Metadata Lineage:** Every chunk stores source path, modality, frame timestamp, and page numbers to guarantee traceable response citations.
* **Index Configuration:** Utilizes cosine distance over normalized 3072-dimension embeddings for fast nearest-neighbor search.

---

## 📄 License

Distributed under the **MIT License**. See `LICENSE` for details.

```

***

<FollowUp label="Want me to generate the corresponding index.json schema file or refine the Python scripts to match keyless Azure authentication?" query="Can you provide the companion index.json vector search schema and update the authentication setup in python code to use DefaultAzureCredential?"/>

```
