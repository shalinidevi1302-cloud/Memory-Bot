# Memory Bot

## Project Overview

Memory Bot is a locally running AI chatbot that uses Ollama and LangChain to remember previous conversations. It provides a simple and interactive chat interface using Streamlit, along with a terminal-based version.

The chatbot runs entirely on your computer, without requiring external API keys or cloud services.

## Key Features

- **Fully Local:** Runs using locally installed Ollama models.
- **Conversation Memory:** Remembers previous messages within a conversation.
- **New Chat:** Start a fresh conversation whenever needed.
- **Chat History:** View, switch between, and delete previous conversations.
- **Saved Conversations:** Automatically stores chat history in `chats.json`.
- **Model Selection:** Choose from available Ollama models.
- **Streaming Responses:** Displays responses as they are generated.
- **Terminal Support:** Provides a command-line chatbot through `chatbot.py`.

## Technologies Used

| Component            | Technology            |
| -------------------- | --------------------- |
| Programming Language | Python 3.10+          |
| Local LLM Runtime    | Ollama                |
| AI Models            | Llama 3.2, Gemma 3:1B |
| LLM Framework        | LangChain             |
| Web Interface        | Streamlit             |
| Data Storage         | JSON                  |

## Project Structure

```text
memory-bot/
│
├── .streamlit/
│   └── config.toml
│
├── app.py
├── chatbot.py
├── requirements.txt
├── chats.json
└── README.md
```

### File Description

- `app.py` – Main Streamlit application with chat interface and history management.
- `chatbot.py` – Terminal-based chatbot with conversation memory.
- `requirements.txt` – Contains the required Python dependencies.
- `chats.json` – Stores previous conversations automatically.
- `config.toml` – Contains Streamlit theme configuration.
- `README.md` – Project documentation.

## Installation and Setup

### Step 1: Install Ollama

Download and install Ollama from its official website.

After installation, open the terminal and download a model:

```bash
ollama pull llama3.2
```

For systems with limited RAM, you can use smaller models:

```bash
ollama pull llama3.2:1b
```

### Step 2: Clone the Repository

```bash
git clone https://github.com/<your-username>/memory-bot.git
```

Navigate to the project folder:

```bash
cd memory-bot
```

### Step 3: Create a Virtual Environment

```bash
python -m venv .venv
```

Activate the environment on Windows:

```bash
.venv\Scripts\Activate.ps1
```

### Step 4: Install Dependencies

```bash
pip install -r requirements.txt
```

### Step 5: Run the Application

**Streamlit Web Application:**

```bash
streamlit run app.py
```

Open your browser and visit:

`http://localhost:8501`

**Terminal Application:**

```bash
python chatbot.py
```

Available terminal commands:

- `/clear` – Clear the current conversation memory.
- `/quit` – Exit the chatbot.

## Testing Conversation Memory

The chatbot can remember information shared earlier in the same conversation.

**Example:**

```text
You: My name is Rhema.

You: What's my name?

Bot: Your name is Rhema.
```

When you click the **New Chat** button, the chatbot starts a fresh conversation without the previous chat's context.

## Working of Conversation Memory

The project uses two different approaches to manage conversation history.

**1. Terminal Version (`chatbot.py`)**

- Uses LangChain's `RunnableWithMessageHistory`.
- Implements a custom `WindowedHistory` class.
- Maintains a limited number of previous messages.
- Prevents the conversation from exceeding the model's context window.

**2. Streamlit Version (`app.py`)**

- Maintains separate message histories for individual chats.
- Sends the most recent messages to the language model.
- Uses `MAX_MESSAGES` to control the memory window.
- Saves conversations in `chats.json` for future access.

## Configuration

| Setting       | Description                      | Default              |
| ------------- | -------------------------------- | -------------------- |
| Default Model | Ollama model used by the chatbot | `llama3.2`           |
| Memory Window | Number of messages retained      | 10–12                |
| System Prompt | Defines chatbot behaviour        | Friendly and concise |
| Theme         | Streamlit interface appearance   | Dark                 |

The memory size and chatbot behaviour can be customized by modifying the corresponding variables in the Python files.

## Troubleshooting

| Problem                     | Solution                                                      |
| --------------------------- | ------------------------------------------------------------- |
| Model not found             | Run `ollama pull llama3.2`.                                   |
| Connection refused          | Start Ollama using `ollama serve`.                            |
| ModuleNotFoundError         | Install dependencies using `pip install -r requirements.txt`. |
| Streamlit import error      | Select the correct `.venv` Python interpreter in VS Code.     |
| Requirements file not found | Make sure the terminal is inside the project directory.       |
| Slow responses              | Try a smaller model such as `llama3.2:1b` or `gemma3:1b`.     |

## Deployment Information

The application is designed to run locally using Ollama. Local Ollama models cannot run directly on Streamlit Community Cloud because the platform does not provide the required local Ollama environment.

For public deployment, the following alternatives are available:

1. Integrate a hosted LLM using an API-based service.
2. Use Cloudflare Tunnel to temporarily share the local application.
3. Deploy the application on a personal server with Ollama installed.

## Future Enhancements

- Add long-term conversation memory.
- Support document uploads and question answering.
- Improve chat history search.
- Add voice-based interaction.
- Support additional local language models.

##
