# ResearchMind

A multi-agent research system that searches the web, extracts relevant source material, writes a structured research report, and critiques the result before returning a polished final output.

Built with Python, LangChain, OpenAI, Tavily, and Streamlit, this project demonstrates how specialized agents can collaborate across a complete research workflow.

## Overview

This project is designed around a multi-step research pipeline:

- Search Agent: finds recent, reliable information on a topic
- Reader Agent: selects a promising URL and scrapes the content for deeper context
- Writer Chain: transforms the gathered research into a detailed report
- Critic Chain: reviews the generated report and provides structured feedback

The repository includes both:
- a Streamlit web app for interactive research sessions
- a Python pipeline for running the workflow from the terminal

## Features

- Multi-agent research workflow
- Web search using Tavily
- URL scraping with BeautifulSoup
- LLM-powered writing and critique stages
- Streamlit dashboard with progress tracking
- Downloadable Markdown research report
- CLI-based pipeline execution

## Tech Stack

- Python 3.10+
- LangChain
- LangChain OpenAI
- OpenAI GPT models
- Tavily Search API
- BeautifulSoup
- Requests
- Streamlit
- python-dotenv

## Repository Structure

```text
.
├── agents.py          # Agent definitions, writer/critic chains, prompts
├── app.py             # Streamlit web application
├── pipeline.py        # Terminal-based research pipeline
├── tools.py           # Search and scraping tools
├── requirements.txt   # Python dependencies
├── .gitignore         # Git ignore rules
├── README.md          # Project documentation
└── __pycache__/       # Generated Python cache files
```

## Prerequisites

Before running the project, make sure you have:

- Python 3.10 or newer
- An OpenAI API key
- A Tavily API key
- Internet access for search and scraping

## Setup

1. Clone the repository:

```bash
git clone https://github.com/AkarshVyas/Multi-agent-research-system.git
cd Multi-agent-research-system
```

2. Create and activate a virtual environment:

```bash
python -m venv .venv
source .venv/bin/activate    # macOS/Linux
# or
.venv\Scripts\activate       # Windows
```

3. Install dependencies:

```bash
pip install -r requirements.txt
```

4. Create a `.env` file in the project root and add your keys:

```env
OPENAI_API_KEY=your_openai_api_key
TAVILY_API_KEY=your_tavily_api_key
```

The project uses `python-dotenv`, so values are automatically loaded from this file.

## Running the Streamlit App

Start the app with:

```bash
streamlit run app.py
```

Then open the local URL displayed in the terminal, typically:

```text
http://localhost:8501
```

Once the app opens:

- enter a research topic
- click the run button
- wait for the search, scrape, write, and critique stages to complete

## Running the CLI Pipeline

You can also run the workflow directly from the terminal:

```bash
python pipeline.py
```

When prompted, enter a research topic such as:

```text
Quantum computing breakthroughs in 2025
```

## How the Workflow Works

The system is built around a few core components:

- `build_search_agent()` creates a search agent with access to the Tavily web search tool
- `build_reader_agent()` creates a reader agent with access to the URL scraping tool
- `writer_chain` converts research findings into a polished structured report
- `critic_chain` reviews the report and returns a score plus suggestions

The `tools.py` file defines the reusable tools used throughout the workflow:

```python
@tool
def web_search(query: str) -> str:
    ...

@tool
def scrape_url(url: str) -> str:
    ...
```

These tools let the agents gather and interpret information from the web before generating the final output.

## Example Output

The writer chain produces a report in a structure like:

- Introduction
- Key Findings
- Conclusion
- Sources

The critic then returns feedback in this format:

```text
Score: 8/10

Strengths:
- Clear structure
- Relevant findings
- Good synthesis of sources

Areas to Improve:
- Add more recent citations
- Expand the technical depth
- Include counterarguments where relevant

One line verdict:
Strong and readable research summary with room for more evidence depth.
```

## Notes

- This project relies on external APIs and internet connectivity.
- Scraped content is intentionally trimmed for readability and token efficiency.
- Report quality depends on the model, source quality, and reliability of the web tools.
- This is best suited for experimentation, research automation demos, and educational multi-agent systems.

## Future Improvements

Potential enhancements include:

- source citation tracking
- processing multiple URLs instead of a single scraped page
- better relevance filtering and ranking
- structured JSON output alongside markdown
- agent memory and iterative refinement loops

## License

This repository does not currently include an explicit license file. If you plan to reuse or redistribute the project, confirm the licensing terms before publishing or distributing it.