## Лабораторная работа №2

Через терминал(с помощью команды touch) создал новый файл `lab_2.sh` в папке Informatics. Далее открыл его (через open), работал в приложении `Xcode`.

<img width="320" alt="image" src="https://github.com/user-attachments/assets/7e06ccbc-75b3-4a1c-8982-24c2993b9b89">

Зная решение на Python уже понимаю примерную схему решения и что оно должно содержать: на вход получаем и считываем строку -> через цикл переводим каждый октет в 2ую СС -> добавляем нули для 8 символов в каждом октете -> 
далее как то записываем в одну строку с точками ip адрес в 2й СС и выводим.

Начнем со считывания данных из строки в переменную, будем использовать метод `read -p текст_который_появится_на_экране имя_переменной` , считываем в переменную 'ip'.

Далее напишем основную функцию:

<img width="350" alt="image" src="https://github.com/user-attachments/assets/484adfed-5810-4cbf-b0f4-3ba25be1a685">

Объяснение:
- Создаем локальную переменную n, это будет аргумент функции.
- Создаем локальную переменную bin, пустую строку, в ней будет храниться двоичная запись.
- Цикл while, пока n не станет больше 0. Он вычисляет двоичный код, беря модуль n на 2 и добавляя его к bin.
- Еще один цикл while для дополнения двоичного числа нулями, пока длина не будет 8 символом.
- Вывод результата.

Далее условно функция main(), часть кода, которая считывает октеты в спиок с помощью опции `-а`, разделяя по точке, и применяет для каждого октета функцию dec_to_bin(). 

<img width="398" alt="image" src="https://github.com/user-attachments/assets/c7f82df9-f68a-4291-be15-b9558cc2ea08">

Переписываем массив октетов вместе с точками и выводим ответ:<br>
<img width="341" alt="image" src="https://github.com/user-attachments/assets/e94a62a8-611c-45a6-9585-b6728076f948">

Весь листинг кода:
```bash
#!/bin/bash

# Function to convert a decimal number to binary
dec_to_bin() {
    local n="$1"
    local bin=""
    while [ $n -gt 0 ]; do
        bin=$(( $n % 2 ))$bin
        n=$(( $n / 2 ))
    done
    # Check, if in octet <8 simbols, add 0
    while [ ${#bin} -lt 8 ]; do
        bin="0"$bin
    done
    echo "$bin"
}

# Read the IP address
read -p "Enter an IPv4 address in decimal format: " ip

# Convert each octet to binary and store in an array
IFS='.' read -r -a octets <<< "$ip"
binary_ip=()
for octet in "${octets[@]}"; do
    binary_ip+=($(dec_to_bin $octet))
done

# Join the binary octets with dots
binary_ip=$(IFS='.'; echo "${binary_ip[*]}")

# Output the binary IP address
echo "Binary format: $binary_ip"
```
