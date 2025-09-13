# Blog Generation using LangGraph

A FastAPI-based blog generation application powered by LangGraph and Groq LLM. This project creates an AI agent that can generate blog content based on given topics using a graph-based workflow approach.

## Features

- **AI-Powered Blog Generation**: Generate blog content using advanced language models
- **LangGraph Integration**: Utilizes LangGraph for creating complex AI workflows
- **Groq LLM**: Fast inference using Groq's language models
- **FastAPI Backend**: RESTful API for blog generation requests
- **Modular Architecture**: Clean separation of concerns with dedicated modules for graphs, LLMs, nodes, and states
- **Environment Configuration**: Easy setup with environment variables

## Project Structure

```
Blog-generation-using-Langgraph/
├── src/
│   ├── __init__.py
│   ├── graphs/
│   │   ├── __init__.py
│   │   └── graph_builder.py      # Graph construction logic
│   ├── llms/
│   │   ├── __init__.py
│   │   └── groqllm.py           # Groq LLM integration
│   ├── nodes/
│   │   ├── __init__.py
│   │   └── blog_node.py         # Blog generation nodes
│   └── states/
│       ├── __init__.py
│       └── blogstate.py         # State management
├── app.py                       # FastAPI application
├── main.py                      # Main entry point
├── requirements.txt             # Dependencies
├── pyproject.toml              # Project configuration
├── langgraph.json              # LangGraph configuration
├── request.json                # Sample request
└── README.md                   # This file
```

## Prerequisites

- Python 3.13 or higher
- Groq API key
- LangChain API key (optional, for LangSmith tracking)

## Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd Blog-generation-using-Langgraph
   ```

2. **Install dependencies**
   
   Using pip:
   ```bash
   pip install -r requirements.txt
   ```
   
   Or using uv (recommended):
   ```bash
   uv install
   ```

3. **Set up environment variables**
   
   Create a `.env` file in the root directory:
   ```env
   GROQ_API_KEY=your_groq_api_key_here
   LANGCHAIN_API_KEY=your_langchain_api_key_here  # Optional
   ```

## Usage

### Running the FastAPI Server

1. **Start the server**
   ```bash
   python app.py
   ```
   
   Or using uvicorn directly:
   ```bash
   uvicorn app:app --host 0.0.0.0 --port 8000 --reload
   ```

2. **The API will be available at**: `http://localhost:8000`

### API Endpoints

#### Generate Blog Content

**POST** `/blogs`

Generate blog content based on a given topic.

**Request Body:**
```json
{
    "topic": "Your blog topic here"
}
```

**Example:**
```bash
curl -X POST "http://localhost:8000/blogs" \
     -H "Content-Type: application/json" \
     -d '{"topic": "Agentic AI"}'
```

**Response:**
```json
{
    "data": {
        // Generated blog content and metadata
    }
}
```

### Using the Command Line Interface

Run the basic CLI version:
```bash
python main.py
```

### Testing with Sample Request

You can test the API using the provided sample request:
```bash
curl -X POST "http://localhost:8000/blogs" \
     -H "Content-Type: application/json" \
     -d @request.json
```

## LangGraph Configuration

The project uses LangGraph for workflow management. The configuration is defined in `langgraph.json`:

- **Dependencies**: The current directory is included as a dependency
- **Graphs**: The blog generator agent is defined in `src/graphs/graph_builder.py`
- **Environment**: Uses `.env` file for configuration

## Development

### Project Components

1. **Graph Builder** (`src/graphs/graph_builder.py`): Constructs the LangGraph workflow
2. **Groq LLM** (`src/llms/groqllm.py`): Handles Groq language model integration
3. **Blog Node** (`src/nodes/blog_node.py`): Defines blog generation logic
4. **Blog State** (`src/states/blogstate.py`): Manages application state

### Adding New Features

1. Create new nodes in the `src/nodes/` directory
2. Update the graph builder to include new workflow steps
3. Modify states if additional data needs to be tracked
4. Add new API endpoints in `app.py` as needed

## Dependencies

- **FastAPI**: Web framework for building APIs
- **LangChain**: Framework for developing applications with language models
- **LangGraph**: Library for building stateful, multi-actor applications
- **Groq**: Fast inference language models
- **Uvicorn**: ASGI server implementation

For a complete list, see `requirements.txt` or `pyproject.toml`.

## Environment Variables

| Variable | Description | Required |
|----------|-------------|---------|
| `GROQ_API_KEY` | API key for Groq services | Yes |
| `LANGCHAIN_API_KEY` | API key for LangSmith (optional) | No |

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments

- Built with [LangGraph](https://github.com/langchain-ai/langgraph)
- Powered by [Groq](https://groq.com/) for fast inference
- API framework provided by [FastAPI](https://fastapi.tiangolo.com/)
