# Анкета кандидата

Работа с анкетой кандидата из Jira

Предварительно необходимо [получить токен](https://talentforce.ru/) приложения

1.  [Получение списка вопросов](#get_quest_list)
2.  [Передача анкеты кандидата](#post_quest_data)
3.  [Получение информации по анкете](#get_quest_info)
4.  [Добавление комментария к анкете](#post_comment_data)
5.  [Получение комментария](#get_comment)
6.  [Загрузка файлов](#upload_file)
7.  [Изменение статуса анкеты](#change_status)
8.  [Возможные ошибки](#errors)
9.  [Список полей и значений ](#fields_list)

* URL для запросов:
`{{talentforce.url}}/index.php` (если не указан дополнительно в описании)

* Необходимые параметры для всех запросов:
`entryPoint : JiraQuestionnaireEntrypoint`

<a name="get_quest_list"></a>
## Получение списка вопросов

* **Запрос**

В *Body* GET-запроса передать:

```json
{
    "token": "{{token}}"
}
```

* **Пример ответа**

Статус 200

```json
[
    {
        "question_id": "4683bde0-bcc8-95c3-941f-60bf6a1ff1a6",
        "question_name": "Начало периода",
        "answer_type": "date_answer",
        "question_type": "base",
        "answer_options": [],
        "free_question": true
    },
    {
        "question_id": "5e5f924e-6921-310d-c30b-60927a329ac4",
        "question_name": "Дата выдачи",
        "answer_type": "date_answer",
        "question_type": "base",
        "answer_options": [],
        "free_question": true
    }
]    
```

<a name="quest_list_descr"></a>
#### Список полей и значений

ID | Вопрос | Тип | Обязательность
--| ------- | ---- | -------------

<a name="post_quest_data"></a>
## Передача анкеты кандидата

* **Запрос**

В *Body* POST-запроса передать:

```json
{
    "token": "{{token}}",

    "external_jira_id": "номер задачи в jira",

    "lkk_candidate_questionnaire": {
        "date_entered": "2021-06-22 08:46:00",
        "id": "в случае создания - id анкеты, в случае обновления - номер задачи в jira",
        "layout_form": "main_job",
        "responsible_hr_email": "test@mail.ru",
        "responsible_hr_name": "Username",
        "vacancy_name": "Vacancyname",
        "verification_stage": "pending_verification",
        "project": "Projectname",
        "system_name": "systemname",
        "for_bank": "yes",
        "check_format": "two_steps"
    },
    "lkk_questionnaires_questions": [
    [
      {
        "sub_group_num": "1627974704095",
        "value": null,
        "id": "f0fad8ef-9e39-184c-47f1-60bf447d8f81"
      },
      {
        "sub_group_num": "1627974704095",
        "value": null,
        "id": "98dc91aa-62e9-fd24-03bf-60bf445b78cd"
      },
      {
        "sub_group_num": "1627974704095",
        "value": "Да",
        "id": "83d47271-f381-6536-5c67-60f7dd595345"
      }
    ]
  ]
}
```
**Полный список вопросов и ответов можно посмотреть тут [Получение списка вопросов](#quest_list_descr)**

#### Список полей и значений
Поле | Описание | Обязательность
-----| -------- | --------------
external_jira_id | ID заявки (внешний ID), по которому можно будет идентифицировать заявку на проверку анкеты для СБ | Да
verification_stage | Этап проверки СБ (Значение: pending_verification => Ожидает проверки, cancelled => Отменено, final_inspection=> На финальной проверке) | Да
responsible_hr_name | ФИО пользователя HR, ответственного за инициацию заявки | Да
responsible_hr_email | E-mail ответственного HR | Да
date_entered | Дата создания заявки на проверку для СБ. Формат данных: гггг-мм-дд чч:мм:сс | Да
vacancy_name | Наименование вакансии | Да
layout_form | Форма оформления (Значения: main_job => Штат (Основное место работы),term_contract => Срочный договор, contract_gpx => Договор ГПХ) | Да
project | Наименование проекта, на который принимается кандидат | Нет
system_name | Юридическое лицо | Да
for_bank | Кандидат оформляется в банк или нет (Значения: 'no' => 'Нет', 'yes' => 'Да') | Да
check_format | Проверка кандидата проходит в 1 этап или в 2 этапа (Значения:  'one_step' => 'В 1 этап',  'two_steps' => 'В 2 этапа') | Да

* **Пример ответа**

Статус 201

```json
{
    "status": "OK",
    "record_id": "e3e16a3f-caf6-9b4c-2f29-61702a74a03d"
}
```
<a name="get_quest_info"></a>
## Получение информации по анкете

* **Запрос**

В *Body* GET-запроса передать:

```json
{
    "token": "{{t1basetoken}}",

    "external_jira_id" : ["номер задачи в Jira"]
}
```

* **Пример ответа**

Статус 200

```json
{
    "6655744": {
        "id": "e3e16a3f-caf6-9b4c-2f29-61702a74a03d",
        "inspector_fio": "Не назначен",
        "verification_stage": "pending_verification",
        "date_entered": "2021-06-22 08:46:00"
    }
}
```

<a name="post_comment_data"></a>
## Добавление комментария к анкете

* **Запрос**

В *Body* POST-запроса передать:

```json
{
    "token": "{{token}}",

    "external_jira_id": "номер задачи в jira",
    
    "parent_id": "идентификатор анкеты, если есть",
    "parent_type": "LKK_CANDIDATE_QUESTIONNAIRE",
    "id": "идентификатор комментария, если нет - создастся новый",
    "date_entered": "2021-06-22 08:46:00",
    "text" : "текст комментария",
    "created_by_name" : "ФИО автора комментария"
}
```

* **Пример ответа**

Статус 201

```json
{
    "status": "OK",
    "record_id": "145344af-dceb-d563-0528-61702a12f345"
}
```
<a name="get_comment"></a>
## Получение комментария

* **Запрос**

В *Body* GET-запроса передать:

```json
{
    "token": "{{t1basetoken}}",

    "comment_id": "идентификатор комментария"
}
```

* **Пример ответа**

Статус 200

```json
{
    "external_jira_id": "номер задачи в jira",
    "parent_id": "id анкеты",
    "date_entered": "22.06.2021 08:46",
    "created_by_name": "ФИО автора комментария",
    "text": "текст комментария"
}
```

<a name="upload_file"></a>
## Загрузка файлов

* **Запрос**

Необходимые параметры для запроса:

`"entryPoint" : "JiraQuestionnaireFileUpload"`

В *Body* POST-запроса (form-data) передать:

```
"external_jira_id"^ : "номер задачи в jira"
"token" : "{{token}}"
"file[]" : "имя_файла.расширение"
```

* **Пример ответа**

Статус 201

```json
{
    "records": {
        "имя_файла.расширение": "1c7cc2a1-bcdb-578b-29d2-61703006ab93"
    },
    "errors": []
}
```

<a name="change_status"></a>
## Изменение статуса анкеты

* **Запрос**

В *Body* POST-запроса передать:

```json
{
    "token": "{{token}}",
    
    "external_jira_id": "номер задачи в jira",

    "lkk_questionnaire_status": {
		"verification_stage": "pending_verification",
		"date_entered": "2021-06-22 08:46:00"
    }
}
```

* **Пример ответа**

Статус 200

```json
{
    "status": "OK",
    "record_id": "e3e16a3f-caf6-9b4c-2f29-61702a74a03d"
}
```
<a name="errors"></a>
## Возможные ошибки

Ошибка | Описание
------ | --------
['status' => 'FAIL', 'error' => 'Unauthorised'] | Отсутствует токен, не корректный токен
['status'=> 'FAIL', 'error'=>'JSON parse fail'] | Невалидный JSON, ошибка форматирования
['status' => 'FAIL', 'error' => 'Method not allowed'] | Не корректный метод запроса
['status' => 'FAIL', 'error' => 'Unknown action'] | В теле запроса не корректные данные
['status' => 'FAIL', 'error' => 'Unknown questionnaire'] | Идентификатор анкеты отсутствует в DB
['records' => '', 'errors' => 'Due to data loses, files data must be an array'] | Передаваемые файлы не в массиве
['records' => '', 'errors' => 'No files received'] | Не передано файлов на entryPoint загруки 
['status' => 'FAIL', 'error' => 'Questionnaire data is empty'] | В запросе по добавлению новой анкеты пустое тело (без вопросов или без основной информации)
['status' => 'FAIL', 'error' => 'Status field is necessary'] | В запросе по изменению статуса не передан статус

<a name="fields_list"></a>
## Список полей и значений

Поле | Описание | Обязательность
-----| -------- | --------------
external_jira_id | ID заявки (внешний ID), по которому можно будет идентифицировать заявку на проверку анкеты для СБ | Да
verification_stage | Этап проверки СБ (Значение: pending_verification => Ожидает проверки, cancelled => Отменено, final_inspection=> На финальной проверке) | Да
responsible_hr_name | ФИО пользователя HR, ответственного за инициацию заявки | Да
responsible_hr_email | E-mail ответственного HR | Да
date_entered | Дата создания заявки на проверку для СБ. Формат данных: гггг-мм-дд чч:мм:сс | Да
vacancy_name | Наименование вакансии | Да
layout_form | Форма оформления (Значения: main_job => Штат (Основное место работы),term_contract => Срочный договор, contract_gpx => Договор ГПХ) | Да
project | Наименование проекта, на который принимается кандидат | Нет
system_name | Юридическое лицо | Да
for_bank | Кандидат оформляется в банк или нет (Значения: 'no' => 'Нет', 'yes' => 'Да') | Да
check_format | Проверка кандидата проходит в 1 этап или в 2 этапа (Значения:  'one_step' => 'В 1 этап',  'two_steps' => 'В 2 этапа') | Да
