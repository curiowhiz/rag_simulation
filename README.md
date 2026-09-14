# RAG Playground

An interactive, in-browser simulator that walks through the full Retrieval-Augmented Generation (RAG) pipeline step by step: ingestion, chunking, embeddings, indexing, hybrid retrieval, reranking, context assembly, generation, guardrails, and observability.

**This project was built for educational purposes only.** It is meant to help product managers, engineers, and anyone curious about how RAG systems actually work build real intuition for each stage, using real algorithms wherever possible. It is not a production retrieval system, and it should not be used as one.

## Live demo

https://rajangupta.ca/rag_simulation/

## What it does

Paste text, or upload a PDF, DOCX, HTML, or TXT file (up to 5MB), then step through nine stages:

1. **Knowledge Base**: ingest and parse documents entirely in the browser
2. **Chunking**: seven real strategies, fixed-size, sliding window, sentence-based, recursive/paragraph-aware, semantic (topic-shift aware), hierarchical (parent-child), and document-type-aware
3. **Vector Embeddings**: real TF-IDF vectors, not a placeholder
4. **Indexing & Storage**: an index stats view and a per-vector table
5. **Retrieval**: hybrid search (TF-IDF cosine blended with real BM25), metadata filtering by source, and a lexical reranking pass
6. **Context Assembly**: the actual prompt string a language model would receive, including parent-chunk expansion where that strategy applies
7. **Generation**: clearly labeled as simulated, since this demo has no backend and no embedded API key
8. **Output & Guardrails**: groundedness scoring, confidence thresholds, a PII pattern scan, and citation checks, all computed for real
9. **Observability & Feedback**: real per-stage timing and a thumbs up / thumbs down feedback loop stored in your browser

## What is real and what is simulated

Most of this pipeline runs real, working algorithms. TF-IDF, BM25, cosine similarity, and every chunking strategy compute genuine results from whatever text you give them. Two things are intentionally simplified:

- **Embeddings** use TF-IDF, a classic lexical vector representation, instead of a neural embedding model. It is a real vector with real cosine similarity, just not one learned from training data.
- **Generation** is simulated. There is no backend and no embedded API key, so this step assembles an extractive answer from the retrieved context instead of calling a real language model. Everything upstream of that step works exactly as shown, and the assembled prompt is exactly what would be sent to a real model in production.

## Tech stack

A single self-contained `index.html`. No build step, no framework, no backend.

- Vanilla HTML, CSS, and JavaScript
- [pdf.js](https://mozilla.github.io/pdf.js/) for client-side PDF parsing
- [mammoth.js](https://github.com/mwilliamson/mammoth.js) for client-side DOCX parsing
- Google Fonts (Inter, JetBrains Mono)

All file parsing happens in your browser. Nothing is uploaded anywhere.

## Running it locally

Clone the repo and open `index.html` directly in a browser, or serve it with any static file server, for example:

```
python3 -m http.server 8000
```

Then visit `http://localhost:8000`.

## Purpose and license

This repository exists to teach RAG concepts, not to ship a product. Feel free to read the source, fork it, or use it as a teaching reference. It should not be treated as a benchmark for production retrieval quality, and none of its "AI" behavior (embeddings, generation) reflects what a real neural model would produce.

Built by [Rajan Gupta](https://rajangupta.ca).
