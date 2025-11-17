# kautilya-OA-SemanticSearch

Overview
This project implements a semantic search engine built on top of the Twitter API v2 Postman documentation.
The goal is to let a user run a natural language query from the command line and retrieve the most relevant API endpoints based on semantic meaning, not keyword matching.

What the System Does
The system loads the entire Twitter API Postman collection, extracts every endpoint, converts each into a textual representation, generates embeddings, stores them in a FAISS vector index, and performs semantic retrieval when queried.
The output is a clean JSON response containing the top matching API endpoints.

How It Works
The workflow is implemented in four main stages:

Documentation Parsing
The project loads the Postman collection from the repository at
https://github.com/xdevplatform/postman-twitter-api

The script walks through all nested folders and extracts endpoint level data:
Endpoint name
HTTP method
URL
Description
Folder hierarchy
Each endpoint is turned into a text chunk that can later be embedded.

Embedding Generation
All extracted chunks are converted into vector embeddings using the sentence transformer model
all-MiniLM-L6-v2
These embeddings capture the semantic meaning of each endpoint so the system can understand intent based queries.

Vector Indexing
The embeddings are stored inside a FAISS IndexFlatL2 index.
This allows fast nearest neighbor search for any query provided by the user.

Querying
When a user runs a command like
python semantic_search.py --query "How do I fetch tweets with expansions"
the script embeds the query, searches the FAISS index, ranks the endpoints, and prints the results as structured JSON.

Example Output
The output includes fields such as
rank
score
chunk id
endpoint name
method
URL
documentation path
text extracted from the Postman file

Project Structure
semantic_search.py
postman-twitter-api folder containing the Postman collection
README.md

Installation and Setup
Clone the Postman documentation repository
git clone https://github.com/xdevplatform/postman-twitter-api

Install dependencies
pip install sentence-transformers faiss-cpu

Run the script
python semantic_search.py --query "your query here"

Why This Project Matters
The Twitter API documentation is long, nested, and hard to navigate with simple keyword search.
This project converts the documentation into a structured, vector searchable knowledge base that responds to intent based questions.
It improves discoverability for developers, speeds up exploration of endpoints, and demonstrates practical machine learning engineering skills involving embeddings, vector search, and document parsing.

Summary
This task delivers a fully working semantic search system with
automatic documentation parsing
text chunking
embedding generation
FAISS indexing
semantic querying
JSON output
It is lightweight, accurate, and designed to run from a simple command line interface.
