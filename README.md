Необходимо написать простую биржу с клиент-серверной архитектурой. 
Биржа будет торговать только долларами (USD) за рубли (RUB).

В случае, если цена на покупку и цена на продажу у нескольких клиентов пересекается — нужно заключать сделки между ними. 
В этом случае купленный объём будет зачисляться на баланс клиентам.

ℹ️ Функциональные требования
Сервер

Поддерживает подключения нескольких клиентов одновременно.
Принимает заявки на покупку или продажу долларов за рубли от разных клиентов.
Даёт возможность просмотра баланса клиента.
Клиент

Подключается к серверу и реализует все его возможности.
Торговая логика

Торговая заявка содержит объём, цену и сторону (покупка/продажа).
Если две заявки пересекаются по цене — для сделки выбирается цена более ранней заявки.
Если заявка пересекается с несколькими заявками по другой стороне — приоритет в исполнении отдаётся заявкам с максимальной ценой для заявок на покупку и с минимальной ценой для заявок на продажу.
Возможно частичное исполнение заявки. (см. пример)
Торговая заявка активна до тех пор, пока по ней есть активный объём.
Баланс клиента не ограничен — он может торговать в минус.
📝 Пример:

Пользователь 1 (П1) выставил заявку на покупку 10 USD за RUB по цене 62.
Пользователь 2 (П2) выставил заявку на покупку 20 USD за RUB по цене 63.
Пользователь 3 (П3) выставил заявку на продажу 50 USD за RUB по цене 61.
Сервер сматчил эти заявки между собой. Получилось две сделки:
На 20$ по цене 63 между П2 и П3.
На 10$ по цене 62 между П1 и П3.
Теперь на балансе пользователей:
Пользователь 1: 10 USD, -620 RUB.
Пользователь 2: 20 USD, -1260 RUB.
Пользователь 3: -30 USD, 1880 RUB.
Торговая заявка пользователя 3 (частично исполненная на 30$) осталась активной на 20$.
