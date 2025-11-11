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
├── Day_1a_From_Prompt_to_Action.ipynb # First notebook - building basic agent
├── CLAUDE.md                          # Development guidance
└── README.md                          # This file
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

## Resources

- [ADK Documentation](https://google.github.io/adk-docs/)
- [ADK Quickstart for Python](https://google.github.io/adk-docs/get-started/python/)
- [Kaggle 5-day AI Agents Course](https://www.kaggle.com/learn-guide/5-day-gen-ai)
