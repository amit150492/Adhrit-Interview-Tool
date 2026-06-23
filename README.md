# Adhrit Chatbot: AI Interview Simulator

Adhrit Chatbot is an interactive web application built with Streamlit and powered by OpenAI's GPT-4o. It simulates a realistic HR technical/behavioral interview tailored to a user's specific background, target position, and target company. At the end of a 5-turn conversation, it provides structured feedback and an overall performance score.

## 🚀 Features

Customized Interview Setup: Dynamically adjusts the interviewer persona based on user-provided profile details (Name, Experience, Skills, Seniority, Role, and Target Company).
Context-Aware Conversational AI: Uses OpenAI's streaming API (`gpt-4o`) to simulate an active, responsive HR executive.
Automatic Conversation Capping: Restricts the interview phase to exactly 5 user responses to keep the assessment concise.
AI-Powered Performance Feedback: Evaluates the entire conversation history to generate a structured numerical score and actionable feedback.
Seamless Application Reset: Integrates native JavaScript window reloads to cleanly wipe state variables and restart the session.

## 🛠️ Tech Stack

Frontend UI: [Streamlit](https://streamlit.io/)
LLM Integration: [OpenAI Python SDK](https://github.com/openai/openai-python) (`gpt-4o`)
Session Utilities: [Streamlit JS Eval](https://github.com/Ghasel/streamlit-js-eval) (for seamless window reloads)

### 2. Install Dependencies

Ensure you have Python 3.8+ installed, then run:

bash
pip install streamlit openai streamlit-js-eval


### 3. Setup Secrets / Environment Variables

Create a Streamlit secrets file at `.streamlit/secrets.toml` in your project root folder and insert your OpenAI API key:

toml
OPENAI_API_KEY = "your-actual-openai-api-key-here"



### 4. Run the Application

bash
streamlit run app.py



## 🕹️ Application Workflow

The application behaves as a finite state machine using `st.session_state` across three major phases:


[ Phase 1: Form Setup ] ──(Click Start)──> [ Phase 2: Live Chat (5 Turns) ] ──(Click Feedback)──> [ Phase 3: AI Scoring ]


### Phase 1: Registration & Profiling

Users enter their personal credentials, write summaries of their technical experience/skills, and select their desired target company and role seniority via drop-downs and radio selections.

### Phase 2: The Interview

Upon clicking "Start Interview", a background system prompt embeds the user's profile info into the AI context. The user communicates back and forth with the AI model.

* An internal counter tracks inputs (`st.session_state.user_message_count`).
* Once the user submits their 5th reply, the chat interface locks automatically.

### Phase 3: Assessment Evaluation

The user clicks "Get Feedback", triggering an independent API call to OpenAI. The complete message history is packaged up and passed to an evaluator persona that outputs:

1. An overall score (scale of 1-10)
2. Comprehensive text breakdown of areas of strength and improvement.



## 🔒 Configuration & Constraints

Character Limits: Input restrictions are enforced on the profile setup (Name: 40 chars max, Experience/Skills: 200 chars max) and chat windows (1000 chars per response) to prevent prompt overflow.
Turn Limit: The loop is set to freeze exactly at `user_message_count >= 5` to simulate a real-world rapid screening test.

