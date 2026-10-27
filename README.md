🚀 Ollama AWS Deployment
Deploy an open-source LLM on AWS EC2 using Ollama and expose it through a FastAPI REST API. This project creates a self-hosted AI endpoint that can be consumed by any application through HTTP requests.

📌 Overview
This project uses:

Ollama for model hosting
FastAPI for API development
Docker for containerization
Docker Compose for service orchestration
AWS EC2 for deployment
The FastAPI service communicates with Ollama and provides REST endpoints for model inference.

🏗️ Architecture
Client Application
      │
      ▼
 FastAPI API
  Port 8000
      │
      ▼
 Ollama Server
 Port 11434
      │
      ▼
 Llama Model
✨ Features
Host open-source LLMs using Ollama
FastAPI REST API
Dockerized deployment
Docker Compose orchestration
Health monitoring endpoint
Model listing endpoint
Text generation endpoint
Persistent model storage
AWS EC2 ready
📂 Project Structure
.
├── app.py
├── Dockerfile
├── docker-compose.yml
├── requirements.txt
├── setup.sh
├── template.py
├── README.md
└── .gitignore
🛠 Tech Stack
Python 3.12
FastAPI
Uvicorn
HTTPX
Pydantic
Ollama
Docker
Docker Compose
AWS EC2
🔌 API Endpoints
Home
GET /
Health Check
GET /health
Returns application status and available models.

List Models
GET /models
Returns all Ollama models installed on the server.

Generate Response
POST /generate
Request Body:

{
  "model": "llama3.2",
  "prompt": "Explain RAG."
}
🐳 Docker Services
Ollama Container
Image: ollama/ollama:latest
Port: 11434
Persistent storage enabled
Health checks enabled
FastAPI Container
Built from local Dockerfile
Port: 8000
Communicates with Ollama using Docker networking
🔧 Environment Variables
OLLAMA_BASE_URL=http://ollama:11434
OLLAMA_MODEL=llama3.2
💾 Persistent Storage
Models are stored in a Docker volume:

volumes:
  ollama_data:
This prevents model downloads from being lost after container restarts.

🚀 Local Setup
Clone the repository:

git clone https://github.com/your-username/ollama-aws-deployment.git

cd ollama-aws-deployment
Install dependencies:

pip install -r requirements.txt
Run FastAPI:

uvicorn app:app --host 0.0.0.0 --port 8000
🐳 Docker Deployment
Start containers:

docker compose up -d
Stop containers:

docker compose down
View logs:

docker compose logs -f
Restart services:

docker compose restart
☁️ AWS Deployment
Recommended Configuration:

Setting	Value
Operating System	Ubuntu 22.04 LTS
Instance Type	t3.large
Storage	30 GB gp3
Required Ports:

Port	Purpose
22	SSH
8000	FastAPI
11434	Ollama
✅ Verify Deployment
Health Check:

http://<EC2_PUBLIC_IP>:8000/health
Available Models:

http://<EC2_PUBLIC_IP>:8000/models
Test Generation:

curl -X POST http://<EC2_PUBLIC_IP>:8000/generate \
-H "Content-Type: application/json" \
-d '{
      "model":"llama3.2",
      "prompt":"Hello"
    }'
🐍 Python Example
import requests

response = requests.post(
    "http://<EC2_PUBLIC_IP>:8000/generate",
    json={
        "model": "llama3.2",
        "prompt": "Explain Retrieval Augmented Generation."
    }
)

print(response.json())
🔒 Security
The AWS private key is excluded from version control:

my-ollama-key.pem
Never upload .pem files to GitHub.

📚 Learning Outcomes
After completing this project, you will understand:

AWS EC2 Deployment
Docker & Docker Compose
Ollama Fundamentals
FastAPI Development
REST API Integration
Self-Hosted LLM Infrastructure
Container-Based AI Deployment
⭐ Support
If this project helped you learn something new, consider giving the repository a star.

Happy Learning 🚀