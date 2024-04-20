# **10 - Implementando o Controller e Front End pt. 2 [Aplicação de Lista de Tarefas com Java e Spring Boot] ✅**

1. [ ] **Adicione a Tabela para listar as tarefas:**
```
<!-- start table-->
    <div th:if="${not #lists.isEmpty(taskDtoList)}">
        <div id="task-container" class="card container"
             style="margin-top:1%; margin-bottom:1%; width: 60%; height:60%; border: none; padding-bottom:2%">
            <div th:each="taskDto, iterStat : ${taskDtoList}">
                <div class="card-body" style="margin-bottom: 8px; margin-bottom: 4px;">
                    <div id="accordion">
                        <div th:id="'card-' + ${taskDto.id}" class="card" style="margin-bottom: -4%;">
                            <div th:id="'heading' + ${iterStat.index}" class="card-header"
                                 style="display: flex; justify-content: space-between; text-align: left;">
                                <div class="col-sm">
                                    <h5 class="mb-0">
                                        <button class="btn btn-link" data-toggle="collapse"
                                                th:data-target="'#collapse' + ${iterStat.index}"
                                                aria-expanded="false" aria-controls="'collapse' + ${iterStat.index}">
                                            <span th:text="${taskDto.title}"></span>
                                        </button>
                                    </h5>
                                </div>
                                <div class="col col-lg-5">
                                    <div class="row">
                                        <div class="col">
                                            <span th:text="${taskDto.priority}">
                                                  <!--th:class="${taskDto.priorityClass}"--></span>
                                        </div>
                                        <div class="col">
                                            <span th:text="${taskDto.status.name()}">
                                                  <!--th:class="${taskDto.statusClass}"--></span>
                                        </div>
                                        <div class="col">
                                            <!--
                                            <a class="btn btn-primary" th:href="@{/edit-task/{id}(id=${taskDto.id})}">
                                                <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16"
                                                     fill="currentColor"
                                                     class="bi bi-pencil" viewBox="0 0 16 16">
                                                    <path d="M12.146.146a.5.5 0 0 1 .708 0l3 3a.5.5 0 0 1 0 .708l-10 10a.5.5 0 0 1-.168.11l-5 2a.5.5 0 0 1-.65-.65l2-5a.5.5 0 0 1 .11-.168l10-10zM11.207 2.5 13.5 4.793 14.793 3.5 12.5 1.207zm1.586 3L10.5 3.207 4 9.707V10h.5a.5.5 0 0 1 .5.5v.5h.5a.5.5 0 0 1 .5.5v.5h.293zm-9.761 5.175-.106.106-1.528 3.821 3.821-1.528.106-.106A.5.5 0 0 1 5 12.5V12h-.5a.5.5 0 0 1-.5-.5V11h-.5a.5.5 0 0 1-.468-.325z"/>
                                                </svg>
                                            </a>
                                            -->
                                            <!--
                                            <button type="button" class="btn btn-primary btn-delete"
                                                    th:attr="hx-get=@{/delete-task/{id}(id=${taskDto.id})},hx-target=|#task-container|"
                                                    hx-trigger="click"
                                                    hx-swap="outerHTML">
                                                <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16"
                                                     fill="currentColor"
                                                     class="bi bi-trash3" viewBox="0 0 16 16">
                                                    <path d="M6.5 1h3a.5.5 0 0 1 .5.5v1H6v-1a.5.5 0 0 1 .5-.5M11 2.5v-1A1.5 1.5 0 0 0 9.5 0h-3A1.5 1.5 0 0 0 5 1.5v1H2.506a.58.58 0 0 0-.01 0H1.5a.5.5 0 0 0 0 1h.538l.853 10.66A2 2 0 0 0 4.885 16h6.23a2 2 0 0 0 1.994-1.84l.853-10.66h.538a.5.5 0 0 0 0-1h-.995a.59.59 0 0 0-.01 0zm1.958 1-.846 10.58a1 1 0 0 1-.997.92h-6.23a1 1 0 0 1-.997-.92L3.042 3.5zm-7.487 1a.5.5 0 0 1 .528.47l.5 8.5a.5.5 0 0 1-.998.06L5 5.03a.5.5 0 0 1 .47-.53Zm5.058 0a.5.5 0 0 1 .47.53l-.5 8.5a.5.5 0 1 1-.998-.06l.5-8.5a.5.5 0 0 1 .528-.47ZM8 4.5a.5.5 0 0 1 .5.5v8.5a.5.5 0 0 1-1 0V5a.5.5 0 0 1 .5-.5"/>
                                                </svg>
                                            </button>
                                            -->
                                        </div>
                                    </div>
                                </div>
                            </div>
                            <div th:id="'collapse' + ${iterStat.index}" class="collapse"
                                 aria-labelledby="'heading' + ${iterStat.index}" data-parent="#accordion">
                                <div class="card-body">
                                    <div style="display: flex; justify-content: space-between; margin-bottom: 10px;">
                                    <span><b>Created on:</b> <span
                                            th:text="${taskDto.createdOn}"></span></span><br>
                                        <span><b>Edited on:</b> <span
                                                th:text="${taskDto.updatedOn}"></span></span><br>
                                        <span><b>Expires in:</b> <span
                                                th:text="${taskDto.expireOn}"></span></span><br>
                                    </div>
                                    <div style="text-align: justify;">
                                        <p th:text="${taskDto.description}"></p>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div>
                <!-- start pagination -->
                
                <!-- end pagination -->
            </div>
        </div>
    </div>
    <!-- end table -->
```

