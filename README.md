# Ask-the-Web Agent 🤖🔍

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.11+](https://img.shields.io/badge/python-3.11+-blue.svg)](https://www.python.org/downloads/)
[![Jupyter Notebook](https://img.shields.io/badge/jupyter-notebook-orange.svg)](https://jupyter.org/)

Build a **Perplexity-style web search agent** from scratch. Learn how LLMs use tools, implement tool-calling patterns, and create autonomous agents that reason and act in real-time.

## 📖 Overview

This project is an **end-to-end educational tutorial** that guides you from foundational concepts to a production-ready web search agent. Instead of abstracting away complexity, we build each layer step-by-step, so you deeply understand how modern AI agents work.

### What You'll Build

A sophisticated agent that:
- ✅ Understands when to search the web
- ✅ Executes web searches via DuckDuckGo
- ✅ Reads and summarizes content
- ✅ Reasons over results to answer complex queries
- ✅ Runs entirely on **local open-source models** (no API keys)

## 🎯 Learning Objectives

By the end of this project, you'll understand:

| Objective | Section |
|-----------|---------|
| Why tool calling matters for AI agents | 1 |
| How to implement manual tool-calling loops | 1-2 |
| JSON schema-based tool definitions | 2 |
| LangChain's ReAct (Reasoning + Acting) pattern | 3 |
| Building multi-tool agents | 4 |
| Connecting to external tool servers (MCP) | 5 |
| Creating conversational interfaces with Chainlit | 6 |

## 🗺️ Project Roadmap

The notebook is organized into 6 progressive sections:

### **Section 0: Environment Setup**
Configure your development environment with Ollama, Python dependencies, and Jupyter kernel registration.

### **Section 1: Tool Calling Fundamentals**
- Implement a simple `get_current_weather()` function
- Teach an LLM to invoke it using structured prompts
- Parse model outputs and execute functions
- **Key Insight:** Manual tool calling works with any model

### **Section 2: Standardize Tool Calling with JSON Schemas**
- Auto-generate JSON schemas from function signatures
- Dynamically provide tool definitions to the LLM
- Scale from 1 tool to many tools without changing the prompt
- **Key Insight:** Function signatures + docstrings = scalable tools

### **Section 3: LangChain for Tool Calling**
- Understand model capability requirements (1B vs 3B+ parameters)
- Use LangChain's `create_agent()` for ReAct patterns
- Explore why larger models support native tool calling
- **Key Insight:** LangChain automates the tool-calling loop

### **Section 4: Build a Web Search Agent** ⭐
- Implement a `search_web()` tool using DuckDuckGo
- Create a fully functional web search agent
- Test with real-world queries
- **Key Insight:** Combine reasoning with real-world data

### **Section 5: MCP — Model Context Protocol** (Optional)
- Connect to external tool servers
- Use `mcp-server-fetch` to retrieve webpage content
- Understand the future of LLM-tool integration
- **Key Insight:** Tools as microservices

### **Section 6: Web UI with Chainlit** (Optional)
- Build a conversational interface
- Stream agent responses in real-time
- Visualize tool execution steps
- **Key Insight:** Move from notebook to production

## 🚀 Quick Start

### Prerequisites

- **Python 3.11+**
- **Ollama** (for local LLM inference)
- **Conda** or **uv** (for environment management)
- **Jupyter Notebook** (included in dependencies)

### Installation

#### Option 1: Conda (Recommended)

```bash
# Clone the repository
git clone https://github.com/poonamjagwani/ask-the-web-agent.git
cd ask-the-web-agent

# Create and activate environment
conda env create -f environment.yaml
conda activate web_agent

# Register Jupyter kernel
python -m ipykernel install --user --name=web_agent --display-name "web_agent"
```

#### Option 2: UV (Faster Alternative)

```bash
# Clone the repository
git clone https://github.com/poonamjagwani/ask-the-web-agent.git
cd ask-the-web-agent

# Create virtual environment and install dependencies
uv venv .venv --python 3.11
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
uv pip install -r requirements.txt
```

### Setup Ollama

1. **Install Ollama** from [ollama.com](https://ollama.com)

2. **Start the Ollama server** in a separate terminal:
   ```bash
   ollama serve
   ```

3. **Pull the models** we'll use:
   ```bash
   ollama pull gemma3:1b      # ~1B parameters, fast
   ollama pull llama3.2:3b    # ~3B parameters, tool-calling capable
   ```

   💡 Explore more models: https://ollama.com/library

### Run the Notebook

1. **Open Jupyter:**
   ```bash
   jupyter notebook
   ```

2. **Open `ask_the_web_agent.ipynb`** and select the `web_agent` kernel

3. **Follow the sections sequentially** — each builds on the previous

## 📊 Key Concepts

### Tool Calling Flow

```
┌─────────────────┐
│   User Query    │
└────────┬────────┘
         │
         ▼
┌─────────────────────────────────────┐
│  LLM (with tool descriptions)       │
│  - Reasons about the query          │
│  - Decides which tools to use       │
└────────┬────────────────────────────┘
         │
         ▼
┌─────────────────────────────────────┐
│  Parser                             │
│  - Extract tool name and arguments  │
│  - Validate against schema          │
└────────┬────────────────────────────┘
         │
         ▼
┌─────────────────────────────────────┐
│  Execute Tool                       │
│  - Call function with arguments     │
│  - Get result                       │
└────────┬────────────────────────────┘
         │
         ▼
┌─────────────────────────────────────┐
│  Feed Result Back to LLM            │
│  - Continue reasoning               │
│  - Generate final answer            │
└────────┬────────────────────────────┘
         │
         ▼
┌─────────────────┐
│  Final Answer   │
└─────────────────┘
```

### Model Capability Matrix

| Model | Size | Native Tool Support | Use Case |
|-------|------|---------------------|----------|
| `gemma3:1b` | 1B | ❌ No | Manual tool calling only |
| `llama3.2:1b` | 1B | ❌ No | Manual tool calling only |
| `llama3.2:3b` | 3B | ✅ Yes | LangChain agents |
| `gemma3` | 4B | ✅ Yes | Production agents |
| `mistral` | 7B | ✅ Yes | Complex reasoning |

## 📚 What's Included

```
ask-the-web-agent/
├── ask_the_web_agent.ipynb     # Main tutorial (830+ cells)
├── environment.yaml             # Conda environment spec
├── requirements.txt             # Pip dependencies
├── assets/
│   ├── tools.png               # Tool calling visualization
│   ├── tool_flow.png           # Execution flow diagram
│   └── react.png               # ReAct pattern illustration
└── README.md                    # This file
```

### Notebook Statistics

- **830+ code and markdown cells**
- **6 complete sections** (0-6)
- **12+ working code examples**
- **Extensive comments and docstrings**
- **Progressive complexity** (manual → automated)

## 🛠️ Technology Stack

### Core Dependencies

| Package | Purpose | Version |
|---------|---------|---------|
| `langchain` | Agent orchestration | 1.2.7+ |
| `langgraph` | ReAct agent framework | 1.0.7+ |
| `langchain-ollama` | Ollama integration | 1.0.1+ |
| `ddgs` | DuckDuckGo search | 9.10.0+ |
| `openai` | OpenAI SDK (Ollama compatible) | 2.15.0+ |

### Optional Extensions

| Package | Purpose | Version |
|---------|---------|---------|
| `chainlit` | Web UI framework | 2.9.6+ |
| `mcp` | Model Context Protocol | 1.26.0+ |
| `langchain-mcp-adapters` | MCP ↔ LangChain bridge | 0.2.1+ |

## 💡 Key Insights

### 1. **Tool Calling is Essential**
LLMs are powerful but bound by their training data cutoff and computational limits. Tool calling lets them leverage external resources—APIs, databases, web searches—in real-time.

### 2. **Scalability Through Schemas**
Instead of hardcoding tool descriptions, extract them from function signatures. This scales linearly with new tools.

### 3. **Not All Models Can Call Tools**
Models under 3B parameters typically lack native tool-calling capability. Smaller models still work—just with manual parsing.

### 4. **Reasoning + Acting = Agents**
The ReAct pattern (Reasoning + Acting) enables agents to think before acting, which is more reliable than simple function calling.

### 5. **Local Models = Privacy + Cost**
Ollama lets you run capable open-source models locally. No API keys, no data leakage, no per-token costs.

## 🔬 Example Usage

Once you've completed the notebook, you can use the web search agent like this:

```python
from langchain_ollama import ChatOllama
from langchain.agents import create_agent
from ddgs import DDGS
from langchain_core.tools import tool

# Define search tool
@tool
def search_web(query: str) -> str:
    """Search the web using DuckDuckGo."""
    results = DDGS().text(query, max_results=3)
    return "\n".join([f"Title: {r['title']}\nURL: {r['href']}\nBody: {r['body']}" 
                      for r in results])

# Create agent
llm = ChatOllama(model="llama3.2:3b", temperature=0)
tools = [search_web]
agent = create_agent(
    model=llm,
    tools=tools,
    system_prompt="You are a helpful assistant that answers questions by searching the web."
)

# Ask a question
result = agent.invoke({
    "messages": [("user", "What are the latest developments in AI safety?")]
})
print(result["messages"][-1].content)
```

## 🎓 Who Is This For?

- **AI/ML Students** — Understand agent architectures from first principles
- **LLM Enthusiasts** — Learn modern tool-calling patterns
- **Python Developers** — Build production agents without external APIs
- **Educators** — Use this as a reference for teaching agent concepts

## 🤝 Contributing

Contributions are welcome! Areas for enhancement:

- [ ] Additional example agents (news aggregator, research assistant, etc.)
- [ ] Integration with more search backends (Google, Bing, etc.)
- [ ] Performance benchmarks across different models
- [ ] Deployment guides (Docker, serverless, etc.)
- [ ] Advanced topics (caching, memory, multi-turn reasoning)

## 📖 Additional Resources

### Official Documentation
- [LangChain Agents](https://docs.langchain.com/oss/python/langchain/agents)
- [LangChain Tools](https://docs.langchain.com/oss/python/langchain/tools)
- [Ollama Documentation](https://github.com/ollama/ollama)
- [Model Context Protocol](https://modelcontextprotocol.io/)
- [Chainlit Docs](https://docs.chainlit.io/)

### Related Articles & Papers
- [ReAct: Synergizing Reasoning and Acting in Language Models](https://arxiv.org/abs/2210.03629)
- [Tool Learning with Foundation Models](https://arxiv.org/abs/2304.08354)
- [OpenAI Function Calling](https://platform.openai.com/docs/guides/function-calling)

### Communities
- [LangChain Discord](https://discord.gg/6adMQxSpJS)
- [Ollama Discussions](https://github.com/ollama/ollama/discussions)
- [AI/ML Reddit Communities](https://www.reddit.com/r/MachineLearning/)

## ⚠️ Troubleshooting

### "Ollama is not running"
**Solution:** Start Ollama in a separate terminal with `ollama serve`, then try again.

### "Model not found" error
**Solution:** Download the model first:
```bash
ollama pull llama3.2:3b
```

### Kernel not found in Jupyter
**Solution:** Register the kernel:
```bash
python -m ipykernel install --user --name=web_agent --display-name "web_agent"
```

### Out of memory errors
**Solution:** Use a smaller model (e.g., `llama3.2:1b`) or reduce `max_results` in search queries.

## 📝 License

This project is licensed under the **MIT License** — see [LICENSE](LICENSE) for details.

## 🙏 Acknowledgments

- Built with [LangChain](https://github.com/langchain-ai/langchain)
- Powered by [Ollama](https://ollama.com)
- Inspired by [Perplexity AI](https://www.perplexity.ai/)
- Uses [DuckDuckGo](https://duckduckgo.com) for web search

## 📧 Contact & Support

- **Author:** [@poonamjagwani](https://github.com/poonamjagwani)
- **Issues:** [GitHub Issues](https://github.com/poonamjagwani/ask-the-web-agent/issues)
- **Discussions:** [GitHub Discussions](https://github.com/poonamjagwani/ask-the-web-agent/discussions)

---

**Happy learning! 🚀**

*Questions about agents? Open an issue or start a discussion—we're here to help!*