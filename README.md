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
├── Day_3a_Sessions.ipynb                    # Day 3a: Session management
├── Day_3b_Agent_Memory.ipynb                # Day 3b: Memory management (with test queries)
├── Day_4a_Agent_Observability.ipynb         # Day 4a: Logging, traces & custom plugins
├── Day_4b_Agent_Evaluation.ipynb            # Day 4b: Agent evaluation & user simulation
├── Day_5a_Agent2Agent_Communication.ipynb   # Day 5a: A2A protocol & multi-agent communication
├── Day_5b_Agent_Deployment.ipynb            # Day 5b: Production deployment to Vertex AI Agent Engine
├── research-agent/                          # Research paper finder agent (Day 4a)
│   ├── .env                                # Agent-specific API key
│   ├── __init__.py                         # Python package file
│   └── agent.py                            # Agent definition
├── home_automation_agent/                   # Home automation agent (Day 4b)
│   ├── .env                                # Agent-specific API key
│   ├── __init__.py                         # Python package file
│   ├── agent.py                            # Agent definition
│   ├── test_config.json                    # Evaluation configuration
│   ├── integration.evalset.json            # Static evaluation test cases
│   ├── conversation_scenarios.json         # User simulation scenarios
│   └── session_input.json                  # Session configuration for eval
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

### Day 3a: Sessions
Manage conversation state and history:
- **Session Management**: Create and retrieve conversation sessions
- **Session Service**: Use `InMemorySessionService` for local development
- **Session Events**: Track all interactions (messages, tool calls, responses)
- **Multi-Session Handling**: Manage multiple independent conversations

Key concepts:
- Using `SessionService.create_session()` and `get_session()`
- Session identifiers: `app_name`, `user_id`, `session_id`
- Accessing session events and conversation history
- Understanding when to create new sessions vs reuse existing ones

### Day 3b: Memory Management
Build agents with long-term knowledge storage:
- **Memory Service**: Store and retrieve information across conversations
- **Memory vs Sessions**: Short-term (session) vs long-term (memory) storage
- **Memory Ingestion**: Transfer session data to memory with `add_session_to_memory()`
- **Memory Retrieval**: Search memories with `load_memory` and `preload_memory` tools
- **Memory Consolidation**: Extract key facts from raw conversations (production feature)

Key concepts:
- `InMemoryMemoryService` for development (keyword matching)
- `VertexAiMemoryBankService` for production (semantic search, LLM-powered consolidation)
- Reactive retrieval (`load_memory`) vs proactive retrieval (`preload_memory`)
- Automating memory storage with `after_agent_callback`
- Understanding keyword matching vs semantic search limitations

**Hands-On Practice**: Test Different Queries
- Query 1: "what color does the user like" - Tests keyword matching with similar words
- Query 2: "haiku" - Tests specific content type retrieval
- Query 3: "age" - Demonstrates memory doesn't hallucinate non-existent data
- Query 4: "preferred hue" - Shows keyword matching limitations vs semantic search

### Day 4a: Agent Observability
Debug and monitor agent behavior in production:
- **Observability Pillars**: Logs, traces, and metrics for agent monitoring
- **ADK Web UI**: Interactive debugging with event traces and LLM request inspection
- **DEBUG Logging**: Enable detailed logging to diagnose agent failures
- **Production Logging**: Use `LoggingPlugin` for automated observability
- **Custom Plugins**: Build plugins to track custom metrics and behavior

Key concepts:
- Debugging pattern: symptom → logs → root cause → fix
- Using `adk web --log_level DEBUG` for development debugging
- Implementing callback hooks: `before_tool_callback`, `after_tool_callback`
- Plugin lifecycle and automatic application to all agents
- Production vs development observability strategies

**Solution Implementation**: Custom Tool Tracking Plugin
- Tracks total number of tool calls made during a session
- Provides detailed breakdown by tool type
- Demonstrates flexible callback signatures using `**kwargs`
- Generates comprehensive summary reports
- Perfect for production monitoring and cost tracking

**Local Development Setup**:
- Modified proxy setup for running ADK web UI outside Kaggle
- Simplified localhost access without proxy configuration
- Environment variable setup for local development

### Day 4b: Agent Evaluation
Systematically test and measure agent performance:
- **Interactive Evaluation**: Create and test cases in ADK Web UI
- **Evaluation Metrics**: Response match score and tool trajectory scoring
- **Regression Testing**: Automated batch testing with `adk eval` CLI
- **Static Test Cases**: Fixed evaluation sets with expected outputs
- **User Simulation**: Dynamic conversation generation with LLM-backed testing

Key concepts:
- Tool trajectory vs response match evaluation
- Creating eval sets and eval cases
- Test configuration with pass/fail thresholds
- Analyzing evaluation results for actionable insights
- Conversation scenarios with starting_prompt and conversation_plan

**Solution Implementation**: User Simulation with Conversation Scenarios
- Define realistic conversation scenarios for dynamic testing
- Create session input configuration for agent targeting
- Use `adk eval_set` commands to build evaluation suites
- Run evaluations with LLM-generated user interactions
- Each run produces different natural conversations
- Discovers edge cases static tests miss

**Files Created**:
- `test_config.json` - Evaluation criteria and thresholds
- `integration.evalset.json` - Static test cases
- `conversation_scenarios.json` - User simulation scenarios
- `session_input.json` - Agent and user configuration

**CLI Workflow**:
```bash
# Create eval set
adk eval_set create <agent_path> <eval_set_name>

# Add conversation scenarios
adk eval_set add_eval_case <agent_path> <eval_set_name> \
  --scenarios_file conversation_scenarios.json \
  --session_input_file session_input.json

# Run evaluation
adk eval <agent_path> <eval_set_name> \
  --config_file_path test_config.json \
  --print_detailed_results
```

