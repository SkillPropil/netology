# Задание 1
https://hub.docker.com/repository/docker/skillpropil/custom-nginx/general
# Задание 2
![Задание2п1](https://github.com/SkillPropil/netology/blob/ДЗ-к-занятию-4-«Оркестрация-группой-Docker-контейнеров-на-примере-Docker-Compose»/задание2_1.png)
![Задание2п2](https://github.com/SkillPropil/netology/blob/ДЗ-к-занятию-4-«Оркестрация-группой-Docker-контейнеров-на-примере-Docker-Compose»/задание2_2.png)
![Задание2п3](https://github.com/SkillPropil/netology/blob/ДЗ-к-занятию-4-«Оркестрация-группой-Docker-контейнеров-на-примере-Docker-Compose»/задание2_3.png)
![Задание2п4](https://github.com/SkillPropil/netology/blob/ДЗ-к-занятию-4-«Оркестрация-группой-Docker-контейнеров-на-примере-Docker-Compose»/задание2_4.png)

# Задание 3

1) так и не понял, что имелось в виду. Подключался просто к shell командой docker exec -u root -it custom-nginx-t2 /bin/sh
2) При нажатии CTRL+C контейнер не останавливался. В теории, если бы у меня все получилось, возможно мы бы дали команде, которая и стартовала контейнер команду CTLR+c (Что посылает SIGTERM основному процессу контейнера)
3) Я просто остановил, после чего заново пришлось поднимать контейнер с помощью docker-run. После этого перезапустил контейнер
4)Перезапустите контейнер (docker restart custom-nginx-t2)
-------------------------------------------------------------
Правка конфигов nginx и его релоад.
Сделал все, что написано. Установил nano при помощи apk (так как выбрал образ на alpine), поправил конфиг - проверил на правильность и выполнил reload.
Дальше все как в инструкции - посмотрел открытые порты, 8080 открыт, НО так как я запускал контейнер с ключом -p 8080:80, с порта ВМ запросы идут на 80 порт контейнера, а внутри контейнера он закрыт, то соответственно будет выдаваться ошибка. (reset by peer с ВМ и connection refused внутри контейнера).
Небольшое замечание к авторам ДЗ - амперсанд "&&" исполнит вторую команду, только если первая завершилась успешно (с кодом 0). В данном случае логичнее было бы использовать "curl http://127.0.0.1:80 || curl http://127.0.0.1:81" или  "curl http://127.0.0.1:80 ; curl http://127.0.0.1:81"

Далее идут скрины
![Задание3п1](https://github.com/SkillPropil/netology/blob/ДЗ-к-занятию-4-«Оркестрация-группой-Docker-контейнеров-на-примере-Docker-Compose»/задание3_1.png)
![Задание3п2](https://github.com/SkillPropil/netology/blob/ДЗ-к-занятию-4-«Оркестрация-группой-Docker-контейнеров-на-примере-Docker-Compose»/задание3_2.png)
![Задание3п3](https://github.com/SkillPropil/netology/blob/ДЗ-к-занятию-4-«Оркестрация-группой-Docker-контейнеров-на-примере-Docker-Compose»/задание3_3.png)
![Задание3п4](https://github.com/SkillPropil/netology/blob/ДЗ-к-занятию-4-«Оркестрация-группой-Docker-контейнеров-на-примере-Docker-Compose»/задание3_4.png)
# Задание 4

Сделано.
![Задание4п1](https://github.com/SkillPropil/netology/blob/ДЗ-к-занятию-4-«Оркестрация-группой-Docker-контейнеров-на-примере-Docker-Compose»/задание4_1.png)
![Задание4п2](https://github.com/SkillPropil/netology/blob/ДЗ-к-занятию-4-«Оркестрация-группой-Docker-контейнеров-на-примере-Docker-Compose»/задание4_2.png)

# Задание 5
1) Создал два файла с указанным содержимым, выполнил команду docker-compose up -d. Запустился файл compose.yaml, так как по-умолчанию docker-compose между compose.yaml и docker-compose.yaml выберет compose.yaml
![Задание5п1](https://github.com/SkillPropil/netology/blob/ДЗ-к-занятию-4-«Оркестрация-группой-Docker-контейнеров-на-примере-Docker-Compose»/задание5_1.png)
2) Отредактировал файл compose.yaml, добавил конструкцию include
![Задание5п2](https://github.com/SkillPropil/netology/blob/ДЗ-к-занятию-4-«Оркестрация-группой-Docker-контейнеров-на-примере-Docker-Compose»/задание5_2.png)
3) Залил образ в локальное registry, перетегировав его
![Задание5п3](https://github.com/SkillPropil/netology/blob/ДЗ-к-занятию-4-«Оркестрация-группой-Docker-контейнеров-на-примере-Docker-Compose»/задание5_3.png)
4) Время ожидание истекло, высветилось предупреждение, что надо перезапустить portainer. Выполнил docker compose restart
![Задание5п4](https://github.com/SkillPropil/netology/blob/ДЗ-к-занятию-4-«Оркестрация-группой-Docker-контейнеров-на-примере-Docker-Compose»/задание5_4.png)
5-6) Задеплоил образ из локального registry
![Задание5п56](https://github.com/SkillPropil/netology/blob/ДЗ-к-занятию-4-«Оркестрация-группой-Docker-контейнеров-на-примере-Docker-Compose»/задание5_5и6.png)
7) Удалил compose.yaml, высветилось предупреждение о контейнерах, которые запущены, но в них нет описания (так как файл удалился, также может быть если удалили описание сервиса из compose.yaml, а контейнер остался жить). Удалил этот контейнер.
![Задание5п7(1)](https://github.com/SkillPropil/netology/blob/ДЗ-к-занятию-4-«Оркестрация-группой-Docker-контейнеров-на-примере-Docker-Compose»/задание5_7(1).png)
![Задание5п7(2)](https://github.com/SkillPropil/netology/blob/ДЗ-к-занятию-4-«Оркестрация-группой-Docker-контейнеров-на-примере-Docker-Compose»/задание5_7(2).png)
