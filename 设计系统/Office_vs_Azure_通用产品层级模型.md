# 从 Office vs Azure 抽象出一套通用产品层级模型

> 技术分享 / 产品架构方法论  
> 关键词：产品架构、抽象层级、平台化、Office、Azure

---

## 一、问题背景

在微软的产品体系中，**Office** 与 **Azure** 经常被拿来对比。  
表面上看，它们分别代表了「应用软件」与「云平台」，但如果深入分析，会发现二者真正的差异并不在“产品类型”，而在于**产品结构方法（Product Structuring Method）**。

本文尝试将 Office 与 Azure 背后的结构思路进行抽象，提炼出一套**可跨行业复用的通用产品层级模型**，用于技术分享与架构分析。

---

## 二、抽象目标

本文关注的不是：

- 办公软件 vs 云服务  
- ToC vs ToB  

而是：

> **产品在设计时，将“哪一层”视为第一公民（Primary Abstraction）**

Office 与 Azure 的差异，本质是：

- 一个以**用户任务**为核心
- 一个以**技术能力**为核心

---

## 三、通用产品层级模型（五层）

我们可以将产品结构抽象为以下五个层级：

```
L0  产品愿景 / 价值主张（Why）
L1  主导抽象层（Primary Abstraction）
L2  能力单元层（Capability Units）
L3  组合 / 编排层（Composition）
L4  交付与体验层（Delivery & UX）
```

该模型与具体行业无关，但可以解释 Office、Azure 及大量现代软件产品。

---

## 四、各层级详解（含 Office / Azure 对照）

### L0｜产品愿景 / 价值主张（Why）

产品存在的根本理由，用于**约束方向而非指导实现**。

- **Office**：帮助人类更高效地完成知识工作  
- **Azure**：提供可规模化、可编程的计算能力  

> L0 决定 L1，但不直接参与架构设计。

---

### L1｜主导抽象层（Primary Abstraction）

这是整个模型的**核心分界点**。

| 产品 | 主导抽象 |
|----|----|
| Office | 用户任务 / 工作流 |
| Azure | 技术资源 / 能力原语 |

- Office 抽象的是：写文档、做演示、协作
- Azure 抽象的是：Compute、Storage、Network、Identity

> **L1 决定了下面所有层级使用的“语言体系”。**

---

### L2｜能力单元层（Capability Units）

可独立演进、可被复用的最小能力模块。

**Office：**
- Word
- Excel
- PowerPoint
- Outlook

特点：
- 面向用户
- 自带语义与 UI
- 本身即完整产品

**Azure：**
- Virtual Machine
- Blob Storage
- Virtual Network
- SQL Database

特点：
- 面向系统
- 无业务语义
- 必须被组合才有意义

> **Office 的能力单元是“产品”，Azure 的能力单元是“构件”。**

---

### L3｜组合 / 编排层（Composition）

将 L2 的能力组织成更高价值形态。

**Office 的组合方式：**
- Microsoft 365
- 跨应用协作（Word + Excel + Teams）
- 模板、插件、宏

特点：
- 组合是隐式的
- 用户感知的是体验，而非结构

**Azure 的组合方式：**
- ARM / Bicep / Terraform
- Reference Architecture
- Solution Blueprint

特点：
- 组合是显式的
- 组合本身即产品能力

> **Office 隐藏组合，Azure 暴露组合。**

---

### L4｜交付与体验层（Delivery & UX）

用户或开发者接触产品的方式。

- **Office**
  - GUI 为核心
  - 文件即接口
  - 默认状态可用

- **Azure**
  - API / CLI / IaC 为核心
  - 配置即接口
  - 默认状态不可用

> 体验层是结构选择的结果，而非起点。

---

## 五、方法论总结

可以将全文压缩为一句话：

> **一个产品的层级结构，取决于它把哪一层当作“第一公民”。**

- 第一公民是用户任务 → Office 型结构
- 第一公民是系统能力 → Azure 型结构

---

## 六、模型的通用性示例

| 产品 | L1 抽象 | 类型 |
|----|----|----|
| Salesforce | 业务对象 | Office 型 |
| AWS | 基础设施能力 | Azure 型 |
| Figma | 设计行为 | Office 型 |
| Kubernetes | 调度与资源 | Azure 型 |

---

## 七、结语

Office 与 Azure 的差异并非偶然，而是**结构选择的必然结果**。  
通过抽象其背后的方法，我们可以更清晰地理解：

- 为什么某些产品必须“好用”
- 为什么某些产品必须“可组合”
- 为什么平台化往往意味着复杂度转移

希望这套模型能为你的产品设计、架构决策或技术分享提供一个清晰的分析工具。
