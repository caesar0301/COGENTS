# COGENTS

**COGENTS: Towards COGnitive aGENTic System**

A comprehensive, modular ecosystem for building intelligent, cognitive agent systems. COGENTS provides foundational abstractions, specialized toolkits, intelligent agents, and powerful search & automation capabilities—all designed to work together seamlessly.

---

## 🎯 Vision

COGENTS is an initiative to develop a cognitive, computation-driven agentic system that combines theoretical foundations with practical implementations. The project emphasizes:

- **Modular Architecture**: Build systems with composable, reusable components
- **Cognitive Design**: Agent systems grounded in multi-agent system (MAS) philosophy
- **Production-Ready**: Battle-tested tools and agents for real-world applications
- **Extensible Framework**: Easy integration and customization for diverse use cases

---

## 🏗️ Architecture

COGENTS is organized into five interconnected subprojects, each addressing a specific aspect of cognitive agent development:

```
COGENTS
├── cogents-core          # Foundational abstractions & core modules (BASE)
├── cogents-smith         # Toolkits ecosystem & production agents
├── cogents-browser-use   # AI-powered browser automation
├── wizsearch             # Multi-engine search orchestration
└── wizagent              # Web automation & research framework
```

---

## 📦 Subprojects

### 1. cogents-core 🧠 **(BASE)**

