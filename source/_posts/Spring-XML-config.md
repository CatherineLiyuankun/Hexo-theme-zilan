---
title: Spring 实战 - 3 最小化 Spring XML config
catalog: true
date: 2021-12-05 19:04:41
subtitle: Spring 实战
header-img:
tags:
- Java
- Spring
categories:
- TECH
- BackEnd
- Spring
---

# 3 最小化 Spring XML config

## 3.1 AutoWiring 自动装配 `autowire`

减少or消除配置`<property>` 和`<constructor-arg>`元素，让Spring自动识别如何装配Bean的依赖关系。

### 3.1.1 自动装配类型

#### byName

`<bean id="lyk" 
    class="com.xxx.yyy.zzz"
    autowire="byName">
</bean>`

#### byType

解决多个bean匹配问题：

##### primary 首选

默认值true 
`primary="false"` 非首选

##### autowire-candidate

`autowire-candidate="false"` 排除

#### constructtor

#### autodetect = constructtor || byType

### 3.1.2 默认自动装配default-autowire

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans-3.1.xsd"
       default-autowire="byType">
</beans>
```

### 3.1.3 自动装配+显示装配

用`constructtor`自动装配时，不能混合使用`autowire="constructtor"` 和`<constructor-arg>`.

## 3.2 注解装配 `<context:annotation-config/>`

减少or消除配置`<property>` 和`<constructor-arg>`元素，让Spring自动识别注解，装配Bean的依赖关系。


```xml
<beans xmlns="http://www.springframewoirk.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans-3.1.xsd"
       default-autowire="byType">
  <context:annotation-config/>     
</beans>
```

### 3.2.1 Sping自带的`@Auttowired`

Spring使用byType自动装配`@Auttowired`注解

#### 可选装配属性`required`

`@Auttowired(required=false)`

#### 限定`@Qualifier("beanID")`

缩小匹配bean的选择范围，默认使用Bean的ID

```java
@Auttowired
@Qualifier("beanID")
```

### 3.2.2 JSR-330的`@Inject`

#### 没有`required`属性

#### 限定`@Named("beanID")`

通过Bean的ID来标识可选择的Bean

### 3.2.3 JSR-3250的`@Resource`


## 3.3 AutoDiscovering 自动检测 `<context:component-scan>`

自动识别哪些类要配置成Spring Bean, 减少`<bean>`元素的使用。

```xml
<beans xmlns="http://www.springframewoirk.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans-3.1.xsd"
       default-autowire="byType">
    <context:annotation-config/>     

    <context:component-scan base-package="com.microstrategy.auth.saml.config">
        <context:include-filter type="assignable" expression="com.xxx.uuu"/>
        <context:exclude-filter type="regex" expression=">org.bouncycastle.*"/>
    </context:component-scan>
</beans>
```

### 3.3.1 自动检测标注Bean

#### `@Component` 通用的构造型注解，将该类定义为Spring 组件

#### `@Controller` 将该类定义为Spring MVC Controller

#### `@Repository` 将该类定义为数据仓库

#### `@Service` 将该类定义为服务

#### 用`@Component`标注的任意自定义注解

### 3.3.2 过滤 `<context:include-filter>``<context:exclude-filter>`

type 类型

#### `type="annotation"`

与expression属性所指定的注解所标注的那些类。

#### `type="assignable"`

与expression属性所指定类型的那些类。

#### `type="aspectj"`

与expression属性所指定的AspectJ表达式所匹配的那些类。

#### `type="custom"`

使用自定义org.springframework.core.type.TypeFilter实现类，由expression属性指定

#### `type="regex"`

与expression属性所指定的正则表达式所匹配的那些类。

## 3.4 使用Spring基于Java的配置

取代xml配置，但是仍需要少量xml配置：

```xml
<beans xmlns="http://www.springframewoirk.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans-3.1.xsd"
       default-autowire="byType">

    <context:component-scan base-package="com.microstrategy.auth.saml.config"/>
</beans>
```

## 3.4.1 `@Configuration` 对应 `<beans>`

## 3.4.2 `@Bean` 对应 `<bean>`
