---
title: 计算机英语-安全Security
catalog: true
date: 2022-09-02 14:24:17
subtitle:
header-img:
tags:
- Security
categories:
- English Learning
- 计算机英语
---

## 攻击类型

英文 | 读音 | 含义
----------|---------|---------
Phishing| 美/ˈfɪʃɪŋ/ | 网络钓鱼 the activity of tricking people by getting them to give their identity, bank account numbers, etc. over the Internet or by email, and then using these to steal money from them 网络诱骗（通过互联网或电邮骗取他人身份证件、银行账号等以盗取金钱）
Injection || 注入 例如 SQL Injection

## 缩写

缩写 | 全称 | 含义
----------|---------|---------
DOS |Denial of Service| 服务不可用 Denial of Service occurs when a web server is made temporarily unavailable or unusable to a valid user. Protection from such threats improves system consistency and availability. 当 Web 服务器暂时不可用或对有效用户不可用时，就会发生拒绝服务。 防范此类威胁可提高系统一致性和可用性。
DFDs  |Data flow diagrams| The threat modeling approach requires you to use data flow diagrams (or DFDs).<br/>A data flow diagram is an organized evaluation and design method used for software analvsis. It represents the flow of data through the system. DFD supports decomposition, to graphically depict the flow of data and functions in the system.<br/>A DFD provides:<br/>- A system design to support the analysis and requirement stage.<br/>- A detailed system diagram.<br/>- Description of the network of activities of the target system.<br/>- Step-by-step modification through tiered disintegration of activities.
 [ASVS](https://owasp.org/www-project-application-security-verification-standard/) |OWASP Application Security Verification Standards| a community-driven attempt to begin a framework of security controls that focuses on outlining the functional and non functional security controls essential for development, design,and testing of modern web services and applications.
CVSS | Common Vulnerability Scoring System|
CVE | Common Vulnerability and Exposure  |
NVD |[National Vulnerability Database](https://nvd.nist.gov/)|
MFA | Multi-factor authentication | (MFA) is an authentication technique in which a user must provide two or more verification factors to access an application. MFA is one of the best defense techniques, which can be used against most password-related attacks. Use MFA wherever possible and feasible.
RBAC | Role-Based Access Control | is the process of making access decisions based on the roles and responsibilities of a user
DAC | Discretionary Access Control | the process of restricting access to information based on the identity of the user.

英文 | threat modeling | approach
----------|---------|---------
PASTA (The Process for Attack Simulation and Threat Analysis) | a type of `threat modeling`| `attack-centric` approach
STRIDE (spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, Elevation of Privilege) | one of the commonly used `threat modeling` methods. a tool developed by `Microsoft` to classify all possible threats on the server.
DREAD | `Damage` – how bad would an attack be?<br/>`Reproducibility` – how easy is it to reproduce the attack?<br/>`Exploitability` – how much work is it to launch the attack?<br/>`Affected users` – how many people will be impacted?<br/>`Discoverability` – how easy is it to discover the threat? |
Microsoft Security Development Lifecycle (SDL)   | a type of `threat modeling`, Microsoft Threat Modeling Tool | `application-centric` approach
OCTAVE (Operationally Critical Threat, Asset, and Vulnerability Evaluation) | a tried and tested `threat modeling` | `asset-centric` approach
TD (Threat Dragon) | open-source threat modeling tool, both online and a desktop application


### [Threat modeling](https://owasp.org/www-community/Threat_Modeling)

`Threat modeling` is a core element of the Microsoft Security Development Lifecycle. You can use threat modeling to identify and mitigate threats, weaknesses, and vulnerabilities in an application.

OWASP suggests gathering the following assessment input.

- A description, design, or model of your application architecture.
- A list of assumptions that can be checked or challenged in the future, as the threat landscape changes.
- A list of potential threats to the system.
- A list of mitigations to be taken for each threat.
- A way of validating the model. threats, and verifying the success of implemented mitigations.

英文 | [threat modeling](https://owasp.org/www-community/Threat_Modeling) | approach
----------|---------|---------
PASTA (The Process for Attack Simulation and Threat Analysis) | a type of `threat modeling`| `attack-centric` approach
STRIDE (spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, Elevation of Privilege) | one of the commonly used `threat modeling` methods. a tool developed by `Microsoft` to classify all possible threats on the server.
DREAD | `Damage` – how bad would an attack be?<br/>`Reproducibility` – how easy is it to reproduce the attack?<br/>`Exploitability` – how much work is it to launch the attack?<br/>`Affected users` – how many people will be impacted?<br/>`Discoverability` – how easy is it to discover the threat? |
Microsoft Security Development Lifecycle (SDL)   | a type of `threat modeling`, Microsoft Threat Modeling Tool | `application-centric` approach
OCTAVE (Operationally Critical Threat, Asset, and Vulnerability Evaluation) | a tried and tested `threat modeling` | `asset-centric` approach
TD (Threat Dragon) | open-source threat modeling tool, both online and a desktop application

STRIDE | 读音 | 含义
----------|---------|---------
spoofing | 美/ˈspuːfɪŋ/ | 电子欺骗; 在网络上或邮件中假冒他人的行为或事例。the act or an instance of impersonating another person on the internet or via email. Refers to illegal access and use of data.
Tampering | 美/ˈtæmpərɪŋ/ | 篡改数据 Refers to malicious modification of data. Can be done to data at rest, or in transit.指恶意修改数据。 可以对静止或传输中的数据进行处理。
Repudiation | 美/rɪˌpjuːdiˈeɪʃ(ə)n/ | 否认、抵赖。不可否认/抵赖性（Non-repudiation）. Occurs when the system cannot trace and prove actions performed by a user. 当系统无法跟踪和证明用户执行的操作时出现。
Information disclosure || Information disclosure refers to exposing information to unauthorized entities. For example, a user is able to read a file that does not belong to them, or a threat actor gains access to data in transit. 信息泄露是指将信息暴露给未经授权的实体。 例如，用户能够读取不属于他们的文件，或者威胁参与者可以访问传输中的数据。
Elevation of privilege || 权限提升 Elevation of privilege refers to a situation where an attacker successfully gains access to restricted levels of a svstem. The attackers can then access sensitive data, restricted functionality, and connected systems.特权提升是指攻击者成功获得对受限制级别的系统的访问权限的情况。 然后，攻击者可以访问敏感数据、受限功能和连接的系统。
DOS (Denial of Service)|| 服务不可用 Denial of Service occurs when a web server is made temporarily unavailable or unusable to a valid user. Protection from such threats improves system consistency and availability. 当 Web 服务器暂时不可用或对有效用户不可用时，就会发生拒绝服务。 防范此类威胁可提高系统一致性和可用性。

DFDs | 读音 | 含义
----------|---------|---------
DFDs (Data flow diagrams)  || The threat modeling approach requires you to use data flow diagrams (or DFDs).<br/>A data flow diagram is an organized evaluation and design method used for software analvsis. It represents the flow of data through the system. DFD supports decomposition, to graphically depict the flow of data and functions in the system.<br/>A DFD provides:<br/>- A system design to support the analysis and requirement stage.<br/>- A detailed system diagram.<br/>- Description of the network of activities of the target system.<br/>- Step-by-step modification through tiered disintegration of activities.

![DFD1](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/security/DFD1.png)
![DFD2](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/security/DFD1.png)

## Application Security Testing

### security assessment methodologies

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
||静态 Scans only static code.<br/>cannot discover run-time vulnerabilities.| 动态 Performs dynamic analysis on an application.<br/>can discover run-time vulnerabilities
||Less expensive<br/>since the vulnerabilities can be detected during the earlier stages of the software development lifecycle.| More expensive<br/>detects vulnerabilities towards the end
of a software development lifecycle
||Need eliminate false positives|

参考： [一文洞悉DAST、SAST、IAST ——Web应用安全测试技术对比浅谈](https://www.aqniu.com/learn/46910.html)

### [Component Analysis](https://owasp.org/www-community/Component_Analysis)

[Software Composition Analysis - OWASP Stammtisch](https://wiki.owasp.org/images/b/bd/Software_Composition_Analysis_OWASP_Stammtisch_-_Stanislav_Sivak.pdf)

解决third-party and open source components依赖带来的security问题。

缩写 | 全称 |  含义 | Advantage | Caution
----------|---------|---------|---------|---------
SCA | Software Composition Analysis | Component Analysis is the process of identifying potential areas of risk from the use of third-party and open-source software and hardware components. A software-only subset of Component Analysis with limited scope is commonly referred to as `Software Composition Analysis (SCA)`. | Component Analysis is a function within an overall [`Cyber Supply Chain Risk Management (C-SCRM)`](https://csrc.nist.gov/projects/supply-chain-risk-management) framework.
C-SCRM | [Cyber Supply Chain Risk Management](https://csrc.nist.gov/projects/supply-chain-risk-management) | ||
SBOM | [Software Bill of Materials](https://owasp.org/www-community/Component_Analysis#software-bill-of-materials-sbom) | 软件透明度通常通过发布软件材料清单来实现。 SBOM 是配方中成分列表的同义词。 两者都是透明度的实现。Software Transparency is often achieved through the publishing of software bill of materials. An SBOM is synonymous to the list of ingredients in a recipe. Both are an implementation of transparency.

![Application_security_pipeline](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/security/Application_security_pipeline.png)
![Application_security_CICDpipeline](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/security/Application_security_CICDpipeline.png)

### Prioritizing security risks

- The likelihood of a threat exploiting the system weaknesses.
- The likely impact of the threat on the weaknesses.
- The capability of the existing information security system controls to reduce the risk.

Risk = Probability of Threat x Impact Value

Value | Probability of Threat
----------|---------
1.0 | High
0.5 | Medium
0.1 | Low

Value | Impact Level
----------|---------
100 | High
50 | Medium
10 | Low

### Secure SDLC 101

Secure Software Development Lifecycle (`SSDLC`)

A software development life cycle (`SDLC`) is a process that outlines the steps used by organizations, to build an application from the beginning until the end. In simple terms, a secure SDLC is set up by adding security-related actions to the current development life cycle.

The phases of SDLC include:

- Planning and requirements Architecture and design
- Test planning
- Coding
- Testing and results
- Release and maintenance

![SSDLC](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/security/SSDLC.png)

Benefits of Secure SDLC:
- Acquaints stakeholders to security considerations.
- Reduces expenses by early detection and issue fixes.
- Results in overall decline in key business risks.

### Code review

[OWASP Code Review Guide 2.0](https://owasp.org/www-project-code-review-guide/assets/OWASP_Code_Review_Guide_v2.pdf)

Best practices before sending the code for review:

- Ensure that the code compiles and passes static analysis, within policy compliance.
- Ensure that the code passes unit, integration
and system tests.
- Check for spelling errors and double-check to tidy up your document.
- Ensure code changes are captured and annotated appropriately.
- Check for logic errors.

Code review techniques | Expain | 特点
----------|---------|---------
Instant Code Review | the code is instantly reviewed while it is being written. The developer writes code, while the reviewer sits beside reading and correcting the code.  | `Highly complex` programs can benefit from instant code review, because two minds working on a problem often solve problems in a speedier and efficient manner.
Ad-Hoc Code Review | called "Over the Shoulder" reviewing. Typically, a developer will ask a reviewer to look at, and give feedback on the code they have written. The emphasis of ad-hoc review is that it is done with the reviewer and developer in a live conversion.| It is one of the `most common` review processes.
Meeting-Based Code Review | coders finish their work and call a meeting. The whole technology team sits together, comments. and attempts to improve the code together. |not commonly practiced because it is a `time-consuming` and `resource-intensive` activity.
Tool-Based(asynchronous) Code Review | is performed by the reviewer, separate from the developer. A developer will make their code available for review and then the reviewer will, in their own time, review the code. Comments and corrections will be left by the reviewer for the developer.|  The developer will be notified of the feedback and if the two parties agree, the code is signed off and accepted as part of the application.

## Rating vulnerabilities

### DREAD rating system

A risk assessment model that evaluates the security threats is called DREAD rating system.

DREAD Category:

- Damage potential
- Reproducibility
- Exploitability
- Affected users
- Discoverability

A rating from 1 to 10 is given to DREAD categories and the sum of all ratings is used to prioritize issues.

### CVSS

CVSS is used to communicate the characteristics and severity of software vulnerabilities.

There are three metric groups used in the CVSS report:

1. `Base`
2. `Temporal`
3. `Environmental`.

The `Base` metrics produces a score range from 0 to 10. The score can be changed by changing the Temporal and Environmental metrics.

- `Base` signifies the essential and vital characteristics of a vulnerability that are constant with time and user environment.
- `Temporal` signifies the features of a vulnerability that change with time, but not with user environments.
- `Environmental` signifies the features of a vulnerabilitv that are unique to a user's environments.

#### CVSS scores

You can obtain the CVSS scores for all vulnerabilities from the `National Vulnerability Database (NVD)`. The [NVD](https://nvd.nist.gov/) helps create a CVSS base score for all vulnerabilities.

Note that the CVSS has two active versions. The score to severitv relationship is different depending on the version.

CVSS v2.0 Ratings - Severity | Base Score Range
----------|---------
Low | 0.0-3.9
Medium | 4.0-6.9
High | 7.0-10.0

CVSS v3.0 Ratings - Severity | Base Score Range
----------|---------
None | 0.0
Low | 0.1-3.9
Medium | 4.0-6.9
High | 7.0-8.9
Critical | 9.0-10.0

### Finding security vulnerabilities online

- [Common Vulnerabilities and Exposure](https://cve.mitre.org/)
  - List of items containing identification number, description, and a public reference for publicly known cybersecurity weaknesses.
  - These CVE entries are used with cybersecurity creations and amenities from all around the world.
- [National Vulnerability Database](https://nvd.nist.gov/)
  - The U.S. government's database of reported and known security vulnerabilities.
  - Synchronized with CVE.
  - Comparatively easier to navigate.
  - Lists each vulnerability along with a description, source, and severity level.
- [OWASP Top 10 Vulnerabilities](https://www.veracode.com/security/owasp-top-10)
- [Vulnerability Database](https://vuldb.com/)
  - A platform that collects, maintains, and disseminates data about common security vulnerabilities.
  - Describes each vulnerability, provides a workaround, assesses the impacts, and issues moderation.

## Secure Architecture and Design

### Access control methodologies

缩写 | 全称 | 含义 | Advantage | Caution
----------|---------|---------|---------|---------
RBAC | Role-Based Access Control | is the process of making access decisions based on the `roles` and responsibilities of a user.<br/>- Roles of a user are defined based on the organizational goals, structure, and security policies.<br/>- Application security administrators use RBAC to define what, when, where, and how an action can be performed by a user. | - Easy to implement and administer.<br/>- Facilitates the principle of least privilege.| - Assign user roles using strict sign-offs and procedures.<br/>- Disable all previously assigned permissions and assign permissions based on the new role.<br/>- Perform strict access control reviews to ensure safe use of RBAC
DAC | Discretionary Access Control | the process of restricting access to information based on the `identity` of the user.<br/>- Access decisions depend on the user's current authorization limits.<br/>- A simple example of DAC would be a system in which passwords are set for files,folders, and other resources.<br/>-Resource owners can grant or revoke permission to any of the objects that are under their control.| - Easy to use and administer.<br/>- Used on par with the principle of least privileges.<br/>- Users have complete control over the access granted to them.| Perform strict access control reviews to ensure the safe use of DAC.
MAC | Mandatory Access Control | is the process of providing access to users based on the `sensitivity` and `confidentiality` of the data. | - Access permissions are granted based on the sensitivity of the data, business requirements, and changes in the scope of a project.<br/>- Only administrators are given control to grant user access. | - Classify data and assign access to sensitive information based on user permission level.<br/>- Ensure that data classification is done at the appropriate level
 . | Permission-Based Access Control | process of converting application access into a series of permissions.<br/>- Permissions are string-based names.<br/>- Access decisions are made by verifying whether the current permission level of a user allows them to perform the requested application action.| |
 . | Multi-Tenant Access Control | Single application instance has multiple users

#### MAC

- Users are granted permission based on need.
- MAC is the most secure access control model because access rules are:
  - Defined manually by system administrators.
  - Implemented by the operating system or security kernel.
  - Used to restrict access to security attributes.

#### Permission-Based Access Control

- Direct Model
  - In the direct model, grant privileges only to the users who need those privileges to complete the assigned tasks.
- Indirect Model
  - The permission is granted to an intermediate entity like a user group.
  - If a user inherits permissions from a user group, that user becomes a member of that user group.
  - If you edit permissions assigned to a user group, all users associated with that user group are affected.

#### Multi-Tenant Access Control

- Single application instance has multiple users
- Tenant resource isolation or segmentation is fundamental to these systems.
- Segmented application enables secure separation between tenants.
  - Example: For your SAAS application, you need to isolate each company on multiple layers.
- Segregation ensures that customer resources cannot be accessed by other tenants.
- MTAC models can address both intra-tenant and cross-tenant access.

[SaaS Tenant Isolation Strategies](https://d1.awsstatic.com/whitepapers/saas-tenant-isolation-strategies.pdf)



# 参考文章

- [STRIDE Threat Modelling vs DREAD Threat Modelling](https://haiderm.com/stride-threat-modelling-vs-dread-threat-modelling/)
