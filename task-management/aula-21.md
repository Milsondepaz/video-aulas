# **21 - Spring Profile & Banco de Dados Remoto [Aplicação de Lista de Tarefas com Java e Spring Boot] ✅**

1. [ ] **Plataforma Render:**

[https://dashboard.render.com/](https://dashboard.render.com/)

2. [ ] **Remover jsessionid:**
```
#----remove path info -- jsessionid-------
server.servlet.session.cookie.path=/
server.servlet.session.cookie.http-only=true
server.servlet.session.tracking-modes=cookie
```