# ai-agents-5-day

Kaggle 5-day AI Agents course - Building AI agents using Google's Agent Development Kit (ADK) with the Gemini API.

## Prerequisites

- Python 3.11+
- [uv](https://github.com/astral-sh/uv) package manager
- Google Gemini API key

## Setup

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd ai-agents-5-day
   ```

2. **Create and activate virtual environment with uv**
   ```bash
   uv venv
   source .venv/bin/activate  # On macOS/Linux
   # or
   .venv\Scripts\activate     # On Windows
   ```

3. **Install dependencies**
   ```bash
   uv pip install google-adk python-dotenv jupyter ipykernel
   ```

4. **Configure API key**

   Create a `.env` file in the project root:
   ```bash
   echo "GOOGLE_API_KEY=your-api-key-here" > .env
   ```

   Get your API key from [Google AI Studio](https://aistudio.google.com/app/api-keys)

5. **Register Jupyter kernel**
   ```bash
   python -m ipykernel install --user --name=ai-agents-5-day --display-name="Python (ai-agents-5-day)"
   ```

## Running the Notebooks

### Option 1: VS Code (Recommended)

1. **Open the project in VS Code**
   ```bash
   code .
   ```

2. **Open the notebook**
   - Open `Day_1a_From_Prompt_to_Action.ipynb`

3. **Select the correct kernel**
   - Click on the kernel name in the top-right corner
   - Select `Python (ai-agents-5-day)` from the dropdown
   - Or press `Cmd+Shift+P` (macOS) / `Ctrl+Shift+P` (Windows/Linux)
   - Type "Select Kernel" and choose `Python (ai-agents-5-day)`

4. **Run cells**
   - Execute cells one at a time (don't use "Run All" to avoid API rate limits)
   - Press `Shift+Enter` to run each cell

### Option 2: Jupyter Notebook

1. **Start Jupyter**
   ```bash
   jupyter notebook
   ```

2. **Open the notebook**
   - Navigate to `Day_1a_From_Prompt_to_Action.ipynb`

3. **Select the correct kernel**
   - In Jupyter: `Kernel` → `Change Kernel` → `Python (ai-agents-5-day)`

4. **Run cells**
   - Execute cells one at a time (don't use "Run All" to avoid API rate limits)

## Project Structure

```
ai-agents-5-day/
├── .env                               # API keys (gitignored)
├── .venv/                             # Virtual environment (gitignored)
├── .gitignore                         # Git ignore patterns
├── sample-agent/                      # Sample agent created by ADK
│   ├── .env                          # Agent-specific API key
│   ├── __init__.py                   # Python package file
│   └── agent.py                      # Agent definition
├── Day_1a_From_Prompt_to_Action.ipynb       # Day 1a: Building your first agent
├── Day_1b_Agent_Architectures.ipynb         # Day 1b: Multi-agent systems & workflows
├── Day_2a_Agent_Tools.ipynb                 # Day 2a: Custom tools & code execution
├── Day_2b_Agent_Tools_Best_Practices.ipynb  # Day 2b: MCP & long-running operations
├── Day_2b_Exercise_Solution.ipynb           # Day 2b: Exercise solution
├── CLAUDE.md                                # Development guidance
└── README.md                                # This file
```

## Working with ADK Web UI (Local Development)

The notebook includes a web UI for testing agents interactively.

### Create a sample agent

```bash
# Make sure GOOGLE_API_KEY is set in .env or environment
source .venv/bin/activate
adk create sample-agent --model gemini-2.5-flash-lite --api_key $GOOGLE_API_KEY
```

This creates a `sample-agent/` directory with:
- `agent.py` - Agent definition
- `.env` - API key configuration
- `__init__.py` - Python package file

### Run ADK web UI locally

```bash
cd sample-agent
adk web
```

The web UI will be available at `http://localhost:8000`

**Note:** For local development, the notebook includes a modified `get_adk_proxy_url()` function that detects whether you're running in Kaggle/Colab or locally and returns the appropriate URL.

## Course Content

### Day 1a: From Prompt to Action
Learn the fundamentals of building AI agents:
- Install and configure ADK
- Create your first simple agent with tools (Google Search)
- Use `InMemoryRunner` to execute agent queries
- Explore the ADK web UI

### Day 1b: Multi-Agent Systems & Workflow Patterns
Build sophisticated agent teams:
- **LLM-based orchestration**: Use an LLM as a "manager" to coordinate agents
- **Sequential workflows**: Create fixed pipelines (outline → write → edit)
- **Parallel workflows**: Run independent tasks concurrently for speed
- **Loop workflows**: Implement iterative refinement cycles (writer ⇄ critic)

Key concepts:
- `Agent`, `SequentialAgent`, `ParallelAgent`, `LoopAgent`
- Using `output_key` to pass state between agents
- Choosing the right workflow pattern for your use case

### Day 2a: Agent Tools
Extend agents with custom functionality:
- **Function Tools**: Convert Python functions into agent tools
- **Agent Tools**: Use specialist agents as tools in other agents
- **Code Execution**: Improve reliability with `BuiltInCodeExecutor`
- **Tool Types**: Overview of custom vs built-in tools

Key concepts:
- Creating custom function tools with proper docstrings and type hints
- Using `AgentTool` to delegate tasks to specialist agents
- Understanding when to use Agent Tools vs Sub-Agents
- Built-in tools: Gemini tools, Google Cloud tools, third-party tools

### Day 2b: Agent Tools Best Practices
Advanced patterns for production-ready agents:
- **MCP Integration**: Connect to external services using Model Context Protocol
- **Long-Running Operations**: Implement human-in-the-loop approvals
- **Resumable Workflows**: Build agents that pause and resume execution
- **State Management**: Maintain conversation state across interruptions

Key concepts:
- Using `McpToolset` to integrate with MCP servers
- Implementing approval flows with `ToolContext.request_confirmation()`
- Creating resumable apps with `App` and `ResumabilityConfig`
- Detecting and handling `adk_request_confirmation` events
- Using `invocation_id` to resume paused executions

**Exercise Solution**: Image generation agent with cost approval
- Combines MCP tool (getTinyImage) with custom approval logic
- Auto-approves single images, requires approval for bulk requests
- Demonstrates both MCP integration and long-running operations patterns

## Resources

### Documentation
- [ADK Documentation](https://google.github.io/adk-docs/)
- [ADK Quickstart for Python](https://google.github.io/adk-docs/get-started/python/)

### Agents
- [ADK Agents Overview](https://google.github.io/adk-docs/agents/)
- [Sequential Agents](https://google.github.io/adk-docs/agents/workflow-agents/sequential-agents/)
- [Parallel Agents](https://google.github.io/adk-docs/agents/workflow-agents/parallel-agents/)
- [Loop Agents](https://google.github.io/adk-docs/agents/workflow-agents/loop-agents/)

### Tools
- [ADK Tools Overview](https://google.github.io/adk-docs/tools/)
- [Custom Tools Guide](https://google.github.io/adk-docs/tools-custom/)
- [Function Tools](https://google.github.io/adk-docs/tools/function-tools/)
- [MCP Tools](https://google.github.io/adk-docs/tools/mcp-tools/)
- [Long-Running Operations](https://google.github.io/adk-docs/tools/function-tools/)
- [Plugins Overview](https://google.github.io/adk-docs/plugins/)

### Runtime & State
- [App and Runner](https://google.github.io/adk-docs/runtime/)
- [Sessions and State Management](https://google.github.io/adk-docs/runtime/)

### MCP (Model Context Protocol)
- [MCP Specification](https://spec.modelcontextprotocol.io/)
- [MCP Servers](https://modelcontextprotocol.io/examples)

### Course
- [Kaggle 5-day AI Agents Course](https://www.kaggle.com/learn-guide/5-day-gen-ai)
