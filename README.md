# Практическое задание 1

| Архитектурный подход | Плюсы                                             | Минусы                                           | Критерии для выбора                             |
|----------------------|--------------------------------------------------|-------------------------------------------------|-------------------------------------------------|
| **DWH (Склад данных)** | - Высокая производительность запросов <br> - Структурированные данные <br> - Поддержка аналитики и отчетности | - Высокие затраты на хранение <br> - Длительная настройка <br> - Жесткие схемы | - Нужен централизованный доступ к структурированным данным <br> - Сложные аналитические запросы |
| **Data Lake**        | - Гибкость в хранении как структурированных, так и неструктурированных данных <br> - Низкая стоимость хранения | - Управление качеством данных сложно <br> - Потенциальные проблемы с безопасностью <br> - Меньше оптимизации для аналитики | - Большие объемы неструктурированных данных <br> - Необходимость в быстром доступе к данным |
| **Lake House**       | - Комбинация подходов Data Lake и DWH <br> - Поддержка как аналитических, так и транзакционных запросов <br> - Упрощенное управление данными | - Сложность в реализации <br> - Высокие требования к ресурсам | - Нужен баланс между структурированными и неструктурированными данными <br> - Необходимость в гибком хранилище |
| **Data Mesh**        | - Децентрализация данных <br> - Командная ответственность за данные <br> - Легче интегрировать с микросервисной архитектурой | - Требует изменения культуры работы с данными <br> - Сложность в обеспечении согласованности данных | - Необходимость гибкости и быстрой адаптации <br> - Уровень зрелости команды и инфраструктуры |
