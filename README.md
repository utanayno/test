# test
## Документация по тестированию API GitHub issues

 
Ссылка на репозиторий: https://github.com/utanayno/test.git <br>
Документация по API GitHub issues: https://docs.github.com/en/rest/issues/issues?apiVersion=2022-11-28#about-issues

Для работы с коллекцией должен быть создан репозиторий в github (test). <br>
Коллекция SkyPro_test в Postman содержит 7 запросов, которая выполняет создание Issue в репозитории test, получение списка Issues, изменение и удаление Issue.
Коллекция должна быть запущена и выполнена строго последовательно.

Для работы с коллекцией необходимо добавить токен авторизации github:
1) Заходим на github во вкладку Settings → Developer Settings → Personal access tokens (classic), копируем.
2) Вставляем в созданную коллекцию SkyPro_test Postman (вкладка Authorization, Type: Bearer Token).
3) У каждого запроса во вкладке Authorization в Type указать: Inherit auth from parent.

Методы, используемые в запросах:
1) **GET**. `https://api.github.com/repos/{owner}/{repo}/issues`
2) **POST**. `https://api.github.com/repos/{owner}/{repo}/issues`
3) **PATCH**. `https://api.github.com/repos/{owner}/{repo}/issues/{issue_number}`

В коллекции SkyPro_test создаем переменную с базовым URL (Variable: github_url; Current value: https://api.github.com)

Запросы, входящие в коллекцию:
1. **GET** - получение списка Issues. <br>
    URL: `{{github_url}}/repos/utanayno/test/issues` <br>
    
2. **POST** - создание Issue в репозитории test. <br>
    URL: `{{github_url}}/repos/utanayno/test/issues` <br>
    Body: `{
    "title": "Issue 1", 
    "body": "Something went wrong", 
    "labels":["bug"], 
    "assignees":["utanayno"] 
         }` <br>
   
3. **GET** - получение списка Issues. <br>
    URL: `{{github_url}}/repos/utanayno/test/issues` <br>
    
5. **PATCH** - изменение названия Issue, созданного в шаге 2. <br>
    URL: `{{github_url}}/repos/utanayno/test/issues/{{number}}` <br>
    Body: `{
    "title": "Issue 2"
    }`
   
6. **GET** - получение Issue, измененного в шаге 4. <br>
    URL: `{{github_url}}/repos/utanayno/test/issues/{{number}}` <br>
    
7. **PATCH** - закрытие Issue, созданного в шаге 2 и изменненного в шаге 4. Удаление Issue возможно только в интерфейсе сервиса. С помощью API не реализовано.<br>
    URL: `{{github_url}}/repos/utanayno/test/issues/{{number}}` <br>
    Body: `{
    "state": "closed"
    }`
    
8. **GET** - получение списка Issues. <br>
    URL: `{{github_url}}/repos/utanayno/test/issues` <br>
   

Во вкладку Tests у каждого запроса коллекции добавляем скрипты:
1) для методов GET, PATCH: проверку на статус 200 ОК в ответе.
2) для метода POST: проверку на статус 201 ОК в ответе.
3) для методов POST, PATCH: скрипт на сохранение переменной номера Issue для передачи в последующие запросы.<br>
`var key = "number"
var value = pm.response.json().number
pm.collectionVariables.set(key, value)`
 
Для выполнения прогона коллекции:
1) выбрать Run collection напротив названия коллекции SkyPro_test.
2) нажать Run SkyPro_test.
3) результаты прогона приведены на вкладке Run Summary.
