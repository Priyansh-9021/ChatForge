<div align="center">

```
   ██████╗██╗  ██╗ █████╗ ████████╗███████╗ ██████╗ ██████╗  ██████╗ ███████╗
  ██╔════╝██║  ██║██╔══██╗╚══██╔══╝██╔════╝██╔═══██╗██╔══██╗██╔════╝ ██╔════╝
  ██║     ███████║███████║   ██║   █████╗  ██║   ██║██████╔╝██║  ███╗█████╗
  ██║     ██╔══██║██╔══██║   ██║   ██╔══╝  ██║   ██║██╔══██╗██║   ██║██╔══╝
  ╚██████╗██║  ██║██║  ██║   ██║   ██║     ╚██████╔╝██║  ██║╚██████╔╝███████╗
   ╚═════╝╚═╝  ╚═╝╚═╝  ╚═╝   ╚═╝   ╚═╝      ╚═════╝ ╚═╝  ╚═╝ ╚═════╝ ╚══════╝
```

**⚡ Forge conversations. Command intelligence. Stay in control. ⚡**

[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![LangGraph](https://img.shields.io/badge/LangGraph-Powered-1C3C3C?style=for-the-badge&logo=langchain&logoColor=white)](https://langchain-ai.github.io/langgraph/)
[![Streamlit](https://img.shields.io/badge/Streamlit-UI-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white)](https://streamlit.io)
[![Groq](https://img.shields.io/badge/Groq-LLM-F55036?style=for-the-badge)](https://groq.com)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](LICENSE)

</div>

---

> *What if your AI assistant didn't just respond — but actually **acted**?*
> **ChatForge** is a fully agentic, stateful AI chatbot that goes beyond language. It thinks, plans, uses tools, and even pauses to ask for your approval before doing anything consequential.

---

## 🧠 What Is ChatForge?

ChatForge is not your average chatbot. It's an **agentic AI system** built on [LangGraph](https://langchain-ai.github.io/langgraph/) — a framework for stateful, multi-step AI workflows. A graph of nodes orchestrates the LLM and a rich toolset to handle complex, real-world tasks.

Think of it as giving your AI a **brain**, a **toolkit**, a **memory**, and a **conscience** — all at once.

```
 You ──► [ ChatForge ] ──► Think ──► Act ──► Verify ──► Respond
              │                         │
              └── Tool Router ──────────┘
                  ├── 🔍 Web Search
                  ├── 📄 PDF / RAG
                  ├── 🧮 Calculator
                  ├── 📈 Stock Price
                  ├── 💸 Stock Purchase (HITL)
                  └── 🌤️  Weather
```

---

## ✨ Features

### 🔁 Stateful Multi-Turn Conversations
Every message is remembered. Every thread is persisted via SQLite checkpointing. Refresh the page, switch conversations, come back tomorrow — your history is always there.

### 🛠️ Agentic Tool Use
ChatForge autonomously selects the right tool for each job:

| Tool | What It Does |
|------|-------------|
| 🔍 **Web Search** | Real-time information via Tavily Advanced Search |
| 📄 **RAG (PDF Q&A)** | Upload a PDF and chat with its contents using FAISS + Google Embeddings |
| 🧮 **Calculator** | Precise mathematical computations without hallucination |
| 📈 **Stock Price** | Live stock quotes via Alpha Vantage |
| 💸 **Stock Purchase** | Simulated trades — with your approval first |
| 🌤️  **Weather** | Real-time weather for any city on Earth |

### 🧑‍✈️ Human-in-the-Loop (HITL)
Before executing high-stakes actions (like purchasing stock), ChatForge **pauses the graph and asks you**. You click ✅ Approve or ❌ Reject. The AI waits. This is real control — not a checkbox.

```
  Bot: "Ready to buy 10 shares of AAPL. Should I proceed?"
  You: [✅ Yes]  or  [❌ No]
  Bot: *executes or cancels accordingly*
```

### 📁 Multi-Conversation Sidebar
Manage multiple independent chat threads from the sidebar — like browser tabs, but smarter. Start fresh, revisit old threads, or run several conversations simultaneously.

### 📄 PDF Ingestion & Retrieval
Drop a PDF into the chat. ChatForge parses it, splits it into chunks, embeds it with Google's Gemini embedding model, and stores it in a FAISS vector store. Your document becomes instantly queryable.

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                        ChatForge                            │
│                                                             │
│  ┌──────────┐     ┌──────────┐     ┌────────────────────┐  │
│  │ Streamlit│────►│ LangGraph│────►│   Tool Node        │  │
│  │    UI    │     │  Graph   │     │  (6 Tools)         │  │
│  └──────────┘     └──────────┘     └────────────────────┘  │
│        │               │                    │               │
│        │         ┌─────▼──────┐      ┌──────▼───────┐      │
│        │         │  SQLite    │      │ FAISS Vector │      │
│        │         │ Checkpoint │      │ Store (RAG)  │      │
│        │         └────────────┘      └──────────────┘      │
│        │                                                    │
│        └──────────── HITL Interrupt System ────────────────┘│
└─────────────────────────────────────────────────────────────┘
```

**Stack at a glance:**

| Layer | Technology |
|-------|-----------|
| 🖥️ Frontend | Streamlit (streaming, file upload, sidebar) |
| 🧩 Orchestration | LangGraph `StateGraph` with conditional edges |
| 🤖 LLM | Groq API (`gpt-oss-20b`) — blazing fast inference |
| 🗄️ Memory | SQLite-backed LangGraph checkpointer |
| 🔢 Embeddings | Google Generative AI (`gemini-embedding-001`) |
| 🗂️ Vector Store | FAISS (local, offline-capable) |
| 🛠️ Tools | Tavily · Alpha Vantage · OpenWeatherMap · custom tools |

---

## 🚀 Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/Priyansh-9021/ChatForge.git
cd ChatForge
```

### 2. Set Up a Virtual Environment

```bash
python -m venv venv

# Windows
venv\Scripts\activate

# macOS / Linux
source venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure Environment Variables

Create a `.env` file in the root directory:

```env
GROQ_API_KEY=your_groq_api_key
GOOGLE_API_KEY=your_google_api_key
OPENWEATHER_API_KEY=your_openweather_api_key
TAVILY_API_KEY=your_tavily_api_key
```

| Variable | Where to Get It |
|----------|----------------|
| `GROQ_API_KEY` | [console.groq.com](https://console.groq.com) |
| `GOOGLE_API_KEY` | [aistudio.google.com](https://aistudio.google.com) |
| `OPENWEATHER_API_KEY` | [openweathermap.org/api](https://openweathermap.org/api) |
| `TAVILY_API_KEY` | [tavily.com](https://tavily.com) |

### 5. Run the App

```bash
streamlit run app.py
```

Open [http://localhost:8501](http://localhost:8501) in your browser and start forging! 🎉

---

## 🐳 Docker

Prefer containers? ChatForge ships with a production-ready `Dockerfile`.

### Build the Image

```bash
docker build -t chatforge .
```

### Run the Container

```bash
docker run -p 8501:8501 \
  --env-file .env \
  -v chatforge_db:/app/chatbot.db \
  -v chatforge_faiss:/app/faiss.db \
  chatforge
```

> **Note:** Pass your API keys via `--env-file .env`. Never bake secrets into the image.
> Volumes keep your chat history and vector store persistent across container restarts.

### Or with Docker Compose

```yaml
# docker-compose.yml
services:
  chatforge:
    build: .
    ports:
      - "8501:8501"
    env_file:
      - .env
    volumes:
      - chatforge_db:/app/chatbot.db
      - chatforge_faiss:/app/faiss.db
    restart: unless-stopped

volumes:
  chatforge_db:
  chatforge_faiss:
```

```bash
docker compose up --build
```

Open [http://localhost:8501](http://localhost:8501) 🎉

---

## 💬 Example Conversations

```
You:  What's the weather like in Tokyo right now?
Bot:  🌤️  Current weather in Tokyo, JP:
       - Condition: Clear Sky
       - Temperature: 27.4°C
       - Humidity: 68% ...

You:  What's the stock price of NVDA?
Bot:  📈 NVDA is currently trading at $127.45.

You:  Buy 5 shares of NVDA for me.
Bot:  ⚠️  Approve buying 5 shares of NVDA? (yes/no)
      [✅ Yes]  [❌ No]

You:  [uploads research_paper.pdf]
      Summarize the key findings of this paper.
Bot:  📄 Based on the uploaded document, the key findings are...
```

---

## 📂 Project Structure

```
ChatForge/
├── app.py              # Streamlit UI, HITL logic, session management
├── backend.py          # LangGraph graph, tools, LLM, vector store
├── requirements.txt    # Python dependencies
├── .env                # API keys (not committed to git)
├── chatbot.db          # SQLite checkpoint DB (auto-created)
├── faiss.db/           # FAISS vector store (auto-created on PDF upload)
└── LICENSE
```

---

## 🔒 Safety & Control

ChatForge is built with **human oversight** as a first-class feature:

- 🛑 **HITL interrupts** pause execution before irreversible actions
- 🧮 **No hallucinated math** — all arithmetic routes through the calculator tool
- 🛡️ **Graceful error handling** across all tool executions and PDF ingestion
- 🔐 **Session isolation** — each conversation thread is fully independent
- 🧹 **Temp file cleanup** — uploaded PDFs are deleted after indexing

---

## 🛣️ Roadmap

- [ ] 🗂️ Multi-PDF support with per-document namespacing
- [ ] 🎙️ Voice input / text-to-speech output
- [ ] 🔐 User authentication & personal thread history
- [ ] 🌐 Web scraping tool integration
- [ ] 📊 Agent execution trace visualization
- [ ] 🤖 Multi-agent collaboration mode

---

## 🤝 Contributing

Contributions are welcome! If you have ideas, bug reports, or feature requests, feel free to open an issue or submit a pull request.

```bash
# Fork → Clone → Branch → Commit → PR
git checkout -b feature/your-amazing-feature
git commit -m "feat: add your amazing feature"
git push origin feature/your-amazing-feature
```

---

## 📄 License

This project is licensed under the **MIT License**. See [LICENSE](LICENSE) for details.

---

<div align="center">

**Built with 🔥 by [Priyansh](https://github.com/Priyansh-9021)**

*If ChatForge sparked something for you, drop a ⭐ — it means more than you think.*

</div>
