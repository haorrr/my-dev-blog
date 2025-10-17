---
title: "Java Collections Framework - Quản lý dữ liệu hiệu quả"
date: 2025-10-13
category: "Java"
image: "images/javacollection.jpg"
description: "Java Collections Framework cung cấp các cấu trúc dữ liệu mạnh mẽ như ArrayList, LinkedList, HashSet, HashMap, Queue. Tìm hiểu cách sử dụng, so sánh hiệu suất và best practices khi làm việc với Collections."
---

Java Collections Framework cung cấp các cấu trúc dữ liệu và algorithms để lưu trữ và xử lý nhóm objects một cách hiệu quả.

## Collections Framework Overview

Collections Framework bao gồm:
- **Interfaces**: Định nghĩa các kiểu collection
- **Implementations**: Các class cài đặt interfaces
- **Algorithms**: Methods để thực hiện các thao tác (sort, search, etc.)

## Các Interface chính

### List Interface

List là collection có thứ tự, cho phép phần tử trùng lặp.

**ArrayList**:
```java
List<String> fruits = new ArrayList<>();
fruits.add("Apple");
fruits.add("Banana");
fruits.add("Orange");
fruits.get(0); // "Apple"
```

**LinkedList**:
```java
List<Integer> numbers = new LinkedList<>();
numbers.add(1);
numbers.add(2);
numbers.addFirst(0); // Thêm vào đầu
```

**Khi nào dùng gì?**
- ArrayList: Truy cập nhanh theo index, thêm/xóa cuối
- LinkedList: Thêm/xóa đầu/giữa nhanh

### Set Interface

Set không cho phép phần tử trùng lặp.

**HashSet**:
```java
Set<String> uniqueNames = new HashSet<>();
uniqueNames.add("John");
uniqueNames.add("Jane");
uniqueNames.add("John"); // Bị bỏ qua
System.out.println(uniqueNames.size()); // 2
```

**TreeSet** (sắp xếp tự động):
```java
Set<Integer> sortedNumbers = new TreeSet<>();
sortedNumbers.add(5);
sortedNumbers.add(1);
sortedNumbers.add(3);
// Output: [1, 3, 5]
```

**LinkedHashSet** (giữ thứ tự thêm vào):
```java
Set<String> orderedSet = new LinkedHashSet<>();
orderedSet.add("First");
orderedSet.add("Second");
```

### Map Interface

Map lưu trữ cặp key-value.

**HashMap**:
```java
Map<String, Integer> ages = new HashMap<>();
ages.put("Alice", 25);
ages.put("Bob", 30);
ages.get("Alice"); // 25
ages.containsKey("Bob"); // true
```

**TreeMap** (keys được sắp xếp):
```java
Map<String, String> sortedMap = new TreeMap<>();
sortedMap.put("C", "Cat");
sortedMap.put("A", "Apple");
sortedMap.put("B", "Ball");
// Keys: [A, B, C]
```

**LinkedHashMap** (giữ thứ tự insertion):
```java
Map<String, Integer> orderedMap = new LinkedHashMap<>();
```

### Queue Interface

Queue theo nguyên tắc FIFO (First In First Out).

**PriorityQueue**:
```java
Queue<Integer> pq = new PriorityQueue<>();
pq.offer(5);
pq.offer(1);
pq.offer(3);
pq.poll(); // 1 (phần tử nhỏ nhất)
```

**ArrayDeque** (double-ended queue):
```java
Deque<String> deque = new ArrayDeque<>();
deque.addFirst("First");
deque.addLast("Last");
```

## Các thao tác phổ biến

### Duyệt qua Collections

**For-each loop**:
```java
for (String fruit : fruits) {
    System.out.println(fruit);
}
```

**Iterator**:
```java
Iterator<String> iterator = fruits.iterator();
while (iterator.hasNext()) {
    System.out.println(iterator.next());
}
```

**Stream API** (Java 8+):
```java
fruits.stream()
    .filter(f -> f.startsWith("A"))
    .forEach(System.out::println);
```

### Sắp xếp

```java
Collections.sort(fruits); // Tăng dần
Collections.sort(fruits, Collections.reverseOrder()); // Giảm dần

// Custom comparator
fruits.sort((a, b) -> a.length() - b.length());
```

### Tìm kiếm

```java
Collections.binarySearch(fruits, "Apple"); // Phải sort trước
fruits.contains("Banana"); // true/false
```

## So sánh hiệu suất

| Operation | ArrayList | LinkedList | HashSet | TreeSet |
|-----------|-----------|------------|---------|---------|
| Add | O(1) | O(1) | O(1) | O(log n) |
| Remove | O(n) | O(1) | O(1) | O(log n) |
| Search | O(n) | O(n) | O(1) | O(log n) |
| Access | O(1) | O(n) | N/A | N/A |

## Best Practices

1. Chọn collection phù hợp với use case
2. Sử dụng generics để type safety
3. Khởi tạo với capacity phù hợp nếu biết size
4. Sử dụng Stream API cho code ngắn gọn
5. Thread-safe: Dùng Collections.synchronizedXXX() hoặc concurrent collections

Collections Framework là công cụ mạnh mẽ giúp developers làm việc với dữ liệu hiệu quả hơn trong Java.