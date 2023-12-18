# **To-do-List - Aula 02**

## **- Objetivo: configurar Banco de Dados**

1. [ ] **Adicionar perfil local**

2. [ ] **Configurar o Banco de dados**
```
spring.jpa.properties.hibernate.dialect = org.hibernate.dialect.PostgreSQLDialect
spring.jpa.hibernate.ddl-auto=update
spring.jpa.hibernate.show-sql=true
spring.datasource.url=jdbc:postgresql://localhost:5432/task-management
spring.datasource.username=postgres
spring.datasource.password=123456
```

3. [ ] **Rodar a aplicacao.**
```
spring.profiles.active=local
```

4. [ ] **Merge to master.**

Boa aula! 🚀