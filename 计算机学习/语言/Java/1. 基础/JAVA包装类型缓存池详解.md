# JAVA包装类型缓存池详解
see [JAVA包装类型缓存池详解](https://blog.csdn.net/stdio_54456153/article/details/98783049)
## 拆箱装箱
基本类型要转换成包装类型，需要调用包装类型的静态valueOf()函数；而包装类型要转换成基本类型，需要调用以基本类型开头的Value()，比如 intValue() 。

在一般情况下，Java会自动帮你实现拆箱装箱，比如
```java
Integer x = 2;     // 装箱   实际是Integer x = Integer.valueOf(2)
int y = x;         // 拆箱   实际是int y = intValue(x)
```

拆箱装箱详情可参考深入剖析Java中的装箱和拆箱（缓存池技术）

## 缓存池介绍
在使用这些基本类型对应的包装类型时，如果该数值范围在缓冲池范围内，就可以直接使用缓冲池中的对象。否则，就创建一个对象存储相应的数据。

各种基本类型的缓存池内容如下：

```java
boolean values true and false                //布尔类型中的两个取值  true和false
all byte values                              //byte类型所有数据，即-128～127
short values between -128 and 127            //short类型大小范围-128~127
int values between -128 and 127              //int类型大小范围  -128~127
char in the range \u0000 to \u007F           //char类型所有数据，即所有字符
```

### Integer 缓冲池
在 jdk 1.8 所有的数值类缓冲池中，Integer 的缓冲池 ```IntegerCache``` 很特殊，这个缓冲池的下界是 - 128，上界默认是 127，但是这个上界是可调的，在启动 jvm 的时候，通过 -XX:AutoBoxCacheMax=<size> 来指定这个缓冲池的大小
可以发现，他是先判断数值是否在缓存池的范围中，如果在就直接返回缓存池中的对象。

### 字符串常量池
字符串常量池（String Pool）保存着所有字符串字面量（literal strings），这些字面量在编译时期就确定。不仅如此，还可以使用 String 的 ```intern()``` 方法在运行过程中将字符串添加到 String Pool 中。
	
当一个字符串调用 intern() 方法时:
	- 如果 String Pool 中已经存在一个字符串和该字符串值相等（使用 equals() 方法进行确定），那么就会返回 String Pool 中字符串的引用；
	- 否则，就会在 String Pool 中添加一个新的字符串，并返回这个新字符串的引用。
	
> 在 Java 7 之前，String Pool 被放在运行时常量池中，它属于永久代。而在 Java 7，String Pool 被移到堆中。这是因为永久代的空间有限，在大量使用字符串的场景下会导致 OutOfMemoryError 错误。