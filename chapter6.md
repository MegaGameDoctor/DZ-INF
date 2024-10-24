# Chapter 6
## 1 (Stack)
```python
class Stack:
    def __init__(self):
        self.items = []

    def is_empty(self):
        return len(self.items) == 0

    def push(self, item):
        self.items.append(item)

    def pop(self):
        return self.items.pop() if not self.is_empty() else None

    def peek(self):
        return self.items[-1] if not self.is_empty() else None

    def size(self):
        return len(self.items)

my_stack = Stack()

my_stack.push(1)
my_stack.push(2)
my_stack.push(3)

print("Stack:", my_stack.items)

popped_item = my_stack.pop()
print("Popped item:", popped_item)

top_item = my_stack.peek()
print("Top item:", top_item)

print("Is stack empty?", my_stack.is_empty())

print("Stack size:", my_stack.size())
```
## 2 (Queue)
```python
class Queue:
    def __init__(self):
        self.items = []

    def is_empty(self):
        return len(self.items) == 0

    def enqueue(self, item, priority=5):
        self.items.append((item, priority))

    def dequeue(self):
        if self.is_empty():
            return None
        # Sort items by priority and return the one with the highest priority (lowest number)
        self.sort_queue()
        return self.items.pop(0)[0]

    def front(self):
        if self.is_empty():
            return None
        # Sort to find the front item
        self.sort_queue()
        return self.items[0][0]

    def size(self):
        return len(self.items)

    def sort_queue(self):
        self.items.sort(key=lambda x: x[1])  # Sort by priority

# Example usage:
my_queue = Queue()

my_queue.enqueue(1, priority=2)
my_queue.enqueue(2, priority=5)
my_queue.enqueue(3, priority=0)

print("Queue:", my_queue.items)

# Dequeue an item from the queue
dequeued_item = my_queue.dequeue()
print("Dequeued item:", dequeued_item)

# Get the front of the queue
front_item = my_queue.front()
print("Front item:", front_item)

# Enqueue a new item with priority
my_queue.enqueue(4, priority=3)
print("Queue after enqueue:", my_queue.items)

# Check if the queue is empty
print("Is queue empty?", my_queue.is_empty())

# Get the size of the queue
print("Queue siz.e:", my_queue.size())
```
## 3 (Linked List)
```python
class Node:
    def __init__(self, data=None):
        self.data = data
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None

    def is_empty(self):
        return self.head is None

    def append(self, data):
        new_node = Node(data)
        if self.is_empty():
            self.head = new_node
            return
        current = self.head
        while current.next:
            current = current.next
        current.next = new_node

    def prepend(self, data):
        new_node = Node(data)
        new_node.next = self.head
        self.head = new_node

    def delete(self, data):
        if self.is_empty():
            return
        if self.head.data == data:
            self.head = self.head.next
            return
        current = self.head
        while current.next:
            if current.next.data == data:
                current.next = current.next.next
                return
            current = current.next

    def display(self):
        current = self.head
        elements = []
        while current:
            elements.append(current.data)
            current = current.next
        print("Linked List:", elements)

# Example usage:
my_linked_list = LinkedList()

my_linked_list.append(1)
my_linked_list.append(2)
my_linked_list.append(3)

my_linked_list.prepend(0)

my_linked_list.display()  # Output: Linked List: [0, 1, 2, 3]

my_linked_list.delete(2)

my_linked_list.display()  # Output: Linked List: [0, 1, 3]
```
## 4 (Unorder map)
```python
class KeyValuePair:
    def __init__(self, key, value):
        self.key = key
        self.value = value

class UnorderedMap:
    def __init__(self, size=10):
        self.size = size
        self.buckets = [[] for _ in range(size)]

    def _hash(self, key):
        return len(key) % self.size

    def set(self, key, value):
        index = self._hash(key)
        # Check if the key already exists and update
        for kvp in self.buckets[index]:
            if kvp.key == key:
                kvp.value = value
                return
        # If key doesn't exist, add a new key-value pair
        self.buckets[index].append(KeyValuePair(key, value))

    def get(self, key, default=None):
        index = self._hash(key)
        for kvp in self.buckets[index]:
            if kvp.key == key:
                return kvp.value
        return default

    def remove(self, key):
        index = self._hash(key)
        bucket = self.buckets[index]
        for i, kvp in enumerate(bucket):
            if kvp.key == key:
                del bucket[i]
                return

    def keys(self):
        all_keys = []
        for bucket in self.buckets:
            for kvp in bucket:
                all_keys.append(kvp.key)
        return all_keys

    def values(self):
        all_values = []
        for bucket in self.buckets:
            for kvp in bucket:
                all_values.append(kvp.value)
        return all_values

    def items(self):
        all_items = []
        for bucket in self.buckets:
            for kvp in bucket:
                all_items.append((kvp.key, kvp.value))
        return all_items

# Example usage:
my_map = UnorderedMap()

my_map.set("name", "John")
my_map.set("age", 25)
my_map.set("city", "Example City")

print("Keys:", my_map.keys())          # Output: Keys: ['name', 'age', 'city']
print("Values:", my_map.values())      # Output: Values: ['John', 25, 'Example City']
print("Items:", my_map.items())        # Output: Items: [('name', 'John'), ('age', 25), ('city', 'Example City')]

# Accessing values by key
print("Name:", my_map.get("name"))     # Output: Name: John
print("Gender:", my_map.get("gender", "Not specified"))  # Output: Gender: Not specified

# Removing a key-value pair
my_map.remove("age")

print("Keys after removing 'age':",  my_map.keys())
```
## 5 (Unordered Set)
```python
class UnorderedSet:
    def __init__(self, size=10):
        self.size = size
        self.buckets = [[] for _ in range(size)]

    def _hash(self, value):
        # A simple hash function for integers
        return hash(value) % self.size

    def add(self, value):
        index = self._hash(value)
        if not self.contains(value):
            self.buckets[index].append(value)

    def remove(self, value):
        index = self._hash(value)
        bucket = self.buckets[index]
        if value in bucket:
            bucket.remove(value)

    def contains(self, value):
        index = self._hash(value)
        return value in self.buckets[index]

    def elements(self):
        all_elements = []
        for bucket in self.buckets:
            all_elements.extend(bucket)
        return all_elements

# Example usage:
my_set = UnorderedSet()

my_set.add(1)
my_set.add(2)
my_set.add(3)

print("Elements:", my_set.elements())  # Output: Elements: [1, 2, 3]

# Check if a value is in the set
value_to_check = 2
print(f"Is {value_to_check} in the set? {my_set.contains(value_to_check)}")  # Output: Is 2 in the set? True

# Remove a value from the set
value_to_remove = 1
my_set.remove(value_to_remove)

print("Elements after removing 1:", my_set.elements())  # Output: Elements after removing 1: [2, 3]
```
## 6 (Binary Tree)
```python
class TreeNode:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

class BinaryTree:
    def __init__(self):
        self.root = None

    def insert(self, data):
        if self.root is None:
            self.root = TreeNode(data)
        else:
            self._insert_recursively(self.root, data)

    def _insert_recursively(self, node, data):
        if data < node.data:
            if node.left is None:
                node.left = TreeNode(data)
            else:
                self._insert_recursively(node.left, data)
        else:
            if node.right is None:
                node.right = TreeNode(data)
            else:
                self._insert_recursively(node.right, data)

    def search(self, data):
        return self._search_recursively(self.root, data)

    def _search_recursively(self, node, data):
        if node is None or node.data == data:
            return node
        if data < node.data:
            return self._search_recursively(node.left, data)
        return self._search_recursively(node.right, data)

    def in_order_traversal(self):
        result = []
        self._in_order_recursively(self.root, result)
        return result

    def _in_order_recursively(self, node, result):
        if node:
            self._in_order_recursively(node.left, result)
            result.append(node.data)
            self._in_order_recursively(node.right, result)

    def pre_order_traversal(self):
        result = []
        self._pre_order_recursively(self.root, result)
        return result

    def _pre_order_recursively(self, node, result):
        if node:
            result.append(node.data)
            self._pre_order_recursively(node.left, result)
            self._pre_order_recursively(node.right, result)

    def post_order_traversal(self):
        result = []
        self._post_order_recursively(self.root, result)
        return result

    def _post_order_recursively(self, node, result):
        if node:
            self._post_order_recursively(node.left, result)
            self._post_order_recursively(node.right, result)
            result.append(node.data)

# Пример использования
tree = BinaryTree()
tree.insert(10)
tree.insert(5)
tree.insert(15)

print(tree.search(5))  # Ожидаемый вывод: <__main__.TreeNode object at ...>
print(tree.search(20))  # Ожидаемый вывод: None

print(tree.in_order_traversal())  # Ожидаемый вывод: [5, 10, 15]
print(tree.pre_order_traversal())  # Ожидаемый вывод: [10, 5, 15]
print(tree.post_order_traversal())  # Ожидаемый вывод: [5, 15, 10]
```
## 7 (Hashmap)
```python
class HashMap:
    def __init__(self, size=10):
        self.size = size
        self.slots = [None] * size  # Storage for keys
        self.data = [None] * size    # Storage for values

    # Private method to compute the hash value of a key
    def _hash(self, key):
        # A simple hash function using the built-in hash and modulo operation
        return hash(key) % self.size

    # Public method to add or update a key-value pair
    def put(self, key, value):
        hash_value = self._hash(key)
        # Linear probing for collision resolution
        while self.slots[hash_value] is not None:
            if self.slots[hash_value] == key:
                self.data[hash_value] = value  # Update existing value
                return
            hash_value = (hash_value + 1) % self.size
        self.slots[hash_value] = key  # Store the key
        self.data[hash_value] = value  # Store the value

    # Public method to retrieve a value by its key
    def get(self, key, default=None):
        hash_value = self._hash(key)
        # Linear probing to find the key
        while self.slots[hash_value] is not None:
            if self.slots[hash_value] == key:
                return self.data[hash_value]  # Return the found value
            hash_value = (hash_value + 1) % self.size
        return default  # Return default if key not found

    # Public method to remove a key-value pair
    def remove(self, key):
        hash_value = self._hash(key)
        while self.slots[hash_value] is not None:
            if self.slots[hash_value] == key:
                self.slots[hash_value] = None  # Remove the key
                self.data[hash_value] = None    # Remove the value
                return
            hash_value = (hash_value + 1) % self.size

    # Public method to get a list of keys
    def keys(self):
        return [key for key in self.slots if key is not None]

    # Public method to get a list of values
    def values(self):
        return [value for value in self.data if value is not None]

    # Public method to get a list of key-value pairs
    def items(self):
        return [(self.slots[i], self.data[i]) for i in range(self.size) if self.slots[i] is not None]

my_hashmap = HashMap() 
my_hashmap.put("name", "John") 
my_hashmap.put("age", 25) 
my_hashmap.put("city", "Example City") 

print("Keys:", my_hashmap.keys())  
print("Values:", my_hashmap.values())  
print("Items:", my_hashmap.items())  

print("Name:", my_hashmap.get("name"))  
print("Gender:", my_hashmap.get("gender", "Not specified")) 


my_hashmap.remove("age") 
print("Keys after removing 'age':", my_hashmap.keys())
```
## 8 (Map)
```python
class SimpleMap:
    def __init__(self):
        self.items = []

    def set(self, key, value):
        for i, (k, v) in enumerate(self.items):
            if k == key:
                self.items[i] = (key, value)
                return
        self.items.append((key, value))

    def get(self, key, default=None):
        for k, v in self.items:
            if k == key:
                return v
        return default

    def remove(self, key):
        for i, (k, _) in enumerate(self.items):
            if k == key:
                del self.items[i]
                return

    def keys(self):
        return [k for k, _ in self.items]

    def values(self):
        return [v for _, v in self.items]

    def items(self):
        return self.items[:]

# Example usage:
my_map = SimpleMap()

my_map.set("name", "John")
my_map.set("age", 25)
my_map.set("city", "Example City")

print("Keys:", my_map.keys())
print("Values:", my_map.values())
print("Items:", my_map.items)

print("Name:", my_map.get("name"))
print("Gender:", my_map.get("gender", "Not specified"))

my_map.remove("age")

print("Keys after removing 'age':", my_map.keys())
```
## 9 (Heap)
```python
class Heap:
    def __init__(self, max_heap=True):
        self.heap = []
        self.max_heap = max_heap

    def is_empty(self):
        return len(self.heap) == 0

    def size(self):
        return len(self.heap)

    def insert(self, value):
        self.heap.append(value)
        self._heapify_up(len(self.heap) - 1)

    def extract(self):
        if self.is_empty():
            return None
        if len(self.heap) == 1:
            return self.heap.pop()
        root = self.heap[0]
        self.heap[0] = self.heap.pop()
        self._heapify_down(0)
        return root

    def peek(self):
        if self.is_empty():
            return None
        return self.heap[0]

    def _heapify_up(self, index):
        parent_index = (index - 1) // 2
        if index > 0 and self._compare(self.heap[index], self.heap[parent_index]):
            self.heap[index], self.heap[parent_index] = self.heap[parent_index], self.heap[index]
            self._heapify_up(parent_index)

    def _heapify_down(self, index):
        left_index = 2 * index + 1
        right_index = 2 * index + 2
        largest_index = index

        if left_index < len(self.heap) and self._compare(self.heap[left_index], self.heap[largest_index]):
            largest_index = left_index
        if right_index < len(self.heap) and self._compare(self.heap[right_index], self.heap[largest_index]):
            largest_index = right_index

        if largest_index != index:
            self.heap[index], self.heap[largest_index] = self.heap[largest_index], self.heap[index]
            self._heapify_down(largest_index)

    def _compare(self, child, parent):
        return child > parent if self.max_heap else child < parent

# Пример использования
h = Heap(max_heap=True)

h.insert(10)
h.insert(4)
h.insert(15)
h.insert(20)
h.insert(3)

print("Корень кучи:", h.peek())  # Ожидаемый вывод: 20

while not h.is_empty():
    print("Извлеченный элемент:", h.extract())
```
## Балльное задание (15 баллов) - Sparse Table
```python
import math

class SparseTable:
    def __init__(self, array):
        self.n = len(array)  # Длина входного массива
        self.log = math.floor(math.log2(self.n)) + 1  # Максимальная степень двойки
        self.st = [[0] * self.log for _ in range(self.n)]  # Инициализируем таблицу
        self.build(array)

    def build(self, array):
        for i in range(self.n):
            self.st[i][0] = array[i]
        j = 1
        while (1 << j) <= self.n:
            i = 0
            while (i + (1 << j) - 1) < self.n:
                self.st[i][j] = min(self.st[i][j - 1], self.st[i + (1 << (j - 1))][j - 1])
                i += 1
            j += 1

    def query(self, left, right):
        length = right - left + 1
        j = math.floor(math.log2(length))  # Находим максимальную степень двойки, которая помещается в диапазон
        return min(self.st[left][j], self.st[right - (1 << j) + 1][j])

# Пример использования
array = [1, 3, 2, 7, 9, 11]
sparse_table = SparseTable(array)

# Запросы на нахождение минимума
print(sparse_table.query(1, 4))  # Ожидаемый вывод: 2
print(sparse_table.query(0, 5))  # Ожидаемый вывод: 1
print(sparse_table.query(2, 2))  # Ожидаемый вывод: 2
```
## Балльное задание (10 баллов) - Двухсвязный список
```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None
        self.prev = None


class DoublyLinkedList:
    def __init__(self):
        self.head = None

    # Добавление в конец списка
    def append(self, data):
        new_node = Node(data)
        if not self.head:
            self.head = new_node
            return
        current = self.head
        while current.next:
            current = current.next
        current.next = new_node
        new_node.prev = current

    # Добавление в начало списка
    def prepend(self, data):
        new_node = Node(data)
        if not self.head:
            self.head = new_node
            return
        new_node.next = self.head
        self.head.prev = new_node
        self.head = new_node

    # Удаление первого узла с заданными данными
    def delete(self, data):
        if not self.head:
            return

        current = self.head

        # Если голова содержит данные, которые нужно удалить
        if current.data == data:
            self.head = current.next
            if self.head:
                self.head.prev = None
            return

        while current and current.data != data:
            current = current.next

        # Если нашли узел с нужными данными
        if current:
            if current.next:
                current.next.prev = current.prev
            if current.prev:
                current.prev.next = current.next

    # Вывод элементов списка от начала до конца
    def display(self):
        current = self.head
        while current:
            print(current.data, end=" <-> ")
            current = current.next
        print("None")

    # Вывод элементов списка от конца до начала
    def display_reverse(self):
        if not self.head:
            print("None")
            return

        # Перемещаемся в конец списка
        current = self.head
        while current.next:
            current = current.next

        # Идем с конца к началу
        while current:
            print(current.data, end=" <-> ")
            current = current.prev
        print("None")


# Пример использования
dll = DoublyLinkedList()
dll.append(1)
dll.append(2)
dll.append(3)
dll.display()  # Ожидаемый вывод: 1 <-> 2 <-> 3 <-> None

dll.prepend(0)
dll.display()  # Ожидаемый вывод: 0 <-> 1 <-> 2 <-> 3 <-> None

dll.delete(2)
dll.display()  # Ожидаемый вывод: 0 <-> 1 <-> 3 <-> None

dll.display_reverse()  # Ожидаемый вывод: 3 <-> 1 <-> 0 <-> None
```
## Балльное задание (10 баллов) - Queue
```python
class Queue:
    def __init__(self):
        self.items = []

    def is_empty(self):
        if len(self.items)==0:
            return True
        else:
            return False
    def enqueue(self, item, priority=5):
        self.items.append([item,priority])
        return self.items
    def dequeue(self):
        i1=0
        for i,j in self.items:
            if j==0:
                return self.items.pop(i1)
            i1 += 1
    def front(self):
        if len(self.items)!=0:
            return self.items[0]
    def size(self):
        return len(self.items)

    def sort_queue(self):
        i1=0
        for i,j in self.items:
            self.items[i1]=[j,i]
            i1+=1
        self.items=sorted(self.items)
        i1 = 0
        for i, j in self.items:
            self.items[i1] = [j,i]
            i1 += 1
        return self.items

# Example usage:
my_queue = Queue()

my_queue.enqueue(1, priority=2)
my_queue.enqueue(2, priority=5)
my_queue.enqueue(3, priority=0)

print("Queue:", my_queue.items)

# Dequeue an item from the queue
dequeued_item = my_queue.dequeue()
print("Dequeued item:", dequeued_item)

# Get the front of the queue
front_item = my_queue.front()
print("Front item:", front_item)

# Enqueue a new item with priority
my_queue.enqueue(4, priority=3)
print("Queue after enqueue:", my_queue.items)

# Check if the queue is empty
print("Is queue empty?", my_queue.is_empty())

# Get the size of the queue
print("Queue size:", my_queue.size())
print("sort_queue:", my_queue.sort_queue())
```

## Обратите внимание: Многие из этих заданий были выполнены с использованием открытых источников GitHub. Заимствованная информация изучена и усвоена
