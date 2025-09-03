# RAG Chatbot - Expert Knowledge Worker

A comprehensive Retrieval Augmented Generation (RAG) chatbot implementation designed to serve as an expert knowledge worker for tech companies. This project provides accurate, cost-effective question-answering capabilities by combining document retrieval with large language models.

## 🎯 Overview

This RAG pipeline creates an intelligent chatbot that can answer questions based on your company's knowledge base with high accuracy. The system uses vector embeddings to find relevant documents and combines them with LLM responses to provide contextually accurate answers.

### Key Features

- **Document Processing**: Automatically processes documents from your knowledge base
- **Vector Storage**: Creates and manages vector embeddings for semantic search
- **Interactive Chat**: Web-based chat interface using Gradio
- **Visualization**: 2D/3D vector space visualization for understanding document relationships
- **Conversation Memory**: Maintains context across conversation turns
- **Flexible Architecture**: Supports multiple embedding and vector database options

## 🚀 Quick Start

### Prerequisites

- Python 3.8+
- OpenAI API key (or alternatives as described below)

### Installation

1. Clone the repository:
```bash
git clone https://github.com/Sameeh07/RAG_Chatbot.git
cd RAG_Chatbot
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Set up environment variables:
```bash
# Create .env file
echo "OPENAI_API_KEY=your_openai_api_key_here" > .env
```

4. Create your knowledge base structure:
```
knowledge-base/
├── company/
│   └── *.md files
├── products/
│   └── *.md files
├── employees/
│   └── *.md files
└── contracts/
    └── *.md files
```

### Usage

1. Open the Jupyter notebook:
```bash
jupyter notebook RAG.ipynb
```

2. Run all cells to:
   - Load and process your documents
   - Create vector embeddings
   - Set up the conversation chain
   - Launch the Gradio chat interface

3. Access the chat interface in your browser and start asking questions!


### Data Flow

```
Documents → Text Splitting → Embeddings → Vector Store → Retrieval → LLM → Response
```

## 🔧 Configuration Options

### Embedding Models

The system supports multiple embedding options:

#### 1. OpenAI Embeddings (Default)
```python
from langchain_openai import OpenAIEmbeddings
embeddings = OpenAIEmbeddings()
```

#### 2. HuggingFace Sentence Transformers (Free Alternative)
```python
from langchain.embeddings import HuggingFaceEmbeddings
embeddings = HuggingFaceEmbeddings(model_name="sentence-transformers/all-MiniLM-L6-v2")
```

#### 3. Google BERT Models
```python
from langchain.embeddings import HuggingFaceEmbeddings
# Using BERT-based models
embeddings = HuggingFaceEmbeddings(model_name="bert-base-uncased")
```

#### 4. Llama.cpp (Local Processing)
```python
from langchain.embeddings import LlamaCppEmbeddings
embeddings = LlamaCppEmbeddings(model_path="path/to/your/model.bin")
```

### Vector Databases

Choose from multiple vector database options:

#### 1. Chroma DB (Default - SQLite-based)
```python
from langchain_chroma import Chroma
vectorstore = Chroma.from_documents(
    documents=chunks, 
    embedding=embeddings, 
    persist_directory="vector_db"
)
```

#### 2. FAISS (Facebook AI Similarity Search)
```python
from langchain.vectorstores import FAISS
vectorstore = FAISS.from_documents(chunks, embeddings)
# Save for persistence
vectorstore.save_local("faiss_index")
```

#### 3. Pinecone (Cloud-based)
```python
from langchain.vectorstores import Pinecone
import pinecone

pinecone.init(api_key="your_pinecone_api_key", environment="your_env")
vectorstore = Pinecone.from_documents(chunks, embeddings, index_name="your_index")
```

### Language Models

#### OpenAI Models (Default)
```python
from langchain_openai import ChatOpenAI
llm = ChatOpenAI(temperature=0.7, model_name="gpt-4o-mini")
```

#### Local Models with Ollama
```python
llm = ChatOpenAI(
    temperature=0.7, 
    model_name='llama3.2', 
    base_url='http://localhost:11434/v1', 
    api_key='ollama'
)
```

## 📊 Vector Visualization

The notebook includes visualization capabilities to understand how your documents are embedded in vector space:

- **2D Visualization**: t-SNE reduction for document clustering analysis
- **3D Visualization**: Enhanced spatial understanding of document relationships
- **Color Coding**: Documents grouped by type for easy identification

## 🛠️ Dependencies

### Required Packages

```
langchain
langchain-openai
langchain-chroma
chromadb
gradio
python-dotenv
numpy
matplotlib
plotly
scikit-learn
```


### Performance Optimization

- **Embedding Models**: Sentence-transformers models are faster but may be less accurate than OpenAI
- **Vector Databases**: FAISS is faster for large datasets; Pinecone offers cloud scalability
- **Chunk Size**: Balance between context richness (larger chunks) and precision (smaller chunks)


## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request


## 🙏 Acknowledgments

- [LangChain](https://langchain.com/) for the RAG framework
- [Chroma](https://www.trychroma.com/) for the vector database
- [OpenAI](https://openai.com/) for embeddings and language models
- [Gradio](https://gradio.app/) for the chat interface

---

**Note**: This RAG chatbot is designed for internal company use. Ensure your knowledge base doesn't contain sensitive information that shouldn't be processed by external APIs when using cloud-based models.
