# **09 - Implementando o Controller e Front End pt. 1 [Aplicação de Lista de Tarefas com Java e Spring Boot] ✅**

1. [ ] **Adicione a Dependência  do Thymeleaf:**
```
<!-- dependência do Thymeleaf -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-thymeleaf</artifactId>
</dependency>
```

2. [ ] **Adicione a Dependência do Thymeleaf Layout Dialect:**

```
<!-- dependência do  Thymeleaf Layout Dialect -->
<dependency>
    <groupId>nz.net.ultraq.thymeleaf</groupId>
    <artifactId>thymeleaf-layout-dialect</artifactId>
    <version>3.3.0</version>
</dependency>
```

3. [ ] **Layout:**
```
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml"
      xmlns:th="http://www.thymeleaf.org"
      xmlns:layout="http://www.ultraq.net.nz/thymeleaf/layout">
<head>
    <meta charset="UTF-8"/>
    <meta name="viewport" content="width=device-width, initial-scale=1,shrink-to-fit=no">
    <meta http-equiv="x-ua-compatible" content="ie=edge">

    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.0.0/dist/css/bootstrap.min.css"
          integrity="sha384-Gn5384xqQ1aoWXA+058RXPxPg6fy4IWvTNh0E263XmFcJlSAwiGgFAW/dAiS6JXm" crossorigin="anonymous">
    <link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.2.0/css/all.css"
          integrity="sha384-hWVjflwFxL6sNzntih27bfxkr27PmbbK/iSvJ+a4+0owXq79v+lsFkW54bOGbiDQ" crossorigin="anonymous">

    <!-- alert dismiss-->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-eOJMYsd53ii+scO/bJGFsiCZc+5NDVN2yr8+0RDqr0Ql0h+rP48ckxlpbzKgwra6" crossorigin="anonymous">

    <!-- meu css />-->
    <link th:href="@{/css/navbar.css}" rel="stylesheet"/>
    <link th:href="@{/css/nova-navbar.css}" rel="stylesheet"/>
    <link th:href="@{/css/footer.css}" rel="stylesheet"/>
    <link th:href="@{/css/alert.css}" rel="stylesheet"/>
</head>

<body style="background-color: lightgray;">
<header th:replace="~{components/header}"></header>
<section layout:fragment="content"></section>
<footer th:replace="~{components/footer}"></footer>

<script src="https://code.jquery.com/jquery-3.6.4.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/popper.js@1.12.9/dist/umd/popper.min.js"
        integrity="sha384-ApNbgh9B+Y1QKtv3Rn7W3mgPxhU9K/ScQsAP7hUibX39j7fakFPskvXusvfa0b4Q"
        crossorigin="anonymous"></script>
<script src="https://cdn.jsdelivr.net/npm/bootstrap@4.0.0/dist/js/bootstrap.min.js"
        integrity="sha384-JZR6Spejh4U02d8jOt6vLEHfe/JQGiRRSQQxSfFWpi1MquVdAyjUar5+76PVCmYl"
        crossorigin="anonymous"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/moment.js/2.29.1/moment.min.js"></script>

<!-- alert dismiss-->
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta3/dist/js/bootstrap.bundle.min.js" integrity="sha384-JEW9xMcG8R+pH31jmWH6WWP0WintQrMb4s7ZOdauHnUtxwoG2vI5DkLtS3qm9Ekf" crossorigin="anonymous"></script>

<script src="https://unpkg.com/htmx.org@1.9.5"
        integrity="sha384-xcuj3WpfgjlKF+FXhSQFQ0ZNr39ln+hwjN3npfM9VBnUskLolQAcN80McRIVOPuO"
        crossorigin="anonymous"></script>


<!-- alert dismiss-->
<script th:src="@{/js/script.js}" th:fragment="js"></script>

<script th:inline="javascript">
    /*<![CDATA[*/
    function buildTaskStatusUrl(status) {
        var baseUrl = /*[[@{/task-by-status}]]*/ '';
        var urlWithParam = baseUrl + '?status=' + status;
        return urlWithParam;
    }
    /*]]>*/
</script>

<script th:inline="javascript">
    /*<![CDATA[*/
    function loadTaskByStatus(status) {
        var url = buildTaskStatusUrl(status);
        var target = '#task-container';

        hx.get(url, { 'hx-swap': 'outerHTML', 'hx-target': target });
    }
    /*]]>*/
</script>


</body>
</html>
```

