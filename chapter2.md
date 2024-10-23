# Задания по Python + c++ (Chapter 2 - все)
## 1
# Python
```python
sm = int(input()) * 100
print("Distance in centimeters: " + str(sm))
```
# C++
```c++
#include <iostream>
using namespace std;

int main()
{
    int meter;
    cin >> meter;
    cout << "Distance in centimeters: " << meter * 100;
    return 0;
}
```
## 2
# Python
```python
kilometers = int(input())
meters = int(input())
if kilometers * 1000 > meters:
    print(kilometers)
else:
    print(meters)
```
# C++
```c++
#include <iostream>
using namespace std;

int main()
{
    int kilometers;
    cin >> kilometers;
    int meters;
    cin >> meters;
    if (kilometers * 1000 > meters) {
        cout << kilometers;
    } else {
        cout << meters;
    }
    return 0;
}
```
## 3
# Python
```python
m = []

for a in range(10):
    m.append(a)

number = int(input())
for part in m:
    print(str(number) + " * " + str(part) + " = " + str(number * part))
```
# C++
```c++
#include <iostream>
using namespace std;

int main()
{
    int n;
    cin >> n;
    for (int i = 0; i < 10; i++) {
        cout << n << " * " << i << " = " << n * i << endl;
    }
    
    return 0;
}
```
## 4
# Python
```python
a = int(input())
b = int(input())

if b % a == 0:
    print("Число a является делителем числа b")
else:
    print("Число a не является делителем числа b")
```
# C++
```c++
#include <iostream>
using namespace std;

int main()
{
    int a;
    int b;
    cin >> a;
    cin >> b;

if (b % a == 0) {
    cout << "Число a является делителем числа b";
} else {
    cout << "Число a не является делителем числа b";
}
    
    return 0;
}
```
## 5
# Python
```python
number = int(input())

print("Thats the number you entered: " + str(number))
```
# C++
```c++
#include <iostream>
using namespace std;

int main()
{
    int number;
    cin >> number;
    
    cout << "Thats the number you entered: " << number;
    
    return 0;
}
```
## 6
# Python
```python
m = int(input())
n = int(input())

if m > n:
    print("Number " + str(m) + " > " + str(n))
else:
    if m < n:
        print("Number " + str(m) + " < " + str(n))
    else:
        print("The numbers are equal")
```
# C++
```c++
#include <iostream>
using namespace std;

int main()
{
    int m,n;
    cin >> m;
    cin >> n;

if (m > n) {
    cout << "Number " << m << " > " << n;
} else if (m < n) {
    cout << "Number " << m << " < " << n;
} else {
    cout << "The numbers are equal";
}
    return 0;
}
```
## 7
# Python
```python
radius = int(input())
print("Диаметр: " + str(radius * 2))

sum = 0
for i in range(100, 501):
    sum += i
print("Сумма всех целых чисел от 100 до 500: " + str(sum))

sum = 0
intI = int(input())
if intI < 500:
    for i in range(intI, 501):
        sum += i
    print("Сумма всех целых чисел от " + str(intI) + " до 500: " + str(sum))
```
# C++
```c++
#include <iostream>
using namespace std;

int main()
{
    int radius;
    cin >> radius;
    cout << "Диаметр: " << radius * 2 << endl;

int sum = 0;
for (int i = 100; i <= 500; i++) {
    sum += i;
}
cout << "Сумма всех целых чисел от 100 до 500: " << sum << endl;

sum = 0;
int intI;
cin >> intI;
if (intI < 500) {
    for (int i = intI; i <= 500; i++) {
        sum += i;
    }
    cout << "Сумма всех целых чисел от " << intI << " до 500: " << sum;
}
    return 0;
}
```
## 8
# Python
```python
print("Введите Ваше имя:")
name = input()
print("Hello, " + name)
```
# C++
```c++
#include <iostream>
using namespace std;

int main()
{
    cout << "Введите Ваше имя:" << endl;
    string name;
    cin >> name;
    cout << "Hello, " << name;
    return 0;
}
```
## 9
# Python
```python
a = int(input())
b = int(input())
c = int(input())

m = max(a,b,c)
print("Максимальное: " + str(m))
```
# C++
```c++
#include <iostream>
using namespace std;

int main()
{
    int a,b,c,m;
    cin >> a;
    cin >> b;
    cin >> c;
    m = max(c, max(a,b));
    cout << "Максимальное: " << m;
    return 0;
}
```
## 10
# Python
```python
first = int(input())
second = int(input())
temp = first
first = second
second = temp

print("Новые значения: first=" + str(first) + ", second=" + str(second))
```
# C++
```c++
#include <iostream>
using namespace std;

int main()
{
    int first, second, temp;
    cin >> first;
    cin >> second;
    temp = first;
    first = second;
    second = temp;

    cout << "Новые значения: first=" << first << ", second=" << second;
    return 0;
}
```
## 11
# Python
```python
mass = [10, -3, -5, 2, 5]
index = 0
mini = min(mass)
for el in mass:
    if el == mini:
        print(index)
        break
    index += 1
```
# C++
```c++
#include <iostream>
using namespace std;

int main()
{
    int mass[] = {10, -3, -5, 2, 5};
    int index = 0;
    int mini = 99999999;
    for (int el : mass) {
        if(el < mini) {
            mini = el;
        }
    }
    for (int el : mass) {
        if (el == mini) {
            cout << index;
            break;
        }
        index++;
    }
    return 0;
}
```
## 12
# Python
```python
def toB(kb):
    return kb * 1024

def toKB(b):
    return b / 1024

print("Введите число для конвертации:")
number = int(input())
print("Выберите действие (1 - В килобайты, 2 - В байты)")
choice = input()

if choice == "1":
    print("Результат в КБ: " + str(toKB(number)))
else:
    print("Результат в Б: " + str(toB(number)))
```
# C++
```c++
#include <iostream>
using namespace std;

int toB(int kb) {
return kb * 1024;
}

int toKB(int b) {
return b / 1024;
}

int main()
{
    cout << "Введите число для конвертации:" << endl;
    int number, choice;
    cin >> number;
    cout << "Выберите действие (1 - В килобайты, 2 - В байты)" << endl;
    cin >> choice;
    if (choice == 1) {
        cout << "Результат в КБ: " << toKB(number);
    } else {
        cout << "Результат в Б: " << toB(number);
    }
    return 0;
}
```
## 13
# Python
```python
print("Введите своё имя:")
name = input()
print("Введите свой возраст:")
age = int(input())
print(name + ", через " + str(100 - age) + " лет Вам будет 100 лет")
```
# C++
```c++
#include <iostream>
using namespace std;

int main()
{
    cout << "Введите своё имя:" << endl;
    string name;
    cin >> name;
    cout << "Введите свой возраст:" << endl;
    int age;
    cin >> age;
    cout << name << ", через " << (100 - age) << " лет Вам будет 100 лет";
    return 0;
}
```
## 14
# Python
```python
import os

print("Введите любую команду:")
os.system(input())
```
# C++
```c++
-
```
