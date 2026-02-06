# 微软式信息结构设计：Office 与 Azure 的统一结构逻辑

---

## 一、Microsoft Office：以「对象 × 任务」定义结构

### 1. 官方结构核心：Object-based + Task-oriented

Microsoft Office 的核心 UI 结构原则是：

> Design around user tasks and the objects they work with.  
> Commands should be organized around what users want to do, not how the system works.

这一定义来自微软长期使用的命令与结构设计哲学，适用于 Office 与 Windows 系统整体。

**官方文档：**  
- Microsoft UX Guide – Command Design  
  https://learn.microsoft.com/en-us/windows/win32/uxguide/command-design

---

### 2. Ribbon（功能区）是结构理论的直接产物

Ribbon 的本质并非视觉创新，而是结构映射机制。

结构逻辑为：

用户目标  
└─ 当前对象（文档 / 表格 / 幻灯片）  
　　└─ 可执行的任务集合  

微软官方对 Ribbon 的定义：

> The Ribbon exposes commands in a way that directly reflects user goals and tasks.  
> Commands are grouped by the type of task they support.

**官方文档：**  
- Ribbon Design Principles  
  https://learn.microsoft.com/en-us/windows/win32/uxguide/ribbon-design

#### Ribbon 中的结构映射

| 结构层级 | Ribbon 中的体现 |
|--------|----------------|
| 对象 | 文档 / 表格 / 图形 |
| 任务 | 编辑 / 插入 / 布局 |
| 操作 | 具体命令按钮 |

**本质总结：**  
Office 的信息结构围绕  
**“我正在操作什么对象 × 我现在想做什么”**

---

### 3. Contextual UI（上下文工具）是层级切换机制

示例：

- 选中文本 → 显示文本工具  
- 选中图片 → 显示图片工具  

微软官方定义：

> Contextual UI reduces complexity by surfacing commands only when they are relevant to the current object.

**官方文档：**  
- Contextual UI Guidelines  
  https://learn.microsoft.com/en-us/windows/apps/design/controls/contextual-ui

**关键结论：**

- 层级不是静态树  
- 而是基于对象状态的动态投影  

---

## 二、Microsoft Azure：以「资源模型」定义结构

Azure 是微软结构思想最工程化、最清晰的体现。

---

### 1. 官方根基：Azure Resource Manager（ARM）

微软对 ARM 的官方定义：

> Azure Resource Manager is the deployment and management service for Azure.  
> It provides a consistent management layer that allows you to manage your resources as a group.

**官方文档（关键）：**  
- Azure Resource Manager Overview  
  https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/overview

---

### 2. Azure 的硬性资源层级（系统定义）

Azure 的结构不是 UI 设计产物，而是系统模型本身。

官方资源层级：

Tenant  
└─ Management Group  
　　└─ Subscription  
　　　　└─ Resource Group  
　　　　　　└─ Resource  

**官方文档：**  
- Management Groups Overview  
  https://learn.microsoft.com/en-us/azure/governance/management-groups/overview

**要点：**

- 这是系统层级  
- 不是设计师绘制的导航层级  

---

### 3. Azure Portal 的信息结构 = 资源模型的可视化投影

微软官方说明：

> The Azure portal is built on Azure Resource Manager and reflects the resource hierarchy.

**官方文档：**  
- Azure Portal Overview  
  https://learn.microsoft.com/en-us/azure/azure-portal/azure-portal-overview

#### Portal 中的结构映射

| 系统结构 | Portal 中的体现 |
|-------|----------------|
| Resource Group | 页面主容器 |
| Resource | 页面主体对象 |
| Capabilities | 左侧导航（Blade） |
| Operations | 顶部 / 操作栏 |

**核心理解：**  
Azure 的 UI 是资源模型的**可视化投影**。

---

### 4. Blade 模型：结构 ≠ 页面

Azure Portal 采用 Blade（刀片）模型，而非传统页面跳转。

微软官方定义：

> Blades provide a way to manage related resources and actions without losing context.

**官方文档：**  
- Azure Portal Blades  
  https://learn.microsoft.com/en-us/azure/azure-portal/azure-portal-blades

**结构思想：**

- 对象保持不变  
- 视角发生切换  
- 层级 ≠ 导航深度  

---

## 三、微软官方对「信息结构」的统一抽象

### 1. 三个核心模型（跨 Office / Azure）

微软官方 UX 文档中反复使用以下抽象：

- **Mental Model（心理模型）**  
  用户如何理解系统  

- **Conceptual Model（概念模型）**  
  系统真实存在的对象与关系  

- **Navigation / Presentation Model（呈现模型）**  
  UI 如何展示这些关系  

**参考文档：**  
- Windows App Design – Signals  
  https://learn.microsoft.com/en-us/windows/apps/design/signals/

---

### 2. 可直接引用的官方观点

> Good UI structure reflects the underlying system model while aligning with user expectations and goals.

**来源：**  
- Microsoft Design Principles  
  https://learn.microsoft.com/en-us/windows/apps/design/design-principles

---

## 四、一句话总结：微软式结构定义

- **Office：** 用「对象 × 任务」定义结构  
- **Azure：** 用「资源模型」定义结构  
- **UI：** 只是这些结构在特定上下文下的投影  

这也是为什么：

- Office 看起来以操作为中心  
- Azure 看起来以对象为中心  

**但两者底层逻辑完全一致。**
