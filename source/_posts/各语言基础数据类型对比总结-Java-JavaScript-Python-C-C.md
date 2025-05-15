---
title: '各编程语言对比总结-Java, JavaScript, Python, C, C++'
catalog: true
date: 2022-01-08 17:57:27
subtitle: 基础数据类型
header-img:
tags:
- TODO
categories:
- TECH
- Language
---

## 基础数据类型

| ​**类型/语言**    | JavaScript      | Java           | Python               | C             | C++       |
| ----------------- | ---------------- |  ----------------- |  ------------ |   ----- |   ----------- |
| ​**整数类型**     | `number`（64位双精度浮点数，统一整数和浮点）[1](@ref) | `byte`（8位，-128~127）、`short`（16位）、`int`（32位）、`long`（64位） | `int`（动态精度，理论无限大）           | `short`（16位）、`int`（32位）、`long`（32/64位）、`long long`（64位） | 同 C，新增固定宽度类型（如 `int32_t`、`int64_t`）[1,3](@ref)       |
| ​**浮点数类型**   | `number`（64位双精度）[1](@ref)    | `float`（32位）、`double`（64位）    | `float`（64位双精度）   | `float`（32位）、`double`（64位）、`long double`（80/128位）           | 同 C，支持 `long double`（更高精度，80/128位）[3,5](@ref)          |
| ​**字符类型**     | 无独立类型，用 `string` 表示      | `char`（16位 Unicode）  | 无独立类型，用长度为1的 `str` 表示      | `char`（8位，-128~127） | `char`（同 C），新增 `wchar_t`（宽字符，16/32位）[1,3](@ref)       |
| ​**布尔类型**     | `boolean`（`true`/`false`）   | `boolean`（逻辑值，JVM 依赖）  | `Bpytool`（继承自 `int`，True=1，False=0） | `_Bool`（C99+，0/1）[4](@ref)         | `bool`（`true`/`false`，1字节）[1,2](@ref)      |
| ​**空值表示**     | `null`、`undefined`  | 原始类型无空值（引用类型默认 `null`， null 不能直接赋值给基本类型（如 int、boolean），否则会导致编译错误） | `None`（NoneType 数据类型的唯一值）   | `NULL`（空指针宏）[2](@ref)      | `nullptr`（类型安全空指针，C++11+）[2,5](@ref)  |
| 大整数支持 | BigInt（ES2020+，后缀 n，支持任意精度整数） | 无原生支持，需通过 BigInteger 类 |	原生 int 支持任意精度，无需特殊类型
| ​**特殊类型**     | `Symbol`（唯一标识符）             | 无             | 无   | 指针（`*`）、联合体（`union`）、枚举（`enum`）[4](@ref)









































































































| 引用（`&`）、类（`class`）、模板（泛型）[2,5](@ref)  |
| ​**类型转换规则** | 隐式转换频繁（如 `"5" + 2 = "52"`）   | 严格类型检查，窄化需显式强制转换  | 隐式转换仅限数字，其他需显式转换        | 隐式转换宽松（如 `int` 转 `float`），强制转换用 `(type)`[4](@ref)      | 支持显式转换（`static_cast`、`reinterpret_cast` 等）[5](@ref)      |
| ​**内存管理**     | 自动垃圾回收    | 自动垃圾回收（对象堆分配）        | 自动垃圾回收         | `malloc`/`free`（手动）[4](@ref) | `new`/`delete`（面向对象），兼容 C 风格[5](@ref)   |
| ​**类型系统特性** | 动态弱类型      | 静态强类型     | 动态强类型           | 弱类型（无编译时检查）[4](@ref)  | 强类型（支持编译时检查，引入 `const` 和类型转换操作符）[1,5](@ref) |

### 关键差异总结

1. ​整数与浮点数

* ​C/C++：明确区分位宽（如 short、long），C++扩展 long long58。
* ​Java：严格固定位宽（如 int=32位）。
* ​Python/JS：动态类型，无固定位宽限制。

2. ​布尔类型
​C：依赖C99的 _Bool，本质是整数0/19。
​C++：原生 bool，逻辑更清晰6。
​Python：bool 是 int 的子类，兼容1/0。

3. ​空值与指针
​C：NULL 是宏定义的 (void*)0，易引发类型问题。
​C++：nullptr 类型安全，避免歧义。
​Java：原始类型无空值，引用类型默认 null。Java 的 null 是引用类型变量的“无值”状态，需通过判空和规范使用避免 NullPointerException。理解其特性（如类型限制、默认值规则）是编写健壮代码的基础，而与其他语言的对比则体现了 Java 在类型安全上的设计取舍。
JavaScript 有 null 和 undefined
Python 用 None

    | 语言 | ​空值表示 | ​特性 |
    | ---------|----------|---------|
    | ​Java | null | 仅用于引用类型，强制类型安全，需显式判空。|
    | ​Python | None | 类似 null，但所有变量均为对象，无基本类型限制。|
    | ​C++ | NULL | 宏定义为 0 或 nullptr（C++11+），用于指针类型。|

4. 类型安全与转换
​C/C++：C允许隐式危险转换，C++引入显式转换操作符增强安全性。
​Java：编译时严格检查，避免隐式窄化转换。

5. ​内存管理
​C/C++：手动管理（malloc/new），C++支持RAII和智能指针。
​其他语言：自动垃圾回收，减少内存泄漏风险。

6. ​类型系统：
​JavaScript：动态弱类型，仅 number 统一表示数字78。
​Java：静态强类型，8种原始类型均有固定位数和范围1011。
​Python：动态强类型，基本类型为对象，但 int 支持无限精度1213。

7. ​数值精度：
JavaScript 和 Python 的浮点数均为64位双精度，但 Java 提供单/双精度选项71012。
大整数支持：JavaScript 需 BigInt，Java 依赖类库，Python 原生支持81012。

8. ​字符处理：
仅 Java 有独立 char 类型，JavaScript 和 Python 用字符串表示字符71012。

9. ​类型安全：
Java 最严格（编译时类型检查），JavaScript 和 Python 更灵活但易产生隐式错误。
此表格综合了三者在设计哲学和应用场景上的差异：JavaScript 强调灵活性，Java 注重性能与类型安全，Python 以简洁和动态性见长。

### ​补充说明

​C++特有类型：引用（变量别名）、类对象、模板（泛型）、智能指针（如 std::unique_ptr）。
​C语言局限：无原生面向对象支持，需通过结构体和函数指针模拟。
​跨语言对比：C/C++注重底层控制，Java/Python/JS侧重开发效率与安全性。

## 操作符
