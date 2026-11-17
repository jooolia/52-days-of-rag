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


