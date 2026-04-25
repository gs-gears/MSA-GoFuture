# Компания «GoFuture»

### О компании

«GoFuture» — это платформа для агрегирования такси, у которой есть пассажирское и водительское приложения, а также веб-портал для корпоративных клиентов.

Компания столкнулась с критическими ограничениями монолитной архитектуры. Та просто не справляется с масштабированием при активной экспансии на рынки Юго-Восточной Азии и Южной Америки. Пиковые нагрузки (более 100 тысяч активных поездок) вызывают каскадные отказы, разработка новых функций затягивается минимум на полгода, а среднее время восстановления (MTTR) превышает четыре часа.

### **Ключевые бизнес-требования**

- Обработка 500 тысяч конкурентных поездок.
- Горизонтальное масштабирование сразу в нескольких географических регионах.
- Обеспечение 99,95% доступности критических сервисов.
- Сокращение времени выхода на рынок новых функций до двух недель.
- Соответствие локальным регуляторным требованиям.
- Поддержка динамического ценообразования в режиме реального времени.
- Оптимизация загрузки водителей в часы пик с помощью «умного» перераспределения (ожидание подходящего водителя вместо выбора ближайшего, чтобы избежать «горячих зон», где концентрируется большинство водителей).
- Интеграция с локальными платёжными и картографическими сервисами.

### **Лендскейп** **компании**

Текущая организационная структура «GoFuture» выглядит так:

- **Восемь продуктовых команд по доменам** — Booking, Driver, Pricing, Payments, Notification, Geography, Analytics и Fraud.
- **Платформенная команда** отвечает за CI/CD, Observability и Developer Tooling.
- **SRE-команда** отвечает за надёжность, планирование ёмкости и управление инцидентами.
- **Data-инженеры** занимаются аналитикой в режиме реального времени, ML-пайплайнами и data governance.
- **Архитектурный комитет** формирует техническую стратегию и стандарты, а также проводит code review.
- **Инфраструктурная команда** управляет оборудованием, VMware, Docker и выполняет ручное масштабирование по алертам.

### **Какие технологии и системы используются**

**Основной стек приложения**

- **Backend Framework** — Django (Python).
- **Task Queue** — Celery.
- **Message Broker** — RabbitMQ.
- **Application Server** — Gunicorn/uWSGI.
- **API** — REST API.

**Базы данных и хранилища**

- **Основная БД** — PostgreSQL RDS.
- **Поисковый движок** — Elasticsearch.
- **Кеширование** — Redis.
- **Аналитическая БД** — ClickHouse.
- **Хранилище образов** — Docker Registry.

**Инфраструктура и платформа**

- **Cloud Provider** — Yandex Cloud.
- **Compute** — EC2 instances.
- **Containerization** — Docker.
- **Orchestration** — Docker Compose (базовое).
- **Load Balancing** — AWS ELB/ALB.

**Мониторинг и observability**

- **Метрики** — Prometheus.
- **Визуализация** — Grafana.
- **Логи** — Loki.
- **Алертинг** — Alertmanager.
- **Метрики БД** — PostgreSQL Exporter.
- **Метрики очередей** — RabbitMQ Exporter.

**CI/CD-пайплайн**

- **CI/CD Server** — Jenkins.
- **Сборка** — Docker builds.
- **Артефакты** — Docker Registry.
- **Воркеры сборки** — VM/Containers.
- **Деплой** — Docker-based deployment.

**Аналитика и BI**

- **Обработка данных** — Spark/Flink.
- **Хранилище данных** — ClickHouse.
- **BI-инструмент** — DataLens.
- **Data pipelines** — ETL-processes.

**Внешние интеграции и API**

- **Платёжный шлюз** — Яндекс Пэй.
- **Картографический сервис** — Яндекс Карты.
- **Push-уведомления** — Firebase Cloud Messaging (FCM) для Android, Apple Push Notification Service (APNS) для iOS и Huawei Push Kit для Huawei-устройств.
- **Банковские API** — интеграции с банками для выплат.

