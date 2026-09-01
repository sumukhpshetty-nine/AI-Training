# Day 3 — Agentic AI Meeting Preparation Assistant

## Objective

Build an Agentic AI Meeting Preparation Assistant that helps a user prepare for an upcoming client meeting.

The assistant gathers information from multiple sources using RAG, vector search, memory, and tools, and uses an LLM to generate a concise meeting preparation brief.

The main goal is to demonstrate an agentic workflow involving:

- Retrieval-Augmented Generation (RAG)
- Vector database search
- Short-term memory
- Long-term memory
- Tool usage
- Multi-tool retrieval
- LLM-based response generation

---

## Problem Statement

A manager may have only a few minutes before an important client meeting and may need to search through different documents, previous meeting notes, and stored information.

Instead of manually searching through multiple sources, the AI assistant can gather the relevant information automatically.

### Example

User:

> Prepare me for my meeting with Acme Corp.

The assistant retrieves:

- Client information
- Project information
- Previous meeting discussions
- Client concerns
- Open action items
- Relevant long-term memories

It then combines the retrieved information and generates a concise meeting preparation brief.

---

# Project Architecture

```text
                         User
                           |
                           v
                    Agent / Gemini
                           |
                    Tool Selection
                           |
          +----------------+----------------+
          |                |                |
          v                v                v
   Document Search    Meeting Notes    Memory Retrieval
          |                |                |
          +----------------+----------------+
                           |
                           v
                    Retrieved Context
                           |
                           v
                     Gemini LLM
                           |
                           v
                  Meeting Preparation
                        Brief
                           |
                           v
                  Short-Term Memory
````

---

# Technologies Used

* Python
* Google Gemini API
* Sentence Transformers
* `all-MiniLM-L6-v2`
* FAISS
* NumPy
* JSON
* Jupyter Notebook

---

# Key Components

## 1. RAG — Retrieval-Augmented Generation

The system uses RAG to retrieve relevant information from the available documents before generating an answer.

The workflow is:

```text
Documents
    |
    v
Text Extraction
    |
    v
Text Chunking
    |
    v
Embeddings
    |
    v
FAISS Vector Store
    |
    v
Semantic Search
    |
    v
Relevant Context
    |
    v
Gemini
    |
    v
Answer
```

This prevents the model from relying only on its general knowledge and allows it to answer using the provided project information.

---

## 2. Embeddings

The project uses:

```text
all-MiniLM-L6-v2
```

to convert text into numerical vectors.

These embeddings allow semantically similar text to be retrieved even when the exact keywords are different.

Example:

```text
Query:
"Acme's main problems"

Relevant document:
"Acme has raised concerns about API integration delays."
```

The semantic similarity between the query and document allows the relevant information to be retrieved.

---

## 3. FAISS Vector Database

FAISS is used to store and search the document embeddings.

The vector search process is:

```text
User Query
    |
    v
Query Embedding
    |
    v
FAISS Search
    |
    v
Top Relevant Chunks
```

FAISS enables fast similarity search over the embedded documents.

---

# 4. Tools

The agent uses multiple tools to gather information.

### Document Search Tool

Used to retrieve information from the available client and project documents.

Examples:

* Client information
* Project status
* Requirements
* Technical issues
* Client concerns

### Meeting Notes Tool

Used to retrieve information from previous meetings.

Examples:

* Previous discussions
* Meeting concerns
* Open action items
* Previous decisions

### Memory Retrieval Tool

Used to retrieve relevant information stored in long-term memory.

Examples:

* Client preferences
* Important previous information
* Historical context

---

# 5. Short-Term Memory

Short-term memory maintains the context of the current conversation.

For example:

```text
User:
Prepare me for my meeting with Acme Corp.

Assistant:
Acme Corp is concerned about API integration delays.

User:
What should I discuss with them?

Assistant:
Discuss the API integration timeline and outstanding issues.
```

The assistant understands that "them" refers to Acme Corp because the previous conversation is stored in short-term memory.

Short-term memory is maintained using the current conversation history.

---

# 6. Long-Term Memory

Long-term memory stores important information that should remain available across sessions.

FAISS stores the vector representations of the memories, while a JSON file stores the original memory text.

```text
Long-Term Memory
       |
       +---- FAISS Index
       |
       +---- JSON Memory File
```

The memory is saved to disk so that it can be loaded again when the application starts.

This allows the system to retrieve information from previous sessions.

---

# 7. Agentic Workflow

The system does not simply answer questions directly.

Instead, the agent determines which tools are required and retrieves information before generating a response.

For example:

```text
User:
What concerns has Acme previously mentioned?

        |
        v

