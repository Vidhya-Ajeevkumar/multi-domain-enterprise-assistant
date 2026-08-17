# Multi-Domain Enterprise Assistant using Hybrid RAG

A multi-document enterprise question-answering assistant built over HR, Finance, and IT policy documents.

## What the project does

The system retrieves relevant policy information and uses the retrieved context to generate an answer.

**Pipeline**

`Documents → Chunking → Embeddings → FAISS + BM25 → Hybrid Retrieval → Re-Ranker → LLM Answer`

## Main components

- **Document processing:** HR, Finance, and IT policy documents
- **Chunking:** Recursive character text splitting with overlap
- **Embeddings:** Sentence Transformers (`all-MiniLM-L6-v2`)
- **Semantic retrieval:** FAISS
- **Keyword retrieval:** BM25
- **Hybrid retrieval:** combines FAISS and BM25 scores
- **Re-ranking:** Cross-Encoder (`cross-encoder/ms-marco-MiniLM-L-6-v2`)
- **Answer generation:** Gemini API
- **Fine-tuning experiment:** LoRA with Qwen2.5-0.5B-Instruct

## Evaluation recorded during development

- Recall@3: **100%**
- Precision@3: **33.33%**
- 3 enterprise domains: HR, Finance, IT
- 10 document chunks in the final multi-document index
- 384-dimensional embedding vectors

## Example questions

1. How many casual leave days are employees eligible for?
2. What is the maximum meal reimbursement amount per day?
3. What should employees do if they receive a suspicious phishing email?

## Notebook

Open `Multi_Domain_Enterprise_Assistant_GitHub.ipynb` in Google Colab or Jupyter.

## Setup

Install the required libraries in Colab/Jupyter as shown in the notebook.

For Gemini API access, store the API key securely (for example, in Google Colab Secrets). **Do not commit API keys to GitHub.**

## Note on the LoRA experiment

LoRA fine-tuning was explored as an adaptation experiment. The main project pipeline is Hybrid RAG with re-ranking because factual enterprise answers should remain grounded in retrieved document context.

## Project structure

```text
multi-domain-enterprise-assistant/
├── Multi_Domain_Enterprise_Assistant_GitHub.ipynb
├── README.md
└── requirements.txt
```
