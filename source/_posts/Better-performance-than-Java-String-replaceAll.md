---
title: Better performance than Java.String.replaceAll
catalog: true
date: 2021-03-09 15:25:44
subtitle:
header-img:
tags:
- Java
categories:
- TECH
- BackEnd
- Java
---


最近在看Spring Security utilize a response wrapper ([FirewalledResponse](https://github.com/spring-projects/spring-security/blob/5.4.x/web/src/main/java/org/springframework/security/web/firewall/FirewalledResponse.java))的时候发现 [Issue 6731 improve performance of checking headers](https://github.com/spring-projects/spring-security/commit/19de13bdc7e84a92811b509fe780c711ddf1405b). 主要的原因就是使用了正则，导致效率降低，如果是简单的匹配尽量避免使用正则。

随之想到使用非常频繁的`Java.String.replaceAll`, 它的效率是否也比其他不使用正则的替换方法低呢？
之前在使用几个不同替换方法的时候并没有关注效率问题。但如果在非常频繁的使用场景下，替换方法效率的提升是否就非常有意义了呢？

# Java 自带replace all方法

```java
public class ReplaceAll {
    String value;

    public String replaceAllWithContains() {
        return value.contains(".") ? value.replaceAll("\\.", "%2E") : value;
    }

    public String replaceAll() {
        return value.replaceAll("\\.", "%2E");
    }

    public String replace() {
        return value.replace(".", "%2E");
    }

    public String replaceWithContains() {
        return value.contains(".") ? value.replace(".", "%2E") : value;
    }
}

```

## java.lang.replace

>replace(CharSequence target, CharSequence replacement)，用replacement替换所有的target，两个参数都是字符串。

## java.lang.replaceAll

>replaceAll(String regex, String replacement)，用replacement替换所有的regex匹配项，regex很明显是个正则表达式，replacement是字符串。

## 对比结果

JDK 11.0.8, OpenJDK 64-Bit Server VM, 11.0.8+10

```shell
Benchmark                                     (value)  Mode  Cnt    Score    Error  Units
ReplaceAll.replace                                     avgt   10    3.836 ±  0.060  ns/op
ReplaceAll.replaceAll                                  avgt   10  147.857 ±  1.550  ns/op
ReplaceAll.replaceAllWithContains                      avgt   10    3.777 ±  0.069  ns/op
ReplaceAll.replaceWithContains                         avgt   10    3.778 ±  0.075  ns/op

ReplaceAll.replace                      somePathNoDoT  avgt   10    7.647 ±  0.646  ns/op
ReplaceAll.replaceAll                   somePathNoDoT  avgt   10  156.495 ±  1.751  ns/op
ReplaceAll.replaceAllWithContains       somePathNoDoT  avgt   10    7.640 ±  0.291  ns/op
ReplaceAll.replaceWithContains          somePathNoDoT  avgt   10    7.545 ±  0.298  ns/op

ReplaceAll.replace                 some.Path.With.Dot  avgt   10  123.856 ±  1.686  ns/op
ReplaceAll.replaceAll              some.Path.With.Dot  avgt   10  389.632 ± 18.308  ns/op
ReplaceAll.replaceAllWithContains  some.Path.With.Dot  avgt   10  378.527 ±  6.434  ns/op
ReplaceAll.replaceWithContains     some.Path.With.Dot  avgt   10  126.918 ±  0.940  ns/op
```

可以看出效率由高到低：
不含target时：
>replaceWithContains > replace > replaceAllWithContains > replaceAll
含有target时：
>replace > replaceWithContains> replaceAllWithContains > replaceAll

结论： 
>尽量使用replace，而非replaceAll.


# 其他实现replace all方法

```java
import org.apache.commons.lang3.StringUtils;

public class ReplaceCustom {

    String value;

    public String replace() {
        return value.replace(".", "/");
    }

    public String replaceSpring() {
        return springReplace(value, ".", "/");
    }

    public String replaceChar() {
        return value.replace('.', '/');
    }

    public String replaceApache() {
        return StringUtils.replace(value, ".", "/");
    }

    public String replaceApacheChar() {
        return StringUtils.replaceChars(value, '.', '/');
    }

    public static boolean hasLength(String str) {
        return (str != null && !str.isEmpty());
    }

    public static String springReplace(String inString, String oldPattern, String newPattern) {
        if (!hasLength(inString) || !hasLength(oldPattern) || newPattern == null) {
            return inString;
        }
        int index = inString.indexOf(oldPattern);
        if (index == -1) {
            // no occurrence -> can return input as-is
            return inString;
        }

        int capacity = inString.length();
        if (newPattern.length() > oldPattern.length()) {
            capacity += 16;
        }
        StringBuilder sb = new StringBuilder(capacity);

        int pos = 0;  // our position in the old string
        int patLen = oldPattern.length();
        while (index >= 0) {
            sb.append(inString, pos, index);
            sb.append(newPattern);
            pos = index + patLen;
            index = inString.indexOf(oldPattern, pos);
        }

        // append any characters to the right of a match
        sb.append(inString, pos, inString.length());
        return sb.toString();
    }
}
```

## java.lang.replace


## Reference Links

- [Faster alternatives to replace method in a Java String?](https://stackoverflow.com/questions/1010928/faster-alternatives-to-replace-method-in-a-java-string)
- [String.replaceAll is considerably slower than doing the job yourself](https://stackoverflow.com/questions/6262397/string-replaceall-is-considerably-slower-than-doing-the-job-yourself)
- [Performance difference between Java Regex and String based replace operations](https://www.logicbig.com/tutorials/core-java-tutorial/java-regular-expressions/performance.html)
- [Micro optimizations in Java. String.replaceAll](https://github.com/CatherineLiyuankun/java-micro-optimizations)
  