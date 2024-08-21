---
title: '日期格式DateTimeFormat-yyyy-MM-dd HH:mm:ss 坑&大小写区别'
catalog: true
date: 2022-11-16 10:34:52
subtitle:
header-img:
tags:
---

# 编程中的时间概念

## [Unix 时间戳（Unix Timestamp）](https://zh.m.wikipedia.org/wiki/UNIX%E6%97%B6%E9%97%B4)

参考文章：

- [为什么编程语言中日期能够实现加减法](https://www.51cto.com/article/526190.html)

`Unix timestamp = Unix 时间戳 = Unix time = Unix epoch = POSIX time`

> 时间戳是自 1970 年 1 月 1 日（00:00:00 ）至当前时间的总秒数, 不考虑闰秒。它也被称为 Unix 时间戳（Unix Timestamp）。
Unix时间戳(Unix timestamp)，或称Unix时间(Unix time)、POSIX时间(POSIX time)，是一种时间表示方式，定义为从1970年01月01日00时00分00秒（UTC/GMT）起至现在的总秒数。Unix时间戳不仅被使用在Unix系统、类Unix系统中(比如 Linux系统)，也在许多其他操作系统中被广泛采用。
>
> UNIX时间戳的 0 按照 ISO 8601 规范为 ：1970-01-01T00:00:00Z.
>
> 时间戳其实就是一个整数。
> 一个小时表示为UNIX时间戳格式为：3600秒；一天表示为UNIX时间戳为86400秒，闰秒不计算。
在大多数的 Unix 系统中 Unix 时间戳存储为 32 位，这样会引发 2038 年问题或 Y2038。

多数编程语言起源于UNIX，UNIX系统的时间纪元是1970-01-01 00:00:00,即所为的UNIX时间戳。

最初计算机都是32位操作系统，时间需要通过number存储，32位能表示数字为2147483647。一年365天的总秒数位31536000 ，两者相除得68.1 (68.0962597349).而选用1970年的，可以支持到2038年。
<!-- 所以如果从0000-00-00 00:00:00 算起的话，计算机到1901年12月13日就溢出了。???? -->

最早版本的Unix时间是32位整型，以60 Hz增加。1971年11月3日发行的第一版《Unix Programmer's Manual》定义了Unix时间为“the time since 00:00:00, 1 January 1971, measured in sixtieths of a second”，即从1971年1月1日00:00:00开始，以60赫兹增加。[2]这意味着以32位无符号整型存储Unix时间，829天（约2.5年）后就将用尽重置。由于该限制，Unix时间原点被重定义多次。Unix V3规定采用60hz的滴答数，从1972年元旦开始计时。直至1973年的Unix V4开始采用1970年1月1日00:00:00UTC为时间原点，以1赫兹计时。由于Unix和C语言采用32位有符号整型表示时间，这可容纳约136年的时间跨度，在1970年之前和之后各占一半。即到2038年1月19日和1901月12月13日用尽重置。

此后，这个Unix 时间定义考虑到时区，闰秒等问题被修订。

当年的电脑需要一个可靠的外部时钟同步源，因此早期的 Unix 系统用一个32位字长表示时间，以1/60秒，即1Hz为时间间隔和外部时间源同步（这道不完全是由于老美的电网频率是60Hz的缘故，当时的系统主板的晶振就是1Hz）。 结果这个时间所表示的跨度只有大约829天（约2.5年），显然不够用，因此需要一个原始的起始（〔纪〕··〔元〕）时间，由于 Unix 系统源自上时间69年代，第一个正式版本于1970年首次运行在 PDP-11 上，1971年11月 UNIX Programmer’s Manual（Unix程序员手册）首次公布，这个手册里面提及了起始时间，将它定义为【1971】年1月1日。－－ 手册也承认，该起始时间大约每 2.5年就要重新修正一次。

之后系统时间同步间隔被修订为 1 秒，这样32位就可表述约136年的跨度，也正是这个期间（具体年份不祥），起始时间被修订为1970.1.1 （Unix开发者认为把之前的 1971.1.1 取整进位到最临近的年代起始（以每10年一个断代算），要比 1971 这个有点不伦不类的时间好），因此从这以后，Unix一直沿用了 1970.1.1 这个起始时间，而相关的程序也相应的沿用了这个时间，而深受 Unix 影响的后续操作系统们，如：OS/2, Windows, Mactonish, Linux。。。。都沿用了这个｛事实标准｝。

现时大部分使用UNIX的系统都是32位的，即它们会以32位有符号整数表示时间类型time_t。因此它可以表示136年的秒数。表示协调世界时间1901年12月13日星期五20时45分52秒 至 2038年1月19日3时14分07秒（二进制：01111111 11111111 11111111 11111111，0x7FFF:FFFF），在下一秒二进制数字会是10000000 00000000 00000000 00000000（0x8000:0000），这是负数，因此各系统会把时间误解作1901年12月13日20时45分52秒（亦有可能回归到1970年）。这时可能会令软件发生问题，导致系统瘫痪。

目前的解决方案是把系统由32位转为64位系统。在64位系统下，此时间最多可以表示到2922亿7702万6596年12月4日15时30分08秒。

| Human Readable Time  | Seconds          |
| -------------------- | ---------------- |
| 1 Hour               | 3600 Seconds     |
| 1 Day                | 86400 Seconds    |
| 1 Week               | 604800 Seconds   |
| 1 Month (30.44 days) | 2629743 Seconds  |
| 1 Year (365.24 days) | 31556926 Seconds |

| 编程语言                                                                                      | 编程中获取Unix时间戳                                                                                                                                                                            | 0对应的默认时间                                                                                                                                                                                                                 |
| --------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Java                                                                                          | `System.currentTimeMillis() / 1000`  对于中国开发者，通过 `System.out.println(new Date(0));` ,控制台打印的时间是1970-01-01 08:00:00 ，这个是因为中国处于东8区的缘由。对于程序内部存储值无影响。 | Unix timestamp, [文档地址](http://docs.oracle.com/javase/8/docs/api/java/util/Date.html#Date)                                                                                                                                   |
| JavaScript                                                                                    | `Math.round(new Date().getTime()/1000)` `getTime()`返回数值的单位是毫秒                                                                                                                         | Unix timestamp, [文档地址](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Date)                                                                                                               |
| Python                                                                                        | 先 `import time` 然后 `time.time()` 返回1476929706.5320001 可以 `int(time.time())`                                                                                                              | Unix timestamp, [文档地址](https://docs.python.org/3/library/datetime.html#date-objects)                                                                                                                                        |
| PHP                                                                                           | `time()`                                                                                                                                                                                        | Unix timestamp, [文档地址](http://php.net/manual/en/function.time.php)                                                                                                                                                          |
| Microsoft .NET / C#                                                                           | `epoch = (DateTime.Now.ToUniversalTime().Ticks - 621355968000000000) / 10000000`                                                                                                                | Not Unix timestamp 默认采用int64位来表示时间戳，并且精确到100ns，开始日期点为0001-01-01 00:00:00.000。[文档地址](https://msdn.microsoft.com/zh-cn/library/z2xf7zzk(v=vs.110).aspx?cs-save-lang=1&cs-lang=csharp#code-snippet-1) |
| Perl                                                                                          | `time`                                                                                                                                                                                          |
| Golang                                                                                        | `time.now().Unix()`                                                                                                                                                                             |
| Ruby                                                                                          | 获取Unix时间戳：`Time.now` 或 `Time.new`; 显示Unix时间戳：`Time.now.to_i`                                                                                                                       |
| ORACLE                                                                                        |                                                                                                                                                                                                 | Unix timestamp, [文档TIMESTAMP object initialized to 1/1/1970](https://docs.oracle.com/cd/E11882_01/appdev.112/e13995/oracle/sql/TIMESTAMP.html)                                                                                |
| PostgreSQL                                                                                    | `SELECT extract(epoch FROM now())`                                                                                                                                                              |
| MySQL                                                                                         | `SELECT unix_timestamp(now())`                                                                                                                                                                  |
| SQL Server                                                                                    | `SELECT DATEDIFF(s, '1970-01-01 00:00:00', GETUTCDATE())`                                                                                                                                       |
| VBScript / ASP                                                                                | `DateDiff("s", "01/01/1970 08:00:00", Now())`                                                                                                                                                   | Not Unix timestamp [文档地址](https://www.microsoft.com/china/vbscript/vbstutor/vbsdatatype.htm). 这个开始时间很奇怪，从API来看，开始时间是从0100-01-01 00:00:00, 不过从代码测试来看，开始时间是从1899-12-30 0 :00:00 开始      |
| lua                                                                                           | `os.time()` 返回时间戳                                                                                                                                                                          |
| Unix /Linux/[类UNIX](https://baike.baidu.com/item/%E7%B1%BBUNIX?fromModule=lemma_inlink)/OS X | 命令行：`date +%s`                                                                                                                                                                              |
| [FreeSWITCH](https://baike.baidu.com/item/FreeSWITCH?fromModule=lemma_inlink)                 | `fs_cli > strepoch`或者：`fs_cli > eval ${strepoch()}`或者：（在 freeswitch里面，获取linux系统的时间戳）`fs_cli > system date +%s`                                                              |
| 其他操作系统(如果Perl被安装在系统中)                                                          | 命令行状态：`perl -e "print time"`                                                                                                                                                              |

### Oracle 数据库

[Oracle date 和 timestamp 区别](https://www.cnblogs.com/java-class/p/4742740.html)

oracle中，一般使用类型INTEGER，获取方式：

```sql
SELECT (SYSDATE - TO_DATE('1970-1-1 8', 'YYYY-MM-DD HH24')) * 86400 FROM DUAL;
```

### Java 中的时间戳

[Java日期类的时间从为什么是从1970年1月1日](https://blog.csdn.net/L1585931143/article/details/53471197)

java中，一般使用类型long，获取方式：

```java
import java.util.Calendar;
import java.util.Date;
public class Main
{
    public static void main(String[] args) {
        // 0. Get default date
        System.out.println(new Date(0)); // Thu Jan 01 00:00:00 GMT 1970
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

### JavaScript 中的时间戳

```javascript

// 0.Get default date 
const date1 = new Date(0);
console.log(date1); // Thu Jan 01 1970 08:00:00 GMT+0800 (China Standard Time) 因为中国处于东8区的缘由。对于程序内部存储值无影响。
// 1.获取的时间戳, 把毫秒改成000显示
const timestamp1 = Date.parse(new Date()); // 1668656204000
// 2.获取当前毫秒的时间戳
const timestamp2 = (new Date()).valueOf(); // 1668656204519
// 3.获取当前毫秒的时间戳
const timestamp3=new Date().getTime()；// 1668656204519
```

## [ISO 8601](https://zh.m.wikipedia.org/wiki/ISO_8601)

## 润秒

## 1988/12/30 12:00:00 am

参考文章：

- [2676: Historical Dates 1970.1.1 & 1899.12.30](https://www.explainxkcd.com/wiki/index.php/2676:_Historical_Dates)
- [What is story behind December 30, 1899 as base date?](https://social.msdn.microsoft.com/Forums/office/en-US/f1eef5fe-ef5e-4ab6-9d92-0998d3fa6e14/what-is-story-behind-december-30-1899-as-base-date?forum=accessdev)
- [Why is 1899-12-30 the zero date in Access / SQL Server instead of 12/31?](https://stackoverflow.com/questions/3963617/why-is-1899-12-30-the-zero-date-in-access-sql-server-instead-of-12-31)
- [System.TDateTime in Delphi](http://docs.embarcadero.com/products/rad_studio/delphiAndcpp2009/HelpUpdate2/EN/html/delphivclwin32/System_TDateTime.html#4465736372697074696F6E)

### In Excel & Lotus 1-2-3

> Dec 30th, 1899 comes from a spreadsheet date compatibility issue between Excel and Lotus 1-2-3 (referenced in the title text.) Spreadsheets store dates as sequential numbers so that they can be used in calculations. In Excel, by default, January 1, 1900 is number 1. Based on that, Excel's integer date representation would be the number of days that have passed since December 31, 1899.
>
> However, because of a bug intentionally carried over from Lotus 1-2-3 where it counts February 29, 1900 as a day even though it actually was not, for any day since then, Excel's integer date representation is actually the number of days that have passed since December 30, 1899. Most other spreadsheet applications copied the behavior of Excel to maintain compatibility with it. This leads to the value of 0 in some applications (notably Open- and LibreOffice Calc and Google Spreadsheets) being interpreted as Dec 30th, 1899. Similarly, Microsoft Visual Basic and Visual Basic for Applications (VBA) interpret 0.0 as Dec 30th, 1899.
>
> 1899 年 12 月 30 日来自 Excel 和 [Lotus 1-2-3](https://zh.wikipedia.org/wiki/Lotus_1-2-3)之间的电子表格日期兼容性问题（在标题文本中引用。）电子表格将日期存储为连续数字，以便可以在计算中使用它们。 在 Excel 中，默认情况下，1900 年 1 月 1 日是数字 1。 基于此，Excel 的整数日期表示将是自 1899 年 12 月 31 日以来经过的天数。但是，由于有意从 Lotus 1-2-3 遗留的错误，它将 1900 年 2 月 29 日算作一天 虽然它实际上不是，但从那以后的任何一天，Excel 的整数日期表示实际上是自 1899 年 12 月 30 日以来经过的天数。大多数其他电子表格应用程序复制 Excel 的行为以保持与它的兼容性。 这导致某些应用程序（特别是 Open- 和 LibreOffice Calc 以及 Google Spreadsheets）中的值 0 被解释为 1899 年 12 月 30 日。类似地，Microsoft Visual Basic 和 Visual Basic for Applications (VBA) 将 0.0 解释为 1899 年 12 月 30 日。

在office excel中存在两种日期格式1900 和 1904，即日期的开始点为 1900-01-01 00：00:00 和 1904-01-01 00:00:00 。一般Excel 默认是按照1900的日期系统，且认为1900年为润年，1900年2月分 按照29天计算。Excel中存储值得起始日期是从1开始的，即，1900-01-01 00:00:00 在excel中对应的存储值为1 （天）。

### In Delphi, C++

> In Delphi, TDateTime is a type that maps to a Double. In C++, the TDateTime class corresponds to the Delphi TDateTime type.  
>
> The integral part of a Delphi TDateTime value is the number of days that have passed since 12/30/1899. The fractional part of the TDateTime value is fraction of a 24 hour day that has elapsed.  

| TDateTime | UTC                 |
| --------- | ------------------- |
| 0         | 12/30/1899 12:00 am |
| 2.75      | 1/1/1900 6:00 pm    |
| -1.25     | 12/29/1899 6:00 am  |
| 35065     | 1/1/1996 12:00 am   |

> To find the fractional number of days between two dates, simply subtract the two values, unless one of the TDateTime values is negative. Similarly, to increment a date and time value by a certain fractional number of days, add the fractional number to the date and time value if the TDateTime value is positive.  
>
> When working with negative TDateTime values, computations must handle time portion separately. The fractional part reflects the fraction of a 24-hour day without regard to the sign of the TDateTime value. For example, 6:00 am on 12/29/1899 is –1.25, not –1 + 0.25, which would be –0.75. There are no TDateTime values between –1 and 0.

## yyyy-MM-dd HH:mm:ss SSS 含义

| Letter | 含义                             | Example                                                                                                                                                                                  |
| ------ | -------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| y      | 不包含纪元的年份                 | y------>9     例如2009用不包含纪元的年份表示就是9。如果年份小于 10，则显示不具有前导零的年份。                                                                                           |
| yy     | 不包含纪元的年份                 | yy----->09   例如2009用不包含纪元的年份表示就是09。如果年份小于 10，则显示具有前导零的年份。                                                                                             |
| yyyy   | 包括纪元的四位数的年份           | yyyy--->2009                                                                                                                                                                             |
| M      | 月份数字                         | M------->2 大写的M    一位数的月份没有前导零。                                                                                                                                           |
| MM     | 月份数字                         | MM------>02 大写的M  一位数的月份有一个前导零。                                                                                                                                          |
| MMM    | 月份的缩写名称                   | MMM----->Feb 大写的M   例如英文中是"Jan", "Apr", "Sep", "Oct", "May", "Jun", "Jul", "Feb", "Mar", "Aug",  "Nov", "Dec"。中文是"1月", "2月", "3月"。C#中在 AbbreviatedMonthNames 中定义。 |
| MMMM   | 月份的完整名称。                 | MMMM---->February 大写的M  例如英文中是'January', 'February'，中文是"一月"，"二月" C#中在 MonthNames 中定义。                                                                            |
| d      | 一月中的天数                     | d--------->3    一位数的日期没有前导零                                                                                                                                                   |
| dd     | 一月中的天数                     | dd-------->03   有前导零                                                                                                                                                                 |
| ddd    | 周中某天的缩写名称               | ddd------->Sun   例如英文是："Sun", "Mon", "Tue", "Wed"，"Thu", "Fri", "Sat"; 中文是："周日"， "周一"等。 C#中在 AbbreviatedDayNames 中定义。                                            |
| dddd   | 周中某天的完整名称               | dddd------>Sunday  例如英文是： ["Sunday", "Monday", "Tuesday", 'Wednesday', "Thursday', 'Friday',"Saturday"; 中文是："星期日"， "星期一"等。 C#中在在 DayNames 中定义。                 |
| H      | 小时（0-23）                     | H--------->9   24 小时制的是大写的H                                                                                                                                                      |
| HH     | 小时（0-23）                     | HH--------->09   24 小时制的是大写的H                                                                                                                                                    |
| h      | 小时（1-12）                     | h---------->6  12小时制的是小写的h，没有前导零， 24小时制 18 = 12小时制 6                                                                                                                |
| hh     | 小时（1-12）                     | hh---------->06  12小时制的是小写的h                                                                                                                                                     |
| m      | 分                               | m-------->7 小写的m 没有前导零                                                                                                                                                           |
| mm     | 分                               | mm-------->07 小写的m                                                                                                                                                                    |
| s      | 秒                               | s-------->9  没有前导零                                                                                                                                                                  |
| ss     | 秒                               | ss-------->09                                                                                                                                                                            |
| a      | displays time with AM/ PM marker | hh:mm:ss a-------->12：59：59 AM                                                                                                                                                         |
| SSS    | 毫秒                             | SSS--------->666                                                                                                                                                                         |
| Y      | Week Year                        | YYYY---->2020                                                                                                                                                                            |
| D      | 一年中天数                       | DD-------->365                                                                                                                                                                           |

### 其他含义

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

# 时间基本概念

> 简单地讲， GMT 是以前的世界时间标准；UTC 是现在在使用的世界时间标准；时区是基于格林威治子午线来偏移的，往东为正，往西为负；夏令时是地方时间制度，施行夏令时的地方，每年有2天很特殊（一天只有23个小时，另一天有25个小时）。

## `UTC`

`UTC`是协调世界时（`Coordinated Universal Time`）的缩写， 协调世界时，又称世界统一时间、世界标准时间、国际协调时间。它以前也被称为`格林威治标准时间`或者“格林尼治标准时间”（`GMT`）。使用UTC而不是CUT作为缩写是英语与法语（Temps Universel Coordonné）之间妥协的结果，不是什么低级错误。由于英文（CUT）和法文（TUC）的缩写不同，作为妥协，简称UTC。
UTC 是现在全球通用的时间标准，全球各地都同意将各自的时间进行同步协调。UTC 时间是经过平均太阳时（以格林威治时间GMT为准）、地轴运动修正后的新时标以及以秒为单位的国际原子时所综合精算而成。
在军事中，协调世界时会使用“Z”来表示。又由于Z在无线电联络中使用“Zulu”作代称，协调世界时也会被称为"Zulu time"。

## `GMT`

`GMT`（Greenwich Mean Time）`格林威治标准时间`或者“格林尼治标准时间”， 它规定太阳每天经过位于英国伦敦郊区的皇家格林威治天文台的时间为中午12点。
1884年10月在美国华盛顿召开了一个国际子午线会议，该会议将格林威治子午线设定为本初子午线，并将格林威治平时 (GMT, Greenwich Mean Time) 作为世界时间标准（UT, Universal Time）。由此也确定了全球24小时自然时区的划分，所有时区都以和 GMT 之间的偏移量做为参考。
后来，格林尼治天文台所在地的地方平太阳时被定义为全世界的时间标准，被称为格林尼治平时（Greenwich Mean Time），“平时（mean time）”就是“平太阳时（mean solar time）”的意思。

后来，由于1925年以前人们在天文观测中，常常把每天的起始（0时）定为正午，而不是通常民用的午夜，给格林尼治平时的意义造成含糊，人们使用世界时（Universal Time, UT）一词来明确表示每天从午夜开始的格林尼治平时。

目前使用的世界时测算标准又称`UT1`。在UT1之前人们曾使用过UT0，但由于UT0没有考虑极移导致的天文台地理坐标变动的问题，因此测出的世界时不准确，现在已经不再被使用。在UT1之后，由于人们发现，因为地球自转本身不均匀的问题，UT1定义的时间的流逝仍然不均匀，于是人们又发展了一些对UT1进行平滑处理后的时间标准，包括`UT1R`和`UT2`，但它们都未能彻底解决定义的时间的流逝不均匀的问题，这些时间标准现在都不再被使用。

后来，人们为了彻底解决定义的时间的流逝不均匀的问题，开始使用原子钟定义时间。人们首先用全世界的原子钟共同为地球确立了一个均匀流动的时间，称为国`际原子时`（`International Atomic Time`, `TAI`）。然后，为了使定义的时间与地球自转相配合，人们通过在TAI的基础上不定期增减闰秒的方式，使定义的时间与世界时（UT1）保持差异在0.9秒以内，这样定义的时间就是协调世界时（Coordinated Universal Time, UTC）。UTC是目前全世界使用的时间标准。UTC与UT1之间的差异被称为DUT1。
1972年之前，格林威治时间（GMT）一直是世界时间的标准。1972年之后，GMT 不再是一个时间标准了。

### GMT vs UTC

GMT是前世界标准时，UTC是现世界标准时。
UTC 比 GMT更精准，以原子时计时，适应现代社会的精确计时。
但在不需要精确到秒的情况下，二者可以视为等同。
每年格林尼治天文台会发调时信息，基于UTC。

## 时区

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
> 查看世界所有时区的名字可以访问这个网站：<https://www.timeanddate.com/time/zones/>

例如同样都是东八区，有很多个不同的时区名称，因为名称中通常会包含该国、该地区的地理信息。

| Abbreviation | Time zone name                               | Location | Offset |
| ------------ | -------------------------------------------- | -------- | ------ |
| CST          | China Standard Time                          | Asia     | UTC +8 |
| HKT          | Hong Kong Time                               | Asia     | UTC +8 |
| SGT          | Singapore Time SST – Singapore Standard Time | Asia     | UTC +8 |

## 夏令时

`DST`（Daylight Saving Time），夏令时又称夏季时间，或者夏时制。
> 它是为节约能源而人为规定地方时间的制度。一般在天亮早的夏季人为将时间提前一小时，可以使人早起早睡，减少照明量，以充分利用光照资源，从而节约照明用电。
>
> 全球约40%的国家在夏季使用夏令时，其他国家则全年只使用标准时间。标准时间在有的国家也因此被相应地称为冬季时间。
>
> 在施行夏令时的国家，一年里面有一天只有23小时（夏令时开始那一天），有一天有25小时（夏令时结束那一天），其他时间每天都是24小时。
>
> `DST`是夏令时（`Daylight Saving Time`）的缩写，在一年的某一段时间中将当地时间调整（通常）一小时。 DST的规则非常神奇（由当地法律确定），并且每年的起止时间都不同。C语言库中有一个表格，记录了各地的夏令时规则（实际上，为了灵活性，C语言库通常是从某个系统文件中读取这张表）。从这个角度而言，这张表是夏令时规则的唯一权威真理。

## 本地时间Local time

> 在日常生活中所使用的时间我们通常称之为本地时间。这个时间等于我们所在（或者所使用）时区内的当地时间，它由与世界标准时间（UTC）之间的偏移量来定义。这个偏移量可以表示为 UTC- 或 UTC+，后面接上偏移的小时和分钟数。
> 本地时间就是用当地时区的时间表示。通常代码会自动获取操作系统的Time zone设置来转换成本地时间， 例如 `new Date()`.

'2024-08-19T17:00:00.380Z' UTC时间
例如在中国的本地时间就是Tue Aug 20 2024 16:33:09 GMT+0800 (China Standard Time)
和其他时区的本地时间不同

# internationalization其他基本概念

`i18n` ( internationalization ) 简称国际化 ，在现代前端开发中，有国际化需求的网站 / app，都需要进行 i18n 进行多语言的处理。

`ISO`(International Organization for Standardization) 国际标准化组织.

[字符编码那些事儿](http://cuihuan.net/2019/05/12/%E5%AD%97%E7%AC%A6%E7%BC%96%E7%A0%81%E9%82%A3%E4%BA%9B%E4%BA%8B%E5%84%BF/)

## [`CLDR`](https://cldr.unicode.org/)

> [`CLDR`](https://cldr.unicode.org/)
> The Unicode `Common Locale Data Repository` (CLDR) provides key building blocks for software to support the world's languages, with the largest and most extensive standard repository of locale data available. This data is used by a wide spectrum of companies for their software internationalization and localization, adapting software to the conventions of different languages for such common software tasks.

通用语言环境数据仓库[`CLDR`](https://cldr.unicode.org/)
通用语言环境数据仓库 (Common Locale Data Repository, CLDR) 项目是 Unicode Consortium 的一个项目，用于提供扩展的语言环境数据。CLDR 包含特定于语言环境的信息，操作系统通常会将该信息提供给应用程序。该信息包含数字格式、日期、时间和货币字符串、字符分类（小写、大写、可打印等）、字符串整理规则以及其他内容。
CLDR 是以 Unicode 的编码标准作为前提，将多国的语言文字进行编码的。
CLDR 不仅阐述了每个国家语言的文字应当如何被解析，并且，为了解析结果的可靠，还规定了结果集排序方式。
该项目每年提供两次版本更新，一次是4月份，一次是10月份。github最新开发版本：[github-unicode-org/cldr](https://github.com/unicode-org/cldr/tree/latest)，可以下载[最新数据](https://github.com/unicode-org/cldr/releases)。
国家下属子区域名称也有各种语言的翻译：[subdivisions](https://github.com/unicode-org/cldr/tree/latest/common/subdivisions)，可用的区域英文名称和代码：[Territory Subdivisions](https://unicode.org/cldr/charts/latest/supplemental/territory_subdivisions.html)，例如代码cnhb的中文简体（目前在yue_Hans.xml文件中）是“湖北”，可以考虑以后用到需要翻译国家下面一级或者两级子区域的网站，例如[邮编库系列网站](https://youbianku.com/)。

CLDR 是 Unicode Consortium（Unicode 联盟）下属的一个项目，并不从属于 Unicode Standard（Unicode 标准，即我们一般说的 Unicode），它们是两个平行的项目。

### Java 中的CLDR

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

## [ICU](https://icu.unicode.org/)

ICU (`International Components for Unicode`)是为软件应用提供Unicode和全球化支持的一套成熟、广泛使用的C/C++、Java和.NET 类库集，可在所有平台的C/C++、Java和C# 软件上获得一致的结果，用于支持软件国际化的开源项目, 软件开发者几乎可以使用ICU 解决任何国际化的问题，根据各地的风俗和语言习惯，实现对数字、货币、时间、日期、和消息的格式化、解析，对字符串进行大小写转换、整理、搜索和排序等功能。ICU的主页是<http://www.icu-project.org/>

> 在unicode的统治下，世界各国的基本编码不会出现乱码等异常。但当中华民族逐步强大，准备冲出中国统一世界的时候，发现各国的货币，时间，数字等表示灰常不统一，例如数字1234.5，英文表示1,234.5，葡语表示确是1.234,5，很是苦恼。
>
> 此时IBM站了出来，叫上google,apple等小伙伴，遵循”IBM公共许可证”，开源了一套基于unicode的国际化组件ICU(International Component for Unicode
> )。根据各地的风俗和语言习惯，实现对数字、货币、时间、日期、和消息的格式化、解析，对字符串进行大小写转换、整理、搜索和排序等功能，ICU4C提供了强大的BIDI算法，对阿拉伯语等BIDI语言提供了完善的支持。
>
> ICU成为了目前国际化组件的实事标准，底层依赖UNICODE和CLDR，官方提供了C/C++和JAVA的SDK，ICU4C和ICU4J，同时，各个语言在此基础上开发了各个语言的版本，例如php的intl组件。

ICU首先是由Taligent(泰利根)公司开发的，Taligent公司被合并为IBM公司全球化认证中心的Unicode研究组后，ICU由IBM和开源组织合作继续开发。

- 开始ICU只有Java平台的版本，后来这个平台下的ICU类被吸纳入SUN公司开发的JDK1.1，并在JDK以后的版本中不断改进。
- C++和C平台下的ICU是由JAVA平台下的ICU移植过来的，移植过的版本被称为ICU4C，来支持这C/C++两个平台下的国际化应用。
- ICU4J和ICU4C区别不大，但由于ICU4C是开源的，并且紧密跟进Unicode标准，ICU4C支持的Unicode标准总是最新的；同时，因为JAVA平台的ICU4J的发布需要和JDK绑定，ICU4C支持Unicode标准改变的速度要比ICU4J快的多。
- 在Linux 操作系统上，.NET Core 使用ICU的全球化API， 从 .NET 5.0 开始，如果应用在 Windows 10 2019 年 5 月更新或更高版本上运行，.NET 库将使用 ICU 全球化 API。.NET 5 统一使用ICU, 引入此更改的原因有两个：

  - 应用跨平台（包括 Linux、macOS 和 Windows）具有相同的全球化行为。
  - 应用可以通过使用自定义 ICU 库来控制全球化行为。

ICU的功能主要有:

- 代码页转换: 对文本数据进行Unicode、几乎任何其他字符集或编码的相互转换。ICU的转化表基于IBM过去几十年收集的字符集数据，在世界各地都是最完整的。
- 排序规则（Collation）: 根据特定语言、区域或国家的管理和标准比较字数串。ICU的排序规则基于Unicode排序规则算法加上来自公共区域性数据仓库（Common locale data repository）的区域特定比较规则。
- 格式化: 根据所选区域设置的惯例，实现对数字、货币、时间、日期、和利率的格式化。包括将月和日名称转换成所选语言、选择适当缩写、正确对字段进行排序等。这些数据也取自公共区域性数据仓库。
- 时间计算: 在传统格里历基础上提供多种历法。提供一整套时区计算API。
- Unicode支持: ICU紧密跟进Unicode标准，通过它可以很容易地访问Unicode标准制定的很多Unicode字符属性、Unicode规范化、大小写转换和其他基础操作。
- 正则表达式: ICU的正则表达式全面支持Unicode并且性能极具竞争力。
- Bidi: 支持不同文字书写顺序混合文字（例如从左到右书写的英语，或者从右到左书写的阿拉伯文和希伯来文）的处理。
- 文本边界: 在一段文本内定位词、句或段落位置、或标识最适合显示文本的自动换行位置。

# 编程语言中的DateTime format

## JavaScript中的DateTime

### 原生JavaScript

[MDN Date()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/Date)

```javascript
const date1 = new Date('December 17, 1995 03:24:00');
// Sun Dec 17 1995 03:24:00 GMT...
const date2 = new Date('1995-12-17T03:24:00');
// Sun Dec 17 1995 03:24:00 GMT...

console.log(date1 === date2);
// Expected output: false
console.log(date1 - date2);
// Expected output: 0
```

#### 语法

```javascript
new Date()   // now
new Date(value)  // timestamp (the number of milliseconds since midnight at the beginning of January 1, 1970, UTC
new Date(dateString)
new Date(dateObject)

new Date(year, monthIndex)
new Date(year, monthIndex, day)
new Date(year, monthIndex, day, hours)
new Date(year, monthIndex, day, hours, minutes)
new Date(year, monthIndex, day, hours, minutes, seconds)
new Date(year, monthIndex, day, hours, minutes, seconds, milliseconds)

Date()
```

```javascript
const today = new Date();
const birthday = new Date("December 17, 1995 03:24:00"); // DISCOURAGED: may not work in all runtimes
const birthday = new Date("1995-12-17T03:24:00"); // This is standardized and will work reliably
const birthday = new Date(1995, 11, 17); // the month is 0-indexed
const birthday = new Date(1995, 11, 17, 3, 24, 0);
const birthday = new Date(628021800000); // passing epoch timestamp
```

```javascript
console.log(new Date(undefined)); // Invalid Date
console.log(new Date(null)); // 1970-01-01T00:00:00.000Z
console.log(new Date(["2020-06-19", "17:13"]));
// 2020-06-19T17:13:00.000Z in Chrome, since it recognizes "2020-06-19,17:13"
// "Invalid Date" in Firefox
```

#### 原生JS时区

> 注意 `new Date()` 会默认生成本地时间, 也就是带时区的时间

```javascript
const date = new Date("2024-08-19T17:28:38.380Z")
// Tue Aug 20 2024 01:28:38 GMT+0800 (China Standard Time)
// new Date会默认生成本地时间，time zone从 OS 操作系统的time zone设置读取

const utcYear = date.getUTCFullYear(); // 2024
const utcMonth = date.getUTCMonth() + 1; // 8, Adding 1 because getUTCMonth() returns zero-based index 7
const utcDay = date.getUTCDate(); // 19

const year = date.getFullYear().toString()   // 2024
const month = (date.getMonth() + 1).toString().padStart(2, '0') // 8
const day = date.getDate().toString().padStart(2, '0') 
// if time zone is GMT+0800, day is 20
// if time zone is GMT+0000, day is 19

// 修改timezone
const date = new Date("2024-08-19T17:28:38.380Z");
const options = { timeZone: 'Asia/Shanghai' };
const dateString = date.toLocaleString('en-US', options);
console.log(dateString); // '8/20/2024, 1:28:38 AM'
```

#### Local date time

- `toString()`, `toDateString()`, `toTimeString()`
- `toLocaleString()`,`toLocaleDateString()`, `toLocaleTimeString()`

```javascript
const event = new Date('05 October 2011 21:48 UTC');

/* ------------------Local------------------ */
console.log(event.toString());
// Expected output: "Thu Oct 06 2011 05:48:00 GMT+0800 (China Standard Time)"
// Note: your timezone may vary
console.log(event.toDateString());
// this date interpreted in the local timezone
// Expected output: 'Thu Oct 06 2011'
event.toTimeString()
// '05:48:00 GMT+0800 (China Standard Time)'

// returns a string with a language-sensitive representation of the date portion of this date in the local timezone
// toLocaleDateString()
// toLocaleDateString(locales)
// toLocaleDateString(locales, options)
console.log(event.toLocaleDateString());
// '10/6/2011'
event.toLocaleDateString("nl-Latn-BE")
// '6-10-2011'
event.toLocaleDateString("fi")
// '6.10.2011'
event.toLocaleDateString("sr-CS")
// '6. 10. 2011.'
event.toLocaleDateString("fr-CA")
// '2011-10-06'
const options = {
  weekday: 'long',
  year: 'numeric',
  month: 'long',
  day: 'numeric',
};
event.toLocaleDateString('de-DE', options)
// 'Donnerstag, 6. Oktober 2011'
event.toLocaleDateString('ar-EG', options)
// 'الخميس، ٦ أكتوبر ٢٠١١'
event.toLocaleDateString(undefined, options)
// 'Thursday, October 6, 2011'

// toLocaleString()
// toLocaleString(locales)
// toLocaleString(locales, options)
// British English uses day-month-year order and 24-hour time without AM/PM
event.toLocaleString('en-GB', { timeZone: 'UTC' })
// '05/10/2011, 21:48:00'
// Korean uses year-month-day order and 12-hour time with AM/PM
event.toLocaleString('ko-KR', { timeZone: 'UTC' })
// '2011. 10. 5. 오후 9:48:00'

// toLocaleTimeString()
// toLocaleTimeString(locales)
// toLocaleTimeString(locales, options)
event.toLocaleTimeString('en-US')
// '5:48:00 AM'
event.toLocaleTimeString('it-IT')
// '05:48:00'
event.toLocaleTimeString('ar-EG')
// '٥:٤٨:٠٠ ص'
```

#### UTC datetime

- `toISOString()`，`toJSON()`
- `toUTCString()`, `toGMTString()`

```javascript
const event = new Date('05 October 2011 21:48 UTC');
/* ------------------UTC------------------ */
console.log(event.toISOString()); 
// a simplified format based on ISO 8601, which is always 24 or 27 characters long (YYYY-MM-DDTHH:mm:ss.sssZ or ±YYYYYY-MM-DDTHH:mm:ss.sssZ, respectively). The timezone is always UTC, as denoted by the suffix Z.
// Expected output: "2011-10-05T21:48:00.000Z"
console.log(event.toJSON());
// in the same ISO format as toISOString()
// '2011-10-05T21:48:00.000Z'

console.log(event.toGMTString());
// Expected output: 'Wed, 05 Oct 2011 21:48:00 GMT'
event.toUTCString()
// 'Wed, 05 Oct 2011 21:48:00 GMT'
// The timezone is always UTC. toGMTString() is an alias of this method.
```

#### 生成current time的UTC String

```javascript
export function getNowUTCFormatted() {
    const date = new Date()
    const year = date.getUTCFullYear()
    const month = String(date.getUTCMonth() + 1).padStart(2, '0')
    const day = String(date.getUTCDate()).padStart(2, '0')
    const hours = String(date.getUTCHours()).padStart(2, '0')
    const minutes = String(date.getUTCMinutes()).padStart(2, '0')
    const seconds = String(date.getUTCSeconds()).padStart(2, '0')
    const milliseconds = String(date.getUTCMilliseconds()).padStart(3, '0')

    // 'YYYY-MM-DDTHH:mm:ss.SSSZZ'
    const utcString = `${year}-${month}-${day}T${hours}:${minutes}:${seconds}.${milliseconds}+0000`
    return utcString
}
```

#### 生成本地时间Local time `MM/dd/yyyy`

```javascript
export function getLocalDateFromUTCTime(utcTimeStr: string, _displayLocale: string): string {
  const date = new Date(utcTimeStr)
  const year = date.getFullYear().toString()
  const month = (date.getMonth() + 1).toString().padStart(2, '0')
  const day = date.getDate().toString().padStart(2, '0')
  return `${month}/${day}/${year}`
  // MM/dd/yyyy
}

// unit test
  describe('getLocalDateFromUTCTime', () => {
    it('should format UTC time correctly', () => {
      const utcTimeStr = '2023-10-01T12:00:00Z'
      const formattedDate = getLocalDateFromUTCTime(utcTimeStr, 'en')
      expect(formattedDate).toBe('10/01/2023')

      const utcTimeStr2 = '2024-08-19T17:00:00.380Z'
      const formattedDate2 = getLocalDateFromUTCTime(utcTimeStr2, 'en')
      // get current timezone
      const timezoneOffsetInMinutes = new Date().getTimezoneOffset()  // -480
      const hours = Math.abs(Math.floor(timezoneOffsetInMinutes / 60)) // 8
      const minutes = Math.abs(timezoneOffsetInMinutes % 60); // 0

      const sign = timezoneOffsetInMinutes > 0 ? '-' : '+' // '+'
      const utcOffset = `UTC${sign}${hours.toString().padStart(2, '0')}:${minutes.toString().padStart(2, '0')}`; // UTC+08:00

      /* eslint-disable */
      if (sign === '+' && hours >= 7) {
        // for Shanghai timezone, the date should be 08/20/2024
        expect(formattedDate2).toBe('08/20/2024')
      } else {
        expect(formattedDate2).toBe('08/19/2024')
      }
      /* eslint-enable */
    })
  })
```

#### 生成UTC `MM/dd/yyyy`

```javascript
export function getLocalDateFromUTCTime(utcTimeStr: string, _displayLocale: string): string {
const date = new Date(utcTimeStr);
const year = date.getUTCFullYear();
const month = date.getUTCMonth() + 1; // Adding 1 because getUTCMonth() returns zero-based index
const day = date.getUTCDate();
console.log(year, month, day);
  // MM/dd/yyyy
}
```

### JS库 - Moment [Deprecated]

#### Moment global import issue

<https://codesandbox.io/s/moment-import-issue-17oqzz>

### [JS库 - dayjs](https://www.npmjs.com/package/dayjs)

[Format token： 'YYYY-MM-DDTHH:mm:ss.SSSZZ'代表什么](https://day.js.org/docs/en/parse/string-format#list-of-all-available-parsing-tokens)

#### dayjs生成current time的UTC String

```javascript
import dayjs from 'dayjs'
import utc from 'dayjs/plugin/utc'

export function getNowUTCFormatted() {
  // new Date(0) = Unix Epoch Start Time(Midnight, January 1, 1970 UTC)
  // Formart new Date(0) to expected format '1970-01-01T00:00:00.000+0000'
  const now = new Date()
  dayjs.extend(utc)
  const formattedDateTime = dayjs(now).utc().format('YYYY-MM-DDTHH:mm:ss.SSSZZ')
  // "SSS" represents the three-digit millisecond. For example, "123" represents 123 milliseconds.
  // "ZZ" represents the time zone offset. In this case, it is "+0000," which means the time is in Coordinated Universal Time (UTC) with no offset.
  return formattedDateTime
}
```

#### 生成本地时间[Local time](https://day.js.org/docs/en/manipulate/local) `MM/dd/yyyy`

```javascript
export function getLocalDateFromUTCTime(utcTimeStr: string, _displayLocale: string): string {
  // utc(keepLocalTime?: boolean)
  const formattedDateTime = dayjs(utcTimeStr).utc(true).format('MM/dd/yyyy')
  return formattedDateTime
}
```

#### dayjs生成[UTC](https://day.js.org/docs/en/manipulate/utc) `MM/dd/yyyy`

```javascript
export function getLocalDateFromUTCTime(utcTimeStr: string, _displayLocale: string): string {
  const formattedDateTime = dayjs(utcTimeStr).utc().format('MM/dd/yyyy')
  return formattedDateTime
}
```

#### dayjs [UTC](https://day.js.org/docs/en/plugin/utc) adds .utc .local .isUTC APIs to parse or display in UTC

```javascript
var utc = require("dayjs/plugin/utc");
// import utc from 'dayjs/plugin/utc' // ES 2015

dayjs.extend(utc);

// default local time
dayjs().format(); //2019-03-06T17:11:55+08:00

// UTC mode
dayjs.utc().format(); // 2019-03-06T09:11:55Z

// convert local time to UTC time
dayjs().utc().format(); // 2019-03-06T09:11:55Z

// While in UTC mode, all display methods will display in UTC time instead of local time.
// And all getters and setters will internally use the Date#getUTC* and Date#setUTC* methods instead of the Date#get* and Date#set* methods.
dayjs.utc().isUTC(); // true
dayjs.utc().local().format(); //2019-03-06T17:11:55+08:00
dayjs.utc("2018-01-01", "YYYY-MM-DD"); // with CustomParseFormat plugin
```

#### [Time Zone](https://day.js.org/docs/en/timezone/timezone)

```javascript
dayjs.extend(utc)
dayjs.extend(timezone)

// current time zone is 'Europe/Berlin' (offset +01:00)
// Parsing
dayjs.tz("2013-11-18 11:55:20", "America/Toronto") // '2013-11-18T11:55:20-05:00'

// Converting (from time zone 'Europe/Berlin'!)
dayjs("2013-11-18 11:55:20").tz("America/Toronto") // '2013-11-18T05:55:20-05:00'
```

## Java 中的DateTime

### [Java 中的时间戳](./%E6%97%A5%E6%9C%9F%E6%A0%BC%E5%BC%8FDateTimeFormat-yyyy-MM-dd-HH-mm-ss-%E5%9D%91-%E5%A4%A7%E5%B0%8F%E5%86%99%E5%8C%BA%E5%88%AB.html#java-%E4%B8%AD%E7%9A%84%E6%97%B6%E9%97%B4%E6%88%B3)

### Java 中的DateTime format

```java
import java.text.Format;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.Calendar;
public class Demo {
    public static void main(String[] args) throws Exception {
        // displaying current date and time
        Calendar cal = Calendar.getInstance();
        String formatStr = "dd/MMMM/yyyy hh:mm:ss zzzz";
        SimpleDateFormat simpleformat = new SimpleDateFormat(formatStr);
        System.out.println("Today's date '" + formatStr + "' = " + simpleformat.format(cal.getTime()));

        formatStr = "dd/MMM/yyy hh:mm:ss zzz";
        Format f = new SimpleDateFormat(formatStr);
        System.out.println("Today's date '" + formatStr + "' = " + f.format(new Date()));

        formatStr = "dd/MM/yy hh:mm:ss zz";
        f = new SimpleDateFormat(formatStr);
        System.out.println("Today's date '" + formatStr + "' = " + f.format(new Date()));

        formatStr = "d/M/y h:mm:s z";
        f = new SimpleDateFormat(formatStr);
        System.out.println("Today's date '" + formatStr + "' = " + f.format(new Date()));

        // current time
        System.out.println("------Time----------");
        formatStr = "hh:mm:ss a";
        f = new SimpleDateFormat(formatStr);
        String strResult = f.format(new Date());
        System.out.println("Time '" + formatStr + "' = "+strResult); // Time = 02:52:28 AM

        // Illegal pattern character 'A'at java.text.SimpleDateFormat.compile(SimpleDateFormat.java:826)
        // formatStr = "hh:mm:ss A";
        // f = new SimpleDateFormat(formatStr);
        // strResult = f.format(new Date());
        // System.out.println("Time '" + formatStr + "' = "+strResult);

        // displaying hour
        f = new SimpleDateFormat("H");
        String strHour = f.format(new Date());
        System.out.println("Current Hour = "+strHour); // Current Hour = 2

        // displaying minutes
        f = new SimpleDateFormat("mm");
        String strMinute = f.format(new Date());
        System.out.println("Current Minutes = "+strMinute); // Current Minutes = 52

        // displaying seconds
        f = new SimpleDateFormat("ss");
        String strSeconds = f.format(new Date());
        System.out.println("Current Seconds = "+strSeconds); // Current Seconds = 28
    }
}
```

输出：

```text
Today's date 'dd/MMMM/yyyy hh:mm:ss zzzz' = 25/November/2022 08:33:21 Coordinated Universal Time
Today's date 'dd/MMM/yyy hh:mm:ss zzz' = 25/Nov/2022 08:33:21 UTC
Today's date 'dd/MM/yy hh:mm:ss zz' = 25/11/22 08:33:21 UTC
Today's date 'd/M/y h:mm:s z' = 25/11/2022 8:33:21 UTC
------Time----------
Time 'hh:mm:ss a' = 08:33:21 AM
Current Hour = 8
Current Minutes = 33
Current Seconds = 21
```

## 参考文章

- [彻底弄懂GMT、UTC、时区和夏令时](https://zhuanlan.zhihu.com/p/135951778)
- [什么是时间戳](https://blog.csdn.net/wildpal/article/details/40039977?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522166865369616800215039495%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=166865369616800215039495&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~baidu_landing_v2~default-6-40039977-null-null.142^v63^control,201^v3^control,213^v2^t3_esquery_v3&utm_term=%E6%97%B6%E9%97%B4%E6%88%B3&spm=1018.2226.3001.4187)

其他语言日期格式

- [C#日期型数据简单剖析](https://www.51cto.com/article/147694.html)
- [在jsp页面中使用EL表达式格式化date日期](https://cloud.tencent.com/developer/article/1653924)
- [3.11.0 Documentation » Python 标准库 » 通用操作系统服务 » time --- 时间的访问和转换](https://docs.python.org/zh-cn/3/library/time.html)
