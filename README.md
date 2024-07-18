# python-flask
This repository demonstrates a multi-stage and multi-file Docker setup for a simple web application with a Python Flask backend, a Node.js frontend, and a PostgreSQL database.

## Directory Structure
```
my_web_app/
├── backend/
│ ├── Dockerfile
│ ├── requirements.txt
│ └── app.py
├── frontend/
│ ├── Dockerfile
│ ├── package.json
│ └── index.js
└── docker-compose.yml
```

## Build and Start
```shell
docker-compose up --build
```

## Stopping the Services
```shell
docker-compose down
```