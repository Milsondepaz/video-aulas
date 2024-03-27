# **02 - Criando Classe Modelo TaskEntity [ Aplicação de Lista de Tarefas com Java e Spring Boot ] ✅**

1. [ ] **Criar uma nova branch:**
   - feature/DEV-001-crud-task

2. [ ] **Adicionar dependencia: Jakarta Validation**
```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-validation</artifactId>
</dependency>
```


3. [ ] **Classe taskEntity:**
```
    @Id
    @GeneratedValue(generator = "uuid2")
    @GenericGenerator(name = "uuid2", strategy = "uuid2")
    @Column(name = "id", columnDefinition = "uuid")
    private UUID id;
    
    @Column(name="title")
    private String title;
    
    @Column(name="created_on")
    private Instant createdOn;
    
    @Column(name="updated_on")
    private Instant updatedOn;
    
    @Column(name="expired_on")
    private Instant expireOn;
    
    @Column(name = "priority")
    @Enumerated(EnumType.STRING)
    private Priority priority;
    
    @Column(name = "status")
    @Enumerated(EnumType.STRING)
    private Status status;
    
    @Column(name = "description", columnDefinition = "TEXT", length=300)
    private String description;
```

4. [ ] **Adicionar arquivo: /resources/schema.sql**
```
-- create schema
CREATE SCHEMA IF NOT EXISTS schema_task;
```

4. [ ] **Testar/Rodar a aplicacao.**


Boa aula! 🚀