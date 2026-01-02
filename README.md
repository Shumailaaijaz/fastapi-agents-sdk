# FastAPI Agents SDK with Gemini

A FastAPI application that integrates Google Gemini AI with the OpenAI Agents SDK and custom function tools for web search, URL metadata extraction, and text analysis.

## Features

- **Google Gemini Integration**: Uses Gemini 2.5 Flash via OpenAI-compatible API
- **Custom Function Tools**:
  - **Web Search**: Search the web using DuckDuckGo
  - **URL Metadata Fetcher**: Extract metadata from web pages
  - **Text Analyzer**: Comprehensive text statistics and analysis
- **FastAPI REST API**: Easy-to-use HTTP endpoints
- **Async Support**: Built with async/await patterns

## Prerequisites

- Python 3.14+
- Google Gemini API Key ([Get one here](https://aistudio.google.com/apikey))

## Installation

1. Clone the repository:
```bash
git clone <your-repo-url>
cd fastapi-agents-sdk
```

2. Install dependencies using uv (recommended) or pip:
```bash
# Using uv
uv pip install -e .

# Or using pip
pip install -e .
```

3. Create a `.env` file:
```bash
cp .env.example .env
```

4. Edit `.env` and add your Gemini API key:
```
GEMINI_API_KEY=your_actual_api_key_here
```

## Running the Application

Start the FastAPI server:
```bash
python main.py
```

The API will be available at `http://localhost:8000`

## API Documentation

Once running, visit:
- Swagger UI: `http://localhost:8000/docs`
- ReDoc: `http://localhost:8000/redoc`

## Available Tools

### 1. Web Search Tool

Performs web searches using DuckDuckGo and returns relevant results.

**Parameters:**
- `query` (str): Search query
- `max_results` (int, optional): Maximum results to return (default: 5, max: 10)

**Example Usage:**
```bash
curl -X POST http://localhost:8000/chat/ \
  -H "Content-Type: application/json" \
  -d '{
    "prompt": "Search for the latest news about artificial intelligence"
  }'
```

### 2. URL Metadata Fetcher

Extracts comprehensive metadata from any URL including title, description, and Open Graph data.

**Parameters:**
- `url` (str): Complete URL (must include http:// or https://)

**Example Usage:**
```bash
curl -X POST http://localhost:8000/chat/ \
  -H "Content-Type: application/json" \
  -d '{
    "prompt": "Fetch metadata from https://github.com/openai/openai-agents-python"
  }'
```

### 3. Text Analyzer

Provides detailed text analysis including word count, reading time, and statistics.

**Parameters:**
- `text` (str): Text to analyze

**Returns:**
- Word count, character count
- Sentence and paragraph count
- Average word length
- Reading time estimate
- Longest word
- Lexical diversity

**Example Usage:**
```bash
curl -X POST http://localhost:8000/chat/ \
  -H "Content-Type: application/json" \
  -d '{
    "prompt": "Analyze this text: The quick brown fox jumps over the lazy dog. This is a sample sentence for testing purposes."
  }'
```

## Example Prompts

Here are some example prompts to try:

1. **Web Search**:
   - "Search for Python best practices 2026"
   - "Find recent articles about machine learning"
   - "What are the top 5 results for FastAPI tutorials?"

2. **URL Metadata**:
   - "Get metadata from https://www.python.org"
   - "What's the title and description of https://fastapi.tiangolo.com?"

3. **Text Analysis**:
   - "Analyze the readability of this paragraph: [your text]"
   - "How many words and sentences are in this text: [your text]"
   - "Calculate reading time for this article: [your text]"

4. **Combined**:
   - "Search for FastAPI tutorials and get metadata from the first result"
   - "Find articles about Python, analyze their titles"

## Project Structure

```
fastapi-agents-sdk/
├── main.py              # FastAPI application
├── connection.py        # Gemini agent setup and configuration
├── tools.py             # Custom function tools
├── .env.example         # Environment variables template
├── .env                 # Your actual environment variables (git-ignored)
├── pyproject.toml       # Project dependencies
└── README.md            # This file
```

## How It Works

1. **Agent Initialization**: The Gemini agent is created with custom function tools
2. **Request Processing**: When you send a prompt, the agent decides which tools to use
3. **Tool Execution**: The agent automatically calls the appropriate tools
4. **Response**: The agent synthesizes the results into a natural language response

## API Endpoints

### `GET /`
Health check endpoint.

**Response:**
```json
{
  "message": "Hello from fastapi-agents-sdk!",
  "status": "running"
}
```

### `POST /chat/`
Chat with the Gemini agent.

**Request Body:**
```json
{
  "prompt": "Your question or task here",
  "model": "gemini-2.5-flash"  // optional
}
```

**Response:**
```json
{
  "response": "Agent's response here",
  "model": "gemini-2.5-flash"
}
```

## Dependencies

- `fastapi` - Web framework
- `uvicorn` - ASGI server
- `python-dotenv` - Environment variable management
- `agents` - OpenAI Agents SDK
- `pydantic` - Data validation
- `duckduckgo-search` - Web search functionality

## Troubleshooting

### "Gemini agent not initialized"
- Make sure you've set `GEMINI_API_KEY` in your `.env` file
- Verify the API key is valid at [Google AI Studio](https://aistudio.google.com/apikey)

### Import errors
- Run `uv pip install -e .` to install all dependencies
- Make sure you're using Python 3.14+

### Web search not working
- The web search tool uses DuckDuckGo which doesn't require an API key
- If you encounter rate limiting, try reducing the number of searches

## Contributing

Feel free to submit issues and enhancement requests!

## License

MIT License

## Resources

- [OpenAI Agents SDK Documentation](https://openai.github.io/openai-agents-python/)
- [Google Gemini API Docs](https://ai.google.dev/gemini-api/docs)
- [FastAPI Documentation](https://fastapi.tiangolo.com/)
