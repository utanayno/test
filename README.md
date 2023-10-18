# test
## Документация коллекции SkyPro_test

 
Ссылка на репозиторий: https://github.com/utanayno/test.git <br>
Документация по API GitHub issues: https://docs.github.com/en/rest/issues/issues?apiVersion=2022-11-28#about-issues

Для работы с коллекцией должен быть создан репозиторий в github (test). <br>
Коллекция SkyPro_test в Postman содержит 7 запросов, которая выполняет создание Issue в репозитории test, получение списка Issues, изменение и удаление Issue.
Коллекция должна быть запущена и выполнена строго последовательно.

Для работы с коллекцией необходимо добавить токен авторизации github:
1) Заходим на github во вкладку Settings → Developer Settings → Personal access tokens (classic), копируем
2) Вставляем в созданную коллекцию SkyPro_test Postman (вкладка Authorization, Type: Bearer Token).

Методы, используемые в запросах:
1) **GET**. `https://api.github.com/repos/{owner}/{repo}/issues`
2) **POST**. `https://api.github.com/repos/{owner}/{repo}/issues`
3) **PATCH**. `https://api.github.com/repos/{owner}/{repo}/issues/{issue_number}`

В коллекции SkyPro_test создаем переменную с базовым URL (Variable: github_url; Current value: https://api.github.com)

Запросы, входящие в коллекцию:
1. **GET** - получение списка Issues. <br>
    URL: `{{github_url}}/repos/utanayno/test/issues` <br>
    Tests: <br>
    `pm.test("Status code is 200", function () { 
    pm.response.to.have.status(201); 
});` <br>
2. **POST** - создание Issue в репозитории test. <br>
    URL: `{{github_url}}/repos/utanayno/test/issues` <br>
    Body: `{
    "title": "Issue 1", 
    "body": "Something went wrong", 
    "labels":["bug"], 
    "assignees":["utanayno"] 
         }` <br>
    Tests: <br>
    `var key = "number" 
    var value = pm.response.json().number 
    pm.collectionVariables.set(key, value)` 
<br>
    `pm.test("Status code is 201", function () {
    pm.response.to.have.status(201);
    });`
3. **GET** - получение списка Issues. <br>
    URL: `{{github_url}}/repos/utanayno/test/issues` <br>
    Tests: <br>
   `pm.test("Status code is 200", function () {
    pm.response.to.have.status(201);
    });` 
5. **PATCH** - изменение названия Issue, созданного в шаге 2. <br>
    URL: `{{github_url}}/repos/utanayno/test/issues/{{number}}` <br>
    Body: `{
    "title": "Issue 2"
    }`
    Tests: <br>
    `var key = "number"
    var value = pm.response.json().number
    pm.collectionVariables.set(key, value)`
    <br>
    `pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
    });`
6. **GET** - получение Issue, измененного в шаге 4. <br>
    URL: `{{github_url}}/repos/utanayno/test/issues/{{number}}` <br>
    Tests: <br>
    `pm.test("Status code is 200", function () {
    pm.response.to.have.status(201);
    });` 
7. **PATCH** - закрытие Issue, созданного в шаге 2 и изменненного в шаге 4. Удаление Issue возможно только в интерфейсе сервиса. С помощью API не реализовано.
    URL: `{{github_url}}/repos/utanayno/test/issues/{{number}}` <br>
    Body: `{
    "state": "closed"
    }`
    Tests: <br>
    `var key = "number"
    var value = pm.response.json().number
    pm.collectionVariables.set(key, value)`
    <br>
    `pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
    });`
8. **GET** - получение списка Issues. <br>
    URL: `{{github_url}}/repos/utanayno/test/issues` <br>
    Tests: <br>
    `pm.test("Status code is 200", function () {
    pm.response.to.have.status(201);
    });`
 
Для выполнения прогона коллекции:
1) выбрать Run collection напротив названия коллекции SkyPro_test.
2) нажать Run SkyPro_test.
3) результаты прогона приведены на вкладке Run Summary.
