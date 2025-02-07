# Retrieval-Augmented Generation (RAG) Question-Answering System

This project implements a **Retrieval-Augmented Generation (RAG)** pipeline as a FastAPI-based web application. The system retrieves relevant information from a dataset, reranks it using semantic similarity, and generates concise answers to user queries using a generative AI model. It combines **BM25** for keyword-based retrieval, **SBERT** for semantic reranking, and **Google Gemini** for answer generation.

---

## Table of Contents
1. [Overview](#overview)
2. [Features](#features)
3. [Pipeline Workflow](#pipeline-workflow)
4. [Installation and Setup](#installation-and-setup)
5. [Usage](#usage)
6. [Directory Structure](#directory-structure)
7. [Technologies Used](#technologies-used)
8. [Deployment](#deployment)
9. [Potential Improvements](#potential-improvements)
10. [Contributing](#contributing)
11. [License](#license)

---

## Overview
The goal of this project is to build a question-answering system that:
1. Retrieves relevant text chunks from a dataset based on a user query.
2. Reranks these chunks using semantic similarity.
3. Generates a concise and informative answer using a large language model.

The system is exposed as a web application using **FastAPI**, allowing users to interact with it via an HTML interface.

---

## Features
- **BM25 Retrieval**: Efficiently retrieves the top `n` most relevant chunks based on keyword matching.
- **SBERT Reranking**: Uses Sentence-BERT to rerank retrieved chunks based on semantic similarity.
- **Gemini Answer Generation**: Leverages Google's generative AI to synthesize answers from the reranked chunks.
- **Web Interface**: Provides a simple and intuitive HTML form for users to submit queries.
- **Containerization**: Includes a `Dockerfile` for easy deployment.

---

## Pipeline Workflow
The system processes user queries in three main steps:

### 1. Retrieve Top Chunks Using BM25
- Tokenizes the query and calculates relevance scores for each chunk in the dataset using BM25.
- Selects the top `n` chunks (default: 10) with the highest scores.

### 2. Rerank Chunks Using SBERT
- Encodes the query and the retrieved chunks into vector representations using SBERT.
- Calculates cosine similarity between the query and each chunk.
- Reranks the chunks based on their similarity scores, selecting the top 3 most relevant chunks.

### 3. Generate Answer Using Gemini
- Concatenates the text from the top 3 reranked chunks.
- Constructs a prompt combining the query and the concatenated text.
- Sends the prompt to the Gemini API to generate a concise and informative answer.

---

## Installation and Setup

### Prerequisites
- Python 3.8 or higher
- Docker (optional, for containerized deployment)

### Steps
1. Clone the repository:
   ```bash
   git clone https://github.com/your-repo/rag-pipeline.git
   cd rag-pipeline
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Download the dataset:
   - Place your dataset in `data_chunks.csv`. Ensure it contains a column named `text` with the text chunks.

4. Set up environment variables:
   - Add your Google Generative AI API key to an environment variable:
     ```bash
     export GOOGLE_API_KEY=your_api_key_here
     ```

5. Run the application:
   ```bash
   uvicorn app.main:app --host 0.0.0.0 --port 8000
   ```

6. Access the application:
   Open your browser and navigate to `http://localhost:8000`.

---

## Usage
1. Visit the homepage (`/`) and enter your query in the input form.
2. Submit the query.
3. The system will process the query through the RAG pipeline and display the generated answer on the same page.

---

## Directory Structure
```
app/
├── main.py               # Main FastAPI application
├── models.py             # Loads BM25, SBERT, and data chunks
├── retrieve.py           # Implements BM25-based retrieval
├── rerank.py             # Implements SBERT-based reranking
├── generate.py           # Uses Gemini to generate answers
├── templates/            # Contains HTML templates (e.g., index.html)
├── static/               # Contains static files like CSS (styles.css)
└── data_chunks.csv       # Dataset containing text chunks
Dockerfile                # Defines the containerization for deployment
requirements.txt          # Lists Python dependencies
README.md                 # This file
```

---

## Technologies Used
- **FastAPI**: For building the web API and serving the HTML interface.
- **BM25**: For efficient keyword-based retrieval.
- **SBERT (Sentence-BERT)**: For semantic similarity-based reranking.
- **Google Gemini**: For generating answers using a large language model.
- **Docker**: For containerization and deployment.
- **Jinja2**: For rendering dynamic HTML templates.

---

## Deployment
To deploy the application using Docker:
1. Build the Docker image:
   ```bash
   docker build -t rag-pipeline .
   ```

2. Run the container:
   ```bash
   docker run -p 8000:8000 rag-pipeline
   ```

3. Access the application at `http://localhost:8000`.

---

## Potential Improvements
- **Caching**: Cache frequently asked queries to reduce computation time.
- **Advanced Reranking**: Experiment with Cross-Encoders for better reranking performance.
- **Error Handling**: Add robust error handling for cases where no relevant chunks are found or the API fails.
- **UI Enhancements**: Improve the HTML/CSS for a more polished user experience.
- **Scalability**: Optimize the system for larger datasets and higher traffic.

---

## Contributing
Contributions are welcome! To contribute:
1. Fork the repository.
2. Create a new branch for your feature or bug fix.
3. Submit a pull request with a detailed description of your changes.

---

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

## Acknowledgments
- **BM25**: Inspired by traditional information retrieval techniques.
- **SBERT**: Developed by the Sentence-Transformers team.
- **Google Gemini**: Powered by Google's generative AI capabilities.
- **FastAPI**: A modern, fast (high-performance) web framework for building APIs.

---
