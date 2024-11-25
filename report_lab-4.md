# Лабораторная работа №4 
## Ход работы
1. Создаем новый образ, так как для установки ping необоходимо получить нужный пакет. Для этого создаем новый Dockerfile
   ```
   FROM ubuntu:latest
   RUN apt-get update && apt-get install -y libaa-bin
   RUN apt-get install -y iputils-ping
   ```
2. В терминале прописываем команду `sudo docker build -t mycontainer`, которая создает новый образ из Dockerfile, котрый находится в текущем каталоге. Созданому образу даем название mycontainer
3. После этого создаем еще один образ из Dockerfile, но уже с название mycontainer2
4. Далее с помощью команды `docker run -it <name_of_container>` проверяем работу приложения aafire в каждом созданном образе. 

<img width="810" alt="image" src="https://github.com/user-attachments/assets/5dbd5904-d5a7-41ea-a5b8-636f56117539">

5. Теперь создаем сеть. Прописываем команду `docker network create myNetwork`
6. С помощью команды `docker network connect myNetwork <name_of_container>` подключаем контейнеры к сети.(далее name_of_container подразумевается именно name, заданный в докере, а не  image, иначе будет выводить ошибку) 
7. Команда `docker network inspect myNetwork` позволяет увидеть настройки нашей сети myNetwork

<img width="528" alt="image" src="https://github.com/user-attachments/assets/14f30759-9c03-4767-8797-71782801fd90">


8. Последний шаг - проверяем тестируем соединение между контейнерами с помощью команды `docker exec -it mycontainer ping mycontainer2`

     <img width="514" alt="image" src="https://github.com/user-attachments/assets/799db24e-44ec-4123-850a-18455c8be807">

