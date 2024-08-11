# **22 - Docker Image e Deploy na Plataforma Render [Aplicação de Lista de Tarefas com Java e Spring Boot] ✅**

1. [ ] **docker-compose.yaml:**
```
version: '3.7'

services:

  task-management:
    build:
      context: ./.
      dockerfile: Dockerfile
    container_name: task-management
    hostname: task-management
    ports:
      - "8080:8080"
    depends_on:
      - postgres
    environment:
      host: "postgres"
      port: 5432
      db: "postgres"
      password: postgres
      user: postgres
    volumes:
      - /data/task-management/data:/var/lib/postgresql/data
    networks:
      - milsondev_network

  postgres:
    image: postgres:14.0
    container_name: postgres
    hostname: postgres
    volumes:
      - /data/task-management/data:/var/lib/postgresql/data
    environment:
      POSTGRES_PASSWORD: postgres
      POSTGRES_USER: postgres
      POSTGRES_DBNAME: postgres
    ports:
      - 5432:5432
    networks:
      - milsondev_network

networks:
  milsondev_network:
    driver: bridge
```

2.[ ] **CI/CD - GitHub Actions:**
```
name: CI/CD

on:
  push:
    branches:
      - '*'
  pull_request:
    branches:
      - '*'

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: checkout source code
        uses: actions/checkout@v2

      - name: JDK configuration
        uses: actions/setup-java@v2
        with:
          java-version: '19'
          distribution: 'adopt'

      - name: install Maven
        run: sudo apt-get install -y maven

      - name: build app
        run: mvn package

      - name: Run tests
        run: mvn test
```