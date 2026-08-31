# Day 2 — Mini Semantic Search Engine using FAISS

## Objective

Build a mini semantic search engine using Python, Sentence Transformers, and FAISS.

The system converts knowledge base sentences into embeddings, stores them in a FAISS vector index, and retrieves the most semantically similar sentences for a user query.

## Tasks Completed

- Created a 10-sentence customer-support knowledge base
- Generated embeddings using `all-MiniLM-L6-v2`
- Verified the embedding matrix shape as `(10, 384)`
- Created a `FAISS IndexFlatL2` index
- Normalized embeddings using `faiss.normalize_L2()`
- Added embeddings to the FAISS index
- Performed top-3 semantic search
- Tested multiple user queries
- Created an interactive CLI search loop
- Documented FAISS theory questions

## Technologies Used

- Python
- Sentence Transformers
- `all-MiniLM-L6-v2`
- FAISS
- NumPy

## Project Structure

```text
Day_2/
│
├── semantic_search.ipynb
├── theory_answers.md
└── README.md