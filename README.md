# DevOps Intern Assignment: Nginx Reverse Proxy + Docker

This project demonstrates routing multiple backend services through a single NGINX reverse proxy using Docker Compose.

## Setup Instructions

The project structure is as follows:
```
.
├── docker-compose.yaml # Docker Compose setup
├── nginx/
│ ├── Dockerfile # Builds NGINX container
│ └── nginx.conf # Reverse proxy config
├── service_1/
│ ├── Dockerfile # Go service Dockerfile
│ └── main.go # Go app
├── service_2/
│ ├── Dockerfile # Flask service Dockerfile
│ └── app.py # Flask app
└── README.md # Project documentation
```
How everything is setup:
    <br>--1.Each service has its own Dockerfile
    <br>--2.A single docker-compose.yaml defines how to build and run them
    <br>--3.Docker Compose creates a private network so services can reach each other by name
    <br>--4.NGINX handles all requests on localhost:80 and routes based on the path prefix

## How Routing Works

All services will run behind NGINX on `http://localhost`. NGINX looks at the **URL path** to decide which backend service to forward the request to.
NGINX receives requests and forwards them based on the path prefix:

|        URL Path          |      Routed To       |
|--------------------------|----------------------|
|    `/service1/hello`     | Go service (8001)    |
|    `/service2/hello`     | Flask service (8002) |
|    `/service1/ping`      | Go service health    |
|    `/service2/ping`      | Flask service health |

Example:

```bash
curl http://localhost/service1/ping
curl http://localhost/service2/hello
```
All services are part of a Docker network. Inside that network:
    <br>--1.service_1 is reachable by name (http://service_1:8001)
    <br>--2.service_2 is reachable by name (http://service_2:8002)
    <br>--3.NGINX uses these names in its config to forward traffic correctly.

Hence,allowing the containers to reach each other by their service names.This keeps everything organized behind a single port while still running multiple services.

## Tech Stack

- Docker & Docker Compose  
- NGINX reverse proxy  
- Golang backend  
- Python Flask backend  
- Healthchecks & multistage Docker builds

  ## Author

Rohana Upadhyay  
[GitHub](https://github.com/Brohan-Tech)
   
