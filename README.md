# CrewAI Email & Marketing Crews

This repository contains a collection of examples and projects for building teams of AI agents using [CrewAI](https://www.crewai.com/). It covers the journey from basic single-agent email automation to full multi-agent marketing crews configured via YAML.

## Prerequisites

- Python 3.10+
- A Gemini API key (used for the `gemini/gemini-3.6-flash` model)
- A Serper API key (used by `SerperDevTool` for web search)

## Setup

```bash
# Create and activate a virtual environment
python -m venv .venv
.venv\Scripts\activate   # Windows

# Install dependencies
pip install -r requirements.txt

# Configure your API keys
# Copy the example below into a .env file
# GOOGLE_API_KEY=your_gemini_api_key
# SERPER_API_KEY=your_serper_api_key
```

> Note: The `.env` file is ignored by git. Create it locally with your keys.

## Project Structure

```
├── 1_email_agent.ipynb            # Single email-writing agent
├── 2_email_agent_with_tool.ipynb  # Email agent using a tool
├── 3_crew.ipynb                   # Intro to multi-agent crews
├── 4_crew_with_tools.ipynb        # Crew with agents+tools
├── 5_yaml.py                      # Blog crew configured via YAML
├── main.py                        # Simple script entry point
├── config/
│   ├── agents.yaml                # Agent definitions (blog crew)
│   └── tasks.yaml                 # Task definitions (blog crew)
├── marketing-crew/
│   ├── crew.py                    # Full marketing crew definition
│   └── config/
│       ├── agents.yaml            # Marketing agents
│       └── tasks.yaml             # Marketing tasks
└── requirements.txt
```

## Notebooks

The notebooks build understanding incrementally:

1. **1_email_agent.ipynb** – A single agent that writes a professional email.
2. **2_email_agent_with_tool.ipynb** – Extends the email agent with a tool (e.g. web search).
3. **3_crew.ipynb** – Introduces a crew of multiple agents collaborating on tasks.
4. **4_crew_with_tools.ipynb** – A crew where agents make use of tools.

## Blog Crew (5_yaml.py)

A two-agent crew (researcher + writer) that produces a short blog post about any topic.

```bash
python 5_yaml.py
```

The behavior is defined entirely in YAML:

- `config/agents.yaml` – researcher and writer agents
- `config/tasks.yaml` – research and blog-writing tasks

The topic can be changed in `5_yaml.py:58` (the `inputs={"topic": ...}` argument).

## Marketing Crew (marketing-crew/)

A production-style crew of four agents that plans and executes a marketing campaign for a product:

- **Head of Marketing** – market research and strategy
- **Content Creator (Social Media)** – social posts, reels, email drafts
- **Content Writer (Blogs)** – blog research and drafting
- **SEO Specialist** – SEO optimization of final blogs

```bash
python marketing-crew/crew.py
```

Inputs (product name, description, target audience, budget, current date) are set in `marketing-crew/crew.py:180`. Generated drafts are saved under `resources/drafts/` in markdown format. Structured outputs (posts, reels, blogs, SEO content) follow the `Content` Pydantic model defined in `crew.py`.

## License

This project is for educational purposes. See the individual dependencies for their respective licenses.
