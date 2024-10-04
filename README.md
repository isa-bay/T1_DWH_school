# Практические задания:

<details>
<summary>1 - 30.09</summary>

  ![Снимок экрана 2024-09-30 172943](https://github.com/user-attachments/assets/a4b25435-41e3-4a2e-abf7-af63afbfcc36)

  | Архитектурный подход | Плюсы                                             | Минусы                                           | Критерии для выбора                             |
|----------------------|--------------------------------------------------|-------------------------------------------------|-------------------------------------------------|
| **DWH** | - Высокая производительность запросов <br> - Структурированные данные <br> - Поддержка аналитики и отчетности | - Высокие затраты на хранение <br> - Длительная настройка <br> - Жесткие схемы | - Нужен централизованный доступ к структурированным данным <br> - Сложные аналитические запросы |
| **Data Lake**        | - Гибкость в хранении как структурированных, так и неструктурированных данных <br> - Низкая стоимость хранения | - Управление качеством данных сложно <br> - Потенциальные проблемы с безопасностью <br> - Меньше оптимизации для аналитики | - Большие объемы неструктурированных данных <br> - Необходимость в быстром доступе к данным |
| **Lake House**       | - Комбинация подходов Data Lake и DWH <br> - Поддержка как аналитических, так и транзакционных запросов <br> - Упрощенное управление данными | - Сложность в реализации <br> - Высокие требования к ресурсам | - Нужен баланс между структурированными и неструктурированными данными <br> - Необходимость в гибком хранилище |
| **Data Mesh**        | - Децентрализация данных <br> - Командная ответственность за данные <br> - Легче интегрировать с микросервисной архитектурой | - Требует изменения культуры работы с данными <br> - Сложность в обеспечении согласованности данных | - Необходимость гибкости и быстрой адаптации <br> - Уровень зрелости команды и инфраструктуры |

</details>
<details>
<summary>2 - 03.10</summary>

![image](https://github.com/user-attachments/assets/feb7213e-038f-4eda-999a-c9b296817b59)

### Таблицы в схеме arenadata_toolkit

| Наименование                | Содержание                                            | Применение                                                    |
|-----------------------------|-------------------------------------------------------|---------------------------------------------------------------|
| `daily_operation`           | информацию об операциях VACUUM и ANALYZE, проводимых над таблицами базы данных автоматически по расписанию   | Используется для анализа и оптимизации хранения данных.       |
| `db_files_current`          | Логи системных операций.                              | Помогает в отладке и мониторинге системы.                     |
| `db_files_history`          | Размер базы данных.                                   | Для наблюдения за использованием дискового пространства.      |
| `operation_exclude`         | Активность очередей ресурсов.                         | Управление и мониторинг использования ресурсов.               |

### Представлений в arenadata_toolkit не найдено!!!

### Представления в схеме gp_toolkit

| Наименование                | Содержание                                            | Применение                                                    |
|-----------------------------|-------------------------------------------------------|---------------------------------------------------------------|
| `gp_bloat_diag`             | Информация о возможных проблемах раздувания таблиц.   | Используется для анализа и оптимизации хранения данных.       |
| `gp_log_system`             | Логи системных операций.                              | Помогает в отладке и мониторинге системы.                     |
| `gp_size_of_database`       | Размер базы данных.                                   | Для наблюдения за использованием дискового пространства.      |
| `gp_resq_activity`          | Активность очередей ресурсов.                         | Управление и мониторинг использования ресурсов.               |
| `gp_skew_coefficients`      | Коэффициенты неравномерности распределения данных.    | Оптимизация запросов и распределения данных на сегментах.     |
  
</details>
<details>
<summary> 3.1 - 08.10</summary>

![image](https://github.com/user-attachments/assets/a1c669b3-90b4-46ae-aef8-334c956e1174)

  
</details>
<details>
<summary> 3.2 - 08.10</summary>

![image](https://github.com/user-attachments/assets/a36e7c6b-1c42-48e5-a6e6-de54bf5c50e9)
  
</details>

# Сквозной проект (второй вариант)
<details>
<summary>Проект №2</summary>
  
![Снимок экрана](https://github.com/user-attachments/assets/709c8a8f-58d7-4b23-af03-d782bb9f5b9b)

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

</details>
<details>
<summary>4.1 - 10.10</summary>
  


</details>
