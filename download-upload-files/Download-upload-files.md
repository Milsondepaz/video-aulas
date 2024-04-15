# ** Download e Upload de Arquivos Com Java e Spring Boot ✅**

1. **Criar o repositorio remoto no Git Hub:** [https://github.com/login](https://github.com/login/)
```
git clone git@github.com:Milsondepaz/download-upload-files.git
```

2. **Gerar o projeto através do Spring Initializr:** [https://start.spring.io/](https://start.spring.io/)
   - **Project:** Maven
   - **Language:** Java
   - **Spring Boot version:** 3.2.4
   - **Group:** com.milsondev
   - **Artifact:** download-and-upload-files
   - **Packaging:** Jar
   - **Java version:** 17
   - **Dependencies:** Spring Web, Spring Data JPA, PostgreSQL Driver, Thymeleaf.

3. **Fazer merge entre o repositorio local e remoto, commit "first commit" e push**

4. **Configurar Spring Profiles, Banco de Dados, fazer commit e push** 

- configurar o Banco de Dados: 
- mantem o sem nada application.properties
- criar um application-dev.properties
```
############### PostgreSQL Local ######################
spring.jpa.properties.hibernate.dialect = org.hibernate.dialect.PostgreSQLDialect
spring.jpa.hibernate.ddl-auto=update
spring.jpa.hibernate.show-sql=true

spring.datasource.url=jdbc:postgresql://localhost:5432/seu-banco-de-dados
spring.datasource.username=seu-usuario
spring.datasource.password=sua-palavra-passe
```
- configurar: spring.profiles.active=dev
- rodar, fazer commit "data base configuration", push

5. **Criar Entidades**
- pacotes: db/entities
- classe: MyFile.java:
```
@Entity
@Table(name = "tb_my_file")
public class MyFile {
    @Id
    @GeneratedValue(generator = "uuid2")
    @GenericGenerator(name = "uuid2", strategy = "uuid2")
    @Column(name = "id", columnDefinition = "uuid")
    private UUID id;
    @Column(name="name")
    private String name;

    @Column(name="upload_date")
    private Instant uploadDate;

    @Column(name="size")
    private String size;

    @Column(name = "category")
    @Enumerated(EnumType.STRING)
    private Category category;

    @Column(name="original_file_name")
    private String originalFilename;

    @Column(name="content_type")
    private String contentType;

    @Column(name ="check_sum")
    private Long checksum;

    @Transient
    private byte[] content;
```
- classe: Filecontent.java
```
@Entity
@Table(name = "tb_my_file_content")
public class FileContent {

    @Id
    @GeneratedValue(generator = "uuid2")
    @GenericGenerator(name = "uuid2", strategy = "uuid2")
    @Column(name = "id", columnDefinition = "uuid")
    private UUID id;

    @Lob
    @Column(name = "content")
    private byte[] content;

    @Column(name = "file_id")
    private UUID fileId;
```
 pacote: api/Category
```
public enum Category {
    CV("CV"),
    PASSAPORT("Passaport"),
    LANGUAGE_CERTIFICATE("Language Certificate"),
    OTHER("Other"),
    LETTER_OF_MOTIVATION("Letter Of Motivation"),
    SCHOOL_CERTIFICATE("School Certificate");

    private final String description;

    Category(String description) {
        this.description = description;
    }

    public String getDescription() {
        return description;
    }

    public static Category fromString(String text) {
        if (text != null) {
            String trimmedText = text.trim().replace(" ", "");
            for (Category category : Category.values()) {
                String trimmedDescription = category.getDescription().trim().replace(" ", "");
                if (trimmedText.equalsIgnoreCase(trimmedDescription)) {
                    return category;
                }
            }
        }
        throw new IllegalArgumentException("Nenhum enum com descrição correspondente a " + text);
    }
}

```
- pacotes: db/repositories - interfaces
- FileContentRepository
```
@Repository
public interface FileContentRepository extends JpaRepository<FileContent, UUID> {
    FileContent findByFileId(UUID fileId);
}
```
- MyFileRepository
```
@Repository
public interface MyFileRepository extends JpaRepository<MyFile, UUID> {
    List<MyFile> findByChecksumAndOriginalFilenameAndSize(Long checksum, String originalFilename, String size);
}
```

- pacotes: service
- MyFileService
```
@Service
public class MyFileService {
    private final MyFileRepository myFileRepository;

    private final FileContentRepository fileContentRepository;

    @Value("${max.file.size:1048576}")
    private long MAX_FILE_SIZE;

    @Value("${max.number.of.files:10}")
    private long MAX_NUMBER_OF_FILES;

    @Value("${delete.and.add.file:false}")
    private boolean DELETE_AND_ADD_FILE;

    @Autowired
    public MyFileService(final MyFileRepository myFileRepository,
                         final FileContentRepository fileContentRepository) {
        this.myFileRepository = myFileRepository;
        this.fileContentRepository = fileContentRepository;
    }

    public void saveFile(final MultipartFile file, Category category) throws IOException {
        if(DELETE_AND_ADD_FILE){
            if(getMyFileList().size() < MAX_NUMBER_OF_FILES  ){
                if(file.getSize() / (1024 * 1024) <= MAX_FILE_SIZE ){
                    if(!isDuplicateFile(file)){
                        MyFile myFile = convertMultipartFileToMyFile(file, category);
                        UUID myFileId = myFileRepository.save(myFile).getId();
                        fileContentRepository.save(new FileContent(file.getBytes(), myFileId));
                    } else {
                        throw new DuplicateFileException("Error: File "+ file.getOriginalFilename() +" already uploaded!");
                    }
                } else {
                    throw new FileSizeException("Error: The file you're trying to upload is too too large " + formatSize(file.getSize()) + "!");
                }
            } else {
                throw new MaximumNumberOfFilesExceptions("Error: You've reached the maximum number of allowed uploads. Please delete one to upload a new file!");
            }
        }
    }

    private boolean isDuplicateFile(MultipartFile file) throws IOException {
        Long checksum = calculateChecksum(file.getBytes());
        String originalFilename = file.getOriginalFilename();
        String size = formatSize(file.getSize());
        List<MyFile> arquivos = myFileRepository.findByChecksumAndOriginalFilenameAndSize(checksum, originalFilename, size);
        return !arquivos.isEmpty();
    }

    private long calculateChecksum(final byte[] bytes) {
        Checksum cRC32Checksum = new CRC32();
        cRC32Checksum.update(bytes, 0, bytes.length);
        return cRC32Checksum.getValue();
    }

    public MyFile convertMultipartFileToMyFile(final MultipartFile file, Category category) throws IOException {
        MyFile myFile = new MyFile();
        myFile.setName(file.getName());
        myFile.setOriginalFilename(file.getOriginalFilename());
        myFile.setSize(formatSize(file.getSize()));
        myFile.setUploadDate(Instant.now());
        myFile.setContentType(file.getContentType());
        myFile.setCategory(category);
        myFile.setChecksum(calculateChecksum(file.getBytes()));
        return myFile;
    }

    public List<MyFile> getMyFileList() {
        return myFileRepository.findAll();
    }

    public List<String> getCategories(){
        return Arrays.asList(Category.CV.toString(),
                Category.PASSAPORT.getDescription(),
                Category.LANGUAGE_CERTIFICATE.getDescription(),
                Category.OTHER.getDescription(),
                Category.LETTER_OF_MOTIVATION.getDescription(),
                Category.SCHOOL_CERTIFICATE.getDescription());
    }

    private String formatSize(long fileSize){
        String size;
        if (fileSize >= 1024 * 1024) {
            double sizeInMB = (double) fileSize / (1024 * 1024);
            size = new DecimalFormat("#.##").format(sizeInMB) + " MB";
        } else {
            double sizeInKB = (double) fileSize / 1024;
            size = new DecimalFormat("#").format(sizeInKB) + " KB";
        }
        return size;
    }

    public void deleteFile(UUID id) {
        if(DELETE_AND_ADD_FILE){
            myFileRepository.deleteById(id);
        }
    }

    @Transactional
    public MyFile downloadFile(UUID id) {
        if(DELETE_AND_ADD_FILE){
            Optional<MyFile> optionalMyFile = myFileRepository.findById(id);
            if(optionalMyFile.isPresent()){
                MyFile myFile = optionalMyFile.get();
                FileContent fileContent = fileContentRepository.findByFileId(id);
                myFile.setContent(fileContent.getContent());
                return myFile;
            }
        }

        return null;
    }
}
```
Boa aula! ✅