# **To-do-List - Aula 02**

## **- Objetivo: configurar Banco de Dados**

1. [ ] **Criar uma nova branch**

2. [ ] **Adicionar/Configurar ambiente de desenvolvimento**

3. [ ] **Criar e Configurar o Banco de dados**
```
spring.jpa.properties.hibernate.dialect = org.hibernate.dialect.PostgreSQLDialect
spring.jpa.hibernate.ddl-auto=update
spring.jpa.hibernate.show-sql=true
spring.datasource.url=jdbc:postgresql://localhost:5432/task-management
spring.datasource.username=postgres
spring.datasource.password=123456
```

4. [ ] **Testar/Rodar a aplicacao.**
```
spring.profiles.active=local
```

5. [ ] **Enviar o código para o reposiotiro remoto.**

Boa aula! 🚀