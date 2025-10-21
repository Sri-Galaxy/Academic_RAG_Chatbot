# Academic_RAG_Chatbot

Simple Retrieval-Augmented-Generation (RAG)

This repository demonstrates how to ingest a PDF and a text file, split content into chunks, create embeddings with sentence-transformers, persist a ChromaDB vector store, and query a Google Gemini LLM to generate answers using retrieved context.

Contents
- `main.ipynb` - Jupyter notebook with the full workflow.
- `data/hello.txt` - example text file.
- `data/Presentation.pdf` - expected PDF to ingest (not included).
- `data/vector_store/` - persisted ChromaDB files (already present in the repo).
- `.env` - environment file for API keys.
- `requirements.txt` - Python dependencies.

Requirements
- Python 3.10+
- Create and activate a virtual environment, then install dependencies from `requirements.txt`.

Quickstart (PowerShell)

1. Create and activate a venv:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1   # or use .\.venv\Scripts\activate for cmd
```

2. Install dependencies:

```powershell
pip install -r requirements.txt
```

3. Add your Google API key to `.env` in the repository root:

```
GOOGLE_API_KEY=your_api_key_here
```

4. Open and run the notebook `main.ipynb` in VS Code or Jupyter. Run cells top-to-bottom.

Usage
- The notebook defines helper classes and functions:
  - `EmbeddingManager` — wraps sentence-transformers to produce embeddings.
  - `VectorStore` — wraps ChromaDB persistent client and collection.
  - `Retriever` — embeds a query and retrieves top-k documents.
  - `generate_answer(query, retriever, llm, top_k=3)` — retrieves context and calls the LLM to answer.

Example in the notebook:

```python
res = generate_answer("What is the pdf about?", retriever, llm, top_k=3)
print(res)
```

Notes
- The notebook expects a file at `./data/Presentation.pdf`. If you don't have it, update the loader cell or use `data/hello.txt` to test.
- If you re-run embedding and want a fresh vector store, remove or back up `data/vector_store/chroma.sqlite3`.
- The notebook currently uses `langchain_google_genai.ChatGoogleGenerativeAI` for LLM calls (requires `GOOGLE_API_KEY`).

