# 🧠 Personal Knowledge Graph

A personal AI-powered knowledge system that converts web content into a **connected, searchable knowledge base**.

This project helps you **ingest articles, automatically summarize them, and create links between related notes**, forming a dynamic knowledge graph that you can query like your own ChatGPT.

---

## 🚀 Features

* 📥 Ingest web articles into markdown files
* 🤖 Generate summaries, key insights, and tags using AI
* 🔗 Automatically link related notes
* 🧠 Build a connected knowledge graph
* 🔍 Query your notes using natural language (RAG-based search)

---

## 🏗️ Architecture

```
URL → Extract Content → AI Summary → Auto-Link → Store → Query
```

1. Input a URL
2. Extract and clean content
3. Generate summary + tags using LLM
4. Link related notes automatically
5. Store as markdown files
6. Query using embeddings + LLM

---

## 📂 Project Structure

```
knowledge-base/
│
├── data/
│   ├── raw/              # Raw scraped content
│   ├── processed/        # AI-generated markdown notes
│   └── embeddings/       # Vector database files
│
├── scripts/
│   ├── ingest.py         # URL → raw content
│   ├── summarize.py      # AI summarization
│   ├── link_notes.py     # auto-link notes
│   └── query.py          # query system (RAG)
│
├── vectorstore/
│   └── db.py             # embeddings + indexing
│
├── sample_data/          # sample notes (for demo)
├── requirements.txt
└── README.md
```

---

## ⚙️ Setup

### 1. Clone the repository

```
git clone https://github.com/your-username/your-repo-name.git
cd your-repo-name
```

### 2. Create a virtual environment

```
python -m venv venv
source venv/bin/activate   # Mac/Linux
venv\Scripts\activate      # Windows
```

### 3. Install dependencies

```
pip install -r requirements.txt
```

### 4. Add API key

Create a `.env` file:

```
OPENAI_API_KEY=your_api_key_here
```

---

## ▶️ Usage

### 1. Ingest a web article

```
python scripts/ingest.py
```

---

### 2. Generate summary

```
python scripts/summarize.py
```

---

### 3. Auto-link notes

```
python scripts/link_notes.py
```

---

### 4. Build embeddings (first time)

```
python vectorstore/db.py
```

---

### 5. Query your knowledge base

```
python scripts/query.py
```

Example:

```
Ask: What do I know about system design?
```

---

## 🔗 Obsidian Integration

* Open Obsidian
* Set vault path to `data/processed/`
* Use Graph View to visualize connections

---

## 💡 Use Cases

* Organize technical learning (DSA, system design, AI)
* Store research articles and notes
* Prepare for interviews
* Build a long-term personal knowledge base

---

## 🔥 Future Improvements

* Chat UI (Streamlit or web app)
* Better semantic linking using embeddings
* Support for PDFs and videos
* Local LLM integration
* Automated ingestion pipeline

