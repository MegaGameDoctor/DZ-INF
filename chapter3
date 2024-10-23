# Chapter 3
## 25
```python
headers = ['name', 'shares', 'price']
converted = ['AA', 100, 32.2]

result = dict(zip(headers, converted))

print(result)
```
## 26
```python
pi = 2.0
for i in range(1, 10001):
    pi *= (4 * i ** 2) / (4 * i ** 2 - 1)

print(pi)
```
## 27
```python
def fff(n):
    ss = [0, 1]
    for i in range(2, n):
        ss.append(ss[-1] + ss[-2])
    return ss[:n]

print(fff(10))
```
## 28
```python
import math
a=6378137.0
c=6356752.314245
e=1-(c**2/a**2)
s=2*math.pi*a**2*(1+((1-e)/e**0.5)*math.atanh(e**0.5))
print (s)
```
## 29
```python
-
```
## 30
```python
k_B = 1.380649e-23
mu_e = -9.28476377e-24
N_A = 6.02214076e23
c = 2.99792458e8
G = 6.6743e-11
G_unc = 1.5e-15
mu_e_unc = 2.3e-31

print("kB = {:.1e} J/K;".format(k_B))
print("kB = {:.7e} J/K".format(k_B))
print("mu_e = {:.7e} J/T".format(mu_e))
print("N_A = {:.7e} mol^-1".format(N_A))
print("c = {:.7e} m/s".format(c))
print("G = {:.7e} [Nm^2/kg^2]  e = {:.7e} [J/T]".format(G, mu_e))
print("G = {:.5e}({:.0e}) Nm^2/kg^2".format(G, G_unc))
print("mu_e = {:.7e}({:.0e}) J/T".format(mu_e, mu_e_unc))

```
## 31
```python
-
```
## 32
```python
def hmm(s1, s2):
    return sum(1 for x, y in zip(s1, s2) if x != y)

s1 = "asdasdasdasda"
s2 = "xcvxcvdfffdfv"
distance = hmm(s1, s2)
print(distance)
```
## 33
```python
def df(n):
    result = 1
    for i in range(n, 0, -2):
        result *= i
    return result

n = 3 # С нечётным
print(df(n))

n = 2 # С чётным
print(df(n))
```
## 34
```python
-
```
## 35
```python
-
```
## 36
```python
-
```
## 37
```python
def fb(n):
    for i in range(1, n+1):
        if i % 3 == 0 and i % 5 == 0:
            print("FizzBuzz")
        elif i % 3 == 0:
            print("Fizz")
        elif i % 5 == 0:
            print("Buzz")
        else:
            print(i)

fb(100)
```
## 38
```python
-
```
## 39
```python
-
```
## 40
```python
-
```
## 41
```python
-
```
## 42
```python
def summa(n):
    sum = 0
    for i in str(n):
        sum  = sum + int(i)
    return sum

def factorial(n):
    result = 1
    for i in range(2, n + 1):
        result *= i
    return result

def small():
    n = 1
    while True:
        fact = factorial(n)
        if fact % summa(fact) != 0:
            return n
        n += 1

result = small()
print(result)
```
