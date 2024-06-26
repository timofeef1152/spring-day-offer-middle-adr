# Проблематика

    Необходима возможность анализа заданий по всех магазинам компании

# Варианты решений

## Вариант 1

    Описание: Приложения магазина должно выполнять функции регистрации и выполнения заданий, 
        а так же их хранение и запись результатов по выполненным заданиям. Функция сбора аналитики
        по всем магазинам должна быть возложена на отдельное приложение, которое будет опрашивать
        приложения магазинов для выгрузки локальной аналитики, и, при необходимости, формировать
        обобщенную аналитику.
    Плюсы:
        - Каждое приложение магазина не зависит друг от друга
        - Возможна смена стека технологий с соблюдением контракта
        - Используется минимальный набор инструментов для выполнения задачи
    Минусы:
        - При разрыве соединения при сборе обобщенной аналитики может потребоваться повторный запрос 
        на формирование аналитики (опросить упавшее приложение магазина повторно)
        - Доступно только in-memory кеширование на уровне сборщика аналитики

## Вариант 2

    Описание: Приложения магазина должно выполнять функции регистрации и выполнения заданий, 
        а так же их хранение и запись результатов по выполненным заданиям. Функция сбора аналитики
        по всем магазинам должна быть возложена на отдельное приложение, которое будет опрашивать
        приложения магазинов для выгрузки локальной аналитики, и, при необходимости, формировать
        обобщенную аналитику. Обобщенная аналитика записывается в БД, даст возможность построить 
        более детальную аналитику и ускорит повторные запросы.
    Плюсы:
        - Каждое приложение магазина не зависит друг от друга
        - Возможна смена стека технологий с соблюдением контракта
        - БД обеспечивает устойчивый к сбоям кеш ранее сформированной аналитики
    Минусы:
        - При разрыве соединения при сборе обобщенной аналитики может потребоваться повторный запрос 
        на формирование аналитики (опросить упавшее приложение магазина повторно)

# Выбранное решение

    Вариант 2

# Обоснование

    С небольшим увеличением финансовых затрат вариан 2 обеспечивает сохранение ранее выполненных 
    запросов и промежуточных результатов, тем самым обеспечивая лучшую скорость формирования 
    аналитики.