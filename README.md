# **Введение**

В данном домашнем задании нам необходимо настроить репликацию Postgres.

---
- Для выполнения данного ДЗ, необходимо скачать стенд и запустить его.

```
https://github.com/Dmitriy-Iv/Otus-Pr-linux-HW27.git
cd Otus-Pr-linux-HW27/
vagrant up
```

- В результате у нас будут созданы два виртуальных сервера, с установленными PostgreSQL 14.5 и настроенной потоковой асинхронной репликацией в режиме Master-Replica. В playbook создаётся тестовая база с тестовой табличкой на master сервере. Проверим её наличие на slave, а также создадим ещё одну и проверим рпликацию.

Проверка репликации:

![alt text](/screenshots/hw27-1.png?raw=true "Screenshot1")  

![alt text](/screenshots/hw27-2.png?raw=true "Screenshot2")

![alt text](/screenshots/hw27-3.png?raw=true "Screenshot3")

А также на slave можно посмотреть статус потоковой передачи командой `SELECT * FROM pg_stat_wal_receiver;`

![alt text](/screenshots/hw27-4.png?raw=true "Screenshot4")

- В качестве бэкапа базы была выбрана встроенная утилита - pg_dump. Создан небольшой скрипт, который бэкапит базу `test_base` и чистит бэкапы старше 7 дней. Задание добавлено в крон - выполнять бэкап каждую минуту. Выполняется на slave сервере. Для проверки, удалим на мастере из базы `test_base` ранее созданные таблицы, далее скачаем бэкап и восстановим его на мастере, и проверим, как данные снова реплицируются на slave.

- Востановление из бэкапа:

![alt text](/screenshots/hw27-4.png?raw=true "Screenshot5")

![alt text](/screenshots/hw27-4.png?raw=true "Screenshot6")