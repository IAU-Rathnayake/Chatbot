# 🤖 AI Chatbot with GitHub Models (Python)

This project demonstrates how to build an interactive AI chatbot using **Python**, **Jupyter Notebooks**, and the **GitHub Models** marketplace (via Azure AI). 

It utilizes the `openai` Python SDK to communicate with models like `gpt-4o` (You can use any models), maintaining conversation history for a natural chat experience.

## 🚀 Features
* **Interactive Chat:** Continuous conversation loop (until you type "exit").
* **Context Awareness:** The bot remembers previous messages in the session using a history list.
* **Secure:** Uses environment variables (`.env`) to keep API keys safe.
* **Cross-Platform:** Runs in a Conda environment using Jupyter Notebooks.

## 🛠️ Prerequisites
Before running this project, ensure you have the following:
* **Anaconda or Miniconda** installed.
* **Visual Studio Code** (recommended) or classic Jupyter Notebook.
* A **GitHub Personal Access Token** with access to GitHub Models.

## 📦 Installation & Setup

### 1. Create the Conda Environment
It is best practice to use a virtual environment. Open your terminal and run:

```bash
# Create a new environment named 'ai-practice'
conda create -n ai-practice python=3.10

# Activate the environment
conda activate ai-practice
```

### 2. Install Required Libraries

Because the Azure/GitHub Models SDKs are distributed via PyPI, we install them using `pip` inside the Conda environment:

```bash
pip install openai python-dotenv ipykernel
```
### 3. Configure Security (.env)
API keys should never be hardcoded. Instead, store sensitive credentials in a .env file.

Steps
Create a file named .env in the project root.

Add your GitHub token:
```bash
GITHUB_TOKEN=ghp_YourLongTokenStringHere...
```
(Optional but recommended) Add .env to your .gitignore file to avoid committing secrets to version control.

## 🧠 How the Code Works
The main implementation lives in chatbot.ipynb. Below is an overview of the workflow and key components.

### Step 1: Load Environment Variables Securely
The python-dotenv package is used to load environment variables from the .env file, keeping credentials separate from source code.

```python
from dotenv import load_dotenv
import os

load_dotenv()  # Load variables from .env
token = os.environ.get("GITHUB_TOKEN")
```
### Step 2: Initialize the Client
The OpenAI client is initialized with an Azure AI inference endpoint. This configuration enables access to GitHub’s free model tier.

```python
Copy code
from openai import OpenAI

client = OpenAI(
    base_url="https://models.inference.ai.azure.com",
    api_key=token,
)
```
### Step 3: Maintain Conversation State
Since large language models are stateless, conversation history must be managed manually. This is done using a messages list.

```python
messages = [
    {"role": "system", "content": "You are a helpful assistant."}
]
```
Roles explained:

* System: Sets the assistant’s behavior and context.
* User: Represents user input.
* Assistant: Stores the model’s responses.

#### Step 4: Chat Loop Execution
* A continuous loop is used to simulate an interactive chat session:

Read user input.
* Append the input to the message history.
* Send the full conversation to the model.
* Display and store the model’s response.
* The loop continues until the user types exit.

### 🏃‍♂️ How to Run the Project
- Open VS Code or Jupyter Notebook.
- Open chatbot.ipynb.
- Select the ai-practice kernel (top-right in VS Code).
- Run the notebook cell.
- Enter your prompt in the input box and press Enter.
- Type exit to terminate the session.

Note: In VS Code, the input field may appear at the top center of the window or directly below the running cell.

### 🤝 Credits
- Models: GitHub Models / Azure AI
- SDK: OpenAI Python Library


