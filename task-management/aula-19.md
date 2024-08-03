# **19 - Pagina de Erro Personalizada [Aplicação de Lista de Tarefas com Java e Spring Boot] ✅**

1. [ ] **mensagens personalizada:**
```
private final static String NOT_FOUND = "Error 404: It seems that the page you are looking for does not exist. The link might be incorrect, or the page may have been removed.";
private final static String BAD_REQUEST = "Error 400: It seems there was a problem with the information you submitted. Some data might be incorrect or missing.";
private final static String INTERNAL_SERVER_ERROR = "Error 500: There was an internal problem on our server. We are working to resolve this as quickly as possible.";
```

2. [ ] **error.html:**

```
<!DOCTYPE html>
<html lang="en"
      xmlns="http://www.w3.org/1999/xhtml"
      xmlns:th="http://www.thymeleaf.org"
      xmlns:layout="http://www.ultraq.net.nz/thymeleaf/layout"
      layout:decorate="~{layout}">
<head>
    <title>Error</title>
</head>
<section layout:fragment="content" class="container-fluid" style="padding-top:15%; padding-bottom:15%; background-color:#DCDCDC; min-height: 100vh;">
    <div class="container">
        <div class="row">
            <div class="col-md-6 offset-md-3">
                <div class="card my-3">
                    <div class="row" style="text-align: center; padding-top:8%; padding-bottom:8%;" >
                        <h1>OOPS!</h1>
                        <h4  th:if= "${errorBadRequest != ''}" th:text="${errorBadRequest}"></h4>
                        <h4  th:if= "${errorNotFound != ''}" th:text="${errorNotFound}"></h4>
                        <h4  th:if= "${errorInternalServerError != ''}" th:text="${errorInternalServerError}"></h4>
                        <div class="text-center">
                            <img src="/img/error.png">
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</section>
</html>
```