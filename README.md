# Разработчик DWH (Открытая школа Т1)

## Сквозной проект №2
![Снимок экрана](https://github.com/user-attachments/assets/709c8a8f-58d7-4b23-af03-d782bb9f5b9b)

<details>
<summary>:large_blue_diamond::large_blue_diamond::large_blue_diamond: Задание 1 - 30.09 :large_blue_diamond::large_blue_diamond::large_blue_diamond:</summary>

<details>
<summary>Практическое задание</summary>

  ![Снимок экрана 2024-09-30 172943](https://github.com/user-attachments/assets/a4b25435-41e3-4a2e-abf7-af63afbfcc36)

  | Архитектурный подход | Плюсы                                             | Минусы                                           | Критерии для выбора                             |
|----------------------|--------------------------------------------------|-------------------------------------------------|-------------------------------------------------|
| **DWH** | - Высокая производительность запросов <br> - Структурированные данные <br> - Поддержка аналитики и отчетности | - Высокие затраты на хранение <br> - Длительная настройка <br> - Жесткие схемы | - Нужен централизованный доступ к структурированным данным <br> - Сложные аналитические запросы |
| **Data Lake**        | - Гибкость в хранении как структурированных, так и неструктурированных данных <br> - Низкая стоимость хранения | - Управление качеством данных сложно <br> - Потенциальные проблемы с безопасностью <br> - Меньше оптимизации для аналитики | - Большие объемы неструктурированных данных <br> - Необходимость в быстром доступе к данным |
| **Lake House**       | - Комбинация подходов Data Lake и DWH <br> - Поддержка как аналитических, так и транзакционных запросов <br> - Упрощенное управление данными | - Сложность в реализации <br> - Высокие требования к ресурсам | - Нужен баланс между структурированными и неструктурированными данными <br> - Необходимость в гибком хранилище |
| **Data Mesh**        | - Децентрализация данных <br> - Командная ответственность за данные <br> - Легче интегрировать с микросервисной архитектурой | - Требует изменения культуры работы с данными <br> - Сложность в обеспечении согласованности данных | - Необходимость гибкости и быстрой адаптации <br> - Уровень зрелости команды и инфраструктуры |

</details>

<details>
<summary>Сквозное задание</summary>

![Снимок экрана](https://github.com/user-attachments/assets/94cd1d31-e909-44d7-8a00-579a4081fe6b)

## Тип хранилища
Поскольку необходимо реализовать локальное хранилище для аналитических и балансовых счетов, которое будет обновляться несколько раз в день, оптимальным выбором является операционное хранилище данных (ODS). Оно позволяет интегрировать данные из разных источников и обрабатывать их в реальном времени, что соответствует требованиям по частому обновлению информации.
## Количество слоев
Для данной задачи подойдет архитектура с тремя слоями:

- Первый слой (Staging/Storage Layer): Здесь данные собираются, обрабатываются и нормализуются. Это служит для глубокого анализа и долгосрочного хранения.
- Второй слой (Presentation Layer): На этом уровне создаются бизнес-витрины данных с агрегированными показателями для пользователей.

Такое разделение слоев позволяет эффективно управлять, хранить и предоставлять доступ к данным, соответствуя современным требованиям к организациям хранилищ данных. 
</details>
</details>

<details>
<summary>:large_blue_diamond::large_blue_diamond::large_blue_diamond: Задание 2 - 03.10 :large_blue_diamond::large_blue_diamond::large_blue_diamond:</summary>

  <details>
<summary>Практическое задание</summary>

![image](https://github.com/user-attachments/assets/feb7213e-038f-4eda-999a-c9b296817b59)

### Таблицы в схеме arenadata_toolkit

| Наименование          | Содержание                                                                                                          | Применение                                                  |
|-----------------------|---------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------|
| `daily_operation`     | Информация об автоматических операциях VACUUM и ANALYZE, проводимых над таблицами базы данных по расписанию  | Анализ и оптимизация процесса хранения данных, обеспечивая регулярное обслуживание таблиц |
| `db_files_current`    | Текущая информация о файлах базы данных на всех сегментах кластера, связываемая с таблицами, индексами и другими объектами базы данных, актуальная на момент последнего запуска скрипта collect_table_stats | Помогает в мониторинге и отладке системы, предоставляя актуальные данные о файловой структуре БД  |
| `db_files_history`    | Хранит историю изменений файлов БД на всех сегментах кластера с привязкой к таблицам, индексам и другим объектам БД (при возможности определения таких связей) |  Наблюдение за изменением использования дискового пространства во времени, что важно для анализа роста и распределения данных   |
| `operation_exclude`   | Информация о схемах базы данных, к которым не применяются операции VACUUM и ANALYZE при запуске соответствующих скриптов | Управление и мониторинг использования ресурсов, позволяя исключать ненужные операции для определённых схем |


### Представлений в arenadata_toolkit не найдено!!!

### Представления в схеме gp_toolkit

| Наименование                             | Содержимое                                                             | Применение                                                  |
|------------------------------------------|------------------------------------------------------------------------|-------------------------------------------------------------|
| `_gp_fullname`                           | Полные имена объектов базы данных                                      | Используется для ссылки на объекты с полными именами        |
| `_gp_is_append_only`                     | Проверка, является ли таблица дополнением только                       | Для оптимизации вставки данных                              |
| `_gp_number_of_segments`                 | Сегментарная информация таблиц                                         | Для анализа распределения данных                            |
| `_gp_user_data_tables`                   | Информация о пользовательских таблицах                                 | Управление и учет пользовательских данных                   |
| `_gp_user_data_tables_readable`          | Читаемые пользовательские таблицы                                      | Для анализа читаемых таблиц                                 |
| `_gp_user_namespaces`                    | Пространства имен пользователей                                        | Для управления пространствами имен                          |
| `_gp_user_tables`                        | Таблицы пользователей                                                  | Учет пользовательских таблиц                                |
| `gp_bloat_diag`                          | Диагностика раздувания таблиц                                          | Анализ и оптимизация хранения данных                        |
| `gp_bloat_expected_pages`                | Ожидаемые страницы раздувания                                          | Для выявления возможного раздувания                         |
| `gp_locks_on_relation`                   | Блокировки на отношениях                                               | Управление блокировками и конкурентным доступом             |
| `gp_locks_on_resqueue`                   | Блокировки на очередях ресурсов                                        | Мониторинг использования ресурсов                           |
| `gp_log_command_timings`                 | Временные метки выполнения команд                                      | Анализ производительности команд                            |
| `gp_log_database`                        | Логи базы данных                                                       | Общий мониторинг и отладка системы                          |
| `gp_log_master_concise`                  | Краткие логи от мастера                                                | Быстрая диагностика проблем                                 |
| `gp_log_system`                          | Системные логи                                                         | Помогает в отладке и мониторинге системы                    |
| `gp_param_settings_seg_value_diffs`      | Различия в параметрах сегментов                                        | Анализ конфигурации сегментов                               |
| `gp_pgdatabase_invalid`                  | Неверные записи в базе данных                                          | Обнаружение и исправление аномалий                          |
| `gp_resgroup_config`                     | Конфигурация групп ресурсов                                            | Управление ресурсными группами                              |
| `gp_resgroup_status`                     | Статус групп ресурсов                                                  | Мониторинг использования ресурсов                           |
| `gp_resgroup_status_per_host`            | Статус групп ресурсов по хостам                                        | Детальный мониторинг по хостам                              |
| `gp_resgroup_status_per_segment`         | Статус групп ресурсов по сегментам                                     | Детальный мониторинг по сегментам                           |
| `gp_resq_activity`                       | Активность очередей ресурсов                                           | Управление и мониторинг использования ресурсов              |
| `gp_resq_activity_by_queue`              | Активность распределена по очередям                                    | Анализ различных очередей                                   |
| `gp_resq_priority_backend`               | Приоритеты бекенда                                                     | Оптимизация использования бекенд ресурсов                   |
| `gp_resq_priority_statement`             | Приоритеты заявлений                                                   | Оптимизация выполнения заявлений                            |
| `gp_role`                                | Информация о ролях                                                     | Управление и контроль доступа                               |
| `gp_resqueue_status`                     | Статус очередей ресурсов                                               | Мониторинг и оптимизация использования ресурсов             |
| `gp_roles_assigned`                      | Назначенные роли в системе                                             | Управление и контроль ролей пользователей                   |
| `gp_size_of_all_table_indexes`           | Общий размер индексов всех таблиц                                      | Анализ потребления пространства индексами                   |
| `gp_size_of_database`                    | Размер базы данных                                                     | Наблюдение за использованием дискового пространства         |
| `gp_size_of_index`                       | Размер конкретного индекса                                             | Оптимизация дизайна индексов                                |
| `gp_size_of_partition_and_indexes_disk`  | Размер разделов и индексов на диске                                    | Управление дисковым пространством                           |
| `gp_size_of_schema_disk`                 | Размер схем на диске                                                   | Оптимизация использования схем                              |
| `gp_size_of_table_and_indexes_disk`      | Размер таблиц и их индексов на диске                                   | Полный учет потребления пространства                        |
| `gp_size_of_table_and_indexes_licensing` | Лицензионная информация о размере таблиц и индексов                    | Анализ соответствия лицензии использования ресурсов         |
| `gp_size_of_table_disk`                  | Размер таблицы на диске                                                | Оптимизация хранения данных                                 |
| `gp_size_of_table_uncompressed`          | Неражатый размер таблицы                                               | Анализ эффективности сжатия данных                          |
| `gp_skew_coefficients`                   | Коэффициенты неравномерности распределения данных                      | Анализ и оптимизация распределения данных на сегментах      |
| `gp_skew_idle_fractions`                 | Пропорции простаивания при несбалансированности                        | Оптимизация производительности                              |
| `gp_stats_missing`                       | Отсутствующие статистические данные                                    | Выявление и исправление статистических аномалий             |
| `gp_table_indexes`                       | Индексы таблиц                                                         | Управление и оптимизация индексов                           |
| `gp_workfile_entries`                    | Записи рабочих файлов                                                  | Управление временными файлами в процессе выполнения запросов|
| `gp_workfile_mgr_used_diskspace`         | Использование дискового пространства менеджером рабочих файлов         | Контроль за временным дисковым пространством                |
| `gp_workfile_usage_per_query`            | Использование рабочих файлов по запросам                               | Анализ потребления ресурсов заданными запросами             |
| `gp_workfile_usage_per_segment`          | Использование рабочих файлов по сегментам                              | Детальный мониторинг использования рабочих файлов           |

  </details>
</details>

<details>
<summary>:large_blue_diamond::large_blue_diamond::large_blue_diamond: Задание 3 - 08.10 :large_blue_diamond::large_blue_diamond::large_blue_diamond:</summary>

  <details>
<summary>Практическое задание R3.1</summary>

![image](https://github.com/user-attachments/assets/53e12351-4371-4895-9d76-6e56a46e30bc)


  
  </details>
    <details>
<summary>Практическое задание R3.2</summary>

![image](https://github.com/user-attachments/assets/ce8b3331-cc9c-4873-9469-fed3b715e53c)

| Индекс        | Назначение                                                                                     | Работа                                                                                      | Особенности                                                                                  |
|---------------|------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------|
| **B-tree**    | Универсальный индекс для большинства типов данных и операций                                   | Быстрая сортировка и поиск благодаря структуре, напоминающей бинарное дерево               | - Автоматически создается для уникальных и первичных ключей;<br> - хорош для диапазонных запросов    |
| **Hash**      | Оптимизирован для операций равенства                                                           | Использует хеш-таблицы для быстрого доступа по ключу                                       | - Не поддерживает уникальные индексы;<br> - рекомендуется для равенства;<br> - поддерживает WAL            |
| **GiST**      | Индексация данных, где порядок и сравнение не являются основными                               | Позволяет использовать специализированные операторы                                        | - Поддерживает различные операции;<br> - отлично подходит для полнотекстового поиска                 |
| **GIN**       | Оптимизирован для сложных структур, таких как массивы или JSONB                                | Поддерживает множество значений в одном поле                                               | - Подходит для быстрого поиска присутствия элементов;<br> - требует много памяти                     |
| **SP-GiST**   | Эффективен для данных с высокой степенью разреженности                                         | Разделяет пространство данных на части                                                    | - Поддерживает нестандартные типы данных;<br> - эффективен в многоуровневых иерархиях                |
| **BRIN**     | Оптимизирован для работы с большими таблицами, где данные имеют физическую корреляцию | Индексирует блоки данных вместо отдельных строк                         | - Экономит память; Идеально подходит для работы с большими, но неоднородными данными на диске                                                                       |
| **RUM**      | Является расширением GIN индексов с дополнительной поддержкой ранжирования и полнотекстового поиска | Расширенные возможности полнотекстового поиска и сортировки | - Расширенный функционал для ранжирования; поддержка полнотекстового поиска с ранжированием; использует больше ресурсов по сравнению с классическим GIN индексом      |
| **Bitmap (Уникальный для GreenPlum)**    | Обработка больших наборов данных для аналитических запросов         | Использует битовые массивы для отслеживания значений                                       | - Эффективен для `OR` условий;<br> - позволяет операции над множествами (объединение, пересечение)   |

  </details>
    <details>
<summary>Сквозное задание S3.1</summary>

![image](https://github.com/user-attachments/assets/e4d95891-1f98-491f-8300-0f0d6f53dc53)

```mermaid
erDiagram
    ORGANIZATIONS {
        serial4 organization_id PK
        varchar name
        varchar registration_number
        varchar address
        varchar contact_info
        timestamp created_at
        timestamp updated_at
    }

    ANALYTIC_ACCOUNTS {
        varchar analytic_account_number PK
        int4 organization_id FK
        varchar synthetic_account_number
        numeric balance
        timestamp created_at
        timestamp updated_at
    }

    SYNTHETIC_ACCOUNTS {
        varchar synthetic_account_number PK
        varchar description
        varchar account_type
        timestamp created_at
        timestamp updated_at
    }

    TRANSACTIONS {
        bigserial transaction_id PK
        varchar analytic_account_number FK
        numeric amount
        timestamp transaction_date
        varchar transaction_type
        varchar description
        timestamp created_at
        timestamp updated_at
    }

    ORGANIZATIONS ||--o{ ANALYTIC_ACCOUNTS : "maintains"
    ANALYTIC_ACCOUNTS ||--o{ TRANSACTIONS : "records"
    SYNTHETIC_ACCOUNTS ||--|{ ANALYTIC_ACCOUNTS : "links"
```

Проектирование на основе 1-2 НФ по Кимбаллу:
- Staging Layer: Все таблицы остаются в более "сырых" и первичных формах. Это позволяет собирать данные для дальнейшей обработки и нормализации.
- Presentation Layer: Упор на аналитику. Каждый факт и измерение должно быть чётко выделено.

Объяснение структуры:
- Организации (organizations): Является справочником, содержащим уникальные идентификаторы и информацию о каждой организации.
- Аналитические счета (analityc_accounts): Содержат информацию о счетах, включая внешние ключи для связи с организациями.
- Синтетические счета (synthetic_accounts): Может быть связано с транзакциями для внутреннего учета и контроля.
- Транзакции (transactions): Хранят данные о каждой финансовой операции, связываясь с аналитическими счетами.
  
  </details>
</details>

<details>
<summary>:large_blue_diamond::large_blue_diamond::large_blue_diamond: Задание 4 - 10.10 :large_blue_diamond::large_blue_diamond::large_blue_diamond:</summary>

  <details>
<summary>Практическое задание R4.1</summary>

![image](https://github.com/user-attachments/assets/8b5bea6b-bf1d-4800-81e9-4a4720755439)
  
  </details>
</details>

<details>
<summary>:large_blue_diamond::large_blue_diamond::large_blue_diamond: Задание 5 - 15.10 :large_blue_diamond::large_blue_diamond::large_blue_diamond:</summary>

<details>
<summary>Практическое задание R5.1</summary>

![image](https://github.com/user-attachments/assets/9d560861-18eb-4d0a-91cf-f5f15aa3cfd9)

  
  </details>
<details>
<summary>Сквозное задание S5.1</summary>

![image](https://github.com/user-attachments/assets/c610737a-b262-4d20-8fdb-997c1c4d6ff9)

  
  </details>
  <details>
<summary>Сквозное задание S5.2</summary>

![image](https://github.com/user-attachments/assets/3bcdf57b-c062-4d27-bf69-93f2f4e4dd0d)

  
  </details>
  
</details>

<details>
<summary>:large_blue_diamond::large_blue_diamond::large_blue_diamond: Задание 6 - 22.10 :large_blue_diamond::large_blue_diamond::large_blue_diamond:</summary>

</details>
