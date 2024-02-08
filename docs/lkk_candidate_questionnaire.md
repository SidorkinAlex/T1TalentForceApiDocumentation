# Анкета кандидата

# Работа с анкетой кандидата из Jira

1.  [Получение списка вопросов](#get_quest_list)
2.  [Передача анкеты кандидата](#post_quest_data)
3.  [Получение информации по анкете](#get_quest_info)
4.  [Добавление комментария к анкете](#post_comment_to_tf)
5.  [Получение комментария](#get_comment_to_tf)
6.  [Загрузка файлов](#upload_file)
7.  [Изменение статуса анкеты](#change_status_to_tf)
8.  [Возможные ошибки](#errors)

* Базовый URL для запросов: `/index.php?entryPoint=JiraQuestionnaireEntrypoint`

<a name="get_quest_list"></a>
## Получение списка вопросов


GET
```json
{
    "token": "{{token}}"
}
```

200 OK

```json
{
    "ef43cf5d-8b23-df98-4e5b-641add028e00": {
        "question_id": "ef43cf5d-8b23-df98-4e5b-641add028e00",
        "question_name": "Гражданином какой страны Вы являетесь?",
        "answer_type": "line_answer",
        "question_type": "base",
        "answer_options": [],
        "display_condition": "4ee072c1-5ee1-1c98-493e-641add0e1a99",
        "parent_question": "",
        "sort": "0"
    },
    "853f064d-4de8-562a-fa10-609272ce227d": {
        "question_id": "853f064d-4de8-562a-fa10-609272ce227d",
        "question_name": "Дата рождения",
        "answer_type": "date_answer",
        "question_type": "base",
        "answer_options": [],
        "display_condition": "",
        "parent_question": "",
        "sort": "2"
    }
}
```


<a name="post_quest_data"></a>
## Передача анкеты кандидата

POST

```json
{
    "token": "{{token}}",

    "external_jira_id": "Номер JIRA",

    "lkk_candidate_questionnaire": {
        "date_entered": "2021-06-22 08:46:00",
        "id": "Номер JIRA",
        "layout_form": "main_job",
        "responsible_hr_email": "test@mail.ru",
        "responsible_hr_name": "ФИО Ответственного HR",
        "vacancy_name": "Название вакансии",
        "verification_stage": "pending_verification",
        "project": "Название проекта",
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
      }
    ]
  ]
}

```

#### Список полей и значений анкеты
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

Поле | Описание 
-----| -------- 
lkk_questionnaires_questions | <a href="lkk_additional.md">Инструкция передачи ответов по анкете</a>


CREATED 201

```json
{
    "status": "OK",
    "record_id": "e3e16a3f-caf6-9b4c-2f29-61702a74a03d"
}
```

<a name="get_quest_info"></a>
## Получение информации по анкете

GET

```json
{
    "token": "{{t1basetoken}}",

    "external_jira_id" : ["номер задачи в Jira"]
}
```

OK 200

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

<a name="post_comment_to_tf"></a>
## Добавление комментария к анкете

POST

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

#### Список полей и значений комментария

Поле | Описание | Обязательность
-----| -------- | --------------
external_jira_id | ID заявки (внешний ID), по которому можно будет идентифицировать заявку на проверку анкеты для СБ | Да
parent_id | ID анкеты кандидата из TF T1, если есть | Да
parent_type | Для всех комментариев значение указать LKK_CANDIDATE_QUESTIONNAIRE  | Да
id| ID комментария | Да
date_entered | Дата создания комментария. Формат данных: гггг-мм-чч чч:мм:сс | Да
text | Текст комментария | Да
created_by_name | ФИО пользователя, который оставил комментарий | Да

200 OK

```json
{
    "status": "OK",
    "record_id": "145344af-dceb-d563-0528-61702a12f345"
}
```

<a name="get_comment_to_tf"></a>
## Получение комментария

GET

```json
{
    "token": "{{t1basetoken}}",

    "comment_id": "идентификатор комментария"
}
```

200 OK

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
## Загрузка бинарных файлов

Базовый URL для загрузки файлов ОТЛИЧАЕТСЯ от основного

URL: ```/index.php?entryPoint=JiraQuestionnaireFileUpload```

POST (form-data) передать:

```
token = token
external_jira_id = НомерJIRA
file[] = multipart бинарные данные файла
```

200 OK

```json
{
    "records": {
        "имя_файла.расширение": "1c7cc2a1-bcdb-578b-29d2-61703006ab93"
    },
    "errors": []
}
```

<a name="change_statusto_tf"></a>
## Изменение статуса анкеты

POST

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

200 OK

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
['status' => 'FAIL', 'error' => 'Stage transition restricted, try another transition']  |  При попытка перевести на этап СБ если такой переход запрещен
