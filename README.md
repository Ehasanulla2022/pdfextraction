# pdfextraction
Code Explanation
This code implements a Retrieval-Augmented Generation (RAG) pipeline for interacting with PDF files using Sentence Transformers, FAISS vector database, and OpenAI's LLM. The pipeline extracts text from PDFs, embeds the text, and allows users to query for information.

Step-by-Step Code Walkthrough
Import Libraries

PyPDF2: Extracts text from PDF files.
sentence_transformers.SentenceTransformer: Embedding model for converting text into vectors.
FAISS: Vector database for storing and retrieving embeddings.
OpenAI: OpenAI's language model for generating responses.
RetrievalQA: A LangChain wrapper that combines retriever and question-answering components.
Extract Text from PDF
The extract_text_from_pdf() function:

Opens the given PDF file using PyPDF2.
Extracts text from all pages.
Chunk the Text
The chunk_text() function:

Splits the extracted text into smaller chunks (default size = 500 characters).
This improves granularity and makes embeddings more manageable for retrieval.
Embed the Chunks

A pre-trained embedding model sentence-transformers/all-MiniLM-L6-v2 is used.
Each text chunk is converted into a numerical vector representation.
Store Chunks in FAISS Vector Database
The store_embeddings_in_faiss() function:

Stores the text chunks and their embeddings in a FAISS vector database for similarity search.
Create RAG Pipeline
The create_rag_pipeline() function:

Initializes the OpenAI language model (text-davinci-003).
Configures a retriever using FAISS for similarity search (returns top 5 most similar chunks).
Combines the retriever and LLM into a RAG pipeline using RetrievalQA.
Handle User Queries
The handle_query() function:

Accepts a user query.
Uses the RAG pipeline to retrieve relevant chunks and generate an answer.
Main Function

Extracts and processes text from a sample PDF.
Builds the RAG pipeline.
Demonstrates the pipeline with two queries:
Unemployment information based on type of degree
Tabular data from page 6
Pre-requirements for Running the Code
Python Installation
Ensure Python is installed. Recommended version: Python 3.8+.

Required Libraries
Install the necessary Python packages using pip:

bash
Copy code
pip install PyPDF2 sentence-transformers langchain openai faiss-cpu pandas
PyPDF2: For reading and extracting text from PDFs.
sentence-transformers: For text embeddings.
langchain: Framework for chaining LLMs and retrievers.
openai: OpenAI library for accessing LLM models.
faiss-cpu: FAISS for storing and retrieving embeddings efficiently.
pandas: (Optional) For handling structured data.
Set OpenAI API Key
You need an OpenAI API key to use text-davinci-003.

Create an account at OpenAI.
Generate an API key.
Set it in your environment:
bash
Copy code
export OPENAI_API_KEY='your_api_key_here'  # For Unix/Linux
set OPENAI_API_KEY=your_api_key_here       # For Windows
Sample PDF File
Place the PDF file (e.g., example.pdf) in the same directory as the script. Ensure the PDF contains textual content.

How the Code Works
The pipeline extracts text from the PDF, splits it into smaller chunks, and generates embeddings using all-MiniLM-L6-v2.
The embeddings are stored in the FAISS vector database.
When a user asks a question, the query is embedded, and FAISS performs a similarity search to retrieve relevant text chunks.
The retrieved chunks are passed to the OpenAI model, which generates a response based on the query.
Output Example
Query 1: What is the unemployment information based on the type of degree?
Response: The unemployment rate for different degrees is ...

Query 2: Provide tabular data from page 6.
Response: Here is the tabular data retrieved from the document:

Degree	Unemployment Rate
Associate	3.1%
Bachelor	2.4%
Notes
If OpenAI usage costs are a concern, consider using local LLMs (e.g., HuggingFace models) instead of text-davinci-003.
FAISS efficiently handles large-scale embedding retrieval. If your data grows, FAISS can scale accordingly.
The chunk size of 500 characters can be adjusted depending on the data size and granularity.
This code demonstrates an efficient and scalable implementation of a RAG pipeline for PDFs!
