# AutoML_AGent

Autonomous AutoML Agent 🤖
An intelligent, conversational AI agent that automates the end-to-end machine learning workflow using natural language. Upload a dataset, and simply talk to the agent to perform data analysis, preprocessing, model training, and visualization.

🌟 Key Features
Natural Language Interface: Control the entire ML pipeline—from data loading to model saving—using simple, conversational commands.

Intelligent Task Routing: A smart LLM-based router understands the user's intent and calls the appropriate specialized tool for the job.

Comprehensive AutoML: Leverages the power of PyCaret to automate complex tasks like data preprocessing, model comparison, and hyperparameter tuning.

Interactive EDA: Perform exploratory data analysis on the fly. Ask for descriptive statistics, missing value reports, or correlation analysis.

Dynamic Visualizations: Generate and view model evaluation plots (like feature importance or confusion matrices) and EDA plots directly within the chat.

Proactive Recommendations: The agent acts as an expert assistant, suggesting logical next steps and example queries to guide the user through the workflow.

Interactive UI: A user-friendly, multi-session chatbot interface built with Streamlit, featuring a landing page, persistent chat history, and a plot gallery.

🏗️ Architecture Overview
This project is built on a modular and scalable architecture designed for reliability and ease of use. The core of the system is a Simple Router Agent pattern.

Streamlit Frontend: A multi-session web UI that serves as the main entry point for the user. It handles file uploads and manages the chat history.

FastAPI Backend: A robust server that exposes a simple /chat API. It manages the state for each user session in memory.

Simple Router Agent: When the backend receives a query, it's passed to a powerful LLM chain (the router). The router's only job is to analyze the user's intent and return a JSON command specifying which tool to call.

Specialized Tools: The backend has a "toolbox" of stateful functions that wrap PyCaret's functionality. Based on the router's command, the backend executes the correct tool, passing it the current state of the ML pipeline.

State Management (MLState): A Pydantic model acts as the central "memory" for each session, holding the dataset, setup pipeline, trained models, and results.

Recommendation Engine: After a tool runs, an AI-powered engine analyzes the current state and the last result to generate intelligent suggestions for the user's next step.

🛠️ Tech Stack
Backend: FastAPI

Frontend: Streamlit

ML Backend: PyCaret

LLM Integration: LangChain, Langchain-Groq

Core Libraries: Pandas, Scikit-learn

📁 Project Structure
AutoML/
├── agent/
│   ├── router.py
│   └── recommendation_engine.py
├── llm/
│   └── task_identifier_nodes.py
├── state/
│   └── graph_state.py
├── tools/
│   ├── setup_tool.py
│   ├── compare_models_tool.py
│   ├── data_analysis_tools.py
│   └── ... (all other tool files)
├── plots/          # Generated plots are saved here
├── models/         # Saved models are stored here
├── reports/        # Generated reports are saved here
├── app.py          # The Streamlit frontend
├── main.py         # The FastAPI backend
└── requirements.txt

🚀 Getting Started
Prerequisites
Python 3.10+

An API key from Groq

Setup and Installation
Clone the repository:

git clone https://github.com/your-username/automl-agent.git
cd automl-agent

Create a virtual environment:

python -m venv .venv
source .venv/bin/activate  # On Windows, use `.venv\Scripts\activate`

Install the dependencies:

pip install -r requirements.txt

Set up your environment variables:

Create a file named .env in the root directory.

Add your Groq API key to this file:

GROQ_API_KEY="your_groq_api_key_here"

How to Run the Application
You need to run the backend and frontend in two separate terminals.

Run the FastAPI Backend:

uvicorn main:app --reload

The API will be available at http://127.0.0.1:8000.

Run the Streamlit Frontend:

streamlit run app.py

Streamlit will open a new tab in your browser at http://localhost:8501.

📖 Example Usage
Open the Streamlit app in your browser.

Click "Start a New Chat Session".

Upload a CSV dataset. The agent will show a preview and suggest a machine learning query.

Click the suggested query or type your own to define the ML task (e.g., "predict the price").

Confirm the task and target column suggested by the agent.

Use the recommendation buttons or type your own commands to proceed with the workflow (e.g., "run setup", "compare models", "plot feature importance").

🔮 Future Improvements
Hierarchical Agent Architecture: Evolve the Simple Router into a true Master Agent that delegates tasks to specialized sub-agents (Data Analysis, ML Execution, Visualization) running in a LangGraph graph.

Model Explainability (XAI): Add a tool to wrap PyCaret's interpret_model function to generate SHAP plots and explain model predictions.

Persistent State: Replace the in-memory session storage with a more robust solution like Redis to allow sessions to persist even if the server restarts.