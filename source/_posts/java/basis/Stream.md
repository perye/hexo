---
abbrlink: c8cecfcc
title: Stream
categories: Java
tags:
  - Stream
---

## 流创建
### 通过已有的集合来创建流
```java
List<String> strings = Arrays.asList("Hello", "World", "Hello1", "Hello2", "HelloWorld1", "HelloWorld2");
Stream<String> stream = strings.stream();
```

### 通过Stream创建流
```java
Stream<String> stream = Stream.of("Hello", "World", "Hello1", "Hello2", "HelloWorld1", "HelloWorld2");
```

## 流中间操作
### filter
filter 方法用于通过设置的条件过滤出元素。以下代码片段使用 filter 方法过滤掉空字符串
```java
List<String> strings = Arrays.asList("Hollis", "", "HollisChuang", "H", "hollis");
strings.stream().filter(string -> !string.isEmpty()).forEach(System.out::println);
//Hollis, HollisChuang, H, hollis
```

### map
map 方法用于映射每个元素到对应的结果，以下代码片段使用 map 输出了元素对应的平方数
```java
List<Integer> numbers = Arrays.asList(3, 2, 2, 3, 7, 3, 5);
numbers.stream().map(i -> i*i).forEach(System.out::println);
//9,4,4,9,49,9,25
```

### limit/skip
limit 返回 Stream 的前面 n 个元素；skip 则是扔掉前 n 个元素。以下代码片段使用 limit 方法保留4个元素：
```java
List<Integer> numbers = Arrays.asList(3, 2, 2, 3, 7, 3, 5);
numbers.stream().limit(4).forEach(System.out::println);
//3,2,2,3
```

### sorted
sorted 方法用于对流进行排序。以下代码片段使用 sorted 方法进行排序
```java
List<Integer> numbers = Arrays.asList(3, 2, 2, 3, 7, 3, 5);
numbers.stream().sorted().forEach(System.out::println);
//2,2,3,3,3,5,7
```

### distinct
distinct主要用来去重，以下代码片段使用 distinct 对元素进行去重：

```java
List<Integer> numbers = Arrays.asList(3, 2, 2, 3, 7, 3, 5);
numbers.stream().distinct().forEach(System.out::println);
//3,2,7,5
```

## 流最终操作

### forEach
Stream 提供了方法 'forEach' 来迭代流中的每个数据。以下代码片段使用 forEach 输出了10个随机数：
```java
Random random = new Random();
random.ints().limit(10).forEach(System.out::println);
```

### count
count用来统计流中的元素个数。

```java
List<String> strings = Arrays.asList("Hollis", "HollisChuang", "hollis", "Hollis666", "Hello", "HelloWorld", "Hollis");
System.out.println(strings.stream().count());
//7
```

### collect
collect就是一个归约操作，可以接受各种做法作为参数，将流中的元素累积成一个汇总结果：

```java

List<String> strings = Arrays.asList("Hollis", "HollisChuang", "hollis","Hollis666", "Hello", "HelloWorld", "Hollis");
strings  = strings.stream().filter(string -> string.startsWith("Hollis")).collect(Collectors.toList());
System.out.println(strings);
//Hollis, HollisChuang, Hollis666, Hollis

```
