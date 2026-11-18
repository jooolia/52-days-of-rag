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