4. [ ] **Index:**
```
<!DOCTYPE html>
<html lang="en"
      xmlns="http://www.w3.org/1999/xhtml"
      xmlns:layout="http://www.ultraq.net.nz/thymeleaf/layout"
      layout:decorate="~{layout}" xmlns:th="http://www.w3.org/1999/xhtml">
<head>
    <title>My To do List</title>
</head>
<section layout:fragment="content" style="min-height: 90vh; background-color: lightgray; margin-top:5%">
    <div>
        <h1>Hello World</h1> 
    </div>
</section>
</html>

```

5. [ ] **Cabeçalho:**
```
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<nav class="navbar navbar-expand-lg navbar-light"
     style="background-color:#191970; padding-top: 4%; padding-bottom:8%;">
    <div class="container">
        <a href="/task-by-status?status=all" class="navbar-brand">
            <figure>
                <img src="/img/logo.png" class="img-fluid" width="100" height="100">
            </figure>
        </a>
        <button type="button" class="navbar-toggler" data-bs-toggle="collapse" data-bs-target="#navbarCollapse">
            <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarCollapse">
            <ul class="navbar-nav">
                <li class="nav-item">
                    <a class="nav-link js-scroll " href="/add-new-task"
                       style="font-weight: bold; font-size: 90%; color: white;">Add New Task</a>
                </li>
                <li class="submenu">
                    <a class="nav-link js-scroll " href="/" style="font-weight: bold; font-size: 90%; color: white;">List
                        Task</a>
                    <ul class="sub-menu">
                        <li><a href="/task-by-status?status=all">All</a></li>
                        <li><a href="/task-by-status?status=Done">Done</a></li>
                        <li><a href="/task-by-status?status=Progress">Progress</a></li>
                        <li><a href="/task-by-status?status=Ready">Ready</a></li>
                    </ul>
                </li>
            </ul>
        </div>
    </div>
</nav>
</html>
```

5. [ ] **Footer:**
```
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<footer style="background-color: #191970; color: lightgray; padding-top: 40px; padding-bottom: 80px; text-align: center; bottom: 0; width: 100%; display: flex; flex-wrap: wrap; justify-content: center;">
    <div style="display: flex; flex-direction: column; align-items: center;">
        <div style="display: flex; flex-direction: column; align-items: center;">
            <div style="display: inline-block; margin-bottom: 10px; margin-top: 20px;">
                <div class="container">
                    <span class="text-center">Copyright @2023 | Developed with ❤️ by <a
                            href="https://www.youtube.com/@MilsonDev" target="_blank">MilsonDev</a></span>
                    <ul class="social_footer_ul">
                        <li><a href="https://www.youtube.com/@MilsonDev" target="_blank"><i class="fab fa-youtube"></i></a></li>
                        <li><a href="https://github.com/Milsondepaz" target="_blank"><i class="fab fa-github"></i></a></li>
                        <li><a href="https://www.linkedin.com/in/milson-ant%C3%B3nio/" target="_blank"><i class="fab fa-linkedin"></i></a></li>
                        <li><a href="https://www.instagram.com/milsondev/" target="_blank"><i class="fab fa-instagram"></i></a></li>
                        <li><a href="https://www.facebook.com/profile.php?id=61551831070531" target="_blank"><i class="fab fa-facebook-f"></i></a></li>
                    </ul>
                </div>
            </div>
        </div>
    </div>
</footer>
</html>
```

Boa aula! ✅