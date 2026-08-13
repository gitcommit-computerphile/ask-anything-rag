# QueryBridge

Ask it something about LangChain, RAG, Groq, embeddings, that sort of thing, and it pulls from a local vector store. Ask it anything else and it falls back to Wikipedia. The router figures it out from the question itself.

Follow ups get rewritten into standalone questions using the chat history before they hit the router, so "what about its downsides" still resolves correctly instead of confusing the retriever. First message in a session skips that step since there's nothing to resolve yet.

Conversations persist to disk, so closing the tab and coming back later picks up right where you left off, past sessions are listed in the sidebar. You can also paste text into the sidebar at any point to grow the knowledge base on the fly.

Stack: LangGraph for the flow, Groq for the LLM, ChromaDB for the vector store, Gradio for the UI.

## Running it

```bash
.venv\Scripts\activate
python app.py
```

Opens at `http://localhost:7860`.

Needs a `.env` with:

```
GROQ_API_KEY=gsk_...
```

Install deps with `pip install -r requirements.txt` first. First run downloads the embedding model (~90MB) and seeds the vector store from `data/sample_docs.txt`, one-time only.

Delete `checkpoints.db` to wipe chat history, delete `chroma_db/` to reseed the knowledge base.
