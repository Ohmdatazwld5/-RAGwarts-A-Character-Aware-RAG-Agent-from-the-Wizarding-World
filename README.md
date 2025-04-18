# -RAGwarts-A-Character-Aware-RAG-Agent-from-the-Wizarding-World
# RAGwarts is a Retrieval-Augmented Generation (RAG) agent that answers questions in the voice of characters from Harry Potter and the Sorcerer’s Stone. Given a user’s question and a chosen character (e.g., Hermione Granger, Harry Potter), the agent retrieves relevant content from the book and generates a response that reflects the personality, behavior, and voice of the specified character.

# AI Engineer Assignment: Harry Potter RAG Agent

## Overview

**Position:** Founding AI Engineer

**Assignment:** Build a Retrieval-Augmented Generation (RAG) agent that answers questions in the voice of a specified character from *Harry Potter and the Sorcerer’s Stone*, using the provided PDF:  
[Harry Potter and the Sorcerer’s Stone](https://hazidesaratcollege.ac.in/library/uploads/85jkr_harrypotter_1.pdf)

---

## Solution Summary

This repository contains an end-to-end RAG pipeline. The system:
- Processes and indexes the Harry Potter PDF.
- Retrieves context passages for a given question and character.
- Generates an answer in the specified character’s authentic voice, grounded in the book.
- Explains how the answer was derived, referencing both retrieved context and character traits.

---

## Architecture

### 1. PDF Processing

- Loads and parses the provided PDF.
- Splits text into overlapping chunks for effective retrieval.
- Removes formatting artifacts if needed.

### 2. Vector Store Indexing

- Generates embeddings for each chunk using a Sentence-BERT model (`all-MPNet-base-v2`).
- Stores embeddings in a FAISS vector index for efficient similarity search.

### 3. Retrieval-Augmented Generation

- On receiving a question and character, retrieves the most relevant book passages using vector search.
- Uses a language model (e.g., LLaMA 3, Hugging Face Transformers) to generate a character-specific response, guided by:
    - The retrieved context.
    - Manually defined character traits and behavioral notes.

- Ensures the response is grounded in the book and matches the character’s voice.

### 4. Evaluation

- Automatically evaluates each output for:
    - **Relevance:** Does the response answer the question?
    - **Character Authenticity:** Is the answer in-character?
    - **Context Accuracy:** Is the answer supported by the retrieved context?

---

## Setup & Usage

### Requirements

- Python 3.8+
- [PyPDF2](https://pypi.org/project/PyPDF2/) or [pdfplumber](https://pypi.org/project/pdfplumber/)
- [langchain](https://github.com/langchain-ai/langchain)
- [faiss-cpu](https://github.com/facebookresearch/faiss)
- [transformers](https://github.com/huggingface/transformers)
- [sentence-transformers](https://www.sbert.net/)
- GPU recommended for model inference

### Installation

```bash
git clone <YOUR_REPO_URL>
cd <YOUR_REPO_DIR>
pip install -r requirements.txt
```

### Running

1. Place `Harrypotter.pdf` in the project directory.
2. Run the RAG pipeline script:
    ```bash
    python rag_pipeline.py
    ```
3. For agentic version (with more dynamic prompt handling):
    ```bash
    python agentic_rag.py
    ```
4. (Optional) Modify the scripts for CLI or notebook interaction.

---

## Example Inputs & Outputs

### Example 1

- **Question:** What would you do if you found a mysterious artifact in Hogwarts?
- **Character:** Hermione Granger

**Generated Response:**  
_I’d take it to the library to research it. Unknown magical objects are dangerous! I’d check Hogwarts: A History or tell Professor McGonagall._

**Explanation:**  
This response uses Hermione’s cautious and studious traits, referencing her research habits from relevant book passages.

---

### Example 2

- **Question:** How would you react to seeing a ghost for the first time?
- **Character:** Ron Weasley

**Generated Response:**  
_Blimey! I’d probably jump out of my skin. I mean, Nearly Headless Nick is friendly, but ghosts still give me the creeps!_

**Explanation:**  
Reflects Ron’s nervous humor and references context about ghosts from the book.

---

### Example 3

- **Question:** What would you say to someone bullying a friend?
- **Character:** Harry Potter

**Generated Response:**  
_I wouldn’t stand by and let it happen. I’d step in and defend my friend, just like when Malfoy tried to pick on Neville._

**Explanation:**  
Shows Harry’s bravery and loyalty, using examples from the book.

---

## Code Structure

- `rag_pipeline.py` – Basic RAG pipeline: PDF ingestion, retrieval, character-based generation, evaluation.
- `agentic_rag.py` – Agentic RAG pipeline: Modular, stepwise agent for reasoning and response.
- `README.md` – This documentation.
- `requirements.txt` – All dependencies.

---

## Testing & Evaluation

- Run the scripts with the provided or your own questions and characters.
- The system will print the response, the supporting context, and evaluation metrics (relevance, authenticity, context accuracy).

---

## Notes

- All character traits are manually defined—no AI or agent meta-language is present in the prompts or code.
- Responses are always grounded in the book and written in the authentic voice of the chosen character.
- The code is modular for easy extension (e.g., adding more characters or a CLI interface).

---

## Contact

For questions or feedback, open an issue or contact the maintainer.
