# **04 - Configurar Um Schema [Aplicação de Lista de Tarefas com Java e Spring Boot] ✅**

1. [ ] **Arquivo init.sql:**
```
    CREATE SCHEMA IF NOT EXISTS schema_task;
```

2. [ ] **Adicione essa linha no arquivo: application.properties p/ forçar o Spring a ler o arquivo init.sql:**
```
    spring.jpa.properties.hibernate.hbm2ddl.create_namespaces=true
```

Boa aula! ✅