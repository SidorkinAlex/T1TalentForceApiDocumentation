# Анкета кандидата

1.  [Работа с анкетой кандидата из Jira](#from_jira_to_tf)
2.  [Работа с анкетой кандидата из TalentForce](#from_tf_to_jira)

<a name="from_jira_to_tf"></a>
# Работа с анкетой кандидата из Jira

Предварительно необходимо [получить токен](https://talentforce.ru/) приложения

1.  [Получение списка вопросов](#get_quest_list)
2.  [Передача анкеты кандидата](#post_quest_data)
3.  [Получение информации по анкете](#get_quest_info)
4.  [Добавление комментария к анкете](#post_comment_to_tf)
5.  [Получение комментария](#get_comment_to_tf)
6.  [Загрузка файлов](#upload_file)
7.  [Изменение статуса анкеты](#change_status_to_tf)
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
#### Список полей и значений вопросов

ID | Вопрос | Тип вопроса | Тип ответа | Обязательность
------| ------- | ----------- | ---------- | --------------
3c156877-c8ea-0ec6-65ee-60f933946efa | Для граждан РФ: паспорт (первая страница и регистрация). Для граждан других стран: паспорт (первая страница) и документ, подтверждающий пребывание на территории РФ (2 стороны) | base |file_answer
1058d835-f4b2-dcaf-e452-609278bd9ecb | E-mail | base | line_answer
10864ab4-1b3e-41b2-ff58-60cb1bf76c43 | Улица | base | line_answer
15bfc15a-b669-2843-ab43-609278cf157b | Являетесь ли Вы руководителем или учредителем какой-либо коммерческой структуры? | group | option_answer
165585ec-54ee-3585-611f-60a78fb96a57 | Отчество | base | line_answer
17c8bfc9-898b-5d1e-47c1-609277c2d0d8 | Улица | base | line_answer
2290432b-2b5c-41f4-cb2f-60cb246fb761 | Страна | base | line_answer
296c5787-b8d7-0619-483d-60cb2458f1fb | Были ли Вы за границей? | group | option_answer
2995b5eb-711c-5c2c-917b-6092747a9abc | Когда и по какой причине Вы меняли гражданство? | base | line_answer
2b994945-a839-2970-0224-60cb1abad29d | Дом | base | line_answer
2ef843d1-3b50-8329-5b6b-609272f09009 | Укажите Вашу прежнюю фамилию / фамилии и причину изменения | base | text_answer
2f8707a3-c25a-2dc9-5487-60927c680360 | Были ли Ваши близкие родственники судимы? | group | option_answer
321b28b0-8c00-5e34-6832-60b8af511c91 | Знание языков | multigroup | line_answer
34b9b728-22e8-66e7-d4e7-60cb29c77703 | Район | base | line_answer
34dd521f-c22c-d4b9-cca4-60927c688a34 | Кто, когда и за что? | base | line_answer
3679b185-76d9-a42b-8650-60e430d36d3a | Укажите ИНН организации | base | line_answer
37d4d306-5484-026c-76dd-609273b7213d | Ваше гражданство | group | option_answer
3cbbe6da-8e6e-b46e-6ed3-60a78cbbc9ed | Имя | base | line_answer
3ec96279-45f9-7fa5-8f2b-60a78ee39617 | Фамилия | base | line_answer
3f236faa-2c85-c5a3-69b8-60cb25d82382 | Цель поездки | base | text_answer
449b4cc3-6245-3223-2fe1-60cb1b5d5e7f | Квартира | base | line_answer
4a6b3fd5-eb81-72db-c41b-6092788a2bfd | СНИЛС | base | line_answer
5474da19-2ac5-4dcf-3685-609273f3fc86 | Вы когда-нибудь меняли гражданство? | group | option_answer
59cfd2d8-8609-141c-1809-609279a25d2f | Номер и серия | base | line_answer
5e5f924e-6921-310d-c30b-60927a329ac4 | Дата выдачи | base | date_answer
62135304-98db-a525-d94d-6090ea6b688c | ФИО | group | line_answer
62629a04-3991-616b-6934-60cb1ce83786 | Мобильный номер телефона | base | line_answer
6653e032-6acb-ac81-077a-60cb1c5d3237 | Дополнительный номер телефона для связи | base | line_answer
6c0d0e8c-aee6-b3ab-b122-60cb1b16fd27 | Дом | base | line_answer
6eb749f2-ca8e-641f-e620-60cb1c65bf83 | Контакты | group | line_answer
7473c2d0-6f6a-653c-bfa8-609274592ce1 | Место выдачи | base | line_answer
7b9015ff-86e1-63ff-24fe-60dd61f2a2e3 | Расскажите о Ваших туристических поездках за последний год и/или перечислите Ваши места учебы / работы за границей в течение последних 5 лет | multigroup | line_answer
7e629f89-2bc1-6ac6-4f65-60cb19d8dc49 | Город/Поселок/Село | base | line_answer
8070efcb-1b12-0797-6fcb-609277e7f3e4 | Квартира | base | line_answer
80866f2d-021e-77ae-dad2-609273d74f74 | Место рождения (как в паспорте) | base | line_answer
83947d1b-3763-26d6-657c-60cb1b2843d5 | Район | base | line_answer
8489f88d-445b-1e5a-9324-60927cfe1fd4 | Когда и за что? | base | line_answer
8512d908-82f5-f691-50cd-609273365c15 | Гражданином какой страны Вы являетесь? | base | line_answer
853f064d-4de8-562a-fa10-609272ce227d | Дата рождения | base | date_answer
8890267b-e768-139f-e67a-6092793d7f18 | Расскажите подробнее, где и кем | base | line_answer
8942ba82-6e28-9d49-a18d-60cb1b6f84cd | Регион | base | line_answer
8987652f-13dc-101c-d43d-60cb1bfaad05 | Город/Поселок/Село | base | line_answer
8bc9b5f0-0f22-5dcf-4551-60cb199d7698 | Регион | base | line_answer
8de1401d-edaa-30d9-5aae-60927ad15d3c | Ваше отношение к воинской обязанности и воинское звание (при наличии) | base | line_answer
8e848ea1-187c-2fa3-f0fd-60927b36ec05 | Какой иностранный язык Вы знаете? | base | line_answer
90ff1d70-b23e-d53c-e8f1-609279a2df4d | У Вас есть заграничный паспорт? | group | option_answer
99bf5ae4-5e1d-3019-22ab-609276f029a4 | Адрес фактического проживания совпадает с адресом регистрации? | group | option_answer
a0e116e7-1392-0a99-f924-609274f8209a | Серия и номер паспорта | base | line_answer
aaf59d9f-119c-777f-d46e-60cb25679ce1 | Начало периода | base | date_answer
b4e5c8bb-80ba-797e-f28f-60927cfb5b28 | Были ли Вы судимы? | group | option_answer
b648d2a7-63a5-d84b-2777-60927a076150 | Место выдачи | base | line_answer
bf960a49-baca-1af8-3de9-60927580a4d0 | Адрес регистрации | group | line_answer
ca9c26af-29a3-6ab9-2eb5-609278f5a24d | ИНН | base | line_answer
cb648901-cc49-6273-6a32-60d97b1e6cb1 | Конец периода | base | date_answer
d5076c7c-22d4-bbc5-76ab-60927459fb4a | Дата выдачи | base | date_answer
e204bd59-bba0-0961-b44e-6092727c5906 | Вы когда-нибудь меняли фамилию? | group | option_answer
e94f03da-8eb9-6aaf-e506-60927b585137 | Ваш уровень владения | base | dropdown_answer
1a69f9de-2911-e2dd-5a25-60bf4d9a691c | Имя | base | line_answer
1ece7b1a-2746-5358-c3dc-60bfa96e8db7 | Занятость | group | option_answer
225704af-4c73-e508-620d-60cb40627112 | Мобильный номер телефона | base | line_answer
3b0b485b-63ec-0a77-86f2-60bf4d9e0739 | Отчество | base | line_answer
416bdace-076a-8068-a270-60cb4153331d | ФИО Родственника | group | line_answer
7aa7b351-45e3-3c69-5713-60bf4e1b3a9b | Дата рождения | base | date_answer
7fee790a-99b8-2923-73bd-60bfaeb0dcc1 | Название компании | base | line_answer
93099a8e-f72a-a86d-9e7f-60d98c871348 | Нет ближайших родственников | base | option_answer
97ad6e18-a386-030d-aee2-60bf4c788a66 | Фамилия | base | line_answer
ab0e0b83-6bde-e8dd-62dc-60bfae7ea640 | Должность | base | line_answer
ab23940f-4bd1-4346-e073-60bf4dcb099b | Родственник | multigroup | line_answer
b33f028d-4930-bcc4-6f30-60bf51f5aec4 | Адрес места жительства | base | line_answer
b3d1e42a-b44f-8cd7-6614-60d5d8196a76 | Укажите  прежнюю фамилию / фамилии и причину изменения | base | text_answer
c450c0f5-d583-5b0e-5929-60cb401744cc | Менял/ла когда-либо фамилию? | group | option_answer
de4f4996-cb8b-ce20-9931-60bfae10d3eb | Адрес организации | base | line_answer
e3fce453-5eaf-8f2a-e0c0-60bf4e5d8ead | Выберите тип родственной связи | group | dropdown_answer
ec5f774b-a5fc-3160-9aa4-60d5d8cc7b22 | Место рождения | base | line_answer
271bf4a4-e418-cc17-7975-60d5d51e4ecd | Название учебного заведения | base | text_answer
34ea5c07-72cf-c753-0b78-60bf45172b81 | Специальность по диплому | base | line_answer
397fe94d-bffe-3ec7-2566-60bf46e14571 | Есть ли у Вас дополнительное образование, документы о повышении квалификации? | group | option_answer
7e081f6e-68d5-2aa0-5cab-60bf3fb449be | Уровень образования | group | dropdown_answer
83d47271-f381-6536-5c67-60f7dd595345 | Учусь по настоящее время | base | option_answer
88a4e947-9d89-f739-9036-60bf3f529f03 | Информация об учебном заведении | multigroup | text_answer
96e4c0e9-5d98-f29f-e486-60bf4795d095 | Перечислите, пожалуйста | base | line_answer
98dc91aa-62e9-fd24-03bf-60bf445b78cd | Номер диплома | base | line_answer
e6b9186d-e07c-b449-ca90-60bf44495329 | Квалификация по диплому | base | line_answer
f0fad8ef-9e39-184c-47f1-60bf447d8f81 | Дата окончания | base | date_answer
1a231e47-e0a1-5745-20dd-60bf68159806 | Название компании | base | line_answer
29c92e48-4855-55bd-df8a-60cc40577407 | Адрес организации | base | line_answer
376a475d-ffe4-8a70-db7e-60cc40861042 | Замещали ли Вы должности государственной или муниципальной службы за последние 2 года? | group | option_answer
3a80434d-edf3-5bed-a4db-60f9516a2631 | По настоящее время | base | option_answer
43bfe933-bb10-a6ec-06f0-60cc426928fc | Основная работа | multigroup | line_answer
4683bde0-bcc8-95c3-941f-60bf6a1ff1a6 | Начало периода | base | date_answer
8941eb64-0553-6f23-ab70-60cc4100e571 | Конец периода | base | date_answer
90c4383d-806d-0bbb-f62a-60bf69d2b7cf | Должность | base | line_answer
99383f83-86e5-9f25-5d30-60cc40b62dbe | Должность | base | line_answer
a6f50be3-35a4-c40f-876e-60cc409c3543 | Государственная или муниципальная служба | multigroup | line_answer
c5498b29-9078-ada5-a913-60bf69e58d75 | Адрес организации | base | line_answer
cb1a842f-c97d-fb95-387b-60bf6a19d0e2 | Конец периода | base | date_answer
cf1e08ef-7dac-3b26-eb99-60cc4031682c | Название компании | base | line_answer
e81b11af-699b-ddf0-97b1-60cc4140834b | Начало периода | base | date_answer
e9d52b64-1131-f4a3-9b2c-60cb469d2261 | Т1 Консалтинг моё первое место работы | base | option_answer

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

* **Пример ответа**

Статус 201

```json
{
    "status": "OK",
    "record_id": "e3e16a3f-caf6-9b4c-2f29-61702a74a03d"
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

<a name="post_comment_to_tf"></a>
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

<a name="get_comment_to_tf"></a>
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
## Загрузка бинарных файлов

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

<a name="change_statusto_tf"></a>
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


<a name="from_jira_to_tf"></a>
# Работа с анкетой кандидата из TalentForce

2.  [Смена статуса](#change_statusto_tf)
1.  [Отправка комментария](#post_comment_to_jira)


<a name="change_statusto_tf"></a>
## Отправка комментария

*Раздел в работе*

#### Список полей и значений статуса

Поле | Описание | Обязательность
-----| -------- | --------------
external_jira_id | ID заявки (внешний ID), по которому можно будет идентифицировать заявку на проверку анкеты для СБ | Да
inspector_fio | ФИО ответственного сотрудника СБ | Да
verification_stage | Этап проверки СБ (Значение: on_clarifying => На уточнении, on_verifying => На проверке, poligraph => Полиграф, pre_approved => Предварительно согласован, 	final_inspection => На финальной проверке, agreed => Согласован, rejection => Отказ) | Да
parent_id | ID анкеты кандидата из CRM TF, если есть | Да
date_entered | Дата создания комментария. Формат данных: гггг-мм-чч чч:мм:сс | Да

<a name="post_comment_to_jira"></a>
## Отправка статуса

*Раздел в работе*

#### Список полей и значений комментария

Поле | Описание | Обязательность
-----| -------- | --------------
external_jira_id | ID заявки (внешний ID), по которому можно будет идентифицировать заявку на проверку анкеты для СБ | Да
parent_id | ID анкеты кандидата из CRM TF, если есть | Да
date_entered | Дата создания комментария. Формат данных: гггг-мм-чч чч:мм:сс | Да
created_by_name | ФИО пользователя, который оставил комментарий | Да
text | Текст комментария | Да
