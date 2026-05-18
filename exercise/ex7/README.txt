# Simple Wikipedia Search Engine

## Project Description

This project implements a simple search engine in Python.

The system receives a search topic, fetches several relevant pages from Wikipedia, builds a word index for the returned documents, and allows the user to search inside those documents.

The project includes:
- A simple ranking mechanism for returned documents
- Support for logical search operators: `AND` and `OR`

---

## Project Goal

The goal of this project is to demonstrate the basic structure of a search engine.

The system performs the following steps:

1. Fetches documents from Wikipedia.
2. Extracts and processes the text.
3. Builds a word-frequency index.
4. Searches the indexed documents according to a user query.
5. Ranks the returned documents.
6. Supports logical operators in search queries.

---

## System Structure


### 1. Fetch Component

This component is responsible for fetching pages from Wikipedia according to a topic selected by the user.

For example, if the user searches for the topic `bird`, the system retrieves several relevant Wikipedia pages and stores their title, URL, and text content.

### 2. Indexing Component

This component is responsible for building a word-frequency index for the fetched pages.

During this stage, the system:
- Splits the text into words
- Converts words to lowercase
- Removes common stop words
- Counts how many times each word appears in each document

### 3. Search Component

This component receives a user query and searches for matching documents using the created index.

Example queries:

```python
engine.search("bird OR wings")
engine.search("bird AND wings")