# Лабораторная работа №5
## Ход работы
### Задание 1
1. Клонируем нужный репозиторий, для этого в терминале вводим `git clone your/repository/url.git` , далее переходим в каталог репозитория.
2. Далее переходим в каталог хуков `cd .git/hooks` и создаем файл `pre-commit`.
3. Открываем и записываем туда bash-скрипт:
 ```
   #!/bin/bash
   # Проверяем все файлы, которые будут закоммичены
   for file in $(git diff --cached --name-only); do
       if [[ $file == *.txt ]]; then
           # Проверяем, что файл не пустой
           if [[ ! -s $file ]]; then
               echo "Ошибка: Файл $file пустой."
               exit 1
           fi
       fi
   done

   echo "Проверка прошла успешно: все .txt файлы соответствуют требованиям."
   ```
Объяснение скрипта: <br>
  - Shebang<br>
  - Далее идет цикл for, который перебирает все файлы, которые были изменены и добавлены к коммиту (т.е. находятся в индексной области). Команда git diff --cached --name-only выводит список изменений, которые будут закоммичены, только по именам файлов. <br>
  - C помощью шаблона `*.txt` проверяем, является ли текущий файл текстовым (расширение .txt?).
  - Проверяем, не является ли файл пустым, с помощью флага -s. Этот флаг возвращает истинное (true) значение, если файл не пустой. Если файл пустой, выводится сообщение об ошибке, и скрипт завершает свою работу с кодом выхода 1, что указывает на ошибку.
  - Завершаем цикл for, который перебирает все файлы.
  - Вывод текста если все выполнилось без ошибок
<br>
4. Далее прописываем команду, чтобы сделать скрипт исполняемым `chmod +x pre-commit` <br>
5. Теперь создадим какаой нибудь txt файл для проверки, например мы создаем файл `test.txt` и пытаемся его закоммитить:<br> 
<img width="495" alt="image" src="https://github.com/user-attachments/assets/a1da08bf-8b72-470e-a20e-72a27adc5ef7" /> <br>
6. Теперь создадим пустой файл и попробуем закоммитить его:<br>
<img width="500" alt="image" src="https://github.com/user-attachments/assets/c4dd74ab-a33f-4184-8fd2-4ed64d1db876" /> <br>
7. В итоге получили работоспособный hook который выполняет проверку txt файлов перед коммитом.
<br>

### Задание 2 <br>

1. На Mac OS на замену `apt-get install` приходит `brew install`, проверяем командой `brew --version` установлен ли он и версию, далее скачиваем `brew install git-flow`.
2. Перемещаемся в папку проекта и вводим `git flow init`, то есть инициализируем git flow, предложенное ветвление оставляем по умолчанию(прожимаем Enter).
3. Далее нам необходимо создать новую ветку для функциональности: <br> <img width="500" alt="image" src="https://github.com/user-attachments/assets/27ffe26c-7e75-4e00-8e1c-db8e7f88cadb" /> <br> Нас автоматически переносит в эту ветку.
4. В ней мы создаем новый файл и вносим туда свои изменения(как в тексте задания), далее добавляем и комиттим этот файл.
5. Завершаем написание фичи, прописываем `git flow feature finish task-management`:<br> <img width="500" alt="image" src="https://github.com/user-attachments/assets/4ba0bd1e-8234-483c-a737-cf19988c6bc0" /> <br> Git Flow автоматически переключится на ветку develop и выполнит слияние.
6. Далее создадим релиз, для этого прописываем `git flow release start v1.0.0`: <br> <img width="500" alt="image" src="https://github.com/user-attachments/assets/13671c77-1cf8-4d4b-abf9-904737137177" /> <br>
7. Далее создадим текстовый файл version.txt, внесем туда изменения `echo "v1.0.0" > version.txt`. Добавим и закомиттим его.
8. Завершим релиз, прописав `git flow release finish v1.0.0`:<br> <img width="500" alt="image" src="https://github.com/user-attachments/assets/82b252d3-5738-403b-92c5-0eea12ef5df8" /> <br> Git Flow переключится на ветку main, выполнит слияние и создаст тег v1.0.0.
9. Создадим hotfix: `git flow hotfix start hotfix-1.0.1` <br> <img width="500" alt="image" src="https://github.com/user-attachments/assets/828a5bff-b371-4ace-98bd-02f78694cf28" /> <br>
Далее создадим, изменим, добавим, закомиттим файл file_with_error.py.
10. Далее завершим hotfix: <br> <img width="500" alt="image" src="https://github.com/user-attachments/assets/ebc4ce9c-df0f-42b2-8a49-5c53ffde066a" /><br>
11. Отправим изменения на удаленный репозиторий:<br> <img width="582" alt="image" src="https://github.com/user-attachments/assets/c14b8358-1602-4de1-b3d5-f94146995d04" />