2. [ ] **new-task.html:**

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
    <div th:if="${alertMessage != null and alertMessage != ''}" class="panel-heading" th:replace="~{components/alert.html}"></div>
    <div id="taskGet-container" class="card container"
         style="margin-top:1%; margin-bottom:1%; width: 50%; height:60%; border: none; padding-bottom:2%">
        <form action="#" th:action="@{/add-or-update-task}" method="post" th:object="${taskDto}">
            <div class="container">
                <div class="row">
                    <div class="col-md-26 mt-5">
                        <div class="card">
                            <article class="card-body">
                                <div class="form-group">
                                    <div class="row">

                                        <div class="col-md-12 mt-2">
                                            <label>Title</label>
                                            <input type="text" class="form-control" name="title" placeholder="Title"
                                                   th:field="*{title}"
                                                   th:classappend="${#fields.hasErrors('title')} ? 'is-invalid' : ''">
                                            <input type="hidden" name="id" th:value="${id}" th:field="*{id}"/>
                                            <div th:if="${#fields.hasErrors('title')}" th:errors="*{title}"
                                                 class="invalid-feedback"></div>
                                        </div>

                                        <div class="col-md-12 mt-2">
                                            <label>Description</label>
                                            <textarea class="form-control" rows="4" name="description"
                                                      placeholder="Description" th:field="*{description}"
                                                      th:classappend="${#fields.hasErrors('description')} ? 'is-invalid' : ''"></textarea>
                                            <div th:if="${#fields.hasErrors('description')}" th:errors="*{description}"
                                                 class="invalid-feedback"></div>
                                        </div>


                                        <div class="col-md-4 mb-3 mt-2">
                                            <label>Priority Level</label>
                                            <select class="form-control" name="priority" th:field="*{priority}">
                                                <option th:each="priority : ${priorities}"
                                                        th:value="${priority}"
                                                        th:text="${priority}"></option>
                                            </select>
                                        </div>

                                        <div class="col-md-4 mb-3 mt-2">
                                            <label>Status</label>
                                            <select class="form-control" name="status" th:field="*{status}">
                                                <option th:each="status : ${statusList}"
                                                        th:value="${status}"
                                                        th:text="${status}"></option>
                                            </select>
                                        </div>

                                        <div class="col-md-4 mb-3 mt-2">
                                            <label>Expira em</label>
                                            <input type="date" class="form-control" name="expireOn"
                                                   th:field="*{expireOn}" placeholder="Data de Conclusão"
                                                   id="expireDatePicker"
                                                   th:classappend="${#fields.hasErrors('expireOn')} ? 'is-invalid' : ''">
                                            <script>
                                                var today = new Date().toISOString().split('T')[0];
                                                document.getElementById('expireDatePicker').min = today;

                                            </script>
                                            <div th:if="${#fields.hasErrors('expireOn')}" th:errors="*{expireOn}"
                                                 class="invalid-feedback"></div>
                                        </div>
                                    </div>
                                </div>
                            </article>
                        </div>
                    </div>

                    <div class="row mt-3" style="padding-top: 2%">
                        <div class="col mt-3">
                            <a class="btn btn-primary" href="/" style="width: 48%;">Cancel</a>
                        </div>
                        <div class="col mt-3 d-flex justify-content-end">
                            <button type="submit" class="btn btn-primary" style="width: 48%;">Save</button>
                        </div>
                    </div>

                </div>
            </div>
        </form>
    </div>
