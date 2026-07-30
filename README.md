# 📚 StuLearn Hybrid RAG Pipeline

A production-style **Retrieval-Augmented Generation (RAG)** pipeline built using **LlamaIndex**, **ChromaDB**, **Hybrid Retrieval (Dense + BM25)**, **Cross-Encoder Reranking**, and **OpenRouter LLMs**.

The project demonstrates how modern RAG systems retrieve, rerank, and generate accurate answers grounded in uploaded academic documents while minimizing hallucinations.

---

## 🚀 Features

- 📄 PDF document ingestion
- ✂️ Sentence-level document chunking
- 🔍 Dense semantic retrieval using OpenAI embeddings
- 📚 Sparse retrieval using BM25
- 🔀 Hybrid Retrieval (Dense + BM25)
- ⭐ Cross-Encoder Reranking (BGE Reranker)
- 🧠 LLM-powered answer generation using OpenRouter
- 💾 Persistent ChromaDB vector database
- 📊 Retrieval evaluation and token analysis
- ⚡ Modular and production-ready notebook

---

# Pipeline Architecture

```
                   User Query
                        │
                        ▼
              Hybrid Retriever
        ┌──────────────┴──────────────┐
        ▼                             ▼
 Dense Semantic Search          BM25 Retrieval
 (Embeddings)                  (Keyword Search)
        │                             │
        └──────────────┬──────────────┘
                       ▼
                Merge Results
                       ▼
          Cross-Encoder Reranker
          (BAAI/bge-reranker-base)
                       ▼
               Top Relevant Chunks
                       ▼
             Prompt Construction
                       ▼
                OpenRouter LLM
                       ▼
              Grounded Response
```

---

# Project Structure

```
StuLearn-RAG/
│
├── data/
│   ├── paper1.pdf
│   ├── paper2.pdf
│   └── ...
│
├── storage/
│   └── chroma_db/
│
├── notebooks/
│   └── Hybrid_RAG.ipynb
│
├── .env
├── requirements.txt
└── README.md
```

---

# Technologies Used

| Category | Technology |
|----------|------------|
| Framework | LlamaIndex |
| Vector Database | ChromaDB |
| Embedding Model | OpenAI text-embedding-3-large |
| Retrieval | Dense + BM25 |
| Reranker | BAAI/bge-reranker-base |
| LLM | OpenRouter |
| Language | Python |

---

# Workflow

## 1. Load Documents

Academic PDFs are loaded from a local directory using LlamaIndex's `SimpleDirectoryReader`.

↓

## 2. Chunk Documents

Documents are split into sentence-aware chunks using the `SentenceSplitter`.

↓

## 3. Generate Embeddings

Each chunk is converted into dense vector embeddings.

↓

## 4. Store in ChromaDB

Embeddings are stored inside a persistent Chroma vector database.

↓

## 5. Hybrid Retrieval

For every query:

- Dense semantic search retrieves contextually similar chunks.
- BM25 retrieves keyword-matching chunks.
- Results are merged and deduplicated.

↓

## 6. Reranking

A Cross-Encoder reranker scores all retrieved chunks based on their relevance to the query.

Only the highest-ranked chunks are selected.

↓

## 7. Prompt Construction

The retrieved context is injected into a custom RAG prompt designed to:

- Reduce hallucinations
- Restrict answers to retrieved context
- Produce structured responses

↓

## 8. Answer Generation

The prompt is sent to an OpenRouter LLM to generate the final grounded response.

---

# Evaluation

The notebook records:

- Number of retrieved chunks
- Retrieval latency
- Generation latency
- Context token count
- Query token count
- Response token count
- Total token usage

These metrics help evaluate retrieval quality and overall pipeline performance.

---

# Installation

Clone the repository

```bash
git clone https://github.com/yourusername/stulearn-rag.git
```

Create a virtual environment

```bash
python -m venv .venv
```

Activate it

Windows

```bash
.venv\Scripts\activate
```

Linux / macOS

```bash
source .venv/bin/activate
```

Install dependencies

```bash
pip install -r requirements.txt
```

---

# Environment Variables

Create a `.env` file.

```
OPENROUTER_API_KEY=your_api_key_here
```

---

# Running the Notebook

Open Jupyter Notebook or VS Code.

Run the notebook from top to bottom.

The pipeline will:

- Load PDFs
- Build the vector index
- Perform hybrid retrieval
- Rerank retrieved chunks
- Generate grounded answers

---

# Example Query

```
What role does machine learning play in the proposed system?
```

The pipeline:

- Retrieves relevant chunks
- Reranks them
- Generates an answer using only the retrieved context

---

# Future Improvements

- Multi-query retrieval
- Reciprocal Rank Fusion (RRF)
- Parent-Child Retrieval
- Metadata filtering
- Query rewriting
- Multi-vector indexing
- GraphRAG
- Citation generation
- Evaluation with RAGAS
- Web search integration

---

# Learning Outcomes

This project demonstrates practical implementation of:

- Retrieval-Augmented Generation (RAG)
- Hybrid Retrieval
- Semantic Search
- Sparse Retrieval (BM25)
- Cross-Encoder Reranking
- Vector Databases
- Embedding Models
- Prompt Engineering
- Large Language Models
- LlamaIndex
- ChromaDB

---

# Acknowledgements

- LlamaIndex
- ChromaDB
- OpenRouter
- Sentence Transformers
- Hugging Face
- OpenAI

---

## Author

**Hrishikesh Sanap**

Computer Engineering Student

Interested in Artificial Intelligence, Retrieval-Augmented Generation (RAG), Machine Learning, and Large Language Models.

---

## License

This project is intended for educational and research purposes.