Agent decides which tools are required

        |
        +---- Document Search
        |
        +---- Meeting Notes
        |
        +---- Memory Retrieval

        |
        v

Retrieved Information

        |
        v

Gemini

        |
        v

Final Answer
```

For requests requiring information from multiple sources, the agent can execute multiple tools and combine their results.

---

# 8. Meeting Preparation Brief

The main feature of the application is the meeting preparation assistant.

For a request such as:

```text
Prepare me for my meeting with Acme Corp.
```

the system gathers information from:

* Client documents
* Previous meeting notes
* Long-term memory

The final meeting brief is designed to contain:

```text
1. Client Overview
2. Key Concerns
3. Previous Meeting Discussion
4. Open Action Items
5. Important Contacts
6. Recommended Talking Points
7. Next Steps
```

This gives the manager a quick overview before the meeting.

---

# Project Structure

```text
Day_3/
│
├── Agentic_Meeting_Preparation_Assistant.ipynb
│
├── README.md
│
├── requirements.txt
│
├── data/
│   ├── client_documents/
│   └── meeting_notes/
│
├── memory/
│   ├── long_term_memory.index
│   └── long_term_memories.json
│
└── screenshots/
```

---

# Installation

Create and activate the virtual environment:

```bash
python3 -m venv .venv
```

Activate it:

```bash
source .venv/bin/activate
```

Install the required packages:

```bash
pip install -r requirements.txt
```

---

# API Key Configuration

Create a `.env` file in the project directory.

```text
GEMINI_API_KEY=your_api_key_here
```

The API key should not be written directly inside the notebook.

Also make sure `.env` is included in `.gitignore`:

```text
.env
.venv/
__pycache__/
.ipynb_checkpoints/
```

Never commit the API key to GitHub.

---

# Running the Project

Activate the virtual environment:

```bash
source .venv/bin/activate
```

Start Jupyter Notebook or open the project in VS Code.

Run the notebook cells in order.

The main workflow can then be tested with:

```python
answer = run_agent(
    "Prepare me for my meeting with Acme Corp."
)

print(answer)
```

---

# Example Workflow

```text
User Request
     |
     v
"Prepare me for my meeting with Acme Corp."
     |
     v
Agent
     |
     +-----------------------+
     |                       |
     v                       v
Retrieve Information    Retrieve Memory
     |                       |
     +-----------+-----------+
                 |
                 v
          Combine Context
                 |
                 v
              Gemini
                 |
                 v
        Meeting Preparation
              Brief
```

---

# Assignment Requirements

| Requirement               | Status           |
| ------------------------- | ---------------- |
| RAG                       | Completed        |
| Vector Database           | FAISS            |
| Embeddings                | all-MiniLM-L6-v2 |
| Short-Term Memory         | Completed        |
| Long-Term Memory          | Completed        |
| Agentic Workflow          | Completed        |
| Document Search Tool      | Completed        |
| Meeting Notes Tool        | Completed        |
| Memory Retrieval Tool     | Completed        |
| Multi-Tool Workflow       | Completed        |
| Meeting Preparation Brief | Implemented      |
| Source Code               | Included         |
| README.md                 | Included         |
| requirements.txt          | Included         |
| Sample Documents          | Included         |
| Screenshots               | Included         |

---

# Learning Outcomes

Through this project, the following concepts were implemented:

* Document retrieval
* Text chunking
* Embeddings
* Semantic search
* FAISS vector databases
* Retrieval-Augmented Generation
* Prompt engineering
* Short-term conversational memory
* Persistent long-term memory
* Tool-based AI agents
* Multi-tool workflows
* Meeting preparation automation

---

# Conclusion

This project demonstrates an Agentic AI workflow where the system can reason about a user's request, select and use appropriate tools, retrieve relevant information, use short-term and long-term memory, and generate a useful meeting preparation brief.

The project goes beyond a simple question-answering chatbot by combining:

```text
Reasoning
    +
RAG
    +
Vector Search
    +
Tool Usage
    +
Short-Term Memory
    +
Long-Term Memory
    +
LLM Generation
```

to solve a practical business problem.

````

### One small change

Since your **Gemini quota is currently exhausted**, don't claim that you successfully generated the final polished meeting brief if you haven't actually captured one. You can keep:

```text
Meeting Preparation Brief | Implemented
````

because the implementation is there, but when you get Gemini access again, run the final test and take a screenshot of the generated brief. That will make the submission much stronger.
