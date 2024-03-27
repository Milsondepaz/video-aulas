# **01 - Configurando Banco de Dados [ Aplicação de Lista de Tarefas com Java e Spring Boot ] ✅**

1. [ ] **Criar o repositorio remoto no Git Hub:** [https://github.com/login](https://github.com/login/)


2. [ ] **Clonar o repositorio remoto:
```
   "link do seu projecto" ex: git clone git@github.com:Milsondepaz/task-management.git
```
- Atencao: Para voce poder clonar repositorio remoto usando ssh, primeiro voce precisa configurar a sua chave, 
se tiver dúvida assista este vídeo: [https://youtu.be/yJwD2ii4pEY?si=VSk4eMnjGJ1NwvJI](https://youtu.be/yJwD2ii4pEY?si=VSk4eMnjGJ1NwvJI)


3. [ ] **Gerar o projeto através do Spring Initializr:** [https://start.spring.io/](https://start.spring.io/)
    - **Project:** Maven
    - **Language:** Java
    - **Spring Boot version:** 3.2.2
    - **Java version:** 21
    - **Dependencies:** Spring Web, Spring Data JPA, PostgreSQL Driver.


4. [ ] **Vizualizar o POM:**
    - Comentar dependências do JPA e PostgreSQL.


5. [ ] **Rodar a aplicação.**


6. [ ] **Vizualizar o POM novamente:**
   - Remover os comentarios nas dependências do Spring Data JPA e PostgreSQL.


7. [ ] **Configurar Banco de Dados:**
   - **Site DZone**: [https://dzone.com/articles/bounty-spring-boot-and-postgresql-database](https://dzone.com/articles/bounty-spring-boot-and-postgresql-database)**

      - Se tiver problemas Em configurar/instalar Banco de Dados assista este video: [https://youtu.be/ypyR3Gxp-vA?si=frJY3XKrTEscgSCN](https://youtu.be/ypyR3Gxp-vA?si=frJY3XKrTEscgSCN)
```
spring.jpa.properties.hibernate.dialect = org.hibernate.dialect.PostgreSQLDialect
spring.jpa.hibernate.ddl-auto=none
spring.jpa.hibernate.show-sql=true

spring.datasource.url=jdbc:postgresql://localhost:5432/seu-banco-de-dados
spring.datasource.username=seu-usuario
spring.datasource.password=sua-palavra-passe
```

8. [ ] **Rodar a aplicação novamente, já com o Banco de Dados configurado.**

9. [ ] **Fazer commit e push para o repositorio remoto.**
   

Boa aula! ✅