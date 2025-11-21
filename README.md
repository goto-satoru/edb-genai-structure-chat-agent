# sample Structure Chat Agent

A Griptape-based conversational agent structure for interacting with knowledge bases through the EDB Postgres AI GenAI Builder platform. This structure provides a powerful interface to query knowledge bases, maintain conversation context, and generate comprehensive responses using AI assistants.

## 🌟 Features

- **Knowledge Base Integration**: Query and interact with Griptape Cloud Knowledge Bases
- **Conversation Memory**: Persistent conversation threads across multiple interactions
- **Assistant Driver**: Leverages Griptape Cloud Assistant for intelligent responses
- **Ruleset Support**: Apply custom rulesets to guide agent behavior
- **Streaming Support**: Optional streaming mode for real-time responses
- **Environment-based Configuration**: Secure credential management using environment variables

## 📋 Prerequisites

- Python 3.11 or higher
- Hybrid Manager Access Key (=~ Griptape Cloud API Key)
- (Optional) Knowledge Base ID for RAG capabilities
- (Optional) Ruleset alias for custom rules

## 🚀 Installation

recommended to run 

1. Clone the repository:
```bash
git clone https://github.com/goto-satoru/genai-structure-chat-agent structure-chat-agent
cd structure_chat_agent
```

2. Create a Python virtual environment:

```bash
python3 -m venv .venv
source .venv/bin/activate  # On Linux/macOS
# or
.venv\Scripts\activate  # On Windows
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

4. Configure environment variables:

Create a `.env` file in the project root:
```bash
GT_CLOUD_BASE_URL=http://upm-griptape-web
GT_CLOUD_API_KEY=your_HM_access_key
GT_CLOUD_ASSISTANT_ID=your_assistant_id
RULES=your_ruleset_id
```

## 🔑 Getting Hybrid Manager Access Key

1. Log in to Hybrid Manager
2. Navigate to the My Account - Access Keys tab
3. press "Generate New Key" to create a new API key
4. Navigate to GenAI Builder
5. Create or select an Assistant and copy its ID
6. Create a Knowledge Base and copy its ID
7. Create a Ruleset and note its alias or ID

## 📖 Usage

### Basic Usage

Run the structure with a simple prompt:
```bash
python structure.py -p "Hello, how can you help me?"
```

### Using with Knowledge Base

Query a specific knowledge base:
```bash
python structure.py -p "summarize the report" -k f047e04f-f879-43a3-abd4-ff0c831165a1
```

### Continuing a Conversation Thread

Continue an existing conversation:
```bash
python structure.py -p "Tell me more about that" -t thread_id_12345
```

### Using Custom Rulesets

Apply a custom ruleset to guide the agent:
```bash
python structure.py -p "Analyze this data" -r my-custom-ruleset
```

### Enable Streaming Mode

Stream responses in real-time:
```bash
python structure.py -p "Write a long explanation" -s
```

### Command Line Arguments

| Argument | Short | Description | Default |
|----------|-------|-------------|---------|
| `--prompt` | `-p` | The prompt/question to ask | "Hello there!" |
| `--knowledge-base-id` | `-k` | Griptape Cloud Knowledge Base ID | None |
| `--thread-id` | `-t` | Conversation Thread ID | None |
| `--ruleset-alias` | `-r` | Ruleset alias to apply | None |
| `--stream` | `-s` | Enable streaming mode | False |

## 🛠️ Structure Configuration

The structure is configured via `structure_config.yaml`:

```yaml
version: 1.0
runtime: python3
runtime_version: 3.11
build:
  requirements_file: requirements.txt
  cache_build_dependencies:
    enabled: true
    watched_files:
      - requirements.txt
      - structure_config.yaml
run:
  main_file: structure.py
```

## 🏗️ Architecture

The agent uses a Pipeline structure with the following components:

- **Pipeline**: Orchestrates the conversation flow
- **AssistantTask**: Processes user prompts using the Griptape Cloud Assistant
- **GriptapeCloudConversationMemoryDriver**: Maintains conversation context
- **GriptapeCloudAssistantDriver**: Interfaces with Griptape Cloud AI models
- **Rulesets**: Optional rules to guide agent behavior


## 📦 Dependencies

- **griptape** : Framework for building AI agents and structures
- **python-dotenv**: Environment variable management
- **pydantic**: Data validation and settings management

See `requirements.txt` for the complete list.

## 🏗️ Project Structure

```
├── structure.py              # Main structure implementation
├── structure_config.yaml     # Structure configuration
├── requirements.txt          # Python dependencies
└── README.md                # This file
```

## 👥 Authors

EnterpriseDB Corporation

## 🔗 Related Resources

- [EDB Postgres AI AI Factory GenAI Builder Tools](https://www.enterprisedb.com/docs/edb-postgres-ai/latest/ai-factory/gen-ai/structures/)
- [Griptape Documentation](https://docs.griptape.ai/)