### **Клиентские приложения**

**Мобильные приложения**

- iOS Native (Swift/Objective-C).
- Android Native (Kotlin/Java).
- Huawei Mobile Services.

**Веб-приложения**

- Корпоративный портал (React/Vue.js и Django).
- Админ-панель (Django Admin).

### **Сетевые протоколы и коммуникация**

- **Синхронные вызовы** — HTTP/REST.
- **Асинхронные вызовы** — AMQP (RabbitMQ).
- **Метрики** — Prometheus Metrics.
- **Логи** — Loki Logs API.
- **Базы данных** — SQL, ORM и прямые подключения.

### **Вспомогательные инструменты**

- **Миграции БД** — Django Migrations.
- **Кеширование** — Redis.
- **Геопоиск** — геозапросы в Elasticsearch.
- **Очереди задач** — Celery Beat для планирования и выполнения периодических задач.
- **Конфигурация** — переменные окружения и конфигурационные файлы.

### **Ключевые характеристики стека**

Архитектура системы «GoFuture» монолитна. Используется единая кодовая база на Django. Все сервисы работают с одной базой данных PostgreSQL. В реализации применяются смешанные паттерны — синхронные вызовы сочетаются с асинхронными задачами.

Мобильные приложения разрабатываются нативно и отдельно для iOS и Android. Мониторинг реализован на базе Prometheus и Grafana, но без сложных настроек. Масштабирование осуществляется вертикально за счёт увеличения ресурсов EC2-инстансов и вручную по алертам, без автоматического скейлинга. Сборки занимают более 30 минут из-за монолитной структуры проекта.

Такой стек отражает типичную эволюцию стартапа, начавшего с монолита и постепенно добавлявшего инструменты по мере роста, но без фундаментального пересмотра архитектуры.

### **Диаграмма системы**

Ключевые взаимодействия (аналогичны целевым, но реализованы внутри монолита):

Пассажиры и водители взаимодействуют через мобильное приложение. Корпоративные клиенты используют веб-портал. Система интегрирована со сторонними сервисами, включая платёжные шлюзы, карты и push-уведомления.

**Текущий контекст (C1):**

```plantuml
@startuml Context_Diagram_With_Payouts
!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Context.puml

Person(passenger, "Пассажир", "Заказывает, отслеживает и оплачивает поездки")
Person(driver, "Водитель", "Принимает заказы, управляет поездками\nи получает выплаты") 
Person(manager, "Корпоративный менеджер", "Управляет корпоративными поездками и счетами")
Person(accountant, "Бухгалтер", "Контролирует выплаты водителям")

System(go_future, "GoFuture Monolithic Platform", "Такси-агрегатор: монолитное приложение")

System_Ext(yandex_pay, "Яндекс Пэй", "Обрабатывает платёжные транзакции")
System_Ext(yandex_maps, "Яндекс Карты", "Предоставляет геоданные и маршруты")
System_Ext(fcm, "Firebase Cloud Messaging", "Отправляет уведомления для iOS/Android")
System_Ext(apns, "Apple Push Notification Service", "Отправляет уведомления для iOS")
System_Ext(huawei_push, "Huawei Push Kit", "Отправляет уведомления для Huawei devices")
System_Ext(bank_api, "API Банка", "Обрабатывает банковские выплаты")

Rel(passenger, go_future, "Использует для заказа поездок")
Rel(driver, go_future, "Использует для работы и получения выплат")
Rel(manager, go_future, "Использует для управления счетами")
Rel(accountant, go_future, "Контролирует выплаты через")

Rel(go_future, yandex_pay, "Обрабатывает платежи через")
Rel(go_future, yandex_maps, "Запрашивает геоданные через")
Rel(go_future, fcm, "Отправляет уведомления через")
Rel(go_future, apns, "Отправляет уведомления через")
Rel(go_future, huawei_push, "Отправляет уведомления через")
Rel(go_future, bank_api, "Инициирует выплаты через")

@enduml
```

**Уровень контейнеров (C2):**

