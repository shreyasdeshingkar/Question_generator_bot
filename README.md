# Question Paper Generator Documentation

## Overview

1. app_embeddings.py: This script focuses on generating vector embeddings from PDF documents (e.g., course materials and syllabi). It processes documents to create searchable vector databases using LangChain and Google Generative AI, storing the outputs in FAISS databases for further retrieval and analysis.

2. qp_gen.py: This script utilizes the vector databases created by app_embeddings.py to automate question paper generation. It employs AI to structure question papers with predefined templates, ensuring adherence to syllabus and formatting requirements.

## Key Functionalities

### app_embeddings.py

- Input and Processing:

Reads PDF files using PyPDFLoader, splitting content into chunks of 512 characters with overlaps for context retention.
Converts text chunks into vector embeddings via Google Generative AI.

- Storage:

Creates and saves FAISS vector databases:
Course material embeddings (vectorstore_data/db_faiss)
Syllabus embeddings (vectorstore_Syllabus/db_faiss).

- Features:

Batch processing with error handling and progress tracking.
Supports memory-efficient and incremental updates to embeddings.

### qp_gen.py

- Input:

Utilizes the embeddings created by app_embeddings.py for course material and syllabus.

- Question Paper Template:

Includes clear instructions for unit-wise distribution, marking schemes, and formatting.
Ensures questions align with the syllabus and maintain quality standards.

- Processing:

Uses Google’s Gemini model with balanced creativity settings (temperature set to 0.6) to generate questions.
Retrieves relevant syllabus content using similarity search in FAISS databases.

- Output:

Saves the formatted question paper, containing university details, course information, and a logical question structure, to a text file (question_paper.txt).

## Dependencies

- Both scripts share common dependencies:

1. LangChain for processing and embeddings.
2. Google Generative AI for text embeddings and question         generation.
3. FAISS for efficient vector storage and retrieval.
4. python-dotenv for managing environment configurations.

## Process Flow

#### Document Processing (app_embeddings.py):
PDFs are split into chunks, embedded, and stored in FAISS databases.

#### Question Generation (qp_gen.py):

1. Relevant vectors are retrieved from the databases.
2. AI generates a structured question paper based on the syllabus.

## Error Handling and Performance

- Both scripts are equipped with robust error handling:

1. app_embeddings.py recovers from processing errors and validates chunk formats.
2. qp_gen.py ensures vector databases are properly initialized and generates detailed error messages for API failures.

Batch processing and memory-efficient methods enhance performance for large datasets.

## Usage Notes

1. Proper setup of Google API credentials is required for embedding and question generation.
2. FAISS vector databases must be initialized with accurate and comprehensive course data.
3. An internet connection is essential for all API operations.



By working together, app_embeddings.py and qp_gen.py form a cohesive system for generating tailored, syllabus-driven question papers with high precision and efficiency.