## 1. Quick Component Mapping

$$\begin{aligned}
\mathbf{Retriever} &\longrightarrow \text{Context Precision, Context Recall, MAP@K, MRR@K, NDCG@K, Context Relevancy} \\
\mathbf{Generator\ (LLM)} &\longrightarrow \text{Faithfulness / Groundedness, Answer Relevancy, Answer Accuracy}
\end{aligned}$$

---

## 2. Master Metrics Summary Table

| Metric | Target | Inputs Required | Range | Core Method / Formula | Key Focus |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Context Precision@K** | Retriever | Query, Chunks, Ground Truth | $[0, 1]$ | $\frac{\sum (\text{Precision@k} \times v_k)}{\text{Total Relevant in Top-K}}$ | Ranks relevant chunks at the top. |
| **Context Recall@K** | Retriever | Chunks, Reference Answer | $[0, 1]$ | $\frac{\text{Supported Reference Claims}}{\text{Total Reference Claims}}$ | Measures context completeness. |
| **MAP@K** | Retriever | Batch Queries, Ground Truth | $[0, 1]$ | $\frac{1}{\|Q\|} \sum \text{AP@K}(q)$ | Average ranking quality across multiple queries. |
| **MRR@K** | Retriever | Query, Chunks, Ground Truth | $[0, 1]$ | $\frac{1}{\text{Rank of 1st Relevant Result}}$ | How fast the system finds the *first* correct chunk. |
| **NDCG@K** | Retriever | Query, Chunks, Ground Truth | $[0, 1]$ | $\frac{\text{DCG@K}}{\text{IDCG@K}}$ | Non-binary, graded relevance positional ranking. |
| **Context Relevancy** | Retriever | Query, Chunks | $[0, 1]$ | Dual LLM prompts ($0, 1, 2$) $\rightarrow$ Normalized average | Measures signal-to-noise ratio in retrieved text. |
| **Faithfulness / Groundedness** | Generator | Response, Chunks | $[0, 1]$ | $\frac{\text{Supported Response Claims}}{\text{Total Response Claims}}$ | Detects hallucinations (LLM adhering to context). |
| **Answer Relevancy** | Generator | Query, Response | $[0, 1]$ | Cosine similarity of Query vs. Generated Queries | Detects evasiveness or off-topic responses. |
| **Answer Accuracy** | Generator | Response, Reference Answer | Scale $0,2,4 \rightarrow [0, 1]$ | Dual-perspective prompt swap (Direct vs. Reversed) | Exact factual alignment with ground truth. |

---

## 3. The RAG Triad (TruLens)

1. **Context Relevance:** $(\text{Query} \leftrightarrow \text{Retrieved Context})$ — Did the retriever find useful context?
2. **Groundedness:** $(\text{Retrieved Context} \leftrightarrow \text{Response})$ — Is the response factual only to the context?
3. **Answer Relevance:** $(\text{Query} \leftrightarrow \text{Response})$ — Did the LLM actually answer what was asked?

---

## 4. NVIDIA LLM-as-a-Judge Evaluation Logic
* **Answer Accuracy:** Rates $0, 2, 4$ using role-swapped templates (Response vs. Reference).
* **Response Groundedness:** Rates $0, 1, 2$ using dual prompts $\rightarrow$ Divided by $2$ for $[0, 1]$ normalization.
* **Context Relevancy:** Rates $0, 1, 2$ using dual prompts $\rightarrow$ Divided by $2$ for $[0, 1]$ normalization.

---

## 5. Cheat Sheet Decision Matrix (Debugging RAG)

| Low Metric | Root Cause | How to Fix |
| :--- | :--- | :--- |
| **Low Context Recall** | Retriever missed crucial info. | Increase $K$, adjust chunk size, improve embeddings. |
| **Low Context Precision / Relevancy** | Retriever brought too much noise. | Add a cross-encoder Reranker, fine-tune vector search. |
| **Low Faithfulness / Groundedness** | LLM hallucinated facts. | Reduce LLM temperature, adjust system prompt ("Answer *only* using context"). |
| **Low Answer Relevancy** | LLM drifted off-topic. | Improve generation prompt structure, add strict response schemas. |
