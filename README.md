**Project Overview**

This repository provides a small retrieval-augmented QA demo for realistic restaurant reviews. It uses Ollama models (local LLM and embedding models) with LangChain-style components to embed reviews, store them in a Chroma vector store, and run a simple prompt chain to answer questions about a pizza restaurant.

**Files**
- `main.py`: Runs a simple prompt -> LLM chain. Uses `OllamaLLM` (model: `llama3.2` in the current code).
- `vector.py`: Reads `realistic_restaurant_reviews.csv`, creates embeddings with `mxbai-embed-large`, and persists a Chroma vector store to `./chrome_langchain_db`.
- `realistic_restaurant_reviews.csv`: Source dataset of review records used to build the vector store.

**Requirements**
- Python 3.9+ (project uses a `venv` in this workspace).
- OS-level: Ollama installed and running locally for model serving.
- Python packages (suggested): `pandas`, `langchain_ollama`, `langchain_core`, `langchain_chroma` (or appropriate LangChain/Chroma integration packages), and `chromadb` if needed. Use a `requirements.txt` with these names or adapt to your package manager.

**Setup**
- Activate the virtual environment in the project root:

```zsh
source venv/bin/activate
```

- Install Python dependencies (if you have a `requirements.txt`):

```zsh
pip install -r requirements.txt
```

- Ensure Ollama is installed and running. Check available local models:

```zsh
ollama list
```

- If a required model is missing, pull it (example):

```zsh
ollama pull llama3.2
ollama pull mxbai-embed-large
```

**Usage**
- Build the vector store (this will read `realistic_restaurant_reviews.csv` and persist embeddings):

```zsh
python3 vector.py
```

- Run the example chain in `main.py`:

```zsh
python3 main.py
```

**Configuration & Notes**
- Model names are currently hard-coded in `main.py` (`llama3.2`) and `vector.py` (`mxbai-embed-large`). If Ollama lists different model names on your machine, update those strings or pull the matching models.
- The urllib3 LibreSSL warning shown earlier is informational — it indicates the system SSL (LibreSSL) is older than the version urllib3 expects. It doesn't prevent the code from running but you can address it by using a Python/OpenSSL build with OpenSSL 1.1.1+.
- The Chroma DB persists to `./chrome_langchain_db`. Delete that folder to force re-embedding.

**Troubleshooting**
- If you see an Ollama ResponseError like `model '<name>' not found`, run `ollama list` and either change the model name in the code or run `ollama pull <name>` to download it.
- If you encounter package import errors, make sure your virtualenv is activated and the required packages are installed into it.

If you want, I can also:
- create a `requirements.txt` with suggested pins, or
- update `main.py` and `vector.py` to read model names from environment variables for easier configuration.
