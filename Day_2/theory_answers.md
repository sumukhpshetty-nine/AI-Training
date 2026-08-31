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

Approximate Nearest Neighbour (ANN) search means that the system tries to find vectors that are very close to the query without necessarily checking every vector in the database.

An exact search guarantees the true nearest neighbours, but it can become computationally expensive when the database contains millions or billions of vectors.

ANN methods trade a small amount of accuracy for significantly faster search.

This trade-off is acceptable in many real-world applications because:

- Search becomes much faster.
- Less computational resources are required.
- The retrieved results are usually highly relevant.
- It allows vector search to scale to very large datasets.

> **Note:** `IndexFlatL2`, which is used in this assignment, actually performs an **exact nearest-neighbour search**, not an approximate search. ANN indexes in FAISS include methods such as IVF and HNSW, which are designed for faster searches on large datasets.