```plantuml
@startuml Container_Diagram_Full_Infrastructure
!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Container.puml

Person(passenger, "Пассажир", "Заказывает поездки")
Person(driver, "Водитель", "Принимает заказы и получает выплаты")
Person(manager, "Корпоративный менеджер", "Управляет счетами")
Person(accountant, "Бухгалтер", "Контролирует выплаты")
Person(dev_engineer, "Разработчик", "Разрабатывает новые функции")
Person(sre_engineer, "SRE инженер", "Мониторит и поддерживает систему")

System_Boundary(go_future_system, "GoFuture Platform") {
    ' ### КЛИЕНТСКИЕ ПРИЛОЖЕНИЯ ###
    Container(web_passenger, "Пассажирское приложение", "iOS/Android/Huawei", "Интерфейс для пассажиров")
    Container(web_driver, "Водительское приложение", "iOS/Android/Huawei", "Интерфейс для водителей")
    Container(web_portal, "Корпоративный веб-портал", "Web Application", "Управление заказами")
    Container(admin_portal, "Админ-панель", "Web Application", "Управление выплатами")

    ' ### ОСНОВНОЙ МОНОЛИТ ###
    Container(app_monolith, "GoFuture Monolith", "Django Application", "Содержит всю бизнес-логику")

    ' ### БАЗЫ ДАННЫХ ###
    ContainerDb(db_main, "Основная БД", "PostgreSQL RDS", "Хранит все бизнес-данные")
    ContainerDb(db_cache, "In-memory кеш", "Redis", "Кеширование данных")
    ContainerDb(db_search, "Поисковый индекс", "Elasticsearch", "Геопоиск водителей")

    ' ### ОЧЕРЕДИ И ВОРКЕРЫ ###
    ContainerQueue(mq_broker, "Брокер сообщений", "RabbitMQ", "Очередь для фоновых задач")
    Container(app_worker, "Воркеры фоновых задач", "Celery", "Обработка асинхронных задач")

    ' ### МОНИТОРИНГ И OBSERVABILITY ###
    Container(monitoring, "Prometheus", "Monitoring System", "Сбор метрик и мониторинг")
    Container(grafana, "Grafana", "Dashboard System", "Визуализация метрик и дашборды")
    Container(loki, "Loki", "Log Aggregation", "Сбор и анализ логов")
    Container(alert_manager, "Alertmanager", "Alert System", "Управление алертами")

    ' ### CI/CD ИНФРАСТРУКТУРА ###
    Container(jenkins, "Jenkins", "CI/CD Server", "Сборка и деплой монолита")
    Container(artifact_repo, "Artifact Repository", "Docker Registry", "Хранение образов приложения")
    Container(ci_worker, "CI/CD Workers", "VM/Containers", "Выполнение задач сборки и тестов")

    ' ### АНАЛИТИЧЕСКАЯ ИНФРАСТРУКТУРА ###
    Container(analytics_engine, "Analytics Engine", "Spark/Flink", "Обработка аналитических данных")
    Container(analytics_db, "Analytics DB", "ClickHouse", "Хранение аналитических данных")
    Container(datalens, "DataLens", "BI Tool", "Визуализация бизнес-метрик")
}

' ### ВНЕШНИЕ СИСТЕМЫ ###
System_Ext(yandex_pay, "Яндекс Пэй", "Платёжный шлюз")
System_Ext(yandex_maps, "Яндекс Карты", "Картографический сервис")
System_Ext(fcm, "FCM", "Push-сервис Google")
System_Ext(apns, "APNs", "Push-сервис Apple")
System_Ext(huawei_push, "Huawei Push Kit", "Push-сервис Huawei")
System_Ext(bank_api, "API Банка", "Банковские выплаты")

' ### СВЯЗИ ПОЛЬЗОВАТЕЛЕЙ ###
Rel(passenger, web_passenger, "Использует")
Rel(driver, web_driver, "Использует")
Rel(manager, web_portal, "Использует")
Rel(accountant, admin_portal, "Использует")
Rel(dev_engineer, jenkins, "Запускает сборки")
Rel(sre_engineer, grafana, "Мониторит систему")
Rel(sre_engineer, alert_manager, "Настраивает алерты")

' ### БИЗНЕС-ЛОГИКА ###
Rel(web_passenger, app_monolith, "HTTP/REST API")
Rel(web_driver, app_monolith, "HTTP/REST API")
Rel(web_portal, app_monolith, "HTTP/REST API")
Rel(admin_portal, app_monolith, "HTTP/REST API")

Rel(app_monolith, db_main, "Чтение/запись (ORM)")
Rel(app_monolith, db_cache, "Кеширование данных")
Rel(app_monolith, db_search, "Геопоиск водителей")
Rel(app_monolith, mq_broker, "Отправка задач")

Rel(app_monolith, yandex_pay, "Обработка платежей")
Rel(app_monolith, yandex_maps, "Запросы геоданных")
Rel(app_monolith, bank_api, "Инициирование выплат")

' ### ASYNC WORKERS ###
Rel(app_worker, mq_broker, "Получает задачи из", "AMQP")
Rel(app_worker, db_main, "Чтение/запись данных", "ORM")
Rel(app_worker, db_main, "Сохраняет результаты", "ORM")
Rel(app_worker, fcm, "Отправляет уведомления", "REST API")
Rel(app_worker, apns, "Отправляет уведомления", "REST API")
Rel(app_worker, huawei_push, "Отправляет уведомления", "REST API")
Rel(app_worker, bank_api, "Выполняет выплаты", "REST API")

' ### МОНИТОРИНГ ###
Rel(app_monolith, monitoring, "Отправляет метрики", "Prometheus Metrics")
Rel(app_worker, monitoring, "Отправляет метрики", "Prometheus Metrics")
Rel(db_main, monitoring, "Метрики БД", "PostgreSQL Exporter")
Rel(mq_broker, monitoring, "Метрики очередей", "RabbitMQ Exporter")

Rel(monitoring, grafana, "Предоставляет данные", "PromQL")
Rel(monitoring, alert_manager, "Отправляет алерты", "Alert Rules")
Rel(alert_manager, sre_engineer, "Отправляет уведомления", "Email/Slack/Pager")

Rel(app_monolith, loki, "Отправляет логи", "Loki Logs")
Rel(app_worker, loki, "Отправляет логи", "Loki Logs")

' ### CI/CD ###
Rel(jenkins, ci_worker, "Запускает задачи", "SSH/API")
Rel(ci_worker, artifact_repo, "Пушит образы", "Docker Push")
Rel(jenkins, artifact_repo, "Деплоит образы", "Docker Pull")
Rel(ci_worker, app_monolith, "Запускает тесты", "Test Execution")

' ### АНАЛИТИКА ###
Rel(app_monolith, analytics_engine, "Отправляет события", "AMQP")
Rel(app_worker, analytics_engine, "Отправляет события", "AMQP")
Rel(analytics_engine, analytics_db, "Записывает данные", "ETL Process")
Rel(analytics_db,datalens, "Предоставляет данные", "SQL Queries")
Rel(datalens, manager, "Бизнес-отчёты", "Dashboards")
Rel(datalens, accountant, "Финансовые отчёты", "Dashboards")

@enduml
```

