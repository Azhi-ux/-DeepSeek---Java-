## 基于大模型（DeepSeek）驱动的性能异常检测系统 - Java版+Vue3.0

***如需要其它开发语言（Python、Go）类型可加v：A-8--8---8***

## 📚 目录
- [一、项目背景与研究意义](#-----------)
- [二、总体目标](#-------------)
- [三、系统架构设计](#--------)
  * [1. 技术架构](#1-----)
- [四、功能模块设计](#--------)
  * [（1）性能指标采集模块](#-1---------)
  * [（2）异常检测模块](#-2-------)
  * [（3）根因分析模块](#-3-------)
  * [（4）告警与通知模块](#-4--------)
  * [（5）可视化监控中心](#-5--------)
  * [（6）系统管理模块](#-6-------)
- [五、核心创新点](#-------)
- [六、项目成果展示](#------)
- [七、适用场景](#------)

## 一、项目背景与研究意义

随着互联网业务规模不断扩大，应用系统的架构日益复杂，微服务、容器化、云原生等技术的广泛应用使得性能问题的定位与诊断变得愈加困难。传统的性能监控手段主要依赖人工设定阈值或基于统计规则的检测方法，难以应对系统复杂性和动态变化带来的挑战。

近年来，大语言模型（Large Language Model, LLM）的快速发展为智能运维（AIOps）提供了全新的思路。DeepSeek 作为一种面向智能分析的开放大模型，具备强大的语义理解和推理能力，能够在复杂数据中自动识别潜在模式并进行智能判断。将 DeepSeek 融入性能异常检测场景，可实现从指标采集、异常检测到根因分析的智能化转变，大幅提升运维效率与系统稳定性。

因此，本项目旨在设计与实现一个**基于大模型（DeepSeek）驱动的性能异常检测系统**，利用 Java + Spring Boot 构建后端服务，结合 Prometheus、SkyWalking、Elasticsearch 等监控与数据分析组件，实现多维度性能指标采集与智能异常检测。

---

## 二、总体目标与项目成果展示

本项目的目标是构建一个可自动监测、分析并智能定位性能异常的系统平台，实现以下功能：

1. 自动采集系统、服务及接口层面的性能指标；
2. 通过 DeepSeek 模型进行异常模式识别与根因分析；
3. 提供可视化的性能监控大屏与告警中心；
4. 支持历史数据回溯与趋势预测；
5. 构建可扩展的 AIOps 架构，支持多源数据接入。

---

## 三、系统架构设计

### 1. 技术架构

<img width="425" height="523" alt="image" src="https://github.com/user-attachments/assets/7f3abf7f-2a1d-476f-95e0-d3a242fc8991" />

系统采用 **前后端分离** 的设计模式，技术栈如下：

* **后端技术：** Spring Boot、Spring Cloud、MyBatis、Elasticsearch、SkyWalking、Prometheus、Redis、MySQL
* **AI 模型接入：** DeepSeek API（或本地部署推理服务）
* **前端技术：** Vue 3、ECharts、Element Plus
* **监控与数据采集：** Prometheus Exporter、SkyWalking Agent
* **日志与可观测性：** ELK（Elasticsearch + Logstash + Kibana）

整体架构分为五个层次：

| 层次     | 功能说明                                                              |
| ------ | ----------------------------------------------------------------- |
| 数据采集层  | 通过 Prometheus Exporter、SkyWalking Agent 收集 CPU、内存、接口延时、吞吐量、错误率等指标 |
| 数据存储层  | 使用 MySQL 存储结构化数据，Elasticsearch 存储时序与日志数据                          |
| 模型分析层  | DeepSeek 模型对采集数据进行语义分析与异常检测                                       |
| 应用服务层  | Spring Boot 提供 API 接口与任务调度，负责数据聚合、分析与告警触发                         |
| 可视化展示层 | Vue 前端实现监控大屏、趋势图、告警中心及模型解释结果展示                                    |

---

## 四、功能模块设计

<img width="488" height="280" alt="image" src="https://github.com/user-attachments/assets/5394310d-49bd-49a1-8dbd-ae01ffc0919e" />

### （1）性能指标采集模块

* 接入 Prometheus、SkyWalking 实现服务指标与调用链数据采集；
* 支持自定义监控项，如数据库连接数、GC 时间、QPS、响应延迟等。

### （2）异常检测模块

* 利用 DeepSeek 模型对多维指标序列进行智能分析；
* 结合统计学与机器学习方法（如 IsolationForest、LOF）进行辅助判断；
* 输出异常等级、可能原因及相关日志片段。

### （3）根因分析模块

* DeepSeek 对异常事件上下文日志与指标数据进行语义理解；
* 自动生成“根因推测报告”，包括影响范围、可能的组件及代码层推测点。

### （4）告警与通知模块

* 根据异常级别触发邮件、企业微信、钉钉等方式通知；
* 支持自定义告警规则与静默策略。

### （5）可视化监控中心

* 展示实时性能曲线、异常分布图、调用链追踪视图；
* 支持时间维度回溯与对比分析；
* 内置异常报告面板，展示模型推理结果与建议。

### （6）系统管理模块

* 用户权限与角色管理；
* 数据源配置与指标管理；
* 模型任务调度与版本管理。

---

## 五、核心创新点

1. **引入大模型 DeepSeek 的智能异常检测机制**

   * 不再依赖传统阈值规则，通过语义推理识别异常模式。
   * 能理解多指标间的复杂关系，提供更准确的根因推测。

2. **多源异构监控数据融合分析**

   * 同时融合 Prometheus 指标、SkyWalking 链路数据与日志信息。
   * 提供统一的异常检测与展示视图。

3. **自解释性 AI 诊断报告**

   * DeepSeek 生成自然语言形式的异常说明与优化建议，帮助开发者快速定位问题。

4. **高扩展性与通用性架构**

   * 模型与监控源可自由替换，支持接入其他 AI 模型或监控工具。

---

## 六、项目成果展示

1. **系统成果**：

   * 一个完整的性能异常检测与分析系统（前后端分离架构）；
   * 支持实时监控、异常识别、根因分析与告警通知；
   * 大模型参与分析与报告生成，实现智能化运维。
  <img width="488" height="280" alt="image" src="https://github.com/user-attachments/assets/725ee576-15b1-4693-910a-e1d5f16f2f8f" />
  <img width="488" height="280" alt="image" src="https://github.com/user-attachments/assets/5c4bbc09-a8ed-4f50-bfbd-20bb971569ac" />
  <img width="488" height="280" alt="image" src="https://github.com/user-attachments/assets/21f6d9b6-cb66-4a9b-8c95-1826d31dd9b1" />
  <img width="488" height="280" alt="image" src="https://github.com/user-attachments/assets/db361616-c229-4c05-a80b-19c19c638a1e" />
  <img width="488" height="280" alt="image" src="https://github.com/user-attachments/assets/f8193497-3f88-41b5-898c-13427346a49c" />
  <img width="488" height="280" alt="image" src="https://github.com/user-attachments/assets/08986e20-56f2-4815-afd3-867802abc06c" />
2. **论文成果**：

   * 系统设计与实现论文一篇；
   * 对比传统监控与 DeepSeek 智能分析在准确率、响应时间等指标上的实验分析报告。
<img width="686" height="351" alt="image" src="https://github.com/user-attachments/assets/a9897e66-97bd-4082-9c87-89c876f5a2c5" />
---

## 七、适用场景

* 企业级微服务系统性能监控；
* 云原生环境下的异常检测与智能运维；
* DevOps / AIOps 实践教学与科研项目；
* 高校毕设项目与创新创业竞赛展示。

---