### Day 5a: Agent2Agent (A2A) Communication
Build multi-agent systems with cross-organization collaboration:
- **A2A Protocol**: Standard for agent-to-agent communication across networks and frameworks
- **Exposing Agents**: Use `to_a2a()` to make agents accessible with auto-generated agent cards
- **Consuming Agents**: Use `RemoteA2aAgent` to integrate remote agents as local sub-agents
- **Architecture Patterns**: Cross-framework, cross-language, and cross-organization integration

Key concepts:
- Understanding A2A vs local sub-agents decision criteria
- Agent cards as formal contracts (`/.well-known/agent-card.json`)
- Using `to_a2a()` to expose agents via FastAPI/Starlette server
- `RemoteA2aAgent` as client-side proxy for remote agents
- Real-world applications: microservices, third-party integrations, vendor services

**Implementation Example**: Product Catalog Integration
- Product Catalog Agent (external vendor) exposed via A2A
- Customer Support Agent consuming remote catalog via A2A protocol
- Demonstrates separation of concerns and cross-organization boundaries
- Local simulation for learning (production would use different hosts)

**Protocol Details**:
- HTTP POST requests to `/tasks` endpoint
- Standardized JSON format following A2A specification
- Language/framework agnostic communication
- Network-based agent collaboration

### Day 5b: Agent Deployment
Deploy agents to production with Vertex AI Agent Engine:
- **Production Readiness**: Package agents for cloud deployment
- **Vertex AI Agent Engine**: Fully managed service with auto-scaling
- **Deployment Configuration**: Resource limits, scaling, and environment setup
- **Cost Management**: Free tier usage and cleanup best practices
- **Long-Term Memory**: Vertex AI Memory Bank for cross-session persistence

Key concepts:
- Creating deployment package (agent.py, requirements.txt, .env, .agent_engine_config.json)
- Using `adk deploy agent_engine` CLI command
- Setting resource limits (CPU, memory, min/max instances)
- Region selection for optimal latency
- Retrieving and testing deployed agents via SDK

**Implementation Example**: Weather Assistant Deployment
- Production-ready agent with `gemini-2.5-flash-lite` model
- Custom `get_weather` tool for demonstration
- Deployment to Agent Engine with auto-scaling configuration
- Async streaming query testing
- Proper cleanup to avoid costs

**Deployment Options**:
- **Vertex AI Agent Engine**: Managed service with session management (this notebook)
- **Cloud Run**: Serverless deployment for demos and small workloads
- **GKE**: Full control for complex multi-agent systems

**Memory Bank Integration**:
- Session memory vs long-term memory across conversations
- `PreloadMemoryTool` for automatic recall of user preferences
- Automatic extraction of key facts after conversations
- Infrastructure provided by Agent Engine deployment

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

### Sessions & Memory
- [ADK Sessions Documentation](https://google.github.io/adk-docs/sessions/)
- [ADK Memory Documentation](https://google.github.io/adk-docs/sessions/memory/)
- [Vertex AI Memory Bank Overview](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/memory-bank/overview)
- [Memory Consolidation Guide](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/memory-bank/generate-memories)

### Observability
- [ADK Observability Documentation](https://google.github.io/adk-docs/observability/logging/)
- [Custom Plugins Guide](https://google.github.io/adk-docs/plugins/)
- [Plugin Callback Hooks](https://google.github.io/adk-docs/plugins/#plugin-callback-hooks)
- [Cloud Trace Integration](https://google.github.io/adk-docs/observability/cloud-trace/)

### Evaluation
- [ADK Evaluation Overview](https://google.github.io/adk-docs/evaluate/)
- [Evaluation Criteria](https://google.github.io/adk-docs/evaluate/criteria/)
- [User Simulation Guide](https://google.github.io/adk-docs/evaluate/user-sim/)
- [Pytest-based Evaluation](https://google.github.io/adk-docs/evaluate/#2-pytest-run-tests-programmatically)
- [Advanced Evaluation Criteria](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/models/determine-eval)

### Agent2Agent Communication
- [A2A Protocol Official Website](https://a2a-protocol.org/)
- [A2A Protocol Specification](https://a2a-protocol.org/latest/specification/)
- [Introduction to A2A in ADK](https://google.github.io/adk-docs/a2a/intro/)
- [Exposing Agents Quickstart](https://google.github.io/adk-docs/a2a/quickstart-exposing/)
- [Consuming Agents Quickstart](https://google.github.io/adk-docs/a2a/quickstart-consuming/)
- [A2A Tutorials](https://a2a-protocol.org/latest/tutorials/)

### Deployment
- [ADK Deployment Guide](https://google.github.io/adk-docs/deploy/)
- [Deploy to Agent Engine](https://google.github.io/adk-docs/deploy/agent-engine/)
- [Deploy to Cloud Run](https://google.github.io/adk-docs/deploy/cloud-run/)
- [Deploy to GKE](https://google.github.io/adk-docs/deploy/gke/)
- [Vertex AI Agent Engine Overview](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/overview)
- [Agent Engine Pricing](https://docs.cloud.google.com/agent-builder/agent-engine/overview#pricing)
- [Agent Starter Pack (GitHub)](https://github.com/GoogleCloudPlatform/agent-starter-pack)
- [Memory Bank with ADK](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/agents/agent_engine/memory_bank/get_started_with_memory_bank_on_adk.ipynb)

### MCP (Model Context Protocol)
- [MCP Specification](https://spec.modelcontextprotocol.io/)
- [MCP Servers](https://modelcontextprotocol.io/examples)

### Course
- [Kaggle 5-day AI Agents Course](https://www.kaggle.com/learn-guide/5-day-gen-ai)