**Уровень компонентов (С3):**

```plantuml
@startuml Component_Diagram_Final
!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Component.puml

' ### СИСТЕМНЫЕ ГРАНИЦЫ ###
System_Boundary(monolith_boundary, "GoFuture Monolith") {
    Container(app_monolith, "Django Application", "Python", "Единая кодовая база со всеми зависимостями")

    System_Boundary(domain_components, "Доменные компоненты") {
        Component(booking_domain, "Booking Domain", "Django App", "Управление бронированиями")
        Component(driver_domain, "Driver Domain", "Django App", "Управление водителями")
        Component(pricing_domain, "Pricing Domain", "Django App", "Ценообразование")
        Component(payments_domain, "Payments Domain", "Django App", "Платежи от пассажиров")
        Component(payouts_domain, "Payouts Domain", "Django App", "Выплаты водителям")
        Component(notification_domain, "Notification Domain", "Django App", "Управление уведомлениями")
        Component(geography_domain, "Geography Domain", "Django App", "Геопоиск и маршрутизация")
        Component(analytics_domain, "Analytics Domain", "Django App", "Сбор аналитики")
        Component(fraud_domain, "Fraud Domain", "Django App", "Обнаружение мошенничества")
    }
}

System_Boundary(celery_boundary, "Celery Workers") {
    Container(app_worker, "Celery Workers", "Python", "Асинхронная обработка задач")

    System_Boundary(celery_tasks, "Celery задачи") {
        Component(notification_tasks, "Notification Tasks", "Celery Task", "Асинхронные задачи уведомлений")
        Component(payout_tasks, "Payout Tasks", "Celery Task", "Асинхронные задачи выплат")
        Component(analytics_tasks, "Analytics Tasks", "Celery Task", "Асинхронная аналитика")
    }
}

System_Boundary(database_boundary, "Базы данных") {
    ContainerDb(db_main, "Основная БД", "PostgreSQL", "Единая база для всех доменов")
    ContainerDb(db_search, "Поисковый индекс", "Elasticsearch", "Геопоиск водителей")
    ContainerDb(db_cache, "In-memory кеш", "Redis", "Кеширование данных")
}

System_Boundary(queue_boundary, "Очереди") {
    ContainerQueue(mq_broker, "Брокер сообщений", "RabbitMQ", "Очередь для фоновых задач")
}

System_Boundary(monitoring_boundary, "Мониторинг") {
    Container(monitoring, "Prometheus", "Monitoring", "Сбор метрик")
    Container(grafana, "Grafana", "Dashboard", "Визуализация метрик")
    Container(loki, "Loki", "Log Aggregation", "Сбор логов")
    Container(alert_manager, "Alertmanager", "Alert System", "Управление алертами")
}

System_Boundary(cicd_boundary, "CI/CD") {
    Container(jenkins, "Jenkins", "CI/CD", "Сборка и деплой")
    Container(artifact_repo, "Docker Registry", "Artifact Storage", "Хранение образов")
}

System_Boundary(analytics_boundary, "Аналитика") {
    Container(analytics_engine, "Analytics Engine", "Spark/Flink", "Обработка данных")
    Container(analytics_db, "Analytics DB", "ClickHouse", "Хранение аналитики")
    Container(datalens, "DataLens", "BI Tool", "Визуализация отчётов")
}

' ### ВНЕШНИЕ СИСТЕМЫ ###
System_Ext(yandex_pay, "Яндекс Пэй", "Платёжный шлюз")
System_Ext(yandex_maps, "Яндекс Карты", "Картографический сервис")
System_Ext(fcm, "FCM", "Push-сервис Google")
System_Ext(apns, "APNs", "Push-сервис Apple")
System_Ext(huawei_push, "Huawei Push Kit", "Push-сервис Huawei")
System_Ext(bank_api, "API Банка", "Банковские выплаты")

' ### КОШМАРНЫЕ СВЯЗИ МЕЖДУ ДОМЕНАМИ ###
Rel(booking_domain, driver_domain, "▶ назначает водителя", "синхронный вызов")
Rel(booking_domain, pricing_domain, "▶ запрашивает цену", "синхронный вызов")
Rel(booking_domain, payments_domain, "▶ инициирует платёж", "синхронный вызов")
Rel(booking_domain, geography_domain, "▶ ищет маршрут", "синхронный вызов")
Rel(booking_domain, fraud_domain, "▶ проверяет на мошенничество", "синхронный вызов")
Rel(booking_domain, notification_domain, "▶ отправляет уведомления", "синхронный вызов")

Rel(driver_domain, pricing_domain, "▶ расчет заработка", "синхронный вызов")
Rel(payments_domain, fraud_domain, "▶ проверка транзакций", "синхронный вызов")
Rel(payouts_domain, driver_domain, "▶ данные водителя", "синхронный вызов")
Rel(geography_domain, analytics_domain, "▶ метрики геопоиска", "синхронный вызов")

' ### ASYNC-СВЯЗИ ЧЕРЕЗ QUEUE ###
Rel(booking_domain, mq_broker, "▶ уведомления и аналитика", "AMQP")
Rel(payouts_domain, mq_broker, "▶ выплаты", "AMQP")
Rel(payments_domain, mq_broker, "▶ отчёты", "AMQP")
Rel(analytics_domain, mq_broker, "▶ события аналитики", "AMQP")

' ### CELERY TASK WORKERS ###
Rel(mq_broker, notification_tasks, "▶ задачи уведомлений", "AMQP")
Rel(mq_broker, payout_tasks, "▶ задачи выплат", "AMQP")
Rel(mq_broker, analytics_tasks, "▶ задачи аналитики", "AMQP")

' ### CELERY → ВНЕШНИЕ СЕРВИСЫ ###
Rel(notification_tasks, fcm, "▶ уведомления Android", "REST API")
Rel(notification_tasks, apns, "▶ уведомления iOS", "REST API")
Rel(notification_tasks, huawei_push, "▶ уведомления Huawei", "REST API")
Rel(payout_tasks, bank_api, "▶ банковские выплаты", "REST API")

' ### CELERY → РАБОТА С БАЗОЙ ###
Rel(notification_tasks, db_main, "▶ данные уведомлений", "ORM")
Rel(payout_tasks, db_main, "▶ выплаты и балансы", "ORM")
Rel(analytics_tasks, db_main, "▶ аналитические данные", "ORM")

' ### МОНИТОРИНГ - МЕТРИКИ ###
Rel(booking_domain, monitoring, "▶ метрики бронирований", "Prometheus")
Rel(payments_domain, monitoring, "▶ метрики платежей", "Prometheus")
Rel(notification_tasks, monitoring, "▶ метрики уведомлений", "Prometheus")
Rel(payout_tasks, monitoring, "▶ метрики выплат", "Prometheus")
Rel(db_main, monitoring, "▶ метрики БД", "PostgreSQL Exporter")
Rel(mq_broker, monitoring, "▶ метрики очередей", "RabbitMQ Exporter")

Rel(monitoring, grafana, "▶ данные для дашбордов", "PromQL")
Rel(grafana, monitoring, "▶ запросы метрик", "PromQL")
Rel(monitoring, alert_manager, "▶ алерты", "Alert Rules")

' ### МОНИТОРИНГ - ЛОГИ ###
Rel(booking_domain, loki, "▶ логи бронирований", "Loki Logs")
Rel(payments_domain, loki, "▶ логи платежей", "Loki Logs")
Rel(notification_tasks, loki, "▶ логи уведомлений", "Loki Logs")
Rel(payout_tasks, loki, "▶ логи выплат", "Loki Logs")
Rel(app_monolith, loki, "▶ логи приложения", "Loki Logs")
Rel(app_worker, loki, "▶ логи воркеров", "Loki Logs")

' ### CI/CD ###
Rel(jenkins, app_monolith, "▶ деплой приложения", "Docker Deploy")
Rel(jenkins, artifact_repo, "▶ управление образами", "Docker API")
Rel(artifact_repo, app_monolith, "▶ хранение образов", "Docker Registry")
Rel(jenkins, app_worker, "▶ деплой воркеров", "Docker Deploy")

' ### АНАЛИТИКА ###
Rel(analytics_domain, analytics_engine, "▶ отправка событий", "AMQP")
Rel(analytics_tasks, analytics_engine, "▶ обработка данных", "Spark Jobs")
Rel(analytics_engine, analytics_db, "▶ запись данных", "ETL")
Rel(analytics_db, datalens, "▶ визуализация отчётов", "SQL")

' ### ПРЯМЫЕ ОБРАЩЕНИЯ К БАЗЕ ДАННЫХ ###
Rel(booking_domain, db_main, "▶ bookings, drivers", "прямые SQL")
Rel(driver_domain, db_main, "▶ drivers, payouts", "прямые SQL")
Rel(pricing_domain, db_main, "▶ pricing_rules", "прямые SQL")
Rel(payments_domain, db_main, "▶ payments", "прямые SQL")
Rel(payouts_domain, db_main, "▶ payouts", "прямые SQL")
Rel(geography_domain, db_main, "▶ drivers, zones", "прямые SQL")
Rel(analytics_domain, db_main, "▶ все таблицы", "прямые SQL")
Rel(fraud_domain, db_main, "▶ payments, bookings", "прямые SQL")

' ### ВНЕШНИЕ ИНТЕГРАЦИИ ###
Rel(geography_domain, yandex_maps, "▶ геоданные", "Yandex Maps API")
Rel(payments_domain, yandex_pay, "▶ платежи", "Yandex Pay API")

' ### КЕШИРОВАНИЕ ###
Rel(pricing_domain, db_cache, "▶ кеш ценовых правил", "Redis")
Rel(notification_domain, db_cache, "▶ кеш устройств", "Redis")
Rel(geography_domain, db_cache, "▶ кеш геоданных", "Redis")

' ### ГЕОПОИСК ###
Rel(geography_domain, db_search, "▶ поиск водителей", "Elasticsearch API")

@enduml
```

