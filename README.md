# Auto-Summary-Bot 🤖

<p align="center">
      <img src="https://img.shields.io/badge/Language-Python-3776AB?style=for-the-badge&logo=python&logoColor=white" />
      <img src="https://img.shields.io/badge/IDE-Visual%20Studio%20Code-007ACC?style=for-the-badge&logo=visualstudiocode&logoColor=white" />
      <img src="https://img.shields.io/badge/Telegram-2CA5E0?style=for-the-badge&logo=telegram&logoColor=white" alt="Telegram" />
</p>

An AI-powered Telegram bot that transforms text, URLs, PDFs, and YouTube videos into clear, concise, and structured summaries.

I originally built Auto-Summary-Bot to solve a small problem in my daily life. I enjoy watching YouTube videos and reading articles, papers, or even novels, but sometimes work gets hectic, and I barely have enough time to keep up with the things I enjoy. Other times, I'm simply too lazy to spend an hour watching a video or going through a lengthy article just to find the information I'm looking for.

---

## ✨ Features

- **Text Summarization** – Convert plain text into concise, structured bullet-point summaries.
- **URL Summarization** – Extract and summarize article content from web pages.
- **PDF Summarization** – Upload PDF documents and automatically extract and summarize their contents.
- **YouTube Summarization** – Retrieve video transcripts and generate summaries of their key points.
- **AI-Powered Processing** – Uses LiteLLM to support different LLM providers and models.
- **Chunk-Based Summarization** – Splits lengthy content into smaller chunks and processes them concurrently.
- **Explore Similar** – Discover related articles and resources based on the generated summary.
- **Why It Matters** – Get additional AI-generated insights explaining the significance of the summarized content.
- **Configurable Output Language** – Customize the language used for generated summaries.
- **User Access Control** – Restrict bot usage to specified Telegram chat IDs.

## 🛠️ Tech Stack

| Technology | Purpose |
|---|---|
| Python | Core application |
| Telegram Bot API | Bot interface and communication |
| python-telegram-bot | Telegram bot framework |
| LiteLLM | LLM provider integration |
| Trafilatura | Web content extraction |
| PyPDF2 | PDF text extraction |
| YouTube Transcript API | YouTube transcript retrieval |
| DuckDuckGo Search | Discover related articles |
| ThreadPoolExecutor | Concurrent summarization |
| Docker | Containerized deployment |

---

## 📂 Project Structure

    Auto-Summary-Bot/
    │
    ├── .github/
    │   └── workflows/          # GitHub Actions workflows
    │
    ├── main.py                 # Main bot application
    ├── requirements.txt        # Python dependencies
    ├── Dockerfile.txt          # Docker configuration
    └── README.md               # Project documentation

---

## 🚀 Getting Started

### Prerequisites

Before installing the project, make sure you have:

