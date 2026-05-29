# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

This is a **Microsoft Learn educational repository** containing structured labs for teaching generative AI development using Microsoft Foundry (Azure AI Studio) and Azure OpenAI. The primary content is exercise instructions in Markdown; the Python labfiles are **intentionally stubbed** — students fill in the implementation as part of the exercise.

## Project Structure

- `Instructions/Exercises/` — Markdown lab instructions (the primary teaching material)
- `Instructions/media/` — Screenshots referenced by exercises
- `labfiles/foundry-chat/python/chat-app/` — Chat application starter code (Exercise 03)
- `labfiles/tools/python/tools-app/` — RAG/tools application starter code (Exercise 04a)
- `data/` — JSONL/CSV datasets for fine-tuning and evaluation exercises
- `generate_lab_catalog.py` — Utility script that parses all exercise `.md` files and outputs `lab_catalog.csv`

## Running the Lab Applications

Each labfile is a standalone Python app. The pattern is the same for both:

```powershell
cd labfiles\foundry-chat\python\chat-app   # or labfiles\tools\python\tools-app
python -m venv venv
.\venv\Scripts\Activate.ps1
pip install -r requirements.txt
# Edit .env with your Azure OpenAI endpoint and model deployment name
python chat-app.py
```

**Python version**: 3.13 is required; Python 3.14 is not yet supported by the dependencies.

### Environment Variables

Both apps use a `.env` file (already present as a template):

```
AZURE_OPENAI_ENDPOINT="your_azure_openai_endpoint"
MODEL_DEPLOYMENT="your_model_deployment"
```

Authentication uses `azure-identity` (Entra ID). No API keys are needed if the user is logged in via Azure CLI.

## Regenerating the Lab Catalog

```powershell
python generate_lab_catalog.py
```

This scans all `.md` files under `Instructions/`, extracts YAML frontmatter and technology mentions, and overwrites `lab_catalog.csv`.

## Documentation Site

The `Instructions/` content is published as a GitHub Pages site via Jekyll. The build uses `_build.yml` (Azure DevOps pipeline) and the `MicrosoftLearning/Jekyll-Theme` remote theme. There is no local Jekyll build command configured for this repo.

## Architecture Notes

- There is no test suite, linting configuration, or CI beyond the Azure DevOps documentation build.
- The labfile Python code is meant to be incomplete. When editing these files, preserve the stub comments that guide students through the exercise steps.
- Exercise numbering skips (01, 02, 03, 04a, 04b, 06) — this is intentional; not all exercises from the broader Learn path live in this repo.
- All exercises assume a deployed **GPT-4.1** model on Microsoft Foundry.
