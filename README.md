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

An end-to-end, production-ready conversational web application built with **Python**, **[Streamlit](https://chatbot-template.streamlit.app/)**, and the **OpenAI API**. 

Unlike standard cloud-hosted consumer chat interfaces, this project serves as a self-hosted, modular architecture that allows developers to maintain full control over API costs, model selection (such as GPT-3.5-Turbo and GPT-4), customized prompt engineering, and UI component behavior.

---

## 🌟 Advantages & Value Proposition

* **Full Data & UI Sovereignty**: Run and host the frontend on your own infrastructure or container environment without being locked into proprietary chat portals.
* **Deterministic Cost & Model Control**: Connect directly to your own OpenAI developer project to specify model engines, adjust context token windows, and optimize API consumption.
* **Extensible & Production-Ready**: Modular structure configured with containerized environments (`.devcontainer`) and GitHub CI/CD configurations (`.github`), making it simple to scale into internal enterprise bots, customer-support assistants, or custom retrieval-augmented generation (RAG) tools.
* **Rapid Prototyping Framework**: Built on Streamlit's stateful reactive engine, simplifying UI state persistence across chat turns using session state dictionaries.

---

## ⚠️ Disadvantages, Trade-offs & Limitations

While self-hosting offers immense control, it introduces specific engineering and operational trade-offs compared to using managed consumer chat apps:

* **Manual Maintenance & No Automatic Model Updates ("Frozen in Time")**: 
  * Whether you connect via API (e.g., OpenAI) or run a local open-source model (e.g., Llama, Mistral), **models do not receive automatic background updates** like consumer web apps. 
  * A downloaded open-source model file is entirely static; it will never learn new world events or fix its own bugs unless you manually pull newer model weights. Even with APIs, behavior can freeze based on version pinning.
* **Direct Financial Responsibility (API Costs)**: 
  * Unlike a flat monthly subscription (e.g., ChatGPT Plus), you pay strictly on a pay-as-you-go token basis. High traffic or heavy prompt debugging can lead to unexpected API expenses if usage limits or rate-limiting are not properly configured.
* **Operational Overhead & Deployment Complexity**: 
  * You are responsible for managing your own environment variables, server hosting, API key security, and uptime. If the local script crashes or the host server goes down, the application is offline until you manually restart it.
* **Hardware Constraints (If Running Locally)**: 
  * If you choose to host an open-source model locally instead of using an API, you must have high-performance local hardware (such as dedicated NVIDIA GPUs with sufficient VRAM) to achieve acceptable token generation speeds.

---

## ⚖️ Custom App vs. Online Chat Platforms

| Feature | Custom Streamlit App (Self-Hosted) | Online Chat Platforms (ChatGPT / Gemini) |
| :--- | :--- | :--- |
| **Hosting & Control** | You own the app interface, code, and where it runs. | Managed entirely in the cloud by the provider. |
| **Cost Structure** | Pay-as-you-go via API tokens. Only pay for what you use. | Flat monthly subscription fee regardless of usage volume. |
| **Customization** | Fully modifiable UI (`streamlit_app.py`), custom system prompts, and local data logging. | Fixed layout, standard UI controls, and platform-enforced rules. |
| **Updates** | **Static & Stable:** Model behavior and software remain frozen unless manually updated. | **Dynamic:** Features, UI layouts, and underlying models update automatically behind the scenes. |

> *Analogy:* Using a self-hosted app is like **owning your own house** (you control the layout, rules, and upkeep, though you rent the AI "brain" via API access), whereas using an online chatbot is like **renting a hotel room** (convenient, but you live by someone else's rules and architecture).

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
