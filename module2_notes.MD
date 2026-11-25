# Module 2 notes

## All about retrievers

- It seems we will see what they do, how they search and how this can be evaluated.
- Right now for searching we have metadata filtering (not really search), keyword search and semantic search.
- Keyword search can work quite well but is often complemented by semantic search. Can see that a result is on both lists and then it is ranked better when it is on both lists. This is called hybrid search. Metadata filtering is often done at the end. 
- Metadata filtering - like date, access rights, authors. This filtering is often done after the keyword and semantic search results have been returned. 

## Keyword search

- Keyword search - if documents share words with the prompt --bag of words. Word counts stored in a vector. Sparse matrix (vector) with the words per document. 
    - TF (term frequency) scoring - look at the counts per document and normalize for document length
    - TF-IDF - inverse document frequency. So rewards rare words. Often use log of the IDF for each word.
    - Most systems use an updated version of this kind of keyword scoring called BM25. 
- BM25 - for best matching 25 from the 25th from a series of algorithms. Improves on TF-IDF by not being so extreme in the document length normalization (e.g. long documents are not down-weighted as much as in TF-IDF) and also with the term frequency, it saturates at a certain frequency meaning that if a term is seen 10x in a document, a document with the term 20x is not ranked 2x better but maybe 1.3. This is called term frequency saturation. Two tunable hyperparameters b and k that can tune it to your corpus of documents. 
- BM25 is a bag of words approach. Also called lexical search (as opposed to semantic).

## Semantic search


Embedding models map words, sentences or documents to space. More similar things are mapped closer together in vector space. 

Cosine similarity - mesures directions of vectors. Closer to 1 means closer to the same orientation. Cosine similarities range from -1 to 1. -1 vectors face in opposite directions. 
Euclidean distance - distance between words, sentences or documents in vector space. Items closer together show smaller distances. 
Dot product - length of the projection of one vector onto another. If two vectors are of similar length and direction the projection will be larger if at 90 degree angle it will be 0. Opposite directions will be negative. 

Both documents and prompts need to be embedded. Then prompt (or query) is compared to the documents, then documents are ranked based on chosen metrics.

Training embedding models is based on negative and positive pairs. Start with random initializaiton. Then contrastive training process. High dimentional space gives more possibilities to represent different concepts. Only compare vectors from the same embedding models. 


## Combining rankings
- Reciprocal rank fusion - rank in each document, score points based on ranking in each list with a a k "hyperparameter". it is in the denominator so increasing it reduces the differences between the 1st and 10th document (e.g. 1/1+1, 1/1+10 vs. 1/50+1, 1/50+10). 

hyperparameters - are set by hand
Beta - sets the amount of semantic vs keyword weighting. 

## Evaluating retriever search quality
Are we finding the relevant documents and how can we tell if adapting hyperparameters is doing anything?
- Precision - number of relevant documents / number of documents retrieved. 
- Recall - number of relevant documents retrieved / number of relevant documents in the knowledge base.
Often trade precision for recall and vice versa. 
K will influence these values. 

Mean Average Precision (MAP) at K - evaluates average precision for relevant documents in first K documents retrieved. So calculated across many prompts and sets of documents retrieved and then averaged. 

Reciprocal rank -  1 / rank of relevant document
Mean reciprocal rank - do reciprocal rank for all relevant documents and then take the average




## Python notes:

- len(np.shape(x)) is the number of dimensions (x.ndim), not the number of elements.
(3,) is one vector. (2, 3) is a batch of 2 vectors.
- Wrapping a single vector: [v] turns shape (3,) into (1, 3), so the same function handles one vector or many. The built-in is np.atleast_2d(v).
That's why functions return an array even for one score, and why you see [0] at the end.
- ** is the power operator, applied element by element on arrays.
enumerate(xs) gives (index, item) pairs. zip(a, b) steps through two lists side by side, with no index needed.
- vectorized_words[words.index(word)] is a lookup across two lists that must stay in the same order. A dictionary is clearer and faster: word_to_vec = dict(zip(words, vectors)).
- Don't put a constant lookup inside a loop. Compute it once, before the loop.
- Tuples are immutable. np.shape() returns one. Tuples can be dict keys (lists can't). A list inside a tuple can still change.

## Questions

# Module 2 · Open questions (answer by Sun 29 Nov)

The graded quiz without options, plus questions that apply it to Gamarello. Answer from memory first, then check the slides. Bring your answers to Claude on Sunday.

1. **TF-IDF in words.** Explain what TF and IDF each measure and why you multiply them. What score does a word like "the" end up with, and why?

2. **What BM25 adds.** Name the two ways BM25 improves on TF-IDF. For each one, give the hyperparameter that controls it (`k1`, `b`) and say what happens at the extremes (for example `b = 0` vs `b = 1`). Then use the chocolate example from the quiz to explain why the cookbook chapters lost out under TF-IDF.

3. **Bag of words.** "Job killed by memory limit" and "memory limit killed by job" look identical to a bag-of-words model. Why? Give one Gamarello query where losing word order would actually matter.

4. **Keyword or semantic? (Gamarello)** For each query, say which kind of search would do better and why:
   - `sbatch --gres=gpu:a100`
   - "my job keeps dying when it runs out of memory" (the doc is titled "OOM killer")
   - "Wie reserviere ich eine GPU?" (and the docs are in English)

5. **How embeddings learn.** Explain contrastive learning with positive and negative pairs. Why does "happy" end up near "glad" when no one ever told the model they mean the same thing?

6. **Metadata filtering.** Name 4 metadata fields worth attaching to Gamarello docs. Give one query where a filter helps and one where it would wrongly exclude the right document.

7. **Hybrid search, in order.** Put these in the right order and justify it: semantic search, metadata filter, RRF, keyword search, top-K to the LLM.

8. **RRF by hand.** With k = 60, a document is ranked 1st by BM25 and 3rd by semantic search. Another is ranked 2nd by both. Which one wins after RRF? Why does RRF use *ranks* instead of the raw scores?

9. **Precision@K and recall@K.** Define both in one sentence each. For your Gamarello eval set, how would you calculate them? For a RAG system, which one matters more, and why isn't the answer simply "both"?

---

## My answers

1.

2.

3.

4.

5.

6.

7.

8.

9.



