# {{ PG }}

В некоторых случаях работа трансфера типа _{{ dt-type-repl }}_ или _{{ dt-type-copy-repl }}_ прерывается из-за ошибки `Cannot set transaction snapshot: ERROR: invalid snapshot identifier: "<идентификатор снапшота>" (SQLSTATE 22023).`

Эта ошибка обусловлена остановкой сессии _мастер-транзакции_ — специальной транзакции, которую {{ data-transfer-name }} создает при начале трансфера. Мастер-транзакция используется для чтения данных из таблиц во время трансфера, ее сессия всегда находится в состоянии `idle`.

Остановка сессии мастер-транзакции чаще всего возникает по следующим причинам:

* На источнике работает cron-задание или другое приложение, которое периодически завершает слишком длительные сессии.
* Кто-то вручную завершил мастер-транзакцию.
* Ресурсов CPU на источнике не хватает для выполнения запроса.

Для устранения проблемы отключите такое cron-задание, а также добавьте дополнительные ресурсы для CPU на источник.

После внесения изменений [активируйте](../operations/transfer.md#activate) трансфер повторно.