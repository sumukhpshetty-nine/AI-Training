# Day 1 — Mini RAG Chatbot

## 📌 Project Overview

This project implements a **Mini Retrieval-Augmented Generation (RAG) Chatbot** that can answer questions based on the content of a PDF document.

The chatbot retrieves relevant information from the PDF and provides it as context to Google's Gemini language model, which then generates the final answer.

The project demonstrates the fundamental components of a RAG pipeline, including:

* PDF text extraction
* Text cleaning
* Text chunking
* Text embeddings
* Vector storage
* Semantic search
* Context retrieval
* Prompt engineering
* LLM-based answer generation

---

## 🎯 Objective

The objective of this assignment is to understand and implement the basic workflow of a Retrieval-Augmented Generation system.

Instead of asking an LLM to answer questions using only its pre-trained knowledge, the chatbot first retrieves relevant information from a provided PDF and uses that information to generate the answer.

---

## 🧠 What is RAG?

**Retrieval-Augmented Generation (RAG)** combines information retrieval with a Large Language Model.

The basic workflow is:

```text
PDF Document
     ↓
Text Extraction
     ↓
Text Cleaning
     ↓
Text Chunking
     ↓
Gemini Embeddings
     ↓
FAISS Vector Store
     ↓
Semantic Search
     ↓
Relevant Chunks
     ↓
RAG Prompt
     ↓
Gemini LLM
     ↓
Final Answer
```

The retrieval step helps the LLM answer questions using information from the provided document.

---

## 🛠️ Technologies Used

| Technology       | Purpose                               |
| ---------------- | ------------------------------------- |
| Python           | Main programming language             |
| Jupyter Notebook | Development environment               |
| PyPDF            | PDF text extraction                   |
| Google Gemini    | Text embeddings and answer generation |
| FAISS            | Vector storage and similarity search  |
| NumPy            | Numerical operations                  |
| python-dotenv    | Loading API keys from `.env`          |

---

## 📂 Project Structure

```text
Day_1/
│
├── Mini_RAG_Chatbot.ipynb
├── README.md
├── requirements.txt
└── .gitignore
```

### Files

**`Mini_RAG_Chatbot.ipynb`**

Contains the complete implementation of the Mini RAG Chatbot.

**`README.md`**

Contains the project documentation and implementation details.

**`requirements.txt`**

Contains the Python dependencies required to run the project.

**`.gitignore`**

Prevents sensitive and unnecessary files such as `.env`, virtual environments, and notebook checkpoints from being committed to GitHub.

---

## 🔄 Implementation Steps

### 1. Project Setup

Set up the Python environment and install the required libraries.

### 2. Load PDF

The PDF document is loaded using PyPDF.

### 3. Text Extraction

Text is extracted from the pages of the PDF.

### 4. Text Cleaning

Unnecessary spaces, line breaks, and other unwanted characters are cleaned from the extracted text.

### 5. Text Chunking

The cleaned document is divided into smaller overlapping chunks.

```text
Document
   ↓
Chunk 1
Chunk 2
Chunk 3
...
Chunk N
```

Overlapping chunks help preserve context between consecutive chunks.

### 6. Generate Embeddings

Each text chunk is converted into a numerical vector using Google's Gemini embedding model.

These embeddings represent the semantic meaning of the text.

### 7. FAISS Vector Store

The generated embeddings are stored in a FAISS index.

FAISS allows efficient similarity searches between vectors.

### 8. Semantic Search

When the user asks a question:

1. The question is converted into an embedding.
2. FAISS compares the question embedding with the stored document embeddings.
3. The most relevant chunks are retrieved.

### 9. RAG Prompt & Answer Generation

The retrieved chunks are combined with the user's question to create a RAG prompt.

Gemini is instructed to answer using the retrieved document context.

If the required information is not available in the retrieved context, the chatbot is instructed to indicate that the answer is not available in the document.

### 10. Chatbot Function

The complete RAG pipeline is combined into a reusable function:

```text
User Question
      ↓
Question Embedding
      ↓
FAISS Search
      ↓
Relevant Chunks
      ↓
Context + Question
      ↓
Gemini
      ↓
Answer
```

### 11. Testing

The chatbot is tested with:

* Questions whose answers exist in the PDF
* Questions about different sections of the PDF
* Questions whose answers are not present in the PDF

This helps verify whether the chatbot is actually using the retrieved document context.

---

## 🔑 Environment Variables

The Gemini API key is stored in a `.env` file.

Example:

```text
GEMINI_API_KEY=your_api_key_here
```

The `.env` file should **never be committed to GitHub**.

Make sure `.gitignore` contains:

```text
.env
.venv/
__pycache__/
.ipynb_checkpoints/
```

---

## ▶️ How to Run

### 1. Clone the repository

```bash
git clone <your-github-repository-url>
```

### 2. Navigate to Day 1

```bash
cd AI_Training_Assignments/Day_1
```

### 3. Create and activate the virtual environment

```bash
python3 -m venv .venv
```

Activate it:

```bash
source .venv/bin/activate
```

### 4. Install dependencies

```bash
pip install -r requirements.txt
```

### 5. Configure the Gemini API key

Create a `.env` file:

```text
GEMINI_API_KEY=your_api_key_here
```

### 6. Open the notebook

Open:

```text
Mini_RAG_Chatbot.ipynb
```

in VS Code or Jupyter Notebook.

### 7. Run the notebook

Execute the cells sequentially from the beginning.

---

## 📚 Learning Outcomes

By completing this assignment, the following concepts were practiced:

* Understanding the RAG architecture
* Extracting text from PDFs
* Cleaning unstructured text
* Splitting documents into chunks
* Understanding embeddings
* Creating vector representations of text
* Using FAISS for similarity search
* Performing semantic retrieval
* Building RAG prompts
* Using Gemini for LLM-based generation
* Building a basic question-answering chatbot
* Managing API keys securely
* Structuring an ML/AI project for GitHub

---

## 🚀 Future Improvements

Possible improvements to this project include:

* Using LangChain for pipeline management
* Using a more advanced text splitter
* Adding metadata to document chunks
* Improving retrieval using similarity thresholds
* Adding conversation memory
* Building a Streamlit interface
* Supporting multiple PDF documents
* Adding source citations to answers
* Implementing hybrid search
* Evaluating retrieval and answer quality

---

## ✅ Day 1 Status

**Mini RAG Chatbot — Completed**

```text
PDF Extraction       ✅
Text Cleaning        ✅
Text Chunking        ✅
Gemini Embeddings    ✅
FAISS Vector Store   ✅
Semantic Search      ✅
RAG Prompt           ✅
Gemini LLM           ✅
Chatbot Function     ✅
Testing              ✅
```