- Python 3.9 or later
- A Telegram account
- A Telegram Bot Token from [@BotFather](https://t.me/BotFather)
- An API key for your selected LLM provider
- Git

### 1. Clone the Repository

    git clone https://github.com/ursleeplessprogrammer/Auto-Summary-Bot.git
    cd Auto-Summary-Bot

### 2. Create a Virtual Environment

    python -m venv venv

Activate the environment:

**Windows:**

    venv\Scripts\activate

**Linux / macOS:**

    source venv/bin/activate

### 3. Install Dependencies

    pip install -r requirements.txt

---

## ⚙️ Configuration

### Environment Variables

Configure the following environment variables before starting the bot.

| Variable | Description | Default |
|---|---|---|
| `TELEGRAM_TOKEN` | Telegram Bot API token | Required |
| `LLM_MODEL` | LLM model identifier supported by LiteLLM | `gpt-3.5-turbo-16k` |
| `TS_LANG` | Language used for generated summaries | `English` |
| `DDG_REGION` | DuckDuckGo search region | `wt-wt` |
| `CHUNK_SIZE` | Maximum target character count per text chunk | `10000` |
| `ALLOWED_USERS` | Comma-separated list of permitted Telegram chat IDs | Empty (all users) |

You must also configure the API credentials required by your selected LLM provider.

**Example configuration:**

    TELEGRAM_TOKEN=your_telegram_bot_token
    LLM_MODEL=gpt-4o-mini
    TS_LANG=English
    DDG_REGION=us-en
    CHUNK_SIZE=10000
    ALLOWED_USERS=123456789,987654321

    OPENAI_API_KEY=your_openai_api_key

> **Security:** Never commit API keys, Telegram tokens, or other sensitive credentials to your GitHub repository. Use environment variables or a secure secrets manager.

## ▶️ Running the Application

Start the bot using:

    python main.py

Once the application starts successfully, open your Telegram bot and send:

    /start

Your Auto-Summary-Bot is now ready to use!

---

## 💬 Usage

### Available Commands

| Command | Description |
|---|---|
| `/start` | Start the bot and display its capabilities |
| `/help` | Display help information |

### 1. Summarize Text

Send any plain text message to the bot.

The bot will automatically process the content and return a concise summary containing the main ideas and important details.

### 2. Summarize a URL

Send a publicly accessible article or webpage URL.

The bot extracts the webpage content and generates a structured summary.

**Example:**

    https://example.com/article

### 3. Summarize a PDF

Upload a PDF document directly to the Telegram chat.

The bot will:

1. Download the uploaded PDF.
2. Extract text from its pages.
3. Process the extracted content using the LLM.
4. Return a concise summary.

### 4. Summarize a YouTube Video

Send a YouTube video URL.

The bot retrieves an available transcript and uses it to generate a summary of the video's key points.

**Supported URL examples:**

    https://www.youtube.com/watch?v=VIDEO_ID
    https://youtu.be/VIDEO_ID

YouTube summarization requires an accessible transcript in one of the supported languages.

---

## 🧠 Interactive AI Features

After generating a summary, the bot provides two additional actions.

### 1. Explore Similar

Discover related content based on the generated summary.

The bot:

1. Extracts five important keywords using the LLM.
2. Searches for related content using DuckDuckGo.
3. Returns up to three relevant search results.

### 2. Why It Matters

Get a deeper understanding of the summarized content.

The LLM analyzes the generated summary and provides additional insights explaining its importance and relevance.

---

## 🏗️ How It Works

The application follows a content extraction and AI summarization pipeline.

    User Input
         |
         v
    Telegram Bot Interface
         |
         v
    Identify Input Type
         |
    +----+----+----+
    |    |    |    |
    Text URL  PDF YouTube
    |    |    |    |
    | Extract  Extract Retrieve
    | Content  Text  Transcript
    |    |    |    |
    +----+----+----+
         |
         v
    Split into Chunks
         |
         v
    Concurrent Processing
         |
         v
    LLM Summarization
         |
         v
    Final Summary Output
         |
    +----+----+
    |         |
    v         v
    Explore   Why It
    Similar   Matters

For lengthy content, the application divides the extracted text into smaller chunks. Each chunk is summarized concurrently using `ThreadPoolExecutor`.

The intermediate summaries are then combined and processed again to produce a consolidated final summary.

---

## 🐳 Docker Deployment

The repository includes a Docker configuration in `Dockerfile.txt` for containerized deployment.

### 1. Build the Docker Image

    docker build -f Dockerfile.txt -t auto-summary-bot .

### 2. Run the Container

    docker run -d \
      --name auto-summary-bot \
      --restart unless-stopped \
      -e TELEGRAM_TOKEN="your_telegram_bot_token" \
      -e LLM_MODEL="gpt-4o-mini" \
      -e TS_LANG="English" \
      -e OPENAI_API_KEY="your_openai_api_key" \
      auto-summary-bot

Add other environment variables as needed, particularly `ALLOWED_USERS` if you want to restrict access.

### 3. Check Container Logs

    docker logs -f auto-summary-bot

### 4. Stop the Container

    docker stop auto-summary-bot

### 5. Remove the Container

    docker rm auto-summary-bot

---

## 🔐 Security & Access Control

Auto-Summary-Bot provides an optional access-control mechanism through the `ALLOWED_USERS` environment variable.

When configured, only Telegram chat IDs included in the list can interact with the bot.

**Example:**

    ALLOWED_USERS=123456789,987654321

Leave this variable empty to allow all users.

For public deployments, configuring an allowlist is recommended to prevent unauthorized usage and unexpected LLM API costs.

---

## ⚠️ Limitations

- Webpage extraction depends on the website's accessibility and content structure.
- PDF summarization requires extractable text; scanned documents may require OCR.
- YouTube summarization depends on the availability of accessible transcripts.
- LLM usage may incur API costs depending on the selected provider and model.
- Summary quality depends on the quality of the extracted source content and the selected LLM.
- Very long inputs may require multiple LLM requests.

## 📦 Dependencies

Project dependencies are maintained in `requirements.txt`.

Install or update them using:

    pip install -r requirements.txt

---

## 🤝 Contributing

Contributions, suggestions, and bug reports are welcome!

1. Fork this repository.
2. Create a new feature branch.

       git checkout -b feature/your-feature

3. Commit your changes.

       git commit -m "Add: your feature description"

4. Push your branch.

       git push origin feature/your-feature

5. Open a Pull Request.

---

## 📄 License

Please refer to the repository for applicable licensing information.

## 👨‍💻 Author

**ursleeplessprogrammer**
