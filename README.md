
# 🧭 Reverse Proxy Microservices with Docker

This project demonstrates routing multiple backend services through a single NGINX reverse proxy using Docker Compose.

## ⚙️ Setup Instructions

1. Clone the repo:
```bash
git clone https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
cd YOUR_REPO_NAME
```

2. Start the services:
```bash
docker compose up --build
```

All services will run behind NGINX on `http://localhost`.

## 🔀 How Routing Works

NGINX receives requests and forwards them based on the path prefix:

| URL Path                 | Routed To          |
|--------------------------|--------------------|
| `/service1/hello`        | Go service (8001)  |
| `/service2/hello`        | Flask service (8002) |
| `/service1/ping`         | Go service health  |
| `/service2/ping`         | Flask service health |

Example:
```bash
curl http://localhost/service1/ping
curl http://localhost/service2/hello
```

## 📁 Services

- `service_1`: Go app exposing `/ping` and `/hello`
- `service_2`: Flask app exposing `/ping` and `/hello`
- `nginx`: Reverse proxy container