# **Цели бизнеса**

Достигнуто динамическое ценообразование с реалтайм-адаптацией цен на основе спроса и предложения. Оптимизирована загрузка водителей для предотвращения «горячих точек». Платформа «GoFuture» стала мультитенантной, поддерживая партнёров в новых регионах. Используются data-driven решения: ML-модели для прогнозирования спроса и предотвращения фрода. Реализована возможность самообслуживания через API для внешних разработчиков и партнёров.

В итоге это дало и свой бизнес-импакт, так что ускорен выход на новые рынки и запуск в новых странах занимает от двух до четырёх недель вместо полугода (а то и дольше). Снижены затраты за счёт оптимизации использования ресурсов на 40% через автоскейлинг. Улучшен клиентский опыт: приложение стало более стабильным и быстрым. Созданы новые источники дохода через партнёрские программы. Повышено конкурентное преимущество за счёт возможности быстрого тестирования и внедрения новых функций.

### **Риски и митигация**

Сложность управления заключается в координации сервисов и обеспечении наблюдаемости. Проблема согласованности данных возникает при распределённых транзакциях. Безопасность поддерживается через централизованное управление идентификацией (Identity Management). Контроль затрат обеспечивается практиками FinOps и автоматическим масштабированием.

### **Промежуточные результаты (через 2 месяца)**

