# 🍅 Tomadoc AI - Intelligent Greenhouse Assistant

**Tomadoc AI** is an advanced, unified dashboard designed to assist tomato growers with real-time crop management, automated leaf disease diagnosis, semantic search capability over agronomic research, and gamified grower tasks. 

The project runs as a multi-tier Python application with microservices executing in background threads inside a **Google Colab** environment, exposing a public UI through Gradio.


## 💡 Project Concept & Features

Tomadoc AI combines machine learning, natural language processing, and IoT data feeds to provide a comprehensive management tool for greenhouses:

1. **🔍 Smart Scan (Disease & Ripeness Diagnosis)**
   - **Leaf Disease Classification**: Analyzes leaf photographs to diagnose diseases (e.g., *Early Blight*, *Late Blight*, *Bacterial Spot*, or *Healthy*) and generates automated treatment protocols.
   - **Ripeness Checker**: Evaluates tomato fruit images to determine ripeness level and advises on harvesting windows.
2. **💬 Research Expert (Semantic RAG Chatbot)**
   - Utilizes a Retrieval-Augmented Generation (RAG) pipeline to search scientific papers and agricultural databases.
   - Combined with Google Gemini, it answers grower queries with cited research context.
3. **📊 IoT Dashboard**
   - Fetches live temperature, humidity, and soil moisture telemetry from a cloud IoT service.
   - Plots historical metrics and runs a local **Greenhouse Agent** microservice to give automated advice (e.g., adjust ventilation, irrigate).
4. **🏆 Garden Dashboard**
   - A gamification layer containing points, grower levels (e.g., *Apprentice Grower*), stats, and daily tasks that dynamically update as users complete scans and resolve IoT warnings.


## 🛠 Technology Stack

- **User Interface**: [Gradio](https://www.gradio.app/) (Minimalist dashboard with customized CSS styling, dynamic status badges, and interactive LinePlots).
- **Generative AI & RAG**:
  - **LLM API**: [Google GenAI SDK](https://github.com/google/generative-ai-python) utilizing the **Gemini 3.1 Flash-Lite** model (`gemini-3.1-flash-lite`).
  - **Vector Embeddings**: Hugging Face's `sentence-transformers` (`all-MiniLM-L6-v2`).
  - **Vector Database**: [ChromaDB](https://www.trychroma.com/) for local semantic indexing of chunked document text.
- **Computer Vision (Image Classification)**:
  - Hugging Face `transformers` pipelines running two custom models:
    - Disease Diagnosis: `oshriagronov/tomadoc-mythos`
    - Ripeness Classifier: `oshriagronov/tomadoc-flash`
- **Database / Inverted Index**:
  - **Firebase Realtime Database** for persistent storage of a global inverted index mapped from processed research documents.
- **Web Scraping & NLP Utilities**:
  - `requests` and `BeautifulSoup4` for scraping research papers.
  - `nltk` (PorterStemmer, tokenizers, and stop words lists) for text preprocessing.
- **Microservice Layer**:
  - Native Python `http.server` endpoints running in background threads:
    - **Greenhouse Agent Service**: Port `8001` (Telemetry analytics & recommendations).
    - **RAG Query Service**: Port `8002` (Semantic context retrieval).


