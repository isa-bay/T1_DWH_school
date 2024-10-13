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

<svg aria-roledescription="er" viewBox="0 0 494.17486572265625 488" xmlns="http://www.w3.org/2000/svg" width="100%" id="remark-mermaid-1728841455922" style="max-width: 494.175px;"><style>#remark-mermaid-1728841455922{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}#remark-mermaid-1728841455922 .error-icon{fill:#552222;}#remark-mermaid-1728841455922 .error-text{fill:#552222;stroke:#552222;}#remark-mermaid-1728841455922 .edge-thickness-normal{stroke-width:2px;}#remark-mermaid-1728841455922 .edge-thickness-thick{stroke-width:3.5px;}#remark-mermaid-1728841455922 .edge-pattern-solid{stroke-dasharray:0;}#remark-mermaid-1728841455922 .edge-pattern-dashed{stroke-dasharray:3;}#remark-mermaid-1728841455922 .edge-pattern-dotted{stroke-dasharray:2;}#remark-mermaid-1728841455922 .marker{fill:#333333;stroke:#333333;}#remark-mermaid-1728841455922 .marker.cross{stroke:#333333;}#remark-mermaid-1728841455922 svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#remark-mermaid-1728841455922 .entityBox{fill:#ECECFF;stroke:#9370DB;}#remark-mermaid-1728841455922 .attributeBoxOdd{fill:#ffffff;stroke:#9370DB;}#remark-mermaid-1728841455922 .attributeBoxEven{fill:#f2f2f2;stroke:#9370DB;}#remark-mermaid-1728841455922 .relationshipLabelBox{fill:hsl(80, 100%, 96.2745098039%);opacity:0.7;background-color:hsl(80, 100%, 96.2745098039%);}#remark-mermaid-1728841455922 .relationshipLabelBox rect{opacity:0.5;}#remark-mermaid-1728841455922 .relationshipLine{stroke:#333333;}#remark-mermaid-1728841455922 .entityTitleText{text-anchor:middle;font-size:18px;fill:#333;}#remark-mermaid-1728841455922 :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}</style><g></g><defs><marker orient="auto" markerHeight="18" markerWidth="18" refY="9" refX="0" id="ONLY_ONE_START"><path d="M9,0 L9,18 M15,0 L15,18" fill="none" stroke="gray"></path></marker></defs><defs><marker orient="auto" markerHeight="18" markerWidth="18" refY="9" refX="18" id="ONLY_ONE_END"><path d="M3,0 L3,18 M9,0 L9,18" fill="none" stroke="gray"></path></marker></defs><defs><marker orient="auto" markerHeight="18" markerWidth="30" refY="9" refX="0" id="ZERO_OR_ONE_START"><circle r="6" cy="9" cx="21" fill="white" stroke="gray"></circle><path d="M9,0 L9,18" fill="none" stroke="gray"></path></marker></defs><defs><marker orient="auto" markerHeight="18" markerWidth="30" refY="9" refX="30" id="ZERO_OR_ONE_END"><circle r="6" cy="9" cx="9" fill="white" stroke="gray"></circle><path d="M21,0 L21,18" fill="none" stroke="gray"></path></marker></defs><defs><marker orient="auto" markerHeight="36" markerWidth="45" refY="18" refX="18" id="ONE_OR_MORE_START"><path d="M0,18 Q 18,0 36,18 Q 18,36 0,18 M42,9 L42,27" fill="none" stroke="gray"></path></marker></defs><defs><marker orient="auto" markerHeight="36" markerWidth="45" refY="18" refX="27" id="ONE_OR_MORE_END"><path d="M3,9 L3,27 M9,18 Q27,0 45,18 Q27,36 9,18" fill="none" stroke="gray"></path></marker></defs><defs><marker orient="auto" markerHeight="36" markerWidth="57" refY="18" refX="18" id="ZERO_OR_MORE_START"><circle r="6" cy="18" cx="48" fill="white" stroke="gray"></circle><path d="M0,18 Q18,0 36,18 Q18,36 0,18" fill="none" stroke="gray"></path></marker></defs><defs><marker orient="auto" markerHeight="36" markerWidth="57" refY="18" refX="39" id="ZERO_OR_MORE_END"><circle r="6" cy="18" cx="9" fill="white" stroke="gray"></circle><path d="M21,18 Q39,0 57,18 Q39,36 21,18" fill="none" stroke="gray"></path></marker></defs><path marker-start="url(#ONLY_ONE_START)" marker-end="url(#ZERO_OR_MORE_END)" d="M113.263,88L113.263,96.333C113.263,104.667,113.263,121.333,113.263,138C113.263,154.667,113.263,171.333,113.263,179.667L113.263,188" class="er relationshipLine" style="stroke: gray; fill: none;"></path><path marker-start="url(#ONLY_ONE_START)" marker-end="url(#ZERO_OR_MORE_END)" d="M113.263,278L113.263,286.333C113.263,294.667,113.263,311.333,124.97,328C136.677,344.667,160.092,361.333,171.799,369.667L183.507,378" class="er relationshipLine" style="stroke: gray; fill: none;"></path><path marker-start="url(#ONLY_ONE_START)" marker-end="url(#ZERO_OR_MORE_END)" d="M380.19,267L380.19,277.167C380.19,287.333,380.19,307.667,368.483,326.167C356.775,344.667,333.361,361.333,321.653,369.667L309.946,378" class="er relationshipLine" style="stroke: gray; fill: none;"></path><g transform="translate(20,20 )" id="entity-ORGANIZATIONS-f00fe499-9a66-4d04-8fcf-38c7cf9e5d17"><rect height="68" width="186.52545166015625" y="0" x="0" class="er entityBox"></rect><text transform="translate(93.26272583007812,12)" y="0" x="0" id="text-entity-ORGANIZATIONS-f00fe499-9a66-4d04-8fcf-38c7cf9e5d17" class="er entityLabel" style="dominant-baseline: middle; text-anchor: middle; font-size: 12px;">ORGANIZATIONS</text><rect height="22" width="36.61909484863281" y="24" x="0" class="er attributeBoxOdd"></rect><text transform="translate(5,35)" y="0" x="0" id="text-entity-ORGANIZATIONS-f00fe499-9a66-4d04-8fcf-38c7cf9e5d17-attr-1-type" class="er entityLabel" style="dominant-baseline: middle; font-size: 10.2px;">int</text><rect height="22" width="127.21867370605469" y="24" x="36.61909484863281" class="er attributeBoxOdd"></rect><text transform="translate(41.61909484863281,35)" y="0" x="0" id="text-entity-ORGANIZATIONS-f00fe499-9a66-4d04-8fcf-38c7cf9e5d17-attr-1-name" class="er entityLabel" style="dominant-baseline: middle; font-size: 10.2px;">Organization_ID</text><rect height="22" width="22.68768310546875" y="24" x="163.8377685546875" class="er attributeBoxOdd"></rect><text transform="translate(168.8377685546875,35)" y="0" x="0" id="text-entity-ORGANIZATIONS-f00fe499-9a66-4d04-8fcf-38c7cf9e5d17-attr-1-key" class="er entityLabel" style="dominant-baseline: middle; font-size: 10.2px;">PK</text><rect height="22" width="36.61909484863281" y="46" x="0" class="er attributeBoxEven"></rect><text transform="translate(5,57)" y="0" x="0" id="text-entity-ORGANIZATIONS-f00fe499-9a66-4d04-8fcf-38c7cf9e5d17-attr-2-type" class="er entityLabel" style="dominant-baseline: middle; font-size: 10.2px;">string</text><rect height="22" width="127.21867370605469" y="46" x="36.61909484863281" class="er attributeBoxEven"></rect><text transform="translate(41.61909484863281,57)" y="0" x="0" id="text-entity-ORGANIZATIONS-f00fe499-9a66-4d04-8fcf-38c7cf9e5d17-attr-2-name" class="er entityLabel" style="dominant-baseline: middle; font-size: 10.2px;">Organization_Information</text><rect height="22" width="22.68768310546875" y="46" x="163.8377685546875" class="er attributeBoxEven"></rect><text transform="translate(168.8377685546875,57)" y="0" x="0" id="text-entity-ORGANIZATIONS-f00fe499-9a66-4d04-8fcf-38c7cf9e5d17-attr-2-key" class="er entityLabel" style="dominant-baseline: middle; font-size: 10.2px;"></text></g><g transform="translate(40.320343017578125,188 )" id="entity-ANALYTICACCOUNTS-a193c38a-f979-4c27-a047-d42a7dee444c"><rect height="90" width="145.884765625" y="0" x="0" class="er entityBox"></rect><text transform="translate(72.9423828125,12)" y="0" x="0" id="text-entity-ANALYTICACCOUNTS-a193c38a-f979-4c27-a047-d42a7dee444c" class="er entityLabel" style="dominant-baseline: middle; text-anchor: middle; font-size: 12px;">ANALYTIC_ACCOUNTS</text><rect height="22" width="37.7499745686849" y="24" x="0" class="er attributeBoxOdd"></rect><text transform="translate(5,35)" y="0" x="0" id="text-entity-ANALYTICACCOUNTS-a193c38a-f979-4c27-a047-d42a7dee444c-attr-1-type" class="er entityLabel" style="dominant-baseline: middle; font-size: 10.2px;">int</text><rect height="22" width="84.31622823079427" y="24" x="37.7499745686849" class="er attributeBoxOdd"></rect><text transform="translate(42.7499745686849,35)" y="0" x="0" id="text-entity-ANALYTICACCOUNTS-a193c38a-f979-4c27-a047-d42a7dee444c-attr-1-name" class="er entityLabel" style="dominant-baseline: middle; font-size: 10.2px;">Account_ID</text><rect height="22" width="23.818562825520832" y="24" x="122.06620279947916" class="er attributeBoxOdd"></rect><text transform="translate(127.06620279947916,35)" y="0" x="0" id="text-entity-ANALYTICACCOUNTS-a193c38a-f979-4c27-a047-d42a7dee444c-attr-1-key" class="er entityLabel" style="dominant-baseline: middle; font-size: 10.2px;">PK</text><rect height="22" width="37.7499745686849" y="46" x="0" class="er attributeBoxEven"></rect><text transform="translate(5,57)" y="0" x="0" id="text-entity-ANALYTICACCOUNTS-a193c38a-f979-4c27-a047-d42a7dee444c-attr-2-type" class="er entityLabel" style="dominant-baseline: middle; font-size: 10.2px;">string</text><rect height="22" width="84.31622823079427" y="46" x="37.7499745686849" class="er attributeBoxEven"></rect><text transform="translate(42.7499745686849,57)" y="0" x="0" id="text-entity-ANALYTICACCOUNTS-a193c38a-f979-4c27-a047-d42a7dee444c-attr-2-name" class="er entityLabel" style="dominant-baseline: middle; font-size: 10.2px;">Account_Data</text><rect height="22" width="23.818562825520832" y="46" x="122.06620279947916" class="er attributeBoxEven"></rect><text transform="translate(127.06620279947916,57)" y="0" x="0" id="text-entity-ANALYTICACCOUNTS-a193c38a-f979-4c27-a047-d42a7dee444c-attr-2-key" class="er entityLabel" style="dominant-baseline: middle; font-size: 10.2px;"></text><rect height="22" width="37.7499745686849" y="68" x="0" class="er attributeBoxOdd"></rect><text transform="translate(5,79)" y="0" x="0" id="text-entity-ANALYTICACCOUNTS-a193c38a-f979-4c27-a047-d42a7dee444c-attr-3-type" class="er entityLabel" style="dominant-baseline: middle; font-size: 10.2px;">int</text><rect height="22" width="84.31622823079427" y="68" x="37.7499745686849" class="er attributeBoxOdd"></rect><text transform="translate(42.7499745686849,79)" y="0" x="0" id="text-entity-ANALYTICACCOUNTS-a193c38a-f979-4c27-a047-d42a7dee444c-attr-3-name" class="er entityLabel" style="dominant-baseline: middle; font-size: 10.2px;">Organization_ID</text><rect height="22" width="23.818562825520832" y="68" x="122.06620279947916" class="er attributeBoxOdd"></rect><text transform="translate(127.06620279947916,79)" y="0" x="0" id="text-entity-ANALYTICACCOUNTS-a193c38a-f979-4c27-a047-d42a7dee444c-attr-3-key" class="er entityLabel" style="dominant-baseline: middle; font-size: 10.2px;">FK</text></g><g transform="translate(286.2051086425781,199 )" id="entity-SYNTHETICACCOUNTS-d9138814-80b1-4152-b24b-00f1c995ede7"><rect height="68" width="187.9697723388672" y="0" x="0" class="er entityBox"></rect><text transform="translate(93.9848861694336,12)" y="0" x="0" id="text-entity-SYNTHETICACCOUNTS-d9138814-80b1-4152-b24b-00f1c995ede7" class="er entityLabel" style="dominant-baseline: middle; text-anchor: middle; font-size: 12px;">SYNTHETIC_ACCOUNTS</text><rect height="22" width="36.61909484863281" y="24" x="0" class="er attributeBoxOdd"></rect><text transform="translate(5,35)" y="0" x="0" id="text-entity-SYNTHETICACCOUNTS-d9138814-80b1-4152-b24b-00f1c995ede7-attr-1-type" class="er entityLabel" style="dominant-baseline: middle; font-size: 10.2px;">int</text><rect height="22" width="128.66299438476562" y="24" x="36.61909484863281" class="er attributeBoxOdd"></rect><text transform="translate(41.61909484863281,35)" y="0" x="0" id="text-entity-SYNTHETICACCOUNTS-d9138814-80b1-4152-b24b-00f1c995ede7-attr-1-name" class="er entityLabel" style="dominant-baseline: middle; font-size: 10.2px;">Synthetic_Account_ID</text><rect height="22" width="22.68768310546875" y="24" x="165.28208923339844" class="er attributeBoxOdd"></rect><text transform="translate(170.28208923339844,35)" y="0" x="0" id="text-entity-SYNTHETICACCOUNTS-d9138814-80b1-4152-b24b-00f1c995ede7-attr-1-key" class="er entityLabel" style="dominant-baseline: middle; font-size: 10.2px;">PK</text><rect height="22" width="36.61909484863281" y="46" x="0" class="er attributeBoxEven"></rect><text transform="translate(5,57)" y="0" x="0" id="text-entity-SYNTHETICACCOUNTS-d9138814-80b1-4152-b24b-00f1c995ede7-attr-2-type" class="er entityLabel" style="dominant-baseline: middle; font-size: 10.2px;">string</text><rect height="22" width="128.66299438476562" y="46" x="36.61909484863281" class="er attributeBoxEven"></rect><text transform="translate(41.61909484863281,57)" y="0" x="0" id="text-entity-SYNTHETICACCOUNTS-d9138814-80b1-4152-b24b-00f1c995ede7-attr-2-name" class="er entityLabel" style="dominant-baseline: middle; font-size: 10.2px;">Internal_Accounting_Data</text><rect height="22" width="22.68768310546875" y="46" x="165.28208923339844" class="er attributeBoxEven"></rect><text transform="translate(170.28208923339844,57)" y="0" x="0" id="text-entity-SYNTHETICACCOUNTS-d9138814-80b1-4152-b24b-00f1c995ede7-attr-2-key" class="er entityLabel" style="dominant-baseline: middle; font-size: 10.2px;"></text></g><g transform="translate(152.6269187927246,378 )" id="entity-TRANSACTIONS-aab3e3c7-cda3-4986-b954-900945350fb2"><rect height="90" width="188.19888305664062" y="0" x="0" class="er entityBox"></rect><text transform="translate(94.09944152832031,12)" y="0" x="0" id="text-entity-TRANSACTIONS-aab3e3c7-cda3-4986-b954-900945350fb2" class="er entityLabel" style="dominant-baseline: middle; text-anchor: middle; font-size: 12px;">TRANSACTIONS</text><rect height="22" width="36.61909484863281" y="24" x="0" class="er attributeBoxOdd"></rect><text transform="translate(5,35)" y="0" x="0" id="text-entity-TRANSACTIONS-aab3e3c7-cda3-4986-b954-900945350fb2-attr-1-type" class="er entityLabel" style="dominant-baseline: middle; font-size: 10.2px;">int</text><rect height="22" width="128.89210510253906" y="24" x="36.61909484863281" class="er attributeBoxOdd"></rect><text transform="translate(41.61909484863281,35)" y="0" x="0" id="text-entity-TRANSACTIONS-aab3e3c7-cda3-4986-b954-900945350fb2-attr-1-name" class="er entityLabel" style="dominant-baseline: middle; font-size: 10.2px;">Transaction_ID</text><rect height="22" width="22.68768310546875" y="24" x="165.51119995117188" class="er attributeBoxOdd"></rect><text transform="translate(170.51119995117188,35)" y="0" x="0" id="text-entity-TRANSACTIONS-aab3e3c7-cda3-4986-b954-900945350fb2-attr-1-key" class="er entityLabel" style="dominant-baseline: middle; font-size: 10.2px;">PK</text><rect height="22" width="36.61909484863281" y="46" x="0" class="er attributeBoxEven"></rect><text transform="translate(5,57)" y="0" x="0" id="text-entity-TRANSACTIONS-aab3e3c7-cda3-4986-b954-900945350fb2-attr-2-type" class="er entityLabel" style="dominant-baseline: middle; font-size: 10.2px;">string</text><rect height="22" width="128.89210510253906" y="46" x="36.61909484863281" class="er attributeBoxEven"></rect><text transform="translate(41.61909484863281,57)" y="0" x="0" id="text-entity-TRANSACTIONS-aab3e3c7-cda3-4986-b954-900945350fb2-attr-2-name" class="er entityLabel" style="dominant-baseline: middle; font-size: 10.2px;">Financial_Operation_Data</text><rect height="22" width="22.68768310546875" y="46" x="165.51119995117188" class="er attributeBoxEven"></rect><text transform="translate(170.51119995117188,57)" y="0" x="0" id="text-entity-TRANSACTIONS-aab3e3c7-cda3-4986-b954-900945350fb2-attr-2-key" class="er entityLabel" style="dominant-baseline: middle; font-size: 10.2px;"></text><rect height="22" width="36.61909484863281" y="68" x="0" class="er attributeBoxOdd"></rect><text transform="translate(5,79)" y="0" x="0" id="text-entity-TRANSACTIONS-aab3e3c7-cda3-4986-b954-900945350fb2-attr-3-type" class="er entityLabel" style="dominant-baseline: middle; font-size: 10.2px;">int</text><rect height="22" width="128.89210510253906" y="68" x="36.61909484863281" class="er attributeBoxOdd"></rect><text transform="translate(41.61909484863281,79)" y="0" x="0" id="text-entity-TRANSACTIONS-aab3e3c7-cda3-4986-b954-900945350fb2-attr-3-name" class="er entityLabel" style="dominant-baseline: middle; font-size: 10.2px;">Account_ID</text><rect height="22" width="22.68768310546875" y="68" x="165.51119995117188" class="er attributeBoxOdd"></rect><text transform="translate(170.51119995117188,79)" y="0" x="0" id="text-entity-TRANSACTIONS-aab3e3c7-cda3-4986-b954-900945350fb2-attr-3-key" class="er entityLabel" style="dominant-baseline: middle; font-size: 10.2px;">FK</text></g><rect height="14" width="52.28515625" y="131" x="87.12042236328125" class="er relationshipLabelBox"></rect><text y="138" x="113.26300048828125" id="rel40" class="er relationshipLabel" style="text-anchor: middle; dominant-baseline: middle; font-size: 12px;">maintains</text><rect height="14" width="39.939453125" y="330.6090393066406" x="112.9366455078125" class="er relationshipLabelBox"></rect><text y="337.6090393066406" x="132.9063720703125" id="rel41" class="er relationshipLabel" style="text-anchor: middle; dominant-baseline: middle; font-size: 12px;">records</text><rect height="14" width="32.720703125" y="326.22430419921875" x="347.0543518066406" class="er relationshipLabelBox"></rect><text y="333.22430419921875" x="363.4147033691406" id="rel42" class="er relationshipLabel" style="text-anchor: middle; dominant-baseline: middle; font-size: 12px;">tracks</text></svg>

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
