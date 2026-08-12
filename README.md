# LangChain Demo Applications

This project contains two simple LangChain examples:

- `app(3).py`: a Streamlit question-answering interface that uses the local Ollama `gemma:2b` model.
- `Simpleapp.ipynb`: a retrieval-augmented generation (RAG) notebook that loads a webpage, splits its content, stores OpenAI embeddings in FAISS, and answers questions with an OpenAI chat model.

Link: https://ueacqz2cgadvg9hlxky5yy.streamlit.app/


## Requirements

- Python 3.10–3.12
- `pip`
- An OpenAI API key for the notebook
- [Ollama](https://ollama.com/) and the `gemma:2b` model for the Streamlit app

## Installation

Create and activate a virtual environment:

```bash
python -m venv .venv
source .venv/bin/activate
```

On Windows PowerShell, activate it with:

```powershell
.venv\Scripts\Activate.ps1
```

Install the Python dependencies:

```bash
pip install -r requirements.txt
```

## Environment variables

Create a `.env` file in the project directory. Add only the variables required by the example you want to run:

```env
OPENAI_API_KEY=your_openai_api_key
LANGCHAIN_API_KEY=your_langsmith_api_key
LANGCHAIN_PROJECT=your_project_name
```

`OPENAI_API_KEY` is required by the notebook. The LangSmith variables are optional if you do not need tracing; the supplied code currently enables tracing.

Do not commit the `.env` file or expose real API keys publicly.

## Run the Streamlit app

Install Ollama, download the model, and confirm that Ollama is running:

```bash
ollama pull gemma:2b
```

Start the application:

```bash
streamlit run "app(3).py"
```

Open the local address shown by Streamlit, enter a question, and the local Gemma model will generate the answer.

## Run the RAG notebook

Start Jupyter from the project directory:

```bash
jupyter notebook "1.2.1-Simpleapp.ipynb"
```

Run the cells in order. The notebook will:

1. Load environment variables.
2. retrieve content from a LangSmith documentation webpage.
3. split the content into overlapping chunks.
4. create OpenAI embeddings and store them in a FAISS vector index.
5. retrieve relevant chunks and use an OpenAI chat model to answer a question.

The notebook accesses an external webpage and the OpenAI API, so an internet connection is required.

## Project files

```text
.
├── app(3).py
├── 1.2.1-Simpleapp.ipynb
├── requirements.txt
└── README.md
```

## Troubleshooting

- **Ollama connection error:** start the Ollama service and verify that `gemma:2b` appears in `ollama list`.
- **Missing API key:** check that `.env` exists in the same directory and contains the correct variable name.
- **FAISS installation error:** use a supported 64-bit Python version, preferably Python 3.10–3.12, in a fresh virtual environment.
- **Web loader warning or empty content:** confirm that the target webpage is reachable and still allows automated loading.