</section>
</html>
```

2. [ ] **alert.html:**
```
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml"
      xmlns:th="http://www.thymeleaf.org">
<svg xmlns="http://www.w3.org/2000/svg" style="display: none;">
    <symbol id="check-circle-fill" fill="currentColor" viewBox="0 0 16 16">
        <path d="M16 8A8 8 0 1 1 0 8a8 8 0 0 1 16 0zm-3.97-3.03a.75.75 0 0 0-1.08.022L7.477 9.417 5.384 7.323a.75.75 0 0 0-1.06 1.06L6.97 11.03a.75.75 0 0 0 1.079-.02l3.992-4.99a.75.75 0 0 0-.01-1.05z"/>
    </symbol>
    <symbol id="info-fill" fill="currentColor" viewBox="0 0 16 16">
        <path d="M8 16A8 8 0 1 0 8 0a8 8 0 0 0 0 16zm.93-9.412-1 4.705c-.07.34.029.533.304.533.194 0 .487-.07.686-.246l-.088.416c-.287.346-.92.598-1.465.598-.703 0-1.002-.422-.808-1.319l.738-3.468c.064-.293.006-.399-.287-.47l-.451-.081.082-.381 2.29-.287zM8 5.5a1 1 0 1 1 0-2 1 1 0 0 1 0 2z"/>
    </symbol>
    <symbol id="exclamation-triangle-fill" fill="currentColor" viewBox="0 0 16 16">
        <path d="M8.982 1.566a1.13 1.13 0 0 0-1.96 0L.165 13.233c-.457.778.091 1.767.98 1.767h13.713c.889 0 1.438-.99.98-1.767L8.982 1.566zM8 5c.535 0 .954.462.9.995l-.35 3.507a.552.552 0 0 1-1.1 0L7.1 5.995A.905.905 0 0 1 8 5zm.002 6a1 1 0 1 1 0 2 1 1 0 0 1 0-2z"/>
    </symbol>
</svg>
<div id="alertID" class="container alert custom-alert" role="alert">
    <svg class="bi flex-shrink-0 me-2" width="24" height="24" role="img" aria-label="Success:">
        <use xlink:href="#check-circle-fill"/>
    </svg>
    <span id="alertMessage" th:text="${alertMessage}"></span>
    <button type="button" class="btn-close" data-bs-dismiss="alert" aria-label="Close"></button>
    <script th:inline="javascript">
        /* <![CDATA[ */
        function hideAlert() {
            document.getElementById('alertID').style.display = 'none';
        }
        setTimeout(hideAlert, 5000);
        var alertMessage = /*[[${alertMessage}]]*/ '';
        var alertElement = document.getElementById('alertID');
        if (alertMessage.startsWith('New task')) {
            alertElement.classList.add('alert-success');
        } else if (alertMessage.startsWith('Task was been')) {
            alertElement.classList.add('alert-info');
        } else if (alertMessage.startsWith('Error, please fill')){
            alertElement.classList.add('alert-danger');
        }
        if (alertMessage.trim() === '') {
            alertElement.style.display = 'none';
        }
        /* ]]> */
    </script>
</div>
</html>
```

Boa aula! ✅