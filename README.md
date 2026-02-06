# Retrieval-Augmented Generation (RAG) System

This project implements a Retrieval-Augmented Generation (RAG) system using Langchain to answer questions based on a provided set of PDF documents.

## Project Description
This RAG system allows users to query a collection of PDF documents using natural language. The system retrieves relevant information from the documents and then uses a Large Language Model (LLM) to generate coherent and context-aware answers. This approach ensures that the answers are grounded in the provided documents, reducing the likelihood of hallucination.

## Features
- **Document Loading**: Loads PDF documents from a specified folder.
- **Text Chunking**: Splits documents into smaller, manageable chunks to improve retrieval accuracy.
- **Embeddings**: Converts text chunks into numerical vectors (embeddings) using a pre-trained sentence transformer model (`all-MiniLM-L6-v2`).
- **Vector Store**: Stores and indexes the document embeddings in a Chroma vector database for efficient semantic search.
- **Contextual Retrieval**: Retrieves the most relevant document chunks based on the user's query.
- **LLM Integration**: Uses an Ollama-hosted `llama3` model to generate answers, guided by the retrieved context.
- **Interactive Query Interface**: Provides a simple command-line interface to ask questions.

## Technologies Used
- Python
- Langchain (for orchestrating the RAG pipeline)
- PyPDFLoader (for loading PDF documents)
- RecursiveCharacterTextSplitter (for text chunking)
- HuggingFaceEmbeddings (for creating document embeddings)
- Chroma (as the vector database)
- Ollama (for running the `llama3` Large Language Model locally or remotely)

## Setup

### 1. Install Dependencies
First, install all the necessary Python packages:

```bash
pip install langchain langchain-community langchain-huggingface langchain-chroma langchain-ollama pypdf sentence-transformers

2. Prepare Documents

Place your PDF documents in a folder named sample_docs within your project directory, or update the folder_path variable in the main function to point to your document directory.

Example structure:

./
├── sample_docs/
│   ├── document1.pdf
│   └── document2.pdf
└── your_script.py

3. Run Ollama

This project relies on an Ollama server running the llama3 model. If you don't have Ollama set up, follow the instructions on the Ollama website to install and run it. Then, pull the llama3 model:

ollama run llama3

Ensure your Ollama server is accessible from where you are running this script. If running in Google Colab, you might need to set up a tunnel or ensure Ollama is hosted on an accessible machine.
Usage

    Run the script:

    # Assuming your code is in a file like `rag_system.py`
    python rag_system.py

    Vector Database Initialization: The script will first check for an existing vector database (./chroma_db). If not found, it will load your PDF documents, chunk them, create embeddings, and build a new Chroma vector store. This process might take some time depending on the number and size of your documents.

    No vector DB found, creating one
    Loading /content/sample_data/sample_docs/document1.pdf
    Created X chunks
    Vector DB created

    If the vector database already exists, it will be loaded directly:

    Loading vector DB

    Ask Questions: Once the vector store is ready, you can start asking questions in the command line:

    Ask a questions : What is RAG?
    Thinking...

     Answer:  
     Retrieval-Augmented Generation (RAG) is a technique that combines information retrieval with text generation, allowing large language models (LLMs) to access and incorporate external knowledge bases to produce more accurate and relevant responses. It addresses the limitations of LLMs that might otherwise hallucinate or provide outdated information by grounding the generated answers in factual, retrieved documents.

    Exit: Type exit to quit the application.

    Ask a questions : exit

Project Structure

    rag_system.py (or your main script): Contains the core logic for loading documents, chunking, embedding, vector store management, and the RAG query system.
    sample_docs/: Directory containing your PDF documents.
    chroma_db/: Directory where the Chroma vector database will be persisted.

Troubleshooting

    ConnectError: [Errno 111] Connection refused: This error indicates that the Ollama server is not running or is not accessible. Ensure Ollama is running (ollama serve) and the llama3 model is available. If in Colab, verify network access or run Ollama within the Colab environment.
    Document Loading Errors: Check if your PDF files are valid and not corrupted
