# Day 2 — FAISS Theory Questions

## Q1. What is the difference between IndexFlatL2 and IndexFlatIP in FAISS? When would you use each?

`IndexFlatL2` uses Euclidean (L2) distance to measure how close two vectors are.

`IndexFlatIP` uses Inner Product (IP) to measure similarity between vectors.

### IndexFlatL2

It calculates the Euclidean distance between vectors.

A smaller distance means that the vectors are more similar.

It can be used when Euclidean distance is the desired similarity measure.

### IndexFlatIP

It calculates the inner product between vectors.

A larger inner product means greater similarity.

When embeddings are normalized to unit length, inner product becomes equivalent to cosine similarity.

Therefore, `IndexFlatIP` is commonly used when cosine similarity is required.

### Summary

| Index | Measures | Better Match |
|---|---|---|
| `IndexFlatL2` | Euclidean distance | Smaller value |
| `IndexFlatIP` | Inner product | Larger value |

---

## Q2. Why do we normalise embeddings before adding to FAISS when we want cosine similarity?

Cosine similarity measures the angle between two vectors rather than their magnitude.

When vectors are normalized to unit length, the inner product between two vectors becomes equal to their cosine similarity.

Therefore, normalization allows FAISS to compare vectors based mainly on their direction or semantic meaning rather than their magnitude.

For example:

```text
Original vector
      ↓
Normalization
      ↓
Unit-length vector
      ↓
Cosine similarity

---

## Q3. FAISS uses ANN (Approximate Nearest Neighbour) search. What does "approximate" mean here and why is it acceptable?

Approximate Nearest Neighbour (ANN) search means finding vectors that are very similar to the query without necessarily checking every vector in the database.

An exact search checks all vectors and guarantees the true nearest neighbours. However, this can become slow and expensive when the database contains millions or billions of vectors.

ANN methods make a trade-off between **speed and accuracy**.

### Approximate Search

- It searches for highly similar vectors.
- It is faster than checking every vector.
- It requires fewer computational resources.
- It may not always return the exact nearest neighbour.

### Why is it acceptable?

A small reduction in accuracy is often acceptable because the retrieved results are still highly relevant while the search becomes much faster.

This is especially useful in large-scale applications such as **RAG systems**, where the vector database may contain millions of documents or chunks.

### Important Note

`IndexFlatL2`, which is used in this assignment, actually performs an **exact nearest-neighbour search**, not an approximate search.

FAISS also provides approximate search indexes such as **IVF** and **HNSW**, which are more suitable for very large datasets.

### Summary

| Search Type | Accuracy | Speed | Use Case |
|---|---|---|---|
| Exact Search | Highest | Slower | Small/medium datasets |
| Approximate Search (ANN) | Very high | Faster | Large-scale datasets |
