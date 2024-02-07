# **To-do-List - Aula 02**

## **- Objetivo: Preparar a aplicacao para executar o CRUD parte 1**

1. [ ] **Criar uma nova branch:**
   - feature/DEV-001-crud-task

- db
    - entities
        - TaskEntity.java
    - repository
        - TaskEntityRepository.java
- service
- api


2. [ ] **Adicionar dependencia: Jakarta Validation**
```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-validation</artifactId>
</dependency>
```


3. [ ] **Atrributos da classe taskEntity:**
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

4. [ ] **Testar/Rodar a aplicacao.**


6. [ ] **Fazer commit e push para o repositorio remoto.**


Boa aula! 🚀