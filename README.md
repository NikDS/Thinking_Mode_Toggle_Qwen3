# 🧠 Dynamic LLM Thinking Mode Demo with LangChain & Ollama (Qwen)

[![Python](https://img.shields.io/badge/Python-3.x-blue)](https://www.python.org/)
[![Ollama](https://img.shields.io/badge/Ollama-Model-green)](https://ollama.com)

**Switching between concise answers and detailed analysis, on demand!**

This Jupyter Notebook demonstrates a simple yet effective way to dynamically control the thinking mode of an LLM (specifically Qwen via Ollama) based on the user's input. Ever wanted your AI to give you just the facts sometimes, and a deep dive others? This notebook shows one approach using simple text classification and Ollama's built-in mode tags (`/think`, `/no_think`).

## ✨ Features

* **Dynamic Mode Switching:** Automatically determines if the AI should respond directly or perform a detailed analysis.
* **Simple Text Analysis:** Uses basic length and keyword checks to classify input.
* **Ollama Integration:** Leverages Ollama's capabilities, specifically the `/think` and `/no_think` tags supported by models like Qwen.
* **LangChain Powered:** Builds the interaction chain using LangChain for clarity.
* **Interactive Demo:** Run cells in the notebook to test with example inputs or your own custom text and see the results directly.

## 💡 Why is this useful?

LLMs are versatile, but their default output style might not always match the user's intent. For simple questions, a direct answer is best. For complex queries, a step-by-step thought process or detailed explanation is needed. This notebook provides a foundational example of how you can build systems that adapt the AI's response style based on the input's apparent complexity or the user's likely intent (inferred through keywords and length).

## 🔧 How it Works

The demonstration within the notebook covers the following logic:

1.  **Input:** Takes user text input (either predefined examples or custom text).
2.  **Classification:** A simple Python function (`determine_thinking_mode_text` shown in the notebook) checks the input's length and scans for specific keywords (like "analyze", "explain the process", "compare", etc.).
3.  **Mode Determination:**
    * If the input is short AND contains no complex keywords, it's classified as `direct`.
    * If the input is long OR contains any complex keywords, it's classified as `analytical`.
4.  **Mode Tagging:** Based on the determined mode, the script appends a specific tag to the original user input:
    * `direct` mode -> `/no_think` tag is added.
    * `analytical` mode -> `/think` tag is added.
    * *(Note: These tags are specific to how models like Qwen are exposed via Ollama and instruct the model's internal processing).*
5.  **LLM Interaction:** The tagged input (`{user_input} /think` or `{user_input} /no_think`) is sent to the Qwen model via LangChain and Ollama.
6.  **Output:** Qwen processes the request, ideally adjusting its internal thought process (making it visible with `<think>` blocks if using `/think`) before generating the final response, resulting in either a concise answer or a more detailed one.

You can easily modify the `determine_thinking_mode_text` function within the notebook cells to change the keyword list or the length threshold.

## 🚀 Getting Started

### Prerequisites

Before you run this notebook, you need:

1.  **Python 3.7+:** Make sure Python is installed on your system.
2.  **Ollama:** Download and install Ollama from [ollama.com](https://ollama.com/).
3.  **Qwen Model in Ollama:** Pull a Qwen model. This code is tested with `qwen3:8b`, but others from the Qwen family that support `/think` tags should work.
    ```bash
    ollama pull qwen3:8b
    ```
4.  **Jupyter Environment:** Access to a Jupyter environment (like JupyterLab, Jupyter Notebook, VS Code with the Python extension, etc.) to run the `.ipynb` file.
5.  **Required Python Libraries:** You'll need `langchain` and `langchain-ollama`. You can install these directly in a notebook cell or in your environment:
    ```bash
    pip install langchain langchain-ollama
    ```

### Running the Notebook

1.  Make sure your Ollama server is running in the background.
2.  Download or clone the `Toggle_thinkingmode_q3.ipynb` file to your local machine.
3.  Open the `.ipynb` file using your preferred Jupyter environment.
4.  Read through the cells and run them sequentially to see the dynamic mode switching in action with the examples provided, or modify a cell to input your own text.

## 🧪 Examples

The notebook includes several examples to illustrate the mode switching logic. You'll see inputs like:

* `"What is the largest ocean?"` -> Classified as **DIRECT**.
* `"Explain the process of photosynthesis step-by-step, detailing the light-dependent and light-independent reactions."` -> Classified as **ANALYTICAL**.
* `"Analyze this short sentence."` -> Classified as **ANALYTICAL**.

Run the notebook cells to see how Qwen responds to these examples based on the dynamically applied `/think` or `/no_think` tags.

---
