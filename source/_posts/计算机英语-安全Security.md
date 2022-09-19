---
title: 计算机英语-安全Security
catalog: true
date: 2022-09-02 14:24:17
subtitle:
header-img:
tags:
categories:
- English Learning
- 计算机英语
---

## 攻击类型

STRIDE英文 | 读音 | 含义
----------|---------|---------
spoofing | 美/ˈspuːfɪŋ/ | 电子欺骗; 在网络上或邮件中假冒他人的行为或事例。the act or an instance of impersonating another person on the internet or via email. Refers to illegal access and use of data.
Tampering | 美/ˈtæmpərɪŋ/ | 篡改数据 Refers to malicious modification of data. Can be done to data at rest, or in transit.指恶意修改数据。 可以对静止或传输中的数据进行处理。
Repudiation | 美/rɪˌpjuːdiˈeɪʃ(ə)n/ | 否认、抵赖。不可否认/抵赖性（Non-repudiation）. Occurs when the system cannot trace and prove actions performed by a user. 当系统无法跟踪和证明用户执行的操作时出现。
Information disclosure || Information disclosure refers to exposing information to unauthorized entities. For example, a user is able to read a file that does not belong to them, or a threat actor gains access to data in transit. 信息泄露是指将信息暴露给未经授权的实体。 例如，用户能够读取不属于他们的文件，或者威胁参与者可以访问传输中的数据。
Elevation of privilege || 权限提升 Elevation of privilege refers to a situation where an attacker successfully gains access to restricted levels of a svstem. The attackers can then access sensitive data, restricted functionality, and connected systems.特权提升是指攻击者成功获得对受限制级别的系统的访问权限的情况。 然后，攻击者可以访问敏感数据、受限功能和连接的系统。
DOS (Denial of Service)|| 服务不可用 Denial of Service occurs when a web server is made temporarily unavailable or unusable to a valid user. Protection from such threats improves system consistency and availability. 当 Web 服务器暂时不可用或对有效用户不可用时，就会发生拒绝服务。 防范此类威胁可提高系统一致性和可用性。


英文 | 读音 | 含义
----------|---------|---------
Phishing| 美/ˈfɪʃɪŋ/ | 网络钓鱼 the activity of tricking people by getting them to give their identity, bank account numbers, etc. over the Internet or by email, and then using these to steal money from them 网络诱骗（通过互联网或电邮骗取他人身份证件、银行账号等以盗取金钱）
Injection || 注入 例如 SQL Injection

## 缩写

英文 | 读音 | 含义
----------|---------|---------
DOS (Denial of Service)|| 服务不可用 Denial of Service occurs when a web server is made temporarily unavailable or unusable to a valid user. Protection from such threats improves system consistency and availability. 当 Web 服务器暂时不可用或对有效用户不可用时，就会发生拒绝服务。 防范此类威胁可提高系统一致性和可用性。
DFDs (Data flow diagrams)  || The threat modeling approach requires you to use data flow diagrams (or DFDs).<br/>A data flow diagram is an organized evaluation and design method used for software analvsis. It represents the flow of data through the system. DFD supports decomposition, to graphically depict the flow of data and functions in the system.<br/>A DFD provides:<br/>- A system design to support the analysis and requirement stage.<br/>- A detailed system diagram.<br/>- Description of the network of activities of the target system.<br/>- Step-by-step modification through tiered disintegration of activities.
OWASP Application Security Verification Standards (ASVS) || a community-driven attempt to begin a framework of security controls that focuses on outlining the functional and non functional security controls essential for development, design,and testing of modern web services and applications.


英文 | security assessment methodologies | 含义
----------|---------|---------
SAST|（Static Application Security Testing）| 测试或运行阶段分析应用程序的动态运行状态。它模拟黑客行为对应用程序进行动态攻击，分析应用程序的反应，从而确定该Web应用是否易受攻击。
DAST|（Dynamic Application Security Testing）| 在编码阶段分析应用程序的源代码或二进制文件的语法、结构、过程、接口等来发现程序代码存在的安全漏洞。
IAST| 交互式应用程序安全测试（Interactive Application Security Testing）| 是2012年Gartner公司提出的一种新的应用程序安全测试方案，通过代理、VPN或者在服务端部署Agent程序，收集、监控Web应用程序运行时函数执行、数据传输，并与扫描器端进行实时交互，高效、准确的识别安全缺陷及漏洞，同时可准确确定漏洞所在的代码文件、行数、函数及参数。IAST相当于是DAST和SAST结合的一种互相关联运行时安全检测技术。

对比 | SAST | DAST
----------|---------|---------
||Inside-out security testing method.| Outside-in security testing method.
||Studies the source code or binary without application execution.| Studies the source code or binary by executing the application.
||Supports assessment of all kinds of software.| Does not support assessment of software other than web applications and web services.
||静态 Scans only static code. | 动态 Performs dynamic analysis on an application.
||Less expensive.| More expensive.

参考： [一文洞悉DAST、SAST、IAST ——Web应用安全测试技术对比浅谈](https://www.aqniu.com/learn/46910.html)



英文 | threat modeling | approach
----------|---------|---------
PASTA (The Process for Attack Simulation and Threat Analysis) | a type of `threat modeling`| `attack-centric` approach
STRIDE (spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, Elevation of Privilege) | one of the commonly used `threat modeling` methods. a tool developed by `Microsoft` to classify all possible threats on the server.
DREAD || `Damage` – how bad would an attack be?<br/>`Reproducibility` – how easy is it to reproduce the attack?<br/>`Exploitability` – how much work is it to launch the attack?<br/>`Affected users` – how many people will be impacted?<br/>`Discoverability` – how easy is it to discover the threat?
Microsoft Security Development Lifecycle (SDL)   | a type of `threat modeling`, Microsoft Threat Modeling Tool | `application-centric` approach
OCTAVE (Operationally Critical Threat, Asset, and Vulnerability Evaluation) | a tried and tested `threat modeling` | `asset-centric` approach
TD (Threat Dragon) | open-source threat modeling tool, both online and a desktop application