Facebook Messenger Backend (Cassandra + FastAPI)
This project is part of the Distributed Systems course assignment. It involves building a simplified backend for Facebook Messenger using Apache Cassandra for distributed data storage and FastAPI for the API layer.

📐 Architecture Overview
The project follows a modular FastAPI structure:

bash
Copy
Edit
app/
├── api/           # API routes
├── controllers/   # Business logic
├── models/        # Cassandra models (to be implemented)
├── schemas/       # Request/response Pydantic models
└── db/            # Cassandra DB connection and utilities
⚙️ Requirements
Python 3.11+

Docker & Docker Compose (recommended)

Optional: Local Cassandra setup (for manual development)

🚀 Quickstart with Docker
Get the app running with minimal setup:

Clone the repository

Install Docker and Docker Compose

Run the setup script:

bash
Copy
Edit
./init.sh
This will:

Start both FastAPI and Cassandra containers

Initialize keyspaces and tables

Optionally generate test data

Launch the app at http://localhost:8000

View API docs at http://localhost:8000/docs

To stop the services:

bash
Copy
Edit
docker-compose down
🧪 Generating Test Data
To populate the database with sample data:

bash
Copy
Edit
docker-compose exec app python scripts/generate_test_data.py
This creates:

10 users

15 random conversations

Multiple time-stamped messages per conversation

🔧 Manual Setup (Without Docker)
Clone the repo

Install and run Cassandra locally

Create a virtual environment:

bash
Copy
Edit
python -m venv venv
source venv/bin/activate  # or venv\Scripts\activate on Windows
Install dependencies:

bash
Copy
Edit
pip install -r requirements.txt
Initialize Cassandra schema:

bash
Copy
Edit
python scripts/setup_db.py
Start the app:

bash
Copy
Edit
uvicorn app.main:app --reload
🧱 Cassandra Data Modeling
Design your Cassandra schema to efficiently support:

Sending messages between users

Fetching conversations for a user (latest first)

Fetching messages in a conversation (by time)

Fetching messages before a specific timestamp

📌 Focus on:

Correct partition and clustering keys

Avoiding hotspots

Efficient pagination

Supporting query patterns

🎯 Assignment Objectives
You must implement:

🔹 Cassandra table schema for messaging and conversations

🔹 Message & Conversation models in app/models/

🔹 Controller logic in app/controllers/:

Send message

Get user conversations (paginated)

Get messages in a conversation (paginated)

Get messages before a timestamp (paginated)

📡 API Overview
Messages
POST /api/messages/ → Send a message

GET /api/messages/conversation/{conversation_id} → Fetch conversation messages

GET /api/messages/conversation/{conversation_id}/before?timestamp=... → Messages before a time

Conversations
GET /api/conversations/user/{user_id} → Fetch user’s conversations

GET /api/conversations/{conversation_id} → Get a conversation by ID

✅ Evaluation Criteria
✔ Correct functionality & endpoints

✔ Error handling

✔ Efficient and scalable Cassandra queries

✔ Pagination implementation

✔ Code quality and modularity

✔ Adherence to best practices for Cassandra and distributed systems

