---
title: '日期格式DateTimeFormat-yyyy-MM-dd HH:mm:ss 坑&大小写区别'
catalog: true
date: 2022-11-16 10:34:52
subtitle:
header-img:
tags:
---

## yyyy-MM-dd HH:mm:ss SSS 含义

| Letter | 含义        | Example                       |
| ------ | --------- | ----------------------------- |
| y      | 不包含纪元的年份        | y------>9     例如2009用不包含纪元的年份表示就是9。如果年份小于 10，则显示不具有前导零的年份。      |
| yy      | 不包含纪元的年份        | yy----->09   例如2009用不包含纪元的年份表示就是09。如果年份小于 10，则显示具有前导零的年份。        |
| yyyy      | 包括纪元的四位数的年份         | yyyy--->2009             |
| M      | 月份数字         | M------->2 大写的M    一位数的月份没有前导零。             |
| MM      | 月份数字         | MM------>02 大写的M  一位数的月份有一个前导零。           |
| MMM      | 月份的缩写名称       | MMM----->Feb 大写的M   例如英文中是"Jan", "Apr", "Sep", "Oct", "May", "Jun", "Jul", "Feb", "Mar", "Aug",  "Nov", "Dec"。中文是"1月", "2月", "3月"。C#中在 AbbreviatedMonthNames 中定义。           |
| MMMM      | 月份的完整名称。 | MMMM---->February 大写的M  例如英文中是'January', 'February'，中文是"一月"，"二月" C#中在 MonthNames 中定义。     |
| d      | 一月中的天数    | d--------->3    一位数的日期没有前导零            |
| dd      | 一月中的天数    | dd-------->03   有前导零           |
| ddd      | 周中某天的缩写名称    | ddd------->Sun   例如英文是："Sun", "Mon", "Tue", "Wed"，"Thu", "Fri", "Sat"; 中文是："周日"， "周一"等。 C#中在 AbbreviatedDayNames 中定义。   |
| dddd      | 周中某天的完整名称    | dddd------>Sunday  例如英文是： ["Sunday", "Monday", "Tuesday", 'Wednesday', "Thursday', 'Friday',"Saturday"; 中文是："星期日"， "星期一"等。 C#中在在 DayNames 中定义。            |
| H      | 小时（0-23）  | H--------->9   24 小时制的是大写的H |
| HH      | 小时（0-23）  | HH--------->09   24 小时制的是大写的H |
| h      | 小时（1-12）  | h---------->6  12小时制的是小写的h，没有前导零， 24小时制 18 = 12小时制 6 |
| hh      | 小时（1-12）  | hh---------->06  12小时制的是小写的h |
| m      | 分         | m-------->7 小写的m 没有前导零           |
| mm      | 分         | mm-------->07 小写的m            |
| s      | 秒         | s-------->9  没有前导零               |
| ss      | 秒         | ss-------->09                 |
| SSS      | 毫秒        | SSS--------->666              |
| Y      | Week Year | YYYY---->2020                 |
| D      | 一年中天数     | DD-------->365                |

### C#中其他含义

　gg 时期或纪元。如果要设置格式的日期不具有关联的时期或纪元字符串，则忽略该模式。
  f 秒的小数精度为一位。其余数字被截断。
　ff 秒的小数精度为两位。其余数字被截断。
　fff 秒的小数精度为三位。其余数字被截断。
　ffff 秒的小数精度为四位。其余数字被截断。
　fffff 秒的小数精度为五位。其余数字被截断。
　ffffff 秒的小数精度为六位。其余数字被截断。
　fffffff 秒的小数精度为七位。其余数字被截断。
　t 在 AMDesignator 或 PMDesignator 中定义的 AM/PM 指示项的第一个字符（如果存在）。
　tt 在 AMDesignator 或 PMDesignator 中定义的 AM/PM 指示项（如果存在）。
　z 时区偏移量（“+”或“-”后面仅跟小时）。一位数的小时数没有前导零。例如，太平洋标准时间是“-8”。
　zz 时区偏移量（“+”或“-”后面仅跟小时）。一位数的小时数有前导零。例如，太平洋标准时间是“-08”。
　zzz 完整时区偏移量（“+”或“-”后面跟有小时和分钟）。一位数的小时数和分钟数有前导零。例如，太平洋标准时间是“-08:00”。
　: 在 TimeSeparator 中定义的默认时间分隔符。
　/ 在 DateSeparator 中定义的默认日期分隔符。
　% c 其中 c 是格式模式（如果单独使用）。如果格式模式与原义字符或其他格式模式合并，则可以省略“%”字符。
　\ c 其中 c 是任意字符。照原义显示字符。若要显示反斜杠字符，请使用“\”。

### hh:mm:ss  

按照12小时制的格式进行字符串格式化

- 如果时间处于00：00：00——12：59：59，则返回的字符串正常
- 如果时间处于13：00：00——23：59：59，则返回的字符串是实际时间-12小时后的值，也就是说比真实的时间少了12个小时。
例如：14:00:00进行格式化后的字符串为“2:00:00”

### HH:mm:ss

按照24小时制的格式进行字符串格式化
当时间为任意一个区间，则返回的字符串都是正常的。

## 时间基本概念

> 简单地讲， GMT 是以前的世界时间标准；UTC 是现在在使用的世界时间标准；时区是基于格林威治子午线来偏移的，往东为正，往西为负；夏令时是地方时间制度，施行夏令时的地方，每年有2天很特殊（一天只有23个小时，另一天有25个小时）。

### `UTC`

`UTC`是协调世界时（`Coordinated Universal Time`）的缩写， 协调世界时，又称世界统一时间、世界标准时间、国际协调时间。它以前也被称为`格林威治标准时间`（`GMT`）。使用UTC而不是CUT作为缩写是英语与法语（Temps Universel Coordonné）之间妥协的结果，不是什么低级错误。由于英文（CUT）和法文（TUC）的缩写不同，作为妥协，简称UTC。
UTC 是现在全球通用的时间标准，全球各地都同意将各自的时间进行同步协调。UTC 时间是经过平均太阳时（以格林威治时间GMT为准）、地轴运动修正后的新时标以及以秒为单位的国际原子时所综合精算而成。
在军事中，协调世界时会使用“Z”来表示。又由于Z在无线电联络中使用“Zulu”作代称，协调世界时也会被称为"Zulu time"。

### Unix 时间戳（Unix Timestamp）

`时间戳 = Unix 时间戳 = Unix time = POSIX time`

> 时间戳是自 1970 年 1 月 1 日（00:00:00 ）至当前时间的总秒数。它也被称为 Unix 时间戳（Unix Timestamp）。
Unix时间戳(Unix timestamp)，或称Unix时间(Unix time)、POSIX时间(POSIX time)，是一种时间表示方式，定义为从 `格林威治时间`1970年01月01日00时00分00秒起至现在的总秒数。Unix时间戳不仅被使用在Unix系统、类Unix系统中(比如 Linux系统)，也在许多其他操作系统中被广泛采用。
>
> 时间戳其实就是一个整数。那么怎么获取呢？


#### Oracle 数据库

oracle中，一般使用类型INTEGER，获取方式：

```sql
SELECT (SYSDATE - TO_DATE('1970-1-1 8', 'YYYY-MM-DD HH24')) * 86400 FROM DUAL;
```

#### Java

java中，一般使用类型long，获取方式：

```java
import java.util.Calendar;
import java.util.Date;
public class Main
{
    public static void main(String[] args) {
        // 1.
        Long t1 = System.currentTimeMillis();
        // 2.
        Long t2 = Calendar.getInstance().getTimeInMillis();
        // 3.
        Long t3 = new Date().getTime();
        System.out.println(t1); // 1668657023995
        System.out.println(t2); // 1668657024730
        System.out.println(t3); // 1668657025323
    }
}
```

#### JavaScript

```javascript
// 1.获取的时间戳, 把毫秒改成000显示
const timestamp1 = Date.parse(new Date()); // 1668656204000
// 2.获取当前毫秒的时间戳
const timestamp2 = (new Date()).valueOf(); // 1668656204519
// 3.获取当前毫秒的时间戳
const timestamp3=new Date().getTime()；// 1668656204519
```

### `GMT`

`GMT`（Greenwich Mean Time）`格林威治标准时间`， 它规定太阳每天经过位于英国伦敦郊区的皇家格林威治天文台的时间为中午12点。
1884年10月在美国华盛顿召开了一个国际子午线会议，该会议将格林威治子午线设定为本初子午线，并将格林威治平时 (GMT, Greenwich Mean Time) 作为世界时间标准（UT, Universal Time）。由此也确定了全球24小时自然时区的划分，所有时区都以和 GMT 之间的偏移量做为参考。
1972年之前，格林威治时间（GMT）一直是世界时间的标准。1972年之后，GMT 不再是一个时间标准了。

### GMT vs UTC

GMT是前世界标准时，UTC是现世界标准时。
UTC 比 GMT更精准，以原子时计时，适应现代社会的精确计时。
但在不需要精确到秒的情况下，二者可以视为等同。
每年格林尼治天文台会发调时信息，基于UTC。

`DST`是夏令时（`Daylight Saving Time`）的缩写，在一年的某一段时间中将当地时间调整（通常）一小时。 DST的规则非常神奇（由当地法律确定），并且每年的起止时间都不同。C语言库中有一个表格，记录了各地的夏令时规则（实际上，为了灵活性，C语言库通常是从某个系统文件中读取这张表）。从这个角度而言，这张表是夏令时规则的唯一权威真理。

### 时区

> 从格林威治本初子午线起，经度每向东或者向西间隔15°，就划分一个时区，在这个区域内，大家使用同样的标准时间。
> 
> 但实际上，为了照顾到行政上的方便，常将1个国家或1个省份划在一起。所以时区并不严格按南北直线来划分，而是按自然条件来划分。另外：由于目前，国际上并没有一个批准各国更改时区的机构。一些国家会由于特定原因改变自己的时区。
> 
> 全球共分为24个标准时区，相邻时区的时间相差一个小时。
> 
> 在不同地区，同一个时区往往会有很多个不同的时区名称，因为名称中通常会包含该国该地区的地理信息。在夏令时期间，当地的时区名称及字母缩写会有所变化（通常会包含“daylight”或“summer”字样）。
> 
> 例如美国东部标准时间叫：`EST`，`Estern Standard Time`；而东部夏令时间叫：`EDT`，`Estern Daylight Time`。
> 
> 查看世界所有时区的名字可以访问这个网站：https://www.timeanddate.com/time/zones/

例如同样都是东八区，有很多个不同的时区名称，因为名称中通常会包含该国、该地区的地理信息。

Abbreviation | Time zone name | Location | Offset
----|---------------------|------------|-----
CST | China Standard Time | Asia | UTC +8|
HKT | Hong Kong Time | Asia | UTC +8|
SGT | Singapore Time SST – Singapore Standard Time|Asia|UTC +8


### 夏令时

`DST`（Daylight Saving Time），夏令时又称夏季时间，或者夏时制。
> 它是为节约能源而人为规定地方时间的制度。一般在天亮早的夏季人为将时间提前一小时，可以使人早起早睡，减少照明量，以充分利用光照资源，从而节约照明用电。
> 
> 全球约40%的国家在夏季使用夏令时，其他国家则全年只使用标准时间。标准时间在有的国家也因此被相应地称为冬季时间。
> 
> 在施行夏令时的国家，一年里面有一天只有23小时（夏令时开始那一天），有一天有25小时（夏令时结束那一天），其他时间每天都是24小时。

### 本地时间

> 在日常生活中所使用的时间我们通常称之为本地时间。这个时间等于我们所在（或者所使用）时区内的当地时间，它由与世界标准时间（UTC）之间的偏移量来定义。这个偏移量可以表示为 UTC- 或 UTC+，后面接上偏移的小时和分钟数。

例如中国就是UTC +8

## 其他基本概念

`i18n` ( internationalization ) 简称国际化 ，在现代前端开发中，有国际化需求的网站 / app，都需要进行 i18n 进行多语言的处理。


### [`CLDR`](https://cldr.unicode.org/)

> [`CLDR`](https://cldr.unicode.org/)
> The Unicode `Common Locale Data Repository` (CLDR) provides key building blocks for software to support the world's languages, with the largest and most extensive standard repository of locale data available. This data is used by a wide spectrum of companies for their software internationalization and localization, adapting software to the conventions of different languages for such common software tasks.

通用语言环境数据仓库[`CLDR`](https://cldr.unicode.org/)
通用语言环境数据仓库 (Common Locale Data Repository, CLDR) 项目是 Unicode Consortium 的一个项目，用于提供扩展的语言环境数据。CLDR 包含特定于语言环境的信息，操作系统通常会将该信息提供给应用程序。该信息包含数字格式、日期、时间和货币字符串、字符分类（小写、大写、可打印等）、字符串整理规则以及其他内容。
CLDR 是以 Unicode 的编码标准作为前提，将多国的语言文字进行编码的。
CLDR 不仅阐述了每个国家语言的文字应当如何被解析，并且，为了解析结果的可靠，还规定了结果集排序方式。
该项目每年提供两次版本更新，一次是4月份，一次是10月份。github最新开发版本：[github-unicode-org/cldr](https://github.com/unicode-org/cldr/tree/latest)，可以下载[最新数据](https://github.com/unicode-org/cldr/releases)。
国家下属子区域名称也有各种语言的翻译：[subdivisions](https://github.com/unicode-org/cldr/tree/latest/common/subdivisions)，可用的区域英文名称和代码：[Territory Subdivisions](https://unicode.org/cldr/charts/latest/supplemental/territory_subdivisions.html)，例如代码cnhb的中文简体（目前在yue_Hans.xml文件中）是“湖北”，可以考虑以后用到需要翻译国家下面一级或者两级子区域的网站，例如[邮编库系列网站](https://youbianku.com/)。

#### Java 中的CLDR

从JDK 9开始，Unicode Consortium的公共区域设置数据存储库（CLDR）数据作为默认区域设置数据启用，因此您可以使用标准区域设置数据而无需任何进一步操作。

在JDK 8中，虽然CLDR区域设置数据与JRE捆绑在一起，但默认情况下不启用它。

使用区域设置敏感服务（如日期，时间和数字格式）的代码可能会使用CLDR区域设置数据生成不同的结果。请记住，即使`System.out.printf（）`也是区域设置感知的。

要启用与JDK 8兼容的行为，请将系统属性设置为例如前面的`java.locale.providers`值。

```java
java.locale.providers=COMPAT,CLDR
```

见[CLDR语言环境数据通过默认启用的Java平台](https://docs.oracle.com/en/java/javase/11/intl/internationalization-enhancements1.html#GUID-9DCDB41C-A989-4220-8140-DBFB844A0FCA)，标准版国际指南和[JEP 252：使用CLDR语言环境数据的默认](https://openjdk.org/jeps/252?spm=a2c6h.12873639.article-detail.98.1f10173fd2EXCx)。

Java 9的国际化增强功能包括默认情况下启用CLDR语言环境数据。

使用以下关键字标识的语言环境数据有四个不同的来源：

- CLDR：Unicode通用语言环境数据存储库(CLDR)项目提供的语言环境数据。

- HOST：当前用户对基础操作系统设置的自定义。根据操作系统的不同，可以支持日期，时间，数字和货币等格式。

- SPI：在已安装的SPI提供程序中实现的对语言环境敏感的服务。

- COMPAT(JRE)：与Java 9之前的发行版兼容的语言环境数据。JRE仍可以用作值，但已弃用，以后会删除。

在Java 8和早期版本中，JRE是默认语言环境数据。Java 9默认将CLDR设置为最高优先级。我们使用java.locale.providers系统属性按首选顺序选择语言环境数据源。如果提供程序未能请求区域设置数据，则可以处理下一个提供程序。

```java
java.locale.providers=COMPAT,CLDR,HOST,SPI
```

如果我们不设置该属性，则默认行为是：

```java
java.locale.providers=CLDR,COMPAT,SPI
```

为了与Java 8兼容，请将COMPAT置于CLDR之前。

```java
java.locale.providers=COMPAT,CLDR
```

Ant 配置 （build.xml）

```xml
<java classname="com.lyk.web.app.PropertySetJsHelper" failonerror="yes" fork="yes">
    <sysproperty key="java.locale.providers" value="COMPAT,CLDR,SPI" />
</java>
```

Gradle 配置 （build.gradle）

```gradle
  systemProperty 'java.locale.providers', 'COMPAT,CLDR,SPI'
```

参考文章： [JDK11变化详解，JDK8升级JDK11详细指南](https://developer.aliyun.com/article/659407)

## JavaScript中的Date

### 原生JavaScript

```javascript
// 1.获取的时间戳, 把毫秒改成000显示
const timestamp1 = Date.parse(new Date()); // 1668656204000
// 2.获取当前毫秒的时间戳
const timestamp2 = (new Date()).valueOf(); // 1668656204519
// 3.获取当前毫秒的时间戳
const timestamp3=new Date().getTime()；// 1668656204519
```

### JS库 - Moment

## 参考文章

- [彻底弄懂GMT、UTC、时区和夏令时](https://zhuanlan.zhihu.com/p/135951778)
- [什么是时间戳](https://blog.csdn.net/wildpal/article/details/40039977?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522166865369616800215039495%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=166865369616800215039495&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~baidu_landing_v2~default-6-40039977-null-null.142^v63^control,201^v3^control,213^v2^t3_esquery_v3&utm_term=%E6%97%B6%E9%97%B4%E6%88%B3&spm=1018.2226.3001.4187)


其他语言日期格式

- [C#日期型数据简单剖析](https://www.51cto.com/article/147694.html)
- [在jsp页面中使用EL表达式格式化date日期](https://cloud.tencent.com/developer/article/1653924)
- [3.11.0 Documentation » Python 标准库 » 通用操作系统服务 » time --- 时间的访问和转换](https://docs.python.org/zh-cn/3/library/time.html)