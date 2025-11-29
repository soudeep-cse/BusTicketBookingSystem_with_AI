
# BussTicketBD - Intelligent Conversational Bus Booking Platform

**An AI-powered bus ticket management system for Bangladesh that revolutionizes travel booking through natural language conversations, featuring advanced intent recognition, multi-step workflow orchestration, and comprehensive ticket lifecycle management.**


### 🛠 **Technology Stack**
- **AI/ML:** OpenAI GPT-4 + LangGraph (conversation orchestration) + Pinecone (vector embeddings)
- **Backend:** FastAPI (async REST API) + MongoDB (operational data) + Motor (async driver)
- **Frontend:** Streamlit (interactive chat interface)
- **Infrastructure:** Docker Compose (containerized deployment)

### 🚀 **Core Capabilities**
- **Smart Route Discovery** - AI-driven route search across 10 major districts with real-time availability
- **Conversational Booking** - Natural language ticket booking with context-aware dialog management  
- **Ticket Management** - Complete booking lifecycle: view, modify, and cancel reservations
- **Provider Intelligence** - Comprehensive coverage of 6 major bus operators with route optimization
- **Memory-Persistent Chat** - Contextual conversations with intelligent state management

## Features
- LLM-driven intent detection and dialog nodes.
   - **search routes**
   - **provider information**
   - **booking ticktets**
   - **view tickets**
   - **cancel tickets**
- MongoDB-backed data for districts, dropping points, and bookings.
- Streamlit demo UI for chat interaction.
- Docker Compose for easy local development with MongoDB.

## Prerequisites
- Python 3.11
- Docker & Docker Compose (optional, recommended for easy setup)
- An OpenAI-compatible API key set in .env as OPENAI_API_KEY
- Pinecone key for using embedding features

## Quick setup (local)
1. Create and activate a virtual environment:
```bash
python -m venv venv
venv/Scripts/activate
```
2. Install dependencies:
```bash
pip install -r requirements.txt
```
3. You have to provide all the secrets on .env file:
```bash
OPENAI_API_KEY="your openai api key"
PINECONE_API_KEY="your pinecone api key"
PINECONE_INDEX="pinecone index"
MONGO_STRING_URI="mongodb://mongo:27017"
```

## Run locally (without Docker)
1. Start the app (FastAPI + Streamlit demo):
```bash
uvicorn app.main:app --reload
streamlit run frontend.py
```
API: FastAPI runs on http://localhost:8000 
Frontend: Streamlit chat runs on http://localhost:8501

## Run with Docker Compose (recommended)
1. Build and start services:
```bash
docker compose up --build
```
2. The stack will expose:
   - FastAPI: http://localhost:8000
   - Streamlit: http://localhost:8501
   - MongoDB: mongodb://localhost:27017

## Project Structure

```text
├── app
│   ├── api
│   │    └── routes
│   │          └── chat.py 
│   ├── schemas
│   │      └── chat_schema.py 
│   ├── services
│   │       ├── langgraph_nodes
│   │       │           ├── detect_intent.py
│   │       │           ├── general_chat.py
│   │       │           ├── ask_for_info.py
│   │       │           ├── book_ticket.py
│   │       │           ├── provider_info.py
│   │       │           ├── view_ticket.py
│   │       │           └── cancel_ticket.py
│   │       ├── chatbot_langgraph.py
│   │       ├── buss_data_loader.py
│   │       └── load_to_pinecone.py
│   ├── utils
│   │     └── chat_memory.py
│   ├── config.py
│   └── main.py
├── data
├── test
├── data.json
├── frontend.py
└── requirements.txt
```
## Langgraph

![Langgraph](https://github.com/soudeep-cse/BusTicketBookingSystem_with_AI/blob/main/images/langgraph.png)

## Notes
- The project expects a single aggregated document in the `busses` collection and `buss provider information` in the vector database. (created by the startup loader).
- For production deployment, secure secrets and consider using a managed DB and API gateway.

## License
This project is licensed under the MIT License – see the [LICENSE](./LICENSE) file for details.

## Screenshot

![Output](https://github.com/soudeep-cse/BusTicketBookingSystem_with_AI/blob/main/images/Output.png)
