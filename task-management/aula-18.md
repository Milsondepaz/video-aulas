# **14 - Implementando o Controller e Front End pt. 10 [Aplicação de Lista de Tarefas com Java e Spring Boot] ✅**

2. [ ] **paginação:**

```
<div class="container text-center" style="padding-top:5%">
                <nav aria-label="Page navigation example" class="text-center">
                    <div th:if="${totalPages > 1}" class="container text-center justify-content-center">
                        <div class="container" style="width: 100%;">
                            <ul class="pagination justify-content-center" style="background: white;">
                                <li class="page-item" style="padding-right: 20px;">
                                    <strong>Total:</strong> [[${totalItems}]]
                                </li>
                                <li class="page-item" style="padding-right: 20px;"
                                    th:each="i: ${#numbers.sequence(1, totalPages)}">
                                    <a th:if="${currentPage != i}" th:href="@{'/page/' + ${i}}"
                                       th:attr="hx-get=@{'/page/' + ${i}}, hx-trigger='click', hx-swap='outerHTML', hx-target='#task-container'">[[${i}]]</a>
                                    <span th:unless="${currentPage != i}">[[${i}]]</span> &nbsp; &nbsp;
                                </li>
                                <li class="page-item" style="padding-right: 20px;">
                                    <a th:if="${currentPage < totalPages}" th:href="@{'/page/' + ${currentPage + 1}}"
                                       th:attr="hx-get=@{'/page/' + ${currentPage + 1}}, hx-trigger='click', hx-swap='outerHTML', hx-target='#task-container'">Próximo</a>
                                    <span th:unless="${currentPage < totalPages}">Próximo</span>
                                </li>
                                <li class="page-item" style="padding-right: 20px;">
                                    <a th:if="${currentPage < totalPages}" th:href="@{'/page/' + ${totalPages}}"
                                       th:attr="hx-get=@{'/page/' + ${totalPages}}, hx-trigger='click', hx-swap='outerHTML', hx-target='#task-container'">Último</a>
                                    <span th:unless="${currentPage < totalPages}">Último</span>
                                </li>
                            </ul>
                        </div>
                    </div>
                </nav>
            </div>
```