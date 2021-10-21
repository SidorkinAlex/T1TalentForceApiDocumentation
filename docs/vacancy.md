# Вакансии

Используется стандартное [API Suite CRM](https://docs.suitecrm.com/developer/api/developer-setup-guide/)
1.  [Получение списка наименований вакансий](#get_vacancy_names)
2.  [Создание наименования вакансии](#create_vacancy_name)
3.  [Получение user ID из user_name](#get_user_id)
4.  [Создание вакансии](#create_vacancy)

<a name="get_vacancy_names"></a>
## Получение списка наименований вакансий

Предварительно необходимо [зарегистрировать](https://talentforce.ru/) приложение.

Добавить в запрос полученный при авторизации access_token

* **Запрос**

Необходимо отправить GET-запрос на:

`{{talentforce.url}}/Api/V8/module/HRPAC_VACANCY_NAMES`

В *параметрах* передать: 

`fields[HRPAC_VACANCY_NAMES] : name`

* **Пример ответа**

Статус 200

```json
{
    "data": [
        {
            "type": "HRPAC_VACANCY_NAMES",
            "id": "104204e0-5bfc-1461-854c-6152bdf1beed",
            "attributes": {
                "name": "Директор по техническому развитию и архитектуре"
            },
            "relationships": {
                "HRPAC_DATA_COLLECTION_MODULE": {
                    "links": {
                        "related": "V8/module/HRPAC_VACANCY_NAMES/104204e0-5bfc-1461-854c-6152bdf1beed/relationships/hrpac_data_collection_module"
                    }
                },
                "SecurityGroups": {
                    "links": {
                        "related": "V8/module/HRPAC_VACANCY_NAMES/104204e0-5bfc-1461-854c-6152bdf1beed/relationships/SecurityGroups"
                    }
                },
                "Users": {
                    "links": {
                        "related": "V8/module/HRPAC_VACANCY_NAMES/104204e0-5bfc-1461-854c-6152bdf1beed/relationships/created_by_link"
                    }
                }
            }
        }
    ]
}
```
<a name="create_vacancy_name"></a>
## Создание наименования вакансии

* **Запрос**

Необходимо отправить POST-запрос на:

`{{talentforce.url}}/Api/V8/module`

В *Body* передать:

```json
{
  "data": {
    "type": "HRPAC_VACANCY_NAMES",
    "attributes": {
      "name": "Новое наименование вакансии"
    }
  }
}
```

* **Пример ответа**

Статус 201

```json
{
    "data": {
        "type": "HRPAC_VACANCY_NAMES",
        "id": "a080274c-a468-74a8-eaf9-617009861f74",
        "attributes": {
            "name": "Новое наименование вакансии",
            "date_entered": "2021-10-20T12:20:00+03:00",
            "date_modified": "2021-10-20T12:20:00+03:00",
            "modified_user_id": "bfe26119-a246-fccd-62da-6113c9557a9b",
            "modified_by_name": "Username",
            "created_by": "bfe26119-a246-fccd-62da-6113c9557a9b",
            "created_by_name": "Username",
            "description": "",
            "deleted": "0",
            "save_trigger": "",
            "created_by_link": "",
            "modified_user_link": "",
            "assigned_user_id": "",
            "assigned_user_name": "",
            "assigned_user_link": "",
            "SecurityGroups": "",
            "hrpac_data_collection_module": ""
        },
        "relationships": {
            "HRPAC_DATA_COLLECTION_MODULE": {
                "links": {
                    "related": "V8/module/a080274c-a468-74a8-eaf9-617009861f74/relationships/hrpac_data_collection_module"
                }
            },
            "SecurityGroups": {
                "links": {
                    "related": "V8/module/a080274c-a468-74a8-eaf9-617009861f74/relationships/SecurityGroups"
                }
            },
            "Users": {
                "links": {
                    "related": "V8/module/a080274c-a468-74a8-eaf9-617009861f74/relationships/created_by_link"
                }
            }
        }
    }
}
```
<a name="get_user_id"></a>
## Получение user ID из user_name

* **Запрос**

Необходимо отправить GET-запрос на:

`{{talentforce.url}}/Api/V8/module/Users`

В *параметрах* передать: 

```
fields[HRPAC_VACANCY_NAMES] : id
filter[user_name][eq] : {{user_name}}
```

* **Пример ответа**

Статус 200

```json
{
    "data": [
        {
            "type": "User",
            "id": "bfe26119-a246-fccd-62da-6113c9557a9b",
            "attributes": [],
            "relationships": {
                "ACLRoles": {
                    "links": {
                        "related": "V8/module/Users/bfe26119-a246-fccd-62da-6113c9557a9b/relationships/role_user_link"
                    }
                },
                "AM_ProjectTemplates": {
                    "links": {
                        "related": "V8/module/Users/bfe26119-a246-fccd-62da-6113c9557a9b/relationships/am_projecttemplates_users_1"
                    }
                },
                "AOR_Reports": {
                    "links": {
                        "related": "V8/module/Users/bfe26119-a246-fccd-62da-6113c9557a9b/relationships/aor_reports_users"
                    }
                },
                "EmailAddress": {
                    "links": {
                        "related": "V8/module/Users/bfe26119-a246-fccd-62da-6113c9557a9b/relationships/email_addresses"
                    }
                },
                "Emails": {
                    "links": {
                        "related": "V8/module/Users/bfe26119-a246-fccd-62da-6113c9557a9b/relationships/emails_users"
                    }
                },
                "HRPAC_DATA_COLLECTION_MODULE": {
                    "links": {
                        "related": "V8/module/Users/bfe26119-a246-fccd-62da-6113c9557a9b/relationships/hrpac_data_collection_module"
                    }
                },
                "HRPAC_VACANCY": {
                    "links": {
                        "related": "V8/module/Users/bfe26119-a246-fccd-62da-6113c9557a9b/relationships/hrpac_vacancy_users_additional_assigned"
                    }
                },
                "OAuthTokens": {
                    "links": {
                        "related": "V8/module/Users/bfe26119-a246-fccd-62da-6113c9557a9b/relationships/oauth_tokens"
                    }
                },
                "Project": {
                    "links": {
                        "related": "V8/module/Users/bfe26119-a246-fccd-62da-6113c9557a9b/relationships/project_users_1"
                    }
                },
                "ProspectLists": {
                    "links": {
                        "related": "V8/module/Users/bfe26119-a246-fccd-62da-6113c9557a9b/relationships/prospect_lists"
                    }
                },
                "SecurityGroups": {
                    "links": {
                        "related": "V8/module/Users/bfe26119-a246-fccd-62da-6113c9557a9b/relationships/SecurityGroups"
                    }
                }
            }
        }
    ]
}
```

<a name="create_vacancy"></a>
## Создание вакансии

* **Запрос**

Необходимо отправить POST-запрос на:

`{{talentforce.url}}/Api/V8/module`

В *Body* передать:

```json
{
  "data": {
    "type": "HRPAC_VACANCY",
    "attributes": {
      "hrpac_vacancy_names_id_c": "143e66e9-cf62-fdde-80f1-5de6663f2ee3",
      "assigned_user_id": "1e2603b9-f733-7a30-ac61-5e0613a3c7e7",
      "line_manager_id": "1e2603b9-f733-7a30-ac61-5e0613a3c7e7",
      "user_id_c": "1e2603b9-f733-7a30-ac61-5e0613a3c7e7",
      "amount": "5",
      "salary_max": "20000",
      "description": "Описание задач и обязанностей",
      "demands": "Описание должностных требований"
    }
  }
}
```

* **Пример ответа**

Статус 201

```json
{
    "data": {
        "type": "HRPAC_VACANCY",
        "id": "8c998ef1-65b9-c822-6ab7-61700bba91df",
        "attributes": {
            "name": "Функциональный архитектор",
            "date_entered": "2021-10-20T12:27:00+03:00",
            "date_modified": "2021-10-20T12:27:00+03:00",
            "modified_user_id": "bfe26119-a246-fccd-62da-6113c9557a9b",
            "modified_by_name": "Username",
            "created_by": "bfe26119-a246-fccd-62da-6113c9557a9b",
            "created_by_name": "Username",
            "description": "Описание задач и обязанностей",
            "deleted": "0",
            "save_trigger": "",
            "created_by_link": "",
            "modified_user_link": "",
            "assigned_user_id": "1e2603b9-f733-7a30-ac61-5e0613a3c7e7",
            "assigned_user_name": "",
            "assigned_user_link": "",
            "SecurityGroups": "",
            "hrpac_business_units_id_c": "",
            "business_unit_id": "",
            "hrpac_departments_id_c": "",
            "department_id": "",
            "project_id_c": "",
            "project_link_id": "",
            "project_description_id": "",
            "hrpac_cities_id_c": "77f28e78-fccb-ac0c-8759-5d7919a2be4e",
            "location_id": "Москва",
            "stage_templates_name": "",
            "stage_templates_id": "",
            "stage_templates_hrpac_vacancy_1": "",
            "user_id_c": "1e2603b9-f733-7a30-ac61-5e0613a3c7e7",
            "manager_id": "",
            "user_id1_c": "",
            "supervisor_id": "",
            "line_manager_name": "",
            "line_manager_id": "1e2603b9-f733-7a30-ac61-5e0613a3c7e7",
            "line_manager_link": "",
            "hrpac_vacancy_statuses_id_c": "f3580e7e-4732-b173-209d-5da47daa4009",
            "status_id": "Новая",
            "salary_min": "",
            "salary_max": "20000.000000",
            "currency_id": "-99",
            "amount": "5",
            "stack": "",
            "date_accept": "",
            "date_going": "",
            "hrpac_vacancy_names_id_c": "143e66e9-cf62-fdde-80f1-5de6663f2ee3",
            "name_id": "Функциональный архитектор",
            "other_name": "",
            "grade": "",
            "additional_managers_ids": "",
            "additional_assigned_ids": "",
            "spectators_ids": "",
            "reason_for_opening_id": "",
            "reason_for_opening": "",
            "progresbar": 0,
            "additional_managers": "",
            "spectators": "",
            "additional_assigned": "",
            "vacansy_url": "",
            "test_url": "",
            "amount_final": 5,
            "ssc": "",
            "stack_skills_ids": "",
            "desirable_skills_ids": "",
            "hrpac_vacancy_difficulty_level_id": "3e98ebbb-2c22-6882-4bd8-5f180f5312e3",
            "hrpac_vacancy_difficulty_level_name": "Базовая",
            "hrpac_vacancy_template_id": "",
            "hrpac_vacancy_template_name": "",
            "office_job": "0",
            "office_adress": "",
            "remote_job": "0",
            "job_experience_from": "",
            "job_experience_to": "",
            "bonuses": "0",
            "frequency": "",
            "external_customer": "0",
            "demands": "Описание должностных требований",
            "external_customer_contact": "",
            "technical_experts_ids": "",
            "hrpac_vacancy_users_technical_experts": "",
            "technical_experts": "",
            "job_experience_group": "",
            "salary_group": "",
            "customer_group": "",
            "comments": "",
            "hrpac_skills_hrpac_vacancy": "",
            "hrpac_stack_skills_hrpac_vacancy": "",
            "hrpac_desirable_skills_hrpac_vacancy": "",
            "hrpac_vacancy_documents_1": "",
            "hrpac_vacancy_hrpac_candidates_1": "",
            "hrpac_vacancy_name_us": "",
            "hrpac_vacancy_business_units_us": "",
            "hrpac_vacancy_departments_us": "",
            "hrpac_vacancy_projects_us": "",
            "hrpac_vacancy_supervisor_us": "",
            "date_status_modified": "2021-10-20T00:00:00+03:00",
            "direction_section": "",
            "hrpac_vacancy_users_additional_assigned": "",
            "hrpac_vacancy_users_additional_managers": "",
            "hrpac_vacancy_users_spectator": "",
            "hrpac_vacancy_hrpac_new_eployee_exit": "",
            "hrpac_data_collection_module": "",
            "hrpac_vacancy_user_name": "",
            "employment_contract_type": "",
            "term_contract": "",
            "business_trips": "",
            "jira_vacancy_id": ""
        },
        "relationships": {
            "Documents": {
                "links": {
                    "related": "V8/module/8c998ef1-65b9-c822-6ab7-61700bba91df/relationships/hrpac_vacancy_documents_1"
                }
            },
            "HRPAC_CANDIDATES": {
                "links": {
                    "related": "V8/module/8c998ef1-65b9-c822-6ab7-61700bba91df/relationships/hrpac_vacancy_hrpac_candidates_1"
                }
            },
            "HRPAC_COMMENTS": {
                "links": {
                    "related": "V8/module/8c998ef1-65b9-c822-6ab7-61700bba91df/relationships/comments"
                }
            },
            "HRPAC_DATA_COLLECTION_MODULE": {
                "links": {
                    "related": "V8/module/8c998ef1-65b9-c822-6ab7-61700bba91df/relationships/hrpac_data_collection_module"
                }
            },
            "HRPAC_NEW_EPLOYEE_EXIT": {
                "links": {
                    "related": "V8/module/8c998ef1-65b9-c822-6ab7-61700bba91df/relationships/hrpac_vacancy_hrpac_new_eployee_exit"
                }
            },
            "HRPAC_SELECTION_STAGE_CANDIDATES_1": {
                "links": {
                    "related": "V8/module/8c998ef1-65b9-c822-6ab7-61700bba91df/relationships/ssc"
                }
            },
            "HRPAC_SKILLS": {
                "links": {
                    "related": "V8/module/8c998ef1-65b9-c822-6ab7-61700bba91df/relationships/hrpac_desirable_skills_hrpac_vacancy"
                }
            },
            "STAGE_Templates": {
                "links": {
                    "related": "V8/module/8c998ef1-65b9-c822-6ab7-61700bba91df/relationships/stage_templates_hrpac_vacancy_1"
                }
            },
            "SecurityGroups": {
                "links": {
                    "related": "V8/module/8c998ef1-65b9-c822-6ab7-61700bba91df/relationships/SecurityGroups"
                }
            },
            "Users": {
                "links": {
                    "related": "V8/module/8c998ef1-65b9-c822-6ab7-61700bba91df/relationships/modified_user_link"
                }
            }
        }
    }
}
```
