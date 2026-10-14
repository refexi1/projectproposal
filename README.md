# Cycle The Right Way

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
AI can turn the assignment to more understandable form for the students

## Solution

Develop an AI-appliation, that helps students with their study material

## Main user workflow

1. **User Input:** User downloads the material into the application
2. **Processing & Guardrails:** The Application's AI will analyze the text or file. RAG will be utilized to search the right spots for the questions.
3. **Model Response:** Language model will

## Architecture

Below is the initial starter architecture. As your project evolves with additional capabilities, replace or extend this diagram in [`docs/architecture.md`](docs/architecture.md).

```text
User
  ↓
Gradio UI (app/ui.py)
  ↓
Application / AI Service (src/services/ai_service.py)
  ↓
Model Client (src/models/model_client.py)
  ↓
Ollama (Local LLM Server)
```

> **Core Architectural Rule:** The user interface must NEVER communicate directly with the model client or Ollama. All interactions must pass through the service layer (`ai_service.py`).

## Model

- **Model used:** e.g., `llama3.2` (or specified local Ollama model)
- **Selection rationale:** Why was this specific model chosen for your project (e.g., lightweight, performance, context size)?

## Additional AI capability

Select at least one additional capability to implement for your final project:

- [ ] RAG (Retrieval-Augmented Generation)
- [ ] Tools / External API integration
- [ ] Model Context Protocol (MCP)
- [ ] Agentic workflow (Model-selected actions based on observations)
- [ ] Memory / Persistent state
- [x] Multimodal interaction (Text + Images)
- [ ] Other: ______________________

### Capability justification
Explain why the selected capability is useful and necessary for your application's user problem.

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

Correctly recognizing the object from test images (e.g., milk carton, battery, plastic bottle or cardboard box).
Successfully identifying multi-part materials (e.g., glass bottle with a metal cap).
Correctly identifying dangerous items (batteries, electronics, chemicals) and directing them to special collection points rather than general waste.

Refer to [`evaluation/README.md`](evaluation/README.md) for guidelines on defining success, edge cases, and failure scenarios.

## Known limitations


- The AI may incorrectly recognize some waste items.
- Similar-looking materials can be difficult to classify correctly.
- Image quality, lighting, and camera angle may affect recognition accuracy.
- Recycling instructions may vary depending on the user's location.

## Future improvements

- Add support for more waste categories.
- Provide recycling instructions based on the user's location.
- Improve the user interface to make the application easier to use.


