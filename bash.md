# Задания по Bash
## Выведите Hello world в терминал
```bash
echo "Hello world"
```
## Выведите Hello world используя переменные
```bash
first="Hello"
second="world"
echo "$first $second"
```
## Выведите Hello world используя ввод пользователя
```bash
echo "Enter text:"
read text
echo "$text"
```
## Выведите Hello world используя ввод пользователя
```bash
echo "What are you doing?"
read action
echo "You are $action"
```
## Запуск скрипта
```bash
#!/bin/bash
deploy=false
uglify=false
while (( $# > 1 )); do case $1 in
--deploy) deploy="$2";;
--uglify) uglify="$2";;
*) break;
esac; shift 2
done
$deploy && echo "will deploy... deploy = $deploy"
$uglify && echo "will uglify... uglify = $uglify"
# how to run it ?
```
# Чтобы запустить - нужно использовать sh название.sh --deploy true --uglify true
## Список файлов без использования ls
```bash
for file in *; do
    echo "$file"
done
```
## Существует ли пользователь
```bash
read user

if grep -q "^$user:" /etc/passwd; then
    echo "The user $user Exists"
else
    echo "The user $user doesn’t exist"
fi
```
## Сравнение чисел
```bash
read input

if [ "$input" -gt "5" ]; then
    echo "The test value $input is greater than 5"
else
    echo "The test value $input is not greater than 5"
fi
```
## Проверка файлов
```bash
read mydir

if [ -d "$mydir" ]; then
    echo "The $mydir directory exists"
elif [ -e "$mydir" ]; then
    echo "The $mydir exists but is not a directory"
else
    echo "The $mydir directory does not exist"
fi
```