[![PyPI version](https://img.shields.io/pypi/v/cogents-core.svg)](https://pypi.org/project/cogents-core/)
[![Ask DeepWiki](https://deepwiki.com/badge.svg)](https://deepwiki.com/caesar0301/cogents-core)

**The foundational layer providing core abstractions and essential modules for all COGENTS projects.**

#### Core Abstractions
- **Agent**: Base classes for building custom agents (BaseAgent, BaseGraphicAgent, BaseConversationAgent, BaseResearcher)
- **Goal Management**: Goal decomposition, conflict detection, and dynamic replanning (Goalith)
- **Tool Management**: Centralized tool registry, execution engine, and repository system (Toolify)
- **Memory Management**: Persistent memory capabilities (under development)
- **Orchestration**: Global orchestration system (under development)

#### Key Features
- **Multi-Model LLM Support**: OpenAI, Google GenAI, Ollama, LlamaCPP with dynamic routing
- **Advanced Routing**: Complexity-based and self-assessment routing strategies
- **Observability**: Built-in token tracking and Opik tracing integration
- **Message Bus**: Inter-agent communication system
- **Extensible Design**: Easy to add new providers and capabilities

```bash
pip install -U cogents-core
```

**Use Cases**: Building custom agents, goal-oriented planning, tool integration, LLM management

---

### 2. cogents-smith 🔨

[![PyPI version](https://img.shields.io/pypi/v/cogents-smith.svg)](https://pypi.org/project/cogents-smith/)
[![Ask DeepWiki](https://deepwiki.com/badge.svg)](https://deepwiki.com/caesar0301/cogents-smith)

**Extensive toolkit ecosystem and production-ready agents built on cogents-core.**

#### Toolkit Ecosystem (18 Specialized Toolkits in 10 Semantic Groups)
- **Academic Research**: arXiv integration for paper discovery and analysis
- **Development Tools**: Bash, file editing, GitHub, Python execution
- **Media Processing**: Image analysis, video processing, audio transcription
- **Information Retrieval**: Wikipedia, web search, knowledge extraction
- **Data Management**: Tabular data, memory systems, document handling
- **Communication**: Gmail integration
- **Human Interaction**: User communication and feedback collection

#### Production-Ready Agents
- **Askura Agent**: Dynamic conversational agent for structured information collection
- **Seekra Agent**: Deep research agent for comprehensive topic investigation and report generation

#### Architecture Features
- **Semantic Organization**: Intuitive grouping for easy discovery
- **Lazy Loading**: Load only what you need
- **Async-First Design**: High-performance concurrent operations
- **Error Resilience**: Graceful handling of missing dependencies

```bash
pip install -U cogents-smith
```

**Use Cases**: Rapid agent development, conversational data collection, deep research, multi-modal processing

---

### 3. cogents-browser-use 🌐

[![PyPI version](https://img.shields.io/pypi/v/cogents-browser-use.svg)](https://pypi.org/project/cogents-browser-use/)

**AI-powered browser automation adapted from browser-use on the COGENTS stack.**

#### Features
- Natural language browser control
- Intelligent web navigation
- Automated interaction with web elements
- Built on COGENTS core abstractions
- Support for headless and headed modes

```bash
pip install -U cogents-browser-use
```

**Use Cases**: Web scraping, automated testing, data extraction, web interaction automation

---

### 4. wizsearch 🔍

[![PyPI version](https://img.shields.io/pypi/v/wizsearch.svg)](https://pypi.org/project/wizsearch/)

**Unified Python library for searching across multiple search engines with a consistent interface.**

#### Features
- **Multiple Search Engines**: Baidu, Bing, Brave, DuckDuckGo, Google, Google AI, SearxNG, Tavily, WeChat
- **Unified Interface**: Single API with consistent `SearchResult` format
- **Multi-Engine Aggregation**: Concurrent searches with round-robin result merging
- **Page Crawling**: Built-in web page content extraction using Crawl4AI
- **Semantic Search**: Optional vector-based semantic search with local storage
- **Full Async/Await Support**: High-performance asynchronous operations

```bash
pip install -U wizsearch
```

**Use Cases**: Multi-source search, web content aggregation, semantic search, research automation

---

### 5. wizagent 🧙

[![PyPI version](https://img.shields.io/pypi/v/wizagent.svg)](https://pypi.org/project/wizagent/)

**Powerful web automation and research framework combining multi-engine search, deep research, browser automation, and structured data extraction.**

#### Core Capabilities
- **Multi-Engine Web Search**: Simultaneous search across multiple engines (Tavily, DuckDuckGo, Google AI, SearXNG, Brave, Baidu, WeChat)
- **Deep Research Agent**: Autonomous research with iterative query refinement and source aggregation
- **Browser Automation**: Intelligent browser control with natural language instructions (via cogents-browser-use)
- **Structured Data Extraction**: Extract data from websites using Pydantic models
- **YAML-Based Schema Parser**: Define data models declaratively with the Gem Parser
- **LangGraph Workflows**: Advanced agent orchestration with state management

#### Architecture Stack
Built on cogents-core, cogents-browser-use, wizsearch, LangGraph, and Pydantic for a complete web intelligence solution.

```bash
pip install -U wizagent
```

**Use Cases**: Market research, competitive analysis, web data extraction, automated web intelligence gathering

---

## 💡 Example Use Cases

### Building a Custom Research Agent

Combine cogents-core, cogents-smith, and wizsearch:

```python
from cogents_core.base import BaseResearcher
from cogents_smith.groups import info_retrieval
from wizsearch import WizSearch

class MyResearchAgent(BaseResearcher):
    def __init__(self):
        super().__init__()
        self.search = WizSearch()
        self.tools = info_retrieval()
    
    async def research(self, topic: str):
        # Use multi-engine search
        results = await self.search.search(topic)
        # Process with LLM
        analysis = await self.llm_client.completion([
            {"role": "user", "content": f"Analyze: {results}"}
        ])
        return analysis
```

### Web Intelligence Gathering

Use wizagent for comprehensive web intelligence:

```python
from wizagent import WizAgent

agent = WizAgent()

# Multi-engine search
search_results = await agent.search(
    query="AI trends 2025",
    max_results_per_engine=5
)

# Deep research
research = await agent.research(
    instruction="Latest quantum computing developments"
)

# Browser automation with data extraction
data = await agent.navigate_and_extract(
    url="https://example.com",
    instruction="Extract key metrics",
    schema=MyDataSchema
)
```

### Conversational Agent with Tools

Use cogents-smith's Askura agent with custom tools:

```python
from cogents_smith.agents.askura_agent import AskuraAgent
from cogents_smith.agents.askura_agent.models import AskuraConfig, InformationSlot

config = AskuraConfig(
    information_slots=[
        InformationSlot(
            name="user_preferences",
            description="User's preferences and requirements",
            required=True
        )
    ]
)

agent = AskuraAgent(config=config)
response = agent.start_conversation(
    user_id="user123",
    initial_message="I need help planning my vacation"
)
```

---

## 📚 Documentation

Each subproject maintains its own detailed documentation in their respective repositories:

- **cogents-core**: [GitHub Repository](https://github.com/caesar0301/cogents-core)
- **cogents-smith**: [GitHub Repository](https://github.com/caesar0301/cogents-smith)
- **cogents-browser-use**: [GitHub Repository](https://github.com/caesar0301/cogents-browser-use)
- **wizsearch**: [GitHub Repository](https://github.com/caesar0301/wizsearch)
- **wizagent**: [GitHub Repository](https://github.com/mirasurf/wizagent)

### Additional Resources

- **DeepWiki Documentation**: 
  - [cogents-core](https://deepwiki.com/caesar0301/cogents-core)
  - [cogents-smith](https://deepwiki.com/caesar0301/cogents-smith)
  - [wizagent](https://deepwiki.com/caesar0301/wizagent)
- **Philosophy**: [Multi-Agent Systems Talk](https://github.com/caesar0301/mas-talk-2508/blob/master/mas-talk-xmingc.pdf)

---

## 🤝 Contributing

We welcome contributions to any of the COGENTS subprojects! Each subproject follows its own contribution guidelines:

1. Fork the specific subproject repository
2. Create your feature branch
3. Follow the project's code style and testing requirements
4. Submit a pull request

For major changes, please open an issue first to discuss what you would like to change.

---

## 📄 License

All COGENTS subprojects are released under the MIT License. See the LICENSE file in each subproject repository for details.

---

## 🔗 Links

### Project Repositories
- **COGENTS**: https://github.com/caesar0301/cogents
- **cogents-core**: https://github.com/caesar0301/cogents-core
- **cogents-smith**: https://github.com/caesar0301/cogents-smith
- **cogents-browser-use**: https://github.com/caesar0301/cogents-browser-use
- **wizagent**: https://github.com/mirasurf/wizagent
- **wizsearch**: https://github.com/caesar0301/wizsearch

### PyPI Packages
- [cogents-core](https://pypi.org/project/cogents-core/)
- [cogents-smith](https://pypi.org/project/cogents-smith/)
- [cogents-browser-use](https://pypi.org/project/cogents-browser-use/)
- [wizagent](https://pypi.org/project/wizagent/)
- [wizsearch](https://pypi.org/project/wizsearch/)

---

## 🌟 Acknowledgments

COGENTS builds upon and integrates with several excellent projects:
- Tencent [Youtu-agent](https://github.com/Tencent/Youtu-agent) for toolkit integration
- [browser-use](https://github.com/browser-use/browser-use) for browser automation foundations
- [LangGraph](https://github.com/langchain-ai/langgraph) for workflow orchestration
- The open-source community for continuous inspiration and support

---

**Built with ❤️ by the COGENTS Community**
