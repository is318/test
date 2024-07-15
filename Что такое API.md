:white_check_mark: **Задание:** Рассказать простыми словами что такое API. Нужно написать небольшую статью (1-2 листа А4) о том, что это такое. Целевая аудитория – среднестатистический пользователь ПК, знающий стандартную терминологию.

---

### Что такое API
**API (application programming interface)** – интерфейс взаимодействия между приложениями, то есть как и с помощью чего одна программа может обращаться к другой. 

Данный термин обычно рассматривается при взаимодействии с каким-либо веб-сервисом. Эти сервисы могут быть как открытыми, так и требующими авторизации, например: 
- [HeadHunter API](https://dev.hh.ru/) – для работы с данными портала [hh.ru](https://hh.ru/); 
- Сервис с данными по полетам [Flightaware.com](https://www.flightaware.com/commercial/aeroapi/);
- Методы СБП API ([sbp.nspk.ru/api](https://sbp.nspk.ru/api/)) позволяют производить регистрацию юридических лиц и оплату по платежным ссылкам (QR-коду).

Для проверки работы сервиса и оценки качества данных можно использовать [Postman](https://www.postman.com/).

Чтобы выполнить запрос, нужно:
1. Выбрать метод http-запроса (например, [метод GET](https://learning.postman.com/docs/sending-requests/create-requests/request-basics/#select-request-methods) – для запроса содержимого ресурса);
2. Ввести URL – путь до нужного ресурса;
3. Заполнить необходимые параметры и отправить запрос.

#### Пример поиска вакансии с окладом 100к в Сочи
<kbd>
<img src="/Screens/Postman.png" width="800">
</kbd>

:information_source: Описание параметров метода: ["Поиск по вакансиям"](https://api.hh.ru/openapi/redoc#tag/Poisk-vakansij/operation/get-vacancies).

**Алгоритм выполнения запроса:**
1. Выбрать метод GET и вставить URL `https://api.hh.ru/vacancies`.
2. Заполнить параметры в графе "Params":
- по зарплате: Key=salary, Value=100000 (по умолчанию используется код валюты RUR);
- по региону: Key=area, Value=237 - `id` региона, извлекается из [справочника регионов](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-areas):

```json
"id": "237",
"parent_id": "1438",
"name": "Сочи",
"areas": []
```
3. Отправить запрос.

**В нижней части интерфейса Postman придет:**
- Статус запроса: `200 OK` - выполнено успешно;
- Ответ с описаниями вакансий в формате JSON;
- Количество найденных результатов `"found": 4492` (в самом низу ответа).

**Пример полного описания [вакансии](https://hh.ru/vacancy/103074680) на hh.ru:**
```json
        {
            "id": "103074680",
            "premium": false,
            "name": "Сотрудник в отель у моря",
            "department": null,
            "has_test": false,
            "response_letter_required": false,
            "area": {
                "id": "237",
                "name": "Сочи",
                "url": "https://api.hh.ru/areas/237"
            },
            "salary": {
                "from": 138000,
                "to": 184000,
                "currency": "RUR",
                "gross": false
            },
            "type": {
                "id": "open",
                "name": "Открытая"
            },
            "address": null,
            "response_url": null,
            "sort_point_distance": null,
            "published_at": "2024-07-01T17:54:43+0300",
            "created_at": "2024-07-01T17:54:43+0300",
            "archived": false,
            "apply_alternate_url": "https://hh.ru/applicant/vacancy_response?vacancyId=103074680",
            "show_logo_in_search": null,
            "insider_interview": null,
            "url": "https://api.hh.ru/vacancies/103074680?host=hh.ru",
            "alternate_url": "https://hh.ru/vacancy/103074680",
            "relations": [],
            "employer": {
                "id": "1250899",
                "name": "СИМПЛЕКС",
                "url": "https://api.hh.ru/employers/1250899",
                "alternate_url": "https://hh.ru/employer/1250899",
                "logo_urls": {
                    "original": "https://img.hhcdn.ru/employer-logo-original/955799.jpg",
                    "90": "https://img.hhcdn.ru/employer-logo/4263724.jpeg",
                    "240": "https://img.hhcdn.ru/employer-logo/4263725.jpeg"
                },
                "vacancies_url": "https://api.hh.ru/vacancies?employer_id=1250899",
                "accredited_it_employer": false,
                "trusted": true
            },
            "snippet": {
                "requirement": "Опыт работы не требуется!",
                "responsibility": "Мытье посуды, уборка обеденного зала. Помощь в приготовлении блюд."
            },
            "contacts": null,
            "schedule": {
                "id": "flyInFlyOut",
                "name": "Вахтовый метод"
            },
            "working_days": [],
            "working_time_intervals": [],
            "working_time_modes": [],
            "accept_temporary": false,
            "professional_roles": [
                {
                    "id": "102",
                    "name": "Разнорабочий"
                }
            ],
            "accept_incomplete_resumes": true,
            "experience": {
                "id": "noExperience",
                "name": "Нет опыта"
            },
            "employment": {
                "id": "full",
                "name": "Полная занятость"
            },
            "adv_response_url": null,
            "is_adv_vacancy": false,
            "adv_context": null
        },
```
