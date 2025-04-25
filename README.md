# Natural Language to SQL Bot (Text to SQL for SQLite)

## 📅 Overview

This project is a **Text-to-SQL Bot** where users can ask questions in simple English, and the system will:
- Generate the correct SQL query.
- Execute the SQL on a **SQLite database** (`employee.db`).
- Return both the **query** and the **output**.

The system is built using **Flask**, **LangChain**, **OpenAI GPT-3.5**, **FAISS**, and **SQLite**.

---

## 📈 Step-by-Step Project Flow

```text
Step 1:
I created a SQLite database with a basic Employee table having fields like name, age, city, gender, total experience, and blood group.

Step 2:
I prepared a CSV file (employee_questions.csv) where I wrote simple natural language questions, their matching SQL queries, and short descriptions.
This CSV acts as few-shot examples to guide the model.

Step 3:
I generated embeddings for these examples using OpenAI embeddings and stored them in FAISS, a fast vector database, for quick searching.

Step 4:
I used LangChain to create:
- A FAISS retriever (to search examples based on user input)
- A Conversational Retrieval Chain that connects the retriever with a language model (LLM).

Step 5:
I connected the system with OpenAI GPT-3.5-turbo as the model.
(But the setup is flexible — it can also work with Gemini, Llama, or any open-source model.)

Step 6:
I built a Flask API where:
- The user sends a question.
- The system finds similar examples from FAISS.
- It creates a final prompt (schema + examples + user query).
- The model generates the SQL query.
- SQL is cleaned and validated.
- The query is run on the employee.db database.
- The API sends back both the SQL query and the query output.

Step 7:
In future, I can enhance this system by:
- Adding support for multi-table joins and data modification queries (INSERT/UPDATE).
- Integrating conversation history, so the bot can understand previous context and give smarter, more connected answers.
- Replacing the model with open-source alternatives for cost-saving.
```

---

## 📞 System Flow

```text
User Question
    ↓
Flask API Endpoint (POST /)
    ↓
FAISS Retriever (Semantic Search on employee_questions.csv examples)
    ↓
Prompt Formation (Database Schema + Retrieved Examples + User Question)
    ↓
LLM (OpenAI GPT-3.5 / Gemini / Llama etc.)
    ↓
Generated SQL Query
    ↓
SQL Cleaning & Validation
    ↓
Execution on SQLite Database (employee.db)
    ↓
Return Query + Output as API Response
```

---

## 📊 Technology Stack

| Component | Technology |
|:----------|:-----------|
| API Server | Flask |
| Database | SQLite (employee.db) |
| Embeddings | OpenAI text-embedding-ada-002 |
| Vectorstore | FAISS |
| LLM | OpenAI GPT-3.5-turbo (flexible to switch) |
| Memory | LangChain ConversationBufferMemory |
| Retrieval Chain | LangChain ConversationalRetrievalChain |

---

## 🔧 Setup Instructions

### 1. Clone the repository
```bash
git clone <https://github.com/kartiktongaria/text2sql-chatbot.git>
cd your-repo-folder
```

### 2. Create and activate a virtual environment
```bash
python3 -m venv env
source env/bin/activate  # For Mac/Linux
# OR
env\Scripts\activate.bat  # For Windows
```

### 3. Install dependencies
```bash
pip install -r requirements.txt
```

### 4. Set up environment variables
Create a `.env` file:
```bash
echo "OPENAI_API_KEY=your_openai_api_key_here" > .env
```

### 5. Start the server
```bash
python chat.py
```
Server will run on:
```bash
http://127.0.0.1:8000/
```

---

## 📡 API Usage

- **Endpoint:** `POST /`
- **Request Body Example:**
```json
{
  "question": "How many employees have more than 5 years of experience?"
}
```

- **Response Example:**
```json
{
  "response": {
    "query": "SELECT COUNT(*) FROM Employee WHERE total_experience > 5;",
    "result": [{"COUNT(*)": 20}]
  }
}
```

You can test using **Postman** or **cURL**.

---

## 🛠️ Future Enhancements
- Add multi-table joins.
- Support Insert, Update, and Delete queries.
- Add conversation history to understand context better.
- Integrate open-source LLMs (to reduce cost and improve control).
- Build a simple frontend UI (Streamlit or React).

---

## 💚 Final Notes

This project shows how natural language questions can be turned into real SQL queries and executed live on a database.  
It's a working example of how **RAG (Retrieval Augmented Generation)** can make databases talk in human language!

✅ To check chatbot outputs, refer to the **`result_img` folder** available in the repository, where screenshots of working results are attached.

---

# 🌟 Thank you for exploring the Natural Language to SQL Bot!

