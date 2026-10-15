# Studyhelper

Starter template for the **Development of AI Applications** course final group project.

## Team members

- YASER AL-DALAWI (yaser.al-dalawi@student.hamk.fi)
- Vesa Wahlström (vesa.wahlstrom@student.hamk.fi)
- Nuutti Tikka (nuutti.tikka@student.hamk.fi)
- Sanna Poikonen (sanna.poikonen@student.hamk.fi)

## Problem

### Intended users
Students who would need assistance with study material and understand it better

### Problem statement
Providing AI-assistance on study material, the material has to be inputted for the AI to analyze it(PDF for example)

### Why AI is appropriate
AI can summarize large amounts of text, explain difficult concepts in simpler terms, 

## Solution

Develop a user-friendly AI application (AI Study Assistant) that helps students learn better. Users can upload PDF study materials, generate summaries and ask questions about the content

## Main user workflow

1. **User Input:** The user uploads a PDF study document or pastes text into the application.
2. **Processing & Guardrails:** The application reads and processes the text. RAG (Retrieval-Augmented Generation) searches the uploaded material for relevant information.
3. **Model Response:** The language model creates an answer and provides source references showing where the information was found in the text.

## Architecture

Below is the initial starter architecture. As your project evolves with additional capabilities, replace or extend this diagram in [`docs/architecture.md`](docs/architecture.md).

```text
User
  ↓
Gradio UI (app/ui.py)
  ↓
Application / AI Service (src/services/ai_service.py)
  ↓
Model Client / RAG (src/models/model_client.py)
  ↓
Ollama/RAG Database (Local LLM Server)
```

> **Core Architectural Rule:** The user interface must NEVER communicate directly with the model client or external APIs. All interactions must pass through the service layer (`ai_service.py`).

## Model

- **Model used:** LLM API or Ollama model like llama3.2
- **Selection rationale:** Chosen for its good context window, reliability in summarizing long text, and ability to generate accurate source references.

## Additional AI capability

Select at least one additional capability to implement for your final project:

- [x] RAG (Retrieval-Augmented Generation)
- [ ] Tools / External API integration
- [ ] Model Context Protocol (MCP)
- [ ] Agentic workflow (Model-selected actions based on observations)
- [ ] Memory / Persistent state
- [] Multimodal interaction (Text + Images)
- [ ] Other: ______________________

### Capability justification
RAG is necessary to ensure the AI answers questions based strictly on the uploaded study material without making up information (hallucinating). It allows the app to find specific sections in the document and show clear references to the student.

## Setup

### 1. Create the Conda environment

```bash
conda env create -f environment.yml
```

### 2. Activate the environment

```bash
conda activate dev-ai-project
```

### 3. Configure environment variables

Copy `.env.example` to create your local `.env` configuration file:

On Linux / macOS:
```bash
cp .env.example .env
```

On Windows (Command Prompt / PowerShell):
```powershell
copy .env.example .env
```

Ensure `.env` contains valid values for `OLLAMA_BASE_URL` and `MODEL_NAME`:
```env
OLLAMA_BASE_URL=http://localhost:11434
MODEL_NAME=llama3.2
```

### 4. Start Ollama

Make sure Ollama is installed and running locally, then pull your configured model:

```bash
ollama run llama3.2
```

### 5. Run the application

Run the application from the root directory of the project:

```bash
python -m app.main
```

Then open your browser at `http://localhost:7860`.

### 6. Run automated tests

```bash
pytest
```

## Evaluation

Check that the application reads PDF files correctly and handles errors (e.g., broken files or API issues).
Evaluate answer accuracy by checking if the RAG search finds the right parts of the document and provides accurate source references.

Refer to [`evaluation/README.md`](evaluation/README.md) for guidelines on defining success, edge cases, and failure scenarios.

## Known limitations


- Splitting and indexing very large PDF files might take time.
- The model may struggle if the uploaded PDF contains low-quality or poorly formatted text.


## Future improvements

- Add automatic practice question generation.
- Support saving chat history and student notes.


