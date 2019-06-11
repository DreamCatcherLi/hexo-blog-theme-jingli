---
title: Java8 - 更优雅的字符串连接(join)收集器 Collectors.joining
date: 2019-06-11 10:41:30
categories: 
- 后端
tags: 
- Java8
---

## Java8中的字符串连接收集器

  在JDK8中，可以采用函数式编程（使用 `Collectors.joining` 收集器）的方式对字符串进行更优雅的连接。
`Collectors.joining` 收集器 支持灵活的参数配置，可以指定字符串连接时的 分隔符，前缀 和 后缀 字符串。
代码参考如下：

```java
// 定义人名数组
final String[] names = {"Zebe", "Hebe", "Mary", "July", "David"};
Stream<String> stream1 = Stream.of(names);
Stream<String> stream2 = Stream.of(names);
Stream<String> stream3 = Stream.of(names);
// 拼接成 [x, y, z] 形式
String result1 = stream1.collect(Collectors.joining(", ", "[", "]"));
// 拼接成 x | y | z 形式
String result2 = stream2.collect(Collectors.joining(" | ", "", ""));
// 拼接成 x -> y -> z] 形式
String result3 = stream3.collect(Collectors.joining(" -> ", "", ""));
System.out.println(result1);
System.out.println(result2);
System.out.println(result3);
```
--------------------- 
程序输出结果如下：
```java
[Zebe, Hebe, Mary, July, David]
Zebe | Hebe | Mary | July | David
Zebe -> Hebe -> Mary -> July -> David
```    
## 一般的做法（不推荐）
  在JAVA8出现之前，我们通常使用循环的方式来拼接字符串，这样做不仅代码冗长丑陋，而且需要仔细阅读代码才知道代码的功能
例如下面的代码：
```java
final String[] names = {"Zebe", "Hebe", "Mary", "July", "David"};
StringBuilder builder = new StringBuilder();
for (int i = 0; i < names.length; i++) {
    if (builder.length() > 1) {
        builder.append(",");
    }
    builder.append(names[i]);
}
System.out.println(builder.toString());
```