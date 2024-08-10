# **21 - Deploy da Aplicação na Plataforma Render [Aplicação de Lista de Tarefas com Java e Spring Boot] ✅**

1. [ ] **Plataforma Render:**

[https://dashboard.render.com/](https://dashboard.render.com/)

Account Settings 
Connect to GitHub

Environment Variables
```
db = taskmanagement_8eig
host = dpg-cqohm70gph6c73b9pl4g-a.singapore-postgres.render.com
password = geE1yl3KqO3DTzVzWyDUjO4ict4tkNpa
user = milsondev
```

Passos para o deploy e conectar o GitHub no Render

2. [ ] **CI/CD - GitHub Actions:**
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

3. [ ] **Dockerfile:**
```
FROM maven:3.9.8-eclipse-temurin-21-alpine as builder

COPY ./src src/
COPY ./pom.xml pom.xml

RUN mvn clean verify

FROM eclipse-temurin:21-jre-alpine
COPY --from=builder target/*.jar task-management.jar
EXPOSE 8080

CMD ["java", "-jar", "task-management.jar"]
```

4. [ ] **docker-compose.yaml:**
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

5. [ ] **application.properties:**
```
spring.jpa.hibernate.ddl-auto=update
spring.jpa.hibernate.show-sql=true

#spring.datasource.url=jdbc:postgresql://dpg-cqohm70gph6c73b9pl4g-a.singapore-postgres.render.com:5432/taskmanagement_8eig
#spring.datasource.username=milsondev
#spring.datasource.password=geE1yl3KqO3DTzVzWyDUjO4ict4tkNpa

spring.datasource.url=jdbc:postgresql://${host}/${db}
spring.datasource.username=${user}
spring.datasource.password=${password}

#postgresql://milsondev:geE1yl3KqO3DTzVzWyDUjO4ict4tkNpa@dpg-cqohm70gph6c73b9pl4g-a.singapore-postgres.render.com/taskmanagement_8eig
#postgresql://milsondev:edtg6DJJV50G1UbWjhDzlPaXdN0NqJFx@dpg-cqnm36o8fa8c73aring0-a.frankfurt-postgres.render.com/taskmanagerdb_j7hy
#postgresql://milsondev:edtg6DJJV50G1UbWjhDzlPaXdN0NqJFx@dpg-cqnm36o8fa8c73aring0-a.frankfurt-postgres.render.com/taskmanagerdb_j7hy


spring.jpa.properties.hibernate.hbm2ddl.create_namespaces=true

#spring.profiles.active=local

#----remove path info -- jsessionid-------
server.servlet.session.cookie.path=/
server.servlet.session.cookie.http-only=true
server.servlet.session.tracking-modes=cookie
```