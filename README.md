# 🤖 BritBot — Conversational Analytical Chatbot

![Company](https://img.shields.io/badge/Company-Britannia%20Industries%20Limited-blue)
![Department](https://img.shields.io/badge/Department-Consumer%20Market%20Insights%20%7C%20Analytics-purple)
![LLM](https://img.shields.io/badge/LLM-Gemini%20Pro-orange)
![Framework](https://img.shields.io/badge/Framework-Streamlit-red)
![Database](https://img.shields.io/badge/Database-SQLite3-green)
![Deployment](https://img.shields.io/badge/Deployment-AWS%20EC2-yellow)

> ⚠️ **Confidentiality Notice:** This repository contains a high-level overview of work done at Britannia Industries Limited. No proprietary data, source code, or confidential business information is shared.

---

## 🏢 Organization

**Britannia Industries Limited** — Department of Consumer Market Insights (CMI), Analytics Team, Bangalore.

**Mentor:** Dipesh Lakhotia, Head of Analytics, CMI

**Team:** Naman Navneet & Nikita Chelani — AI Analyst Interns

---

## 🎯 Project Overview

**BritBot** is an interactive **Conversational-Analytical Chatbot** that enables business users at Britannia to perform complex data analysis using plain English — no SQL knowledge required. Users can upload CSV files, ask natural language questions, and receive:

- Automatically generated and executed **SQL queries**
- **Tabular results** and **natural language summaries**
- **Interactive visualizations** (bar charts, line graphs, etc.)

The goal was to democratize data access within Britannia's analytics function — making it possible for non-technical stakeholders to extract insights directly from datasets through conversation.

---

## ✨ Key Features

| Feature | Description |
|---|---|
| 💬 **Natural Language to SQL** | Users ask questions in plain English; Gemini Pro generates accurate SQL queries |
| 📁 **CSV Upload & Auto DB Creation** | Upload any CSV → auto-converts to SQLite database with schema inference |
| 🔍 **SQL Execution Engine** | Generated SQL executed against SQLite3; results returned as structured dataframes |
| 📊 **Auto Visualization** | Summary graphs (bar, line) and calculations (averages, sums) generated via Matplotlib/Pyplot |
| 🧠 **Conversational Memory** | Chat History Buffer maintains context across multi-turn conversations |
| 🎯 **Few-Shot Prompting** | Prompt engineering with examples to guide accurate SQL generation |
| 🌐 **Web App Deployment** | Deployed on **AWS EC2**, hosted publicly via Streamlit port forwarding |

---

## 🏗️ System Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                     BRITBOT SYSTEM                          │
│                                                             │
│  User Question                                              │
│       │                                                     │
│       ▼                                                     │
│  Chat History Buffer (Conversation Context)                 │
│       │                                                     │
│       ▼                                                     │
│  NLP Generator ──► Gemini Pro LLM API                      │
│       │                    │                               │
│       │              [Prompt 1: Intent]                    │
│       ▼                                                     │
│  Response SQL Generator                                     │
│       │                                                     │
│       │         [Prompt 2: SQL Generation + Few-Shot]      │
│       ▼                                                     │
│  SQL Executor ──► SQLite3 Database ◄── CSV Upload          │
│       │                                                     │
│       ▼                                                     │
│  Required Dataframe                                         │
│       │                                                     │
│       ▼                                                     │
│  Final Response (NL Summary + Table)                       │
│       │                                                     │
│       ▼                                                     │
│  Data Visualization Model [Prompt 3]                       │
│       │                                                     │
│       ▼                                                     │
│  Matplotlib/Pyplot Chart ──► Streamlit UI                  │
└─────────────────────────────────────────────────────────────┘
```

---

## 🔍 Detailed Step-by-Step Workflow

### Step 1 — User Interaction
User types a natural language question via the Streamlit UI (e.g., *"Show me total sales by region for Q3"*)

### Step 2 — Chat History Buffer
Previous conversation turns are loaded into context, ensuring multi-turn coherence and continuity

### Step 3 — NLP Generator
Analyses user question + chat history to extract intent and context — frames the query for the LLM

### Step 4 — Gemini Pro LLM (API Call)
**Prompt 1** is constructed with:
- User question
- Table schema (column names, types)
- Few-shot examples of NL → SQL pairs
- Instructions for SQL dialect and formatting

Gemini Pro returns a structured SQL query

### Step 5 — SQL Query Generation
**Response SQL Generator** cleans and validates the LLM-generated SQL before execution

### Step 6 — Database Interaction
- CSV file → automatically parsed → SQLite3 database created with inferred schema
- SQL query executed via `sqlite3` Python library

### Step 7 — Data Retrieval
SQL Executor fetches results → structured into a **Pandas DataFrame**

### Step 8 — Final Response
**Prompt 2** sends the dataframe back to Gemini Pro for natural language summarization → final readable response returned to user

### Step 9 — Data Visualization
**Prompt 3** triggers the visualization model → Matplotlib/Pyplot generates charts based on query results → displayed in Streamlit UI

---

## 🛠️ Tech Stack

| Component | Technology |
|---|---|
| **LLM** | Google Gemini Pro (via API) |
| **Web Framework** | Streamlit |
| **Database** | SQLite3 |
| **Data Processing** | Pandas, NumPy |
| **Visualization** | Matplotlib, Pyplot |
| **Deployment** | AWS EC2 (port forwarding → public Streamlit URL) |
| **IDE** | PyCharm / Visual Studio Code |
| **Prompting Strategy** | Few-Shot Prompting (3-prompt architecture) |

---

## 🎯 Applications

- **Accessibility** — Enables non-SQL users across Britannia's CMI team to run complex data queries independently
- **Efficiency** — Eliminates manual query writing; reduces time-to-insight from hours to seconds
- **Insightful Analysis** — Auto-generated summaries and charts support faster, data-driven decisions
- **Scalable** — Works with any CSV dataset; schema-agnostic design adapts to new data sources

---

## 💡 Key Technical Highlights

- **3-Prompt Architecture** — Separate, specialized prompts for (1) intent parsing, (2) SQL generation with few-shot examples, and (3) visualization triggering
- **Few-Shot Prompting** — SQL generation accuracy improved by providing the LLM with relevant NL→SQL examples in the prompt
- **Auto Schema Inference** — CSV files automatically parsed and converted to SQLite tables with correct column types
- **Stateful Conversation** — Chat History Buffer enables follow-up questions like *"Now filter that for just North India"* without re-specifying context
- **AWS EC2 Deployment** — App hosted on EC2 instance with Streamlit port forwarded to a public URL for company-wide access

---

## ✅ Work Completed

- [x] Natural language to SQL pipeline built and tested
- [x] Gemini Pro API integrated with 3-stage prompt architecture
- [x] CSV → SQLite auto-conversion module
- [x] SQL execution engine with Pandas dataframe output
- [x] Natural language response generation from query results
- [x] Data visualization module (bar charts, line graphs)
- [x] Streamlit web application UI
- [x] Deployed on AWS EC2 with public access

---

## 🔮 Further Improvements

- [ ] Support for **multi-table joins** — enable analysis across multiple CSV files simultaneously
- [ ] Add **LangChain Agents** for more complex, multi-step analytical workflows
- [ ] Integrate **Agentic-RAG** for retrieval from document knowledge bases (PDFs, reports)
- [ ] Add **fine-tuned Llama2** as a locally deployed alternative to Gemini Pro (no API dependency)
- [ ] Support **voice input** for hands-free query entry
- [ ] Add **export functionality** — download results as Excel/PDF reports
- [ ] Extend to **real-time database connections** (PostgreSQL, MySQL) beyond CSV uploads

---

## 💡 Key Learnings

- Building end-to-end **NL-to-SQL pipelines** using LLMs
- Designing effective **few-shot prompts** for structured output generation
- Working with **Google Gemini Pro API** for production use cases
- Creating **multi-prompt architectures** where each prompt serves a distinct role
- Deploying **Streamlit apps on AWS EC2** with public port forwarding
- Managing **conversational state** in multi-turn chatbot interactions

---

## 👤 Authors

**Naman Navneet** | Data Scientist, Britannia Industries Limited (Aug 2023 – Jun 2024)
- 🔗 [LinkedIn](https://www.linkedin.com/in/naman-navneet)
- 💻 [GitHub](https://github.com/NamanNavneet)

**Nikita Chelani** | AI Analyst Intern, Britannia Industries Limited

**Mentor:** Dipesh Lakhotia, Head of Analytics, CMI — Britannia Industries

---

## 📄 License

This project overview is shared for portfolio purposes only. All business data, prompts, and proprietary models remain confidential to Britannia Industries Limited.
