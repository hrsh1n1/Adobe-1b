# 📄 Document Intelligence System – Adobe Round 1B

This system intelligently **extracts and ranks the most relevant sections** from a collection of PDF documents based on a given **persona** and their **job-to-be-done**.

Designed with **offline-first architecture**, it runs entirely inside Docker, ensuring reproducibility, portability, and compliance with strict **Adobe Round 1B constraints**.

---

## ✨ Features

* ✅ PDF text extraction with page number retention
* ✅ Rule-based section and subsection identification
* ✅ TF-IDF based semantic relevance ranking
* ✅ Persona + task-driven scoring heuristics
* ✅ Fully containerized Docker deployment
* ✅ Produces structured JSON output with metadata

---

## ⚙️ Requirements

* [Docker](https://www.docker.com/) installed and running on your system
* No internet connection required during execution

---

## 📂 Folder Structure

Each collection should follow this format:

```
Collection_X/
├── challenge1b_input.json
├── PDFs/
│   ├── file1.pdf
│   ├── file2.pdf
│   └── ...
```

---

## ⚖️ Input Format

Your `challenge1b_input.json` should look like this:

```json
{
    "documents": [
        {"filename": "document1.pdf", "title": "Document 1"},
        {"filename": "document2.pdf", "title": "Document 2"}
    ],
    "persona": { "role": "Travel Planner" },
    "job_to_be_done": { "task": "Plan a trip of 4 days for a group of 10 college friends." }
}
```

---

## 📅 Building the Docker Image

From the project root directory:

```bash
docker build --platform linux/amd64 -t document-intelligence .
```

---

## 🚀 Running the System

### ✨ Basic Run:

```bash
docker run --rm \
  -v "$(pwd)/Collection_X:/data/input" \
  -v "$(pwd)/Collection_X:/data/output" \
  --network none \
  document-intelligence
```

### ✉️ Custom Input/Output Files

```bash
docker run --rm \
  -v "/path/to/input:/data/input" \
  -v "/path/to/output:/data/output" \
  document-intelligence \
  --input /data/input/my_input.json \
  --output /data/output/my_output.json
```

---

## 📝 Output Format

Your generated `challenge1b_output.json` will follow this format:

```json
{
  "metadata": {
    "input_documents": ["document1.pdf"],
    "persona": "Travel Planner",
    "job_to_be_done": "Plan a trip...",
    "processing_timestamp": "2025-07-24T15:30:45.123456"
  },
  "extracted_sections": [
    {
      "document": "document1.pdf",
      "section_title": "Introduction",
      "importance_rank": 1,
      "page_number": 2
    }
  ],
  "subsection_analysis": [
    {
      "document": "document1.pdf",
      "refined_text": "Summary of best trip options...",
      "page_number": 2
    }
  ]
}
```

---

## ⏱️ Performance Constraints

| Constraint               | Compliance      |
| ------------------------ | --------------- |
| CPU only                 | ✅ Yes           |
| Model size ≤ 1GB         | ✅ Yes           |
| Runtime ≤ 60s (3-5 PDFs) | ✅ Optimized     |
| No internet              | ✅ Fully offline |

---

## 🚀 Ready to Connect the Dots

This system is designed to meet the exact expectations of Adobe Round 1B and is extensible for downstream use in Round 2. Simply mount your input/output directories, provide the persona and job, and the system will do the rest.

Let the documents speak — intelligently. 🤖
