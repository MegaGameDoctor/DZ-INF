# Chapter 4
## 1
```python
a = [1, 2, 3]
b = [4, 5, 3]

def scalar(a, b):
    return a[0] * b[0] + a[1] * b[1] + a[2] * b[2]
def vector(a, b):
    return [
        a[1] * b[2] - a[2] * b[1],
        a[2] * b[0] - a[0] * b[2],
        a[0] * b[1] - a[1] * b[0]
    ]
print("Скалярное произведение:", scalar(a, b))
print("Векторное произведение:", vector(a, b))
```
## 2
Норвежец пьет воду
Японец держит зебру
## 3
```python
def tet(a, n):
    if n == 1:
        return a
    return a ** tet(a, n - 1)

print(tet(1,2))
```
## 4
```python
cok=["bk","br","rd",'or','yl','gr','bl','vi','gy','wh','au','ag',' ']
znah=[0,1,2,3,4,5,6,7,8,9,0,0]
mnog=[1,10,100,10**4,10**5,10**6,10**7,10**8,10**9,0,0,0]
otkl=[0,1,2,0,5,0.5,0.25,0.1,0.05,0,5,10]

def res(mac):
    if len(mac)<=3:
        return [None,None]
    if mac[0] not in cok or mac[1] not in cok or mac[2] not in cok or mac[3] not in cok :
        return [None,None]
    a=znah[cok.index(mac[0])]
    b=znah[cok.index(mac[1])]
    c=mnog[cok.index(mac[2])]
    d=otkl[cok.index(mac[3])]
    return [int(str(a)+str(b))*c,d]

print(res(['br', 'bk', 'yl', 'ag']))
print(res(['yl', 'vi', 'rd', 'au']))
print(res(['vi', 'yl', 'rd', 'gr']))
print(res(['ws', 'yl', 'rd', 'rd']))
print(res(['vi', 'yl', 'rd']))
```
## 5
```python
morse_code_dict = {
    'A': '.-', 'B': '-...', 'C': '-.-.', 'D': '-..', 'E': '.', 'F': '..-.',
    'G': '--.', 'H': '....', 'I': '..', 'J': '.---', 'K': '-.-', 'L': '.-..',
    'M': '--', 'N': '-.', 'O': '---', 'P': '.--.', 'Q': '--.-', 'R': '.-.',
    'S': '...', 'T': '-', 'U': '..-', 'V': '...-', 'W': '.--', 'X': '-..-',
    'Y': '-.--', 'Z': '--..', '1': '.----', '2': '..---', '3': '...--',
    '4': '....-', '5': '.....', '6': '-....', '7': '--...', '8': '---..',
    '9': '----.', '0': '-----', ',': '--..--', '.': '.-.-.-', '?': '..--..',
    '/': '-..-.', '-': '-....-', '(': '-.--.', ')': '-.--.-'
}
reverse_morse_code_dict = {}

for key, value in morse_code_dict.items():
    reverse_morse_code_dict[value] = key

def text_to_morse(text):
    text = text.upper()
    morse_code = []
    for char in text:
        if char == ' ':
            morse_code.append('/')
        elif char in morse_code_dict:
            morse_code.append(morse_code_dict[char])
    return ' '.join(morse_code)

def morse_to_text(morse):
    morse_words = morse.split(' / ')
    decoded_message = []
    for word in morse_words:
        morse_chars = word.split()
        decoded_word = ''.join([reverse_morse_code_dict[char] for char in morse_chars])
        decoded_message.append(decoded_word)
    return ' '.join(decoded_message)

text = "PYTHON 3"
morse_code = text_to_morse(text)
print(f"Текст в Морзе: {morse_code}")

decoded_text = morse_to_text(morse_code)
print(f"Расшифрованный: {decoded_text}")
```
## 6
```python
-
```
## 7
```python
def f(n,k):
    s=0
    for i in range(1,n+1):
        if k**i>n:
            break
        s+=n//k**i
    return s
print(f(11,2))
```
## 8
```python
def test(a, b):
    return sorted(str(a)) == sorted(str(b))

def f(k1):
    k2 = k1 + 1
    n = 1
    while True:
        if test(n * k1, n * k2):
            return n
        n += 1

print(f(100))
print(f(325))

```
## 9
```python
g = {}
file = open("iban_length.txt")
    for line in file:
        code, length = line.split()
        g[code] = int(length)

print(g)
```
