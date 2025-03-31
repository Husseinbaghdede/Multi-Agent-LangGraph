# LangGraph RAG Router

A sophisticated question-answering system that intelligently routes queries between a custom vector store and Wikipedia based on the question content.

## Overview

This project demonstrates how to build an intelligent routing system using LangGraph, LangChain, and Astra DB. The application analyzes user questions and automatically determines the most appropriate knowledge source to query:

- **Vector Store**: For questions about agents, prompt engineering, and adversarial attacks (using pre-indexed blog posts)
- **Wikipedia API**: For general knowledge questions

## Features

- **Smart Query Routing**: Uses LLM-based classification to direct questions to the appropriate data source
- **Vector Search with Astra DB**: Stores and retrieves document embeddings for specialized topics
- **Wikipedia Integration**: Accesses Wikipedia for general knowledge questions
- **Streaming Architecture**: Provides incremental updates as the workflow progresses
- **Structured Workflow**: Built with LangGraph for clear, manageable processing steps

## Technical Components

- **LangGraph**: For building the workflow and handling state transitions
- **LangChain**: For document loading, text splitting, and vectorstore interactions
- **Cassandra / Astra DB**: For vector storage and similarity search
- **Groq API**: Powers the LLM for query routing with Llama-3.1-70b-Versatile
- **HuggingFace Embeddings**: Uses all-MiniLM-L6-v2 for document embeddings

## Setup and Installation

1. Clone this repository
2. Install required dependencies:
   ```bash
   pip install cassio langchain langchain_community langchain_huggingface langchain_groq langgraph python-dotenv
   ```
3. Set up environment variables:
   ```
   ASTRA_DB_APPLICATION_TOKEN="your-astra-token"
   ASTRA_DB_ID="your-astra-db-id"
   GROQ_API_KEY="your-groq-api-key"
   ```

## Usage

```python
# Initialize the application
app = workflow.compile()

# Ask a question
inputs = {
    "question": "What is an agent?"
}

# Get a response with reasoning steps
for output in app.stream(inputs):
    for key, value in output.items():
        print(f"Node '{key}':")
        print(value)
        print("\n---\n")
```

## Data Sources

The vector store is pre-populated with content from the following blog posts:
- https://lilianweng.github.io/posts/2023-06-23-agent/
- https://lilianweng.github.io/posts/2023-03-15-prompt-engineering/
- https://lilianweng.github.io/posts/2023-10-25-adv-attack-llm/

## Architecture

1. **Query Routing**: Analyzes the question to determine the appropriate data source
2. **Document Retrieval**: Fetches relevant documents from either vector store or Wikipedia
3. **Response Generation**: Returns the retrieved documents

## License

[Your License Here]

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
