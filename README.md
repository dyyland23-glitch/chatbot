# 💬 Chatbot template

A simple Streamlit app that shows how to build a chatbot using OpenAI's GPT-3.5.

[![Open in Streamlit](https://static.streamlit.io/badges/streamlit_badge_black_white.svg)](https://chatbot-template.streamlit.app/)

### How to run it on your own machine

1. Install the requirements

   ```
   $ pip install -r requirements.txt
   ```

2. Run the app

   ```
   $ streamlit run streamlit_app.py
   ```


   # 💬 Custom Streamlit & OpenAI Conversational Web App

An end-to-end, production-ready conversational web application built with **Python**, **Streamlit**, and the **OpenAI API**. 

Unlike standard cloud-hosted consumer chat interfaces, this project serves as a self-hosted, modular architecture that allows developers to maintain full control over API costs, model selection (such as GPT-3.5-Turbo and GPT-4), customized prompt engineering, and UI component behavior.

---

## 🌟 Value Proposition & Architectural Advantages

* **Full Data & UI Sovereignty**: Run and host the frontend on your own infrastructure or container environment without being locked into proprietary chat portals.
* **Deterministic Cost & Model Control**: Connect directly to your own OpenAI developer project to specify model engines, adjust context token windows, and optimize API consumption.
* **Extensible & Production-Ready**: Modular structure configured with containerized environments (`.devcontainer`) and GitHub CI/CD configurations (`.github`), making it simple to scale into internal enterprise bots, customer-support assistants, or custom retrieval-augmented generation (RAG) tools.
* **Rapid Prototyping Framework**: Built on Streamlit's stateful reactive engine, simplifying UI state persistence across chat turns using session state dictionaries.

---

## 📂 Repository Contents

* **[`streamlit_app.py`](https://github.com/dyyland23-glitch/chatbot/blob/main/streamlit_app.py)**: The core entry point containing the reactive user interface, chat message history management (`st.session_state`), and asynchronous streaming response handling via the OpenAI API client.
* **[`requirements.txt`](https://github.com/dyyland23-glitch/chatbot/blob/main/requirements.txt)**: Pins essential dependencies (`streamlit`, `openai`) ensuring deterministic environments across installations.
* **[`.devcontainer`](https://github.com/dyyland23-glitch/chatbot/tree/main/.devcontainer)**: Configuration files for Visual Studio Code Dev Containers, allowing instant development inside pre-configured Docker containers.
* **[`.github`](https://github.com/dyyland23-glitch/chatbot/tree/main/.github)**: Automated workflows and actions for continuous integration and deployment.

---

## 🛠️ Tech Stack & Key Libraries

* **Language**: Python 3.10+
* **Frontend Framework**: [Streamlit](https://chatbot-template.streamlit.app/) (`st.chat_message`, `st.chat_input`, `st.session_state`)
* **LLM Engine**: OpenAI API Python SDK (`openai.OpenAI()`, chat completions endpoint)
* **Environment & Containerization**: Docker, VS Code Dev Containers

---

## 🚀 Getting Started

### 1. Clone the Repository
```bash
git clone [https://github.com/dyyland23-glitch/chatbot.git](https://github.com/dyyland23-glitch/chatbot.git)
cd chatbot
