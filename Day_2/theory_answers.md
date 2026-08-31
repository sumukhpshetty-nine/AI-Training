# Day 2 — FAISS Theory Questions

## Q1. Difference between `IndexFlatL2` and `IndexFlatIP`

FAISS supports different distance/similarity metrics depending on the index type. `IndexFlatL2` and `IndexFlatIP` differ in how they measure closeness between vectors.

**`IndexFlatL2`**
- Uses **Euclidean (L2) distance** to measure how far apart two vectors are.
- A **smaller distance** indicates higher similarity.
- Best suited when the actual geometric distance between vectors matters — for example, when vector magnitude carries meaningful information.

**`IndexFlatIP`**
- Uses **Inner Product (dot product)** to measure similarity.
- A **larger inner product** indicates higher similarity.
- If embeddings are **normalized to unit length**, the inner product becomes mathematically equivalent to **cosine similarity**.
- Commonly used when cosine similarity is the desired metric (typical in text/semantic search).

**Summary**

| Index | Metric | Better Match | Typical Use Case |
|---|---|---|---|
| `IndexFlatL2` | Euclidean distance | Smaller value | Distance-sensitive tasks, raw (unnormalized) embeddings |
| `IndexFlatIP` | Inner product | Larger value | Cosine-similarity search (requires normalized vectors) |

---

## Q2. Why normalize embeddings before adding them to FAISS for cosine similarity?

Cosine similarity is defined as the **cosine of the angle** between two vectors — it captures *direction*, not magnitude:

$$\cos(\theta) = \frac{A \cdot B}{\|A\| \|B\|}$$

FAISS's `IndexFlatIP` only computes the raw dot product (\(A \cdot B\)), without dividing by the vector norms. This means:

- If vectors are **not normalized**, the inner product is influenced by both direction *and* magnitude, which can distort similarity rankings (a longer vector could score higher even if less semantically similar).
- If vectors are **normalized to unit length** (\(\|A\| = \|B\| = 1\)), the denominator becomes 1, and the dot product becomes **exactly equal to cosine similarity**.

So normalization is what lets `IndexFlatIP` behave as a cosine similarity search — it removes magnitude from the equation and leaves only the semantic direction of the vectors.

**Process:**
```text
Original vector
      ↓
Normalization
      ↓
Unit-length vector
      ↓
Cosine similarity
```

---

## Q3. What does "approximate" mean in ANN search, and why is it acceptable?

**Approximate Nearest Neighbour (ANN)** search finds vectors that are *very close* to a query vector without exhaustively comparing it against every vector in the database.

This is in contrast to **exact search**, which checks all vectors and guarantees the true nearest neighbours — but becomes computationally expensive as the dataset grows to millions or billions of vectors.

ANN methods trade a small amount of accuracy for a large gain in speed and efficiency.

**Characteristics of approximate search:**
- Retrieves highly similar (not always the mathematically closest) vectors.
- Much faster than brute-force comparison.
- Uses less memory and computation.
- May occasionally miss the single true nearest neighbour.

**Why this trade-off is acceptable:**
In practice, the small drop in exactness rarely affects usefulness — the results returned are still highly relevant. This makes ANN ideal for large-scale applications such as **RAG (Retrieval-Augmented Generation) systems**, where the vector store may contain millions of document chunks and query latency matters more than perfect precision.

> **Note:** `IndexFlatL2` (used in this assignment) actually performs **exact** nearest-neighbour search — it compares the query against every stored vector. FAISS also offers genuinely approximate indexes like **IVF** and **HNSW**, designed for large-scale datasets where exact search would be too slow.

**Summary**

| Search Type | Accuracy | Speed | Best Use Case |
|---|---|---|---|
| Exact Search (e.g., `IndexFlatL2`) | Highest | Slower on large data | Small/medium datasets |
| Approximate Search (ANN, e.g., IVF, HNSW) | Very high (not guaranteed exact) | Much faster | Large-scale datasets (millions+ vectors) |
