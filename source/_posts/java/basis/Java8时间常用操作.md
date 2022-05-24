---
title: Java8时间常用操作
top: false
cover: false
categories: Java
tags:
  - time
keywords: Markdown
abbrlink: a8f5cf9e
date: 2020-9-27 16:18:22
---

## 常用方法总结

### 获取当前时间

```java
// 当前日期：2020-09-27
LocalDate date = LocalDate.now();

// 当前时间：16:30:23.126
LocalTime time = LocalTime.now();

// 当前日期和时间：2020-09-27T16:30:23.126
LocalDateTime dateTime = LocalDateTime.now();
```

### 月份的第一天和最后一天

```java
LocalDate now = LocalDate.now();
// 本月第一天： 2020-09-01
LocalDate begin = now.with(TemporalAdjusters.firstDayOfMonth());
// 本月最后一天：2020-09-30
LocalDate end = now.with(TemporalAdjusters.lastDayOfMonth());
```

### 下一月的第一天和下一年的第一天

```java
LocalDate now = LocalDate.now();
// 下一个月的第一天：2020-10-01
LocalDate nextMonthBegin = now.with(TemporalAdjusters.firstDayOfNextMonth());
// 下一年的第一天：2021-01-01
LocalDate nextYearBegin = now.with(TemporalAdjusters.firstDayOfNextYear());
```

### 获取当前年第一个周一的日期

```java
LocalDate now = LocalDate.now();
// 获取当前年的第一天
LocalDate begin = now.with(TemporalAdjusters.firstDayOfYear());
// 获取当前年的第一个周一所在的日期：2020-01-06
LocalDate date = LocalDate.parse(begin.toString()).with(TemporalAdjusters.firstInMonth(DayOfWeek.MONDAY));
```

### 指定时间的后几天日期

```java
LocalDate now = LocalDate.now();
// 当前时间的后两天： 2020-09-29
LocalDate date1 = now.plusDays(2);
// 当前时间的后两月：2020-11-27
LocalDate date2 = now.plusMonths(2);
```

### 计算两个日期相距

```java
LocalDate now = LocalDate.now();
// 实例化一个时间
LocalDate of = LocalDate.of(2013, 6, 26);
// 相距多少年
long until = of.until(now, ChronoUnit.YEARS);
// 相距多少月
long until2 = of.until(now, ChronoUnit.MONTHS);
// 相距多少天
long until3 = of.until(now, ChronoUnit.DAYS);
```

### 判断年月的周期性

```java
LocalDate nowDate = LocalDate.of(2020, 9, 27);
LocalDate birthDayTime = LocalDate.of(1998, 2, 11);
MonthDay birthday = MonthDay.of(birthDayTime.getMonth(), birthDayTime.getDayOfMonth());
MonthDay today = MonthDay.from(nowDate);
if(birthday.equals(today)){
    System.out.println("今天是我的生日");
}else{
    System.out.println("今天不是我的生日");
}
```

### 一周后的日期

```java
LocalDate today = LocalDate.now();  
LocalDate nextWeek = today.plus(1, ChronoUnit.WEEKS); 
```

### 一年前或一年后的日期

```java
LocalDate today = LocalDate.now();  
LocalDate preYear = today.minus(1, ChronoUnit.YEARS);  
LocalDate nextYear = today.plus(1, ChronoUnit.YEARS); 
```

### 检查闰年

```java
LocalDate today = LocalDate.now();  
if (today.isLeapYear()) {  
    System.out.println("今年是闰年！");
} else {
    System.out.println("今年不是闰年！");
}
```

## 附录

### date转为LocalTime

```java
// date转为LocalTime
Date from = Date.from(instant);
Instant instant2 = from.toInstant();
instant2.atZone(zone).toLocalTime();
```

### 将LocalDateTime转为date

```java
// 将LocalDateTime转为date
ZoneId zone = ZoneId.systemDefault();
Instant instant = now.atZone(zone).toInstant();
Date from = Date.from(instant);
```