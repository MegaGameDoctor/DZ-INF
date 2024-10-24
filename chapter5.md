# Chapter 5
## 1 (С рыбами)
```python
sea_fish = ["shark", "flounder", "tuna", "cod", "herring", "Marlin"]
freshwater_fish = ["Asp", "Pike", "Carp", "Salmon", "Ide", "Trout"]

all_fish = sea_fish + freshwater_fish

capitalized_fish = []

for fish in all_fish:
    capitalized_fish.append(fish.capitalize())

s_capitalized_fish = sorted(capitalized_fish)

result = []
for fish in s_capitalized_fish:
    for original_fish in sea_fish:
        if fish == original_fish.capitalize():
            result.append(original_fish)
            break

    for original_fish in freshwater_fish:
        if fish == original_fish.capitalize():
            result.append(original_fish)
            break

print(result)
```
## 2 (Количество возможных цветов)
```python
flowers_set = ["rose", "jasmine", "lily"]
flowers_set1 = ["orchid", "tulip", "violet", "daisy"]
flowers_set2 = ["lavender", "sunflower"]

set1 = 2**(len(flowers_set))
set2 = 2**(len(flowers_set1))
set3 = 2**(len(flowers_set2))
res = set1 + set2 + set3
print(res)
```
## 3 (Выгодное золото)
```python
gold_prices_list = [
    [100, 120, 140, 160, 180, 200, 220],
    [200, 180, 160, 240, 260, 260, 210],
    [250, 230, 220, 190, 170, 150, 130],
    [200, 200, 200, 200, 200, 200],
    [150, 160, 155, 170, 180, 175, 165]
]


def max_profit(prices):
    min_price = prices[0]
    min_day = 1
    max_profit = 0
    maxx = 0
    mmn = 999
    buy_day = 1
    sell_day = 1

    for day in range(1, len(prices)):
        if prices[day] < min_price:
            min_price = prices[day]
            min_day = day + 1

        profit = prices[day] - min_price

        if profit > max_profit:
            max_profit = profit
            buy_day = min_day
            sell_day = day + 1

    return (sell_day, buy_day, max_profit)



for prices in gold_prices_list:
    print(max_profit(prices))
```
## 4 (Рюкзак)
```python
def calc(items, weight_limit):
    items = sorted([(value / weight, weight, value) for weight, value in items], reverse=True)

    total_value = 0
    remaning_weight = weight_limit

    for value_per_weight, weight, value in items:
        if remaning_weight >= weight:
            remaning_weight -= weight
            total_value += value
        continue

    return total_value, remaning_weight

items_1 = [(2, 10), (3, 15), (5, 30)]
weight_limit_1 = 5

items_2 = [(2, 10), (3, 15), (5, 30), (7, 20), (1, 5), (4, 10)]
weight_limit_2 = 10

items_3 = [(2, 20), (3, 15), (5, 30), (1, 25), (4, 10)]
weight_limit_3 = 7

items_4 = [(2, 5), (3, 8), (5, 15), (1, 3), (4, 10)]
weight_limit_4 = 7

items_5 = [(6, 10), (8, 15), (12, 30)]
weight_limit_5 = 5

print(calc(items_1, weight_limit_1))
print(calc(items_2, weight_limit_2))
print(calc(items_3, weight_limit_3))
print(calc(items_4, weight_limit_4))
print(calc(items_5, weight_limit_5))
```
## 5
```python
def fff(items, time_limit, weight_limit):
    sorted_items = []
    for value, time, weight in items:
        value_per_time = value / time
        value_per_weight = value / weight
        sorted_items.append((max(value_per_time, value_per_weight), value, time, weight))

    total_value = 0

    for sdf, value, time, weight in sorted_items:
        if time_limit >= time and weight_limit >= weight:
            time_limit -= time
            weight_limit -= weight
            total_value += value

    return total_value

items_1 = [(10, 5, 2), (15, 4, 3), (30, 7, 5)]
time_limit_1 = 10
weight_limit_1 = 10

items_2 = [(20, 6, 4), (15, 3, 3), (25, 5, 5), (10, 2, 2), (12, 4, 3)]
time_limit_2 = 12
weight_limit_2 = 10

items_3 = [(15, 5, 3), (12, 4, 2), (30, 7, 5), (25, 6, 4), (20, 3, 3)]
time_limit_3 = 15
weight_limit_3 = 12

items_4 = [(10, 4, 2), (20, 5, 3), (15, 3, 2), (25, 6, 4), (18, 4, 3)]
time_limit_4 = 13
weight_limit_4 = 11

print(fff(items_1, time_limit_1, weight_limit_1))
print(fff(items_2, time_limit_2, weight_limit_2))
print(fff(items_3, time_limit_3, weight_limit_3))
print(fff(items_4, time_limit_4, weight_limit_4))
```
## 6
```python
import random
import time


# Реализация сортировки слиянием
def merge_sort(arr):
    if len(arr) <= 1:
        return arr

    # Разделяем массив на две части
    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])

    # Сливаем отсортированные части
    return merge(left, right)


def merge(left, right):
    result = []
    i = j = 0

    # Сливаем два отсортированных подмассива
    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1

    # Добавляем оставшиеся элементы
    result.extend(left[i:])
    result.extend(right[j:])

    return result


# Реализация сортировки выбором
def selection_sort(arr):
    n = len(arr)
    for i in range(n):
        # Предполагаем, что текущий элемент минимальный
        min_index = i
        for j in range(i + 1, n):
            if arr[j] < arr[min_index]:
                min_index = j
        # Меняем местами минимальный элемент с текущей позицией
        arr[i], arr[min_index] = arr[min_index], arr[i]
    return arr


# Функция для генерации случайного списка заданной длины
def generate_random_list(length):
    return [random.randint(1, 1000) for _ in range(length)]


# Функция для тестирования алгоритмов сортировки
def test():
    # Сравнение эффективности алгоритмов на случайных списках разных размеров
    for size in [100, 1000, 10000, 100000]:
        arr = generate_random_list(size)

        # Измерение времени выполнения сортировки слиянием
        start_time = time.time()
        merge_sort(arr.copy())
        merge_sort_time = time.time() - start_time

        selection_sort(arr.copy())
        selection_sort_time = time.time() - start_time

        print(f"Размер списка: {size}")
        print(f"Время выполнения сортировки слиянием: {merge_sort_time:.5f} сек")
        print(f"Время выполнения сортировки выбором: {selection_sort_time}")
        print("=" * 50)


if __name__ == "__main__":
    test()
```
## Балльное задание (10 баллов) - Два массива и обмены
```python
def f(t, test):
    results = []

    for dddd in range(t):
        n, k = test[dddd][0]
        a = test[dddd][1]
        b = test[dddd][2]

        a.sort()
        b.sort(reverse=True)

        for i in range(min(k, n)):
            if b[i] > a[i]:
                a[i], b[i] = b[i], a[i]
            else:
                break

        results.append(sum(a))

    return results

t = int(input())
test = []
for aaaa in range(t):
    n, k = map(int, input().split())
    a = list(map(int, input().split()))
    b = list(map(int, input().split()))
    test.append(((n, k), a, b))

results = f(t, test)
for result in results:
    print(result)
```
## Балльное задание (10 баллов) - Числа Хэмминга
```python
def f(n):
    hn = [1]
    i2 = i3 = i5 = 0

    next_2 = 2
    next_3 = 3
    next_5 = 5

    while len(hn) < n:
        next_hamming = min(next_2, next_3, next_5)
        hn.append(next_hamming)

        if next_hamming == next_2:
            i2 += 1
            next_2 = hn[i2] * 2
        if next_hamming == next_3:
            i3 += 1
            next_3 = hn[i3] * 3
        if next_hamming == next_5:
            i5 += 1
            next_5 = hn[i5] * 5

    return hn[-1]


print(f(1))
print(f(5000))
```
## Балльное задание (5 баллов) - Перемещение нулей в конец
```python
def move_zeros(lst):
    non_zeros = []
    for x in lst:
        if x != 0:
            non_zeros.append(x)

    zero_count = lst.count(0)

    return non_zeros + [0] * zero_count

# Тесты не определяются в pycharm-е, синтаксис в задании неверный
```
