# Разработчик DWH (Открытая школа Т1)

## Сквозной проект №2

![Снимок экрана](https://github.com/user-attachments/assets/709c8a8f-58d7-4b23-af03-d782bb9f5b9b)

<details>
<summary>✦✦✦ Задание 1 - 30.09 ✦✦✦</summary>

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

- Слой загрузки данных (Staging Layer): Здесь данные собираются из источников в неизменном виде. Это позволяет иметь чистый источник данных для дальнейшей обработки.
- Ядро хранилища (Storage Layer): В этом слое данные уже обработаны и нормализованы. Он служит для глубокого анализа и долгосрочного хранения данных.
-  Презентационный слой (Presentation Layer): На этом уровне создаются бизнес-витрины данных, которые предоставляют агрегированные показатели для пользователей. Это соответствует задаче создания витрин данных с агрегационными показателями.

Такое разделение слоев позволяет эффективно управлять, хранить и предоставлять доступ к данным, соответствуя современным требованиям к организациям хранилищ данных. 
</details>
</details>

<details>
<summary>✦✦✦ Задание 2 - 03.10 ✦✦✦</summary>

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
<summary><span style="color: blue;">Задание 3 - 08.10</span></summary>

![image](https://github.com/user-attachments/assets/a1c669b3-90b4-46ae-aef8-334c956e1174)

  
</details>
<details>
<summary> 3.2 - 08.10</summary>

![image](https://github.com/user-attachments/assets/a36e7c6b-1c42-48e5-a6e6-de54bf5c50e9)
  
</details>
<details>
<summary>4.1 - 10.10</summary>
  
![image](https://github.com/user-attachments/assets/7962d8bd-0cff-4963-b873-cba1d87f0482)


</details>

<details>
<summary>1 - 30.09</summary>
  
![Снимок экрана](https://github.com/user-attachments/assets/94cd1d31-e909-44d7-8a00-579a4081fe6b)

## Тип хранилища
Поскольку необходимо реализовать локальное хранилище для аналитических и балансовых счетов, которое будет обновляться несколько раз в день, оптимальным выбором является операционное хранилище данных (ODS). Оно позволяет интегрировать данные из разных источников и обрабатывать их в реальном времени, что соответствует требованиям по частому обновлению информации.
## Количество слоев
Для данной задачи подойдет архитектура с тремя слоями:

- Слой загрузки данных (Staging Layer): Здесь данные собираются из источников в неизменном виде. Это позволяет иметь чистый источник данных для дальнейшей обработки.
- Ядро хранилища (Storage Layer): В этом слое данные уже обработаны и нормализованы. Он служит для глубокого анализа и долгосрочного хранения данных.
-  Презентационный слой (Presentation Layer): На этом уровне создаются бизнес-витрины данных, которые предоставляют агрегированные показатели для пользователей. Это соответствует задаче создания витрин данных с агрегационными показателями.

Такое разделение слоев позволяет эффективно управлять, хранить и предоставлять доступ к данным, соответствуя современным требованиям к организациям хранилищ данных.
</details>
<details>
<summary>3.1 - 08.10</summary>
  
![image](https://github.com/user-attachments/assets/17c53824-7c06-4547-806b-9ec0bb568581)