Стабилизирована текущая система, так что количество инцидентов снижено на 70%. Начата подготовка к декомпозиции, и уже выделены первые независимые сервисы. Время разработки сокращено до трёх месяцев.

**Метрики:**

- **Надёжность:** среднее время восстановления системы (MTTR) сокращено с более чем четырёх часов до одного.
- **Производительность:** система обрабатывает более 200 тысяч конкурентных поездок без каскадных отказов.
- **Разработка:** время сборки уменьшено с более чем получаса до 15 минут.
- **Мониторинг:** обеспечено полное (100%) покрытие критических метрик и алертов.

### **Финальные результаты (через год)**

Реализована полная микросервисная архитектура с независимыми доменами. Обеспечено глобальное масштабирование с развёртыванием в более чем трёх географических регионах. Платформа «GoFuture» стала целой экосистемой: партнёры могут запускать свои сервисы без глобальных изменений, включая локальные сервисы такси, банки, e-commerce и другие.

**Метрики:**

- **Производительность:** обработка более 500 тысяч конкурентных поездок.
- **Доступность:** 99,95% времени работы критических сервисов.
- **Разработка:** время выхода на рынок новых функций сокращено до двух недель.
- **Масштабирование:** автоматическое горизонтальное масштабирование в более чем трёх регионах.
- **Безопасность:** соблюдение локальных регуляторных требований.
