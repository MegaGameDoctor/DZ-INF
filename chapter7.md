# Chapter 7
## 1 (Сортировка)
```python
import random

def quick_sort_deck(deck):
    if len(deck) < 4:
        return sorted(deck)

    pivot = random.choice(deck)

    less_than_pivot = []
    equal_to_pivot = []
    greater_than_pivot = []

    for card in deck:
        if card < pivot:
            less_than_pivot.append(card)
        elif card == pivot:
            equal_to_pivot.append(card)
        else:
            greater_than_pivot.append(card)

    sorted_less = quick_sort_deck(less_than_pivot)
    sorted_greater = quick_sort_deck(greater_than_pivot)
    result = sorted_less + equal_to_pivot + sorted_greater

    return result

deck = [4, 2, 7, 1, 3, 5]
sorted_deck = quick_sort_deck(deck)
print(sorted_deck)
# Тест 1
assert quick_sort_deck([4, 2, 7, 1, 3, 5]) == [1, 2, 3, 4, 5, 7]
# Тест 2
assert quick_sort_deck([10, 5, 3, 8]) == [3, 5, 8, 10]
# Тест 3
assert quick_sort_deck([1]) == [1]
# Тест 4
assert quick_sort_deck([3, 2]) == [2, 3]
# Тест 5
assert quick_sort_deck([7, 3, 3, 4, 1, 2, 5]) == [1, 2, 3, 3, 4, 5, 7]
print("OK!")
```
## 2 (Сортировка пузырьком)
```python
def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        swapped = False
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swapped = True
        if not swapped:
            break
    return arr

numbers = [5, 2, 9, 1, 5, 6]
sorted_numbers = bubble_sort(numbers)
print(sorted_numbers)  # Ожидаемый вывод: [1, 2, 5, 5, 6, 9]
# Тест 1
assert bubble_sort([5, 2, 9, 1, 5, 6]) == [1, 2, 5, 5, 6, 9]
# Тест 2
assert bubble_sort([10, 7, 8, 9]) == [7, 8, 9, 10]
# Тест 3
assert bubble_sort([1]) == [1]
# Тест 4
assert bubble_sort([3, 3, 3, 2, 2]) == [2, 2, 3, 3, 3]
# Тест 5
assert bubble_sort([]) == []
print("OK!")
```
## 3 (Сортировка вставками)
```python
def insertion_sort(arr):
    for i in range(1, len(arr)):
        current_value = arr[i]
        j = i - 1
        while j >= 0 and arr[j] > current_value:
            arr[j + 1] = arr[j]
            j -= 1
        arr[j + 1] = current_value

    return arr

# Пример использования
grades = [5, 2, 9, 1, 5, 6]
sorted_grades = insertion_sort(grades)
print(sorted_grades)  # Ожидаемый вывод: [1, 2, 5, 5, 6, 9]
# Тест 1
assert insertion_sort([5, 2, 9, 1, 5, 6]) == [1, 2, 5, 5, 6, 9]
# Тест 2
assert insertion_sort([10, 7, 8, 9]) == [7, 8, 9, 10]
# Тест 3
assert insertion_sort([1]) == [1]
# Тест 4
assert insertion_sort([3, 3, 3, 2, 2]) == [2, 2, 3, 3, 3]
# Тест 5
assert insertion_sort([]) == []
print("OK!")

```
## 4 (Сортировка слиянием)
```python
def merge_sort(arr):
    if len(arr) <= 1:
        return arr
    mid = len(arr) // 2
    left_half = merge_sort(arr[:mid])
    right_half = merge_sort(arr[mid:])
    return merge(left_half, right_half)

def merge(left, right):
    sorted_arr = []
    i = j = 0
    while i < len(left) and j < len(right):
        if left[i] < right[j]:
            sorted_arr.append(left[i])
            i += 1
        else:
            sorted_arr.append(right[j])
            j += 1

    while i < len(left):
        sorted_arr.append(left[i])
        i += 1

    while j < len(right):
        sorted_arr.append(right[j])
        j += 1

    return sorted_arr

# Пример использования
numbers = [38, 27, 43, 3, 9, 82, 10]
sorted_numbers = merge_sort(numbers)
print(sorted_numbers)  # Ожидаемый вывод: [3, 9, 10, 27, 38, 43, 82]
# Тест 1
assert merge_sort([38, 27, 43, 3, 9, 82, 10]) == [3, 9, 10, 27, 38, 43, 82]
# Тест 2
assert merge_sort([10, 7, 8, 9]) == [7, 8, 9, 10]
# Тест 3
assert merge_sort([1]) == [1]
# Тест 4
assert merge_sort([3, 3, 3, 2, 2]) == [2, 2, 3, 3, 3]
# Тест 5
assert merge_sort([]) == []
print("OK!")
```
## 5 (Сортировка Шелла)
```python
def shell_sort(arr):
    n = len(arr)
    gap = n // 2

    while gap > 0:
        for i in range(gap, n):
            temp = arr[i]
            j = i
            while j >= gap and arr[j - gap] > temp:
                arr[j] = arr[j - gap]
                j -= gap
            arr[j] = temp
        gap //= 2
    return arr

# Пример использования
numbers = [12, 34, 54, 2, 3]
sorted_numbers = shell_sort(numbers)
print(sorted_numbers)  # Ожидаемый вывод: [2, 3, 12, 34, 54]
# Тест 1
assert shell_sort([12, 34, 54, 2, 3]) == [2, 3, 12, 34, 54]
# Тест 2
assert shell_sort([10, 7, 8, 9]) == [7, 8, 9, 10]
# Тест 3
assert shell_sort([1]) == [1]
# Тест 4
assert shell_sort([3, 3, 3, 2, 2]) == [2, 2, 3, 3, 3]
# Тест 5
assert shell_sort([]) == []
print("Все тесты пройдены!")
```
## 6 (Линейный поиск)
```python
def linear_search(arr, target):
    n = len(arr)
    for i in range(n):
        if target == arr[i]:
            return i
    return -1

# Тест 1
assert linear_search([5, 3, 7, 1, 4], 1) == 3
# Тест 2
assert linear_search([10, 20, 30, 40], 30) == 2
# Тест 3
assert linear_search([1, 2, 3, 4], 5) == -1
# Тест 4
assert linear_search([1], 1) == 0
# Тест 5
assert linear_search([], 1) == -1
print("OK!")
```
## 7 (Бинарный поиск)
```python
def binary_search(arr, target):
    left = 0
    right = len(arr) - 1

    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid

        elif arr[mid] > target:
            right = mid - 1
        else:
            left = mid + 1

    return -1

# Пример использования
sorted_numbers = [1, 2, 3, 4, 5, 6, 7]
index_of_four = binary_search(sorted_numbers, 4)
print(index_of_four)  # Ожидаемый вывод: 3

index_of_eight = binary_search(sorted_numbers, 8)
print(index_of_eight)  # Ожидаемый вывод: -1
# Тест 1
assert binary_search([1, 2, 3, 4, 5, 6, 7], 4) == 3
# Тест 2
assert binary_search([1, 2, 3, 4, 5, 6, 7], 6) == 5
# Тест 3
assert binary_search([1, 2, 3, 4, 5, 6, 7], 1) == 0
# Тест 4
assert binary_search([1, 2, 3, 4, 5, 6, 7], 8) == -1
# Тест 5
assert binary_search([], 1) == -1  # Пустой массив
print("Все тесты пройдены!")
```
## 8 (Тенарный поиск)
```python
def ternary_search(arr, target):
    left = 0
    right = len(arr) - 1

    while left <= right:
        mid1 = left + (right - left) // 3
        mid2 = right - (right - left) // 3

        if arr[mid1] == target:
            return mid1
        if arr[mid2] == target:
            return mid2

        if target < arr[mid1]:
            right = mid1 - 1

        elif target > arr[mid2]:
            left = mid2 + 1

        else:
            left = mid1 + 1
            right = mid2 - 1

    return -1

# Пример использования
sorted_numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9]
index_of_five = ternary_search(sorted_numbers, 5)
print(index_of_five)  # Ожидаемый вывод: 4

index_of_ten = ternary_search(sorted_numbers, 10)
print(index_of_ten)  # Ожидаемый вывод: -1
# Тест 1
assert ternary_search([1, 2, 3, 4, 5, 6, 7, 8, 9], 5) == 4
# Тест 2
assert ternary_search([1, 2, 3, 4, 5, 6, 7, 8, 9], 3) == 2
# Тест 3
assert ternary_search([1, 2, 3, 4, 5, 6, 7, 8, 9], 1) == 0
# Тест 4
assert ternary_search([1, 2, 3, 4, 5, 6, 7, 8, 9], 10) == -1
# Тест 5
assert ternary_search([], 1) == -1  # Пустой массив
print("Все тесты пройдены!")
```
## 9 (BFS)
```python
def bfs(graph, start):
    v = []
    q = [start]
    while q:
        i = q.pop(0)
        if i not in v:
            v.append(i)
            q.extend([neighbor for neighbor in graph[i] if neighbor not in v])

    return v

# Тестовый граф в виде словаря смежности
graph = {
    'A': ['B', 'C'],
    'B': ['A', 'D', 'E'],
    'C': ['A', 'F', 'G'],
    'D': ['B'],
    'E': ['B', 'H'],
    'F': ['C'],
    'G': ['C', 'I'],
    'H': ['E'],
    'I': ['G']
}

# Тестовый пример
start_vertex = 'A'
result = bfs(graph, start_vertex)
print("Обход в ширину:", result)
# Ожидаемый результат: ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I']
```
## 10 (DFS)
```python
def dfs(graph, start):
    v = []
    q = [start]
    while q:
        i = q.pop()
        if i not in v:
            v.append(i)
            q.extend(reversed([neighbor for neighbor in graph[i] if neighbor not in v]))

    return v

# Тестовый граф в виде словаря смежности
graph = {
    'A': ['B', 'C'],
    'B': ['A', 'D', 'E'],
    'C': ['A', 'F', 'G'],
    'D': ['B'],
    'E': ['B', 'H'],
    'F': ['C'],
    'G': ['C', 'I'],
    'H': ['E'],
    'I': ['G']
}

# Тестовый пример
start_vertex = 'A'
result = dfs(graph, start_vertex)
print("Обход в глубину:", result)
# Ожидаемый результат: ['A', 'B', 'D', 'E', 'H', 'C', 'F', 'G', 'I']
```
## Балльное задание (15 баллов) - 123
```python

```
