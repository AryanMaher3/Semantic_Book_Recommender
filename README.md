# Semantic Book Recommender

A content-based book recommendation system that leverages Large Language Models (LLMs) and vector search to suggest books based on plot, genre, and emotional tone. Unlike traditional keyword search, this system understands the *meaning* of your query (e.g., "a story about redemption in a dystopian future").

## 🚀 Features

* **Semantic Search**: Find books using natural language queries. The system understands context and nuance rather than just matching words.
* **Emotion-Based Filtering**: Sort recommendations by the "vibe" of the book. Looking for a tear-jerker or a nail-biter? Filter by tones like *Happy*, *Suspenseful*, *Sad*, *Angry*, or *Surprising*.
* **Smart Categorization**: Filters books by simplified genres (Fiction, Non-Fiction, etc.) derived from zero-shot classification.
* **Interactive Dashboard**: A user-friendly web interface built with Gradio.

## 🛠️ Components & Pipeline

This project consists of five main components, representing the data science lifecycle:

1.  **Data Exploration & Cleaning** (`data-exploration.ipynb`)
    * Initial cleaning of the 7k books dataset.
    * Handling missing values and preparing text fields for processing.

2.  **Text Classification** (`text-classification.ipynb`)
    * Uses LLMs (Zero-Shot Classification) to reorganize specific book tags into broader, user-friendly categories (e.g., mapping "Juvenile Fiction" to "Fiction").

3.  **Sentiment Analysis** (`sentiment-analysis.ipynb`)
    * Analyzes book descriptions using the `j-hartmann/emotion-english-distilroberta-base` model.
    * Assigns probability scores for emotions: **Anger, Fear, Joy, Sadness, Surprise**.
    * These scores allow users to sort search results by emotional intensity.

4.  **Vector Search Engine** (`vector-search.ipynb`)
    * Converts book descriptions into dense vector embeddings using `sentence-transformers/all-MiniLM-L6-v2`.
    * Builds a **FAISS** (Facebook AI Similarity Search) index to allow for efficient similarity matching between user queries and books.

5.  **Web Application** (`gradio-dashboard.py`)
    * The front-end application that ties everything together.
    * Loads the pre-processed data (`books_with_emotions.csv`) and builds the vector index on startup.
    * Provides filters for Category and Tone and displays book covers and descriptions.

## 📦 Installation

This project requires **Python 3.11+**.

1.  **Clone the repository**
    ```bash
    git clone [https://github.com/aryanmaher3/semantic_book_recommender.git](https://github.com/aryanmaher3/semantic_book_recommender.git)
    cd semantic_book_recommender
    ```

2.  **Install Dependencies**
    A `requirements.txt` file is provided.
    ```bash
    pip install -r requirements.txt
    ```

3.  **Environment Setup**
    Create a `.env` file in the root directory. While the current dashboard uses local Hugging Face models, having your API keys set up is recommended for running the preprocessing notebooks.
    ```bash
    # .env file
    HUGGINGFACEHUB_API_TOKEN=your_token_here
    OPENAI_API_KEY=your_key_here  # Optional: depending on notebook experiments
    ```

## 🏃‍♂️ Usage

To launch the recommendation dashboard:

```bash
python gradio-dashboard.py
