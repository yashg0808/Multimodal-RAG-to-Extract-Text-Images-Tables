# Multimodal RAG with Amazon Titan, FAISS, and Google Gemini

This Jupyter Notebook demonstrates a complete, end-to-end Retrieval-Augmented Generation (RAG) pipeline capable of processing complex PDF documents that contain a mix of text, tables, and images. The system intelligently extracts all content, generates powerful multimodal embeddings using Amazon Titan, retrieves the most relevant information using a FAISS vector store, and generates insightful answers using Google's Gemini Pro model.

## 🚀 Overview

The primary goal of this project is to build a sophisticated question-answering system that goes beyond simple text-based retrieval. By creating a multimodal RAG pipeline, the system can understand and reason over different types of content within a PDF. This allows it to synthesize information from text, analyze data in tables, and interpret visual information from images, leading to more comprehensive and contextually-aware answers.

## ✨ Features

* **Comprehensive PDF Parsing**: Extracts text, tables, and images from every page of a PDF document.
* **Multimodal Embeddings**: Uses Amazon Titan's advanced Multimodal Embeddings model to generate rich vector representations for text, tables, and images.
* **High-Speed Vector Search**: Employs FAISS (Facebook AI Similarity Search) for efficient, in-memory storage and rapid retrieval of embeddings.
* **State-of-the-Art Generation**: Leverages the powerful Google Gemini model to generate human-like, context-aware answers based on the retrieved multimodal information.
* **End-to-End Pipeline**: Provides a single, executable notebook that covers the entire workflow, from data ingestion and processing to final answer generation.

## ⚙️ Workflow

The notebook executes the following steps in sequence:

1.  **Setup**: Installs all necessary Python libraries, including `tabula-py`, `PyMuPDF`, `langchain`, `boto3`, `faiss-cpu`, and the `langchain-google-genai` SDK.
2.  **Data Ingestion**: Downloads the famous research paper "Attention Is All You Need" as a sample PDF to demonstrate the pipeline's capabilities.
3.  **Content Extraction**:
    * Uses `PyMuPDF` to extract raw text and images from each page.
    * Uses `tabula-py` to accurately identify and extract tables into a structured format.
    * Saves each extracted piece of content (text chunk, table, image) as a separate file for organization and reference.
4.  **Embedding Generation**:
    * For each extracted item, it generates a 384-dimensional embedding using the **Amazon Titan Multimodal Embeddings** model, accessed via Amazon Bedrock.
    * Text and table data are passed as `inputText`.
    * Images are passed as base64-encoded `inputImage` strings.
5.  **Vector Indexing**:
    * All generated embeddings are loaded into a **FAISS `IndexFlatL2`** index. This index is stored in memory for extremely fast similarity searches.
6.  **Query and Retrieval**:
    * The user provides a natural language query (e.g., "How is this model different from prior art? Describe its novelty and use cases in detail.").
    * The query is converted into an embedding using the same Amazon Titan model to ensure vector space consistency.
    * The FAISS index is searched to find the top-k most relevant items (which can be a mix of text, tables, or images) based on the query embedding.
7.  **Answer Generation (RAG)**:
    * The retrieved items are compiled into a rich, multimodal context.
    * This context is passed to the **Google Gemini 1.5 Flash** model along with the original query.
    * The model synthesizes the information from the context to generate a detailed, human-readable answer.

## 🛠️ Technologies Used

* **Programming Language**: Python
* **PDF Processing**: `PyMuPDF`, `tabula-py`
* **Machine Learning**:
    * **Embeddings**: Amazon Titan Multimodal Embeddings (via AWS Bedrock)
    * **Vector Store**: `faiss-cpu`
    * **Language Model**: Google Gemini 1.5 Flash
* **Orchestration**: `langchain`
* **Cloud Integration**: `boto3` (for AWS), `langchain-google-genai` (for Google AI)

## 📋 Setup and Installation

1.  **Clone the repository** or download the `Untitled4.ipynb` notebook file.
2.  **Install dependencies**: The notebook installs dependencies directly. For a manual setup, you can create a `requirements.txt` file with the following content and run `pip install -r requirements.txt`:
    ```
    boto3
    langchain
    langchain-aws
    langchain-community
    PyMuPDF
    tabula-py
    faiss-cpu
    tqdm
    requests
    python-dotenv
    langchain-google-genai
    Pillow
    ```
3.  **Set up Credentials**: The notebook is designed to be secure and will prompt you to enter the following credentials when you run the corresponding cells:
    * **AWS Access Key ID**
    * **AWS Secret Access Key**
    * **AWS Region** (e.g., `us-east-1`, `ap-south-1`)
    * **Google API Key**

## ▶️ How to Run

1.  Open the Jupyter Notebook in your preferred environment (like VS Code, Jupyter Lab, or Google Colab).
2.  Run the cells in sequential order from top to bottom.
3.  When prompted, enter your AWS and Google API credentials.
4.  The notebook will automatically handle downloading the sample PDF, processing it, generating embeddings, and building the FAISS index.
5.  To ask your own questions, simply modify the `query` variable in the **"User Query"** section of the notebook.
6.  The final cell will execute the complete RAG pipeline and display the generated answer in a clean Markdown format.
