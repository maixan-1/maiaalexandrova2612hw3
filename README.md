Домашнее задание 3

Docker

команды запуска: создать файл по примеру: cp .env.example .env 

проверить, работает ли приложение: curl http://localhost:8000/

увеличить счетчик: curl -X POST http://localhost:8000/increment

текущее значение счётчика: curl http://localhost:8000/

остановить: sudo docker compose down

проверить состояние: curl -i http://localhost:8000/healthz

curl -i http://localhost:8000/readyz



настройки докера: порт - 8000 по умолчанию, задаётся через APP\_PORT

приветствие - hello по умолчанию, задается через GREETING



отчёт о проверках

счётчик работает. логи: app-1  | 2026-11-16 19:03:56,174 listening port=8000 storage=redis

app-1  | 2026-11-16 19:05:00,614 http 172.18.0.1 "GET / HTTP/1.1" 200 -

app-1  | 2026-11-16 19:05:07,076 http 172.18.0.1 "POST /increment HTTP/1.1" 200 

app-1  | 2026-11-16 19:05:13,841 http 127.0.0.1 "GET /healthz HTTP/1.1" 200 -



проверка того, что счетчик сохраняется после удаления и повторного создания контейнера:

&#x20;curl http://localhost:8000/: получено значение, равное 3

остановка

заново запустить 

&#x20;curl http://localhost:8000/: все еще 3



приложение работает с Redis. работает healthcheck, все сохраняется в redis\_data. после stop redis и потом sudo docker compose start redis приложение восстанавливает работу без перезапуска get не меняет счётчик, post - увеличивает на 1

