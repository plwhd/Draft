# 三大设计体系中的 UX 文案设计理论  
## Material · Apple · Microsoft 的深化分析与案例对照

> 适用场景：  
> - UX / 内容设计技术分享  
> - 设计系统 & DesignOps  
> - 产品与设计团队统一文案决策逻辑  
>  
> 本文在前三份基础理论整理之上，**进一步下钻到「设计假设 → 决策逻辑 → 真实案例」层级**，帮助你理解：  
> **为什么同一个场景，在三个体系里要“写得完全不一样”。**

---

## 一、先给结论：三大体系的 UX 文案不是风格差异，而是「产品哲学差异」

| 体系 | 文案的核心职责 | 对用户的隐性假设 |
|----|----|----|
| Material | 支持用户做出正确决策 | 用户是理性的决策者 |
| Apple | 尽量不出现，减少感知 | 用户愿意探索、理解界面 |
| Microsoft | 帮助用户完成任务 | 用户背景差异大、需要引导 |

这不是“谁好谁坏”，而是**服务对象不同**。

---

## 二、深化一：打断（Interruption）背后的设计逻辑

### 2.1 Material：打断 = 决策成本管理

Material 明确区分打断等级，每一次打断都意味着系统在向用户“索要注意力”。

#### 案例：删除文件（可撤销）

- **Snackbar**  
  > 文件已删除 · 撤销  

逻辑：  
- 行为已完成  
- 可撤销  
- 不值得用户停下来

#### 案例：删除账号（不可逆）

- **Dialog**  
  - 标题：删除账号？  
  - 正文：删除后，你的所有数据将被永久移除，且无法恢复。  
  - 按钮：删除账号 / 取消  

👉 Material 在这里承担了**全部信息责任**。

---

### 2.2 Apple：打断是一种失败

Apple 的理想状态是：  
> 如果可以不用打断，那就绝不用。

#### 案例：删除照片（iOS）

- 系统默认：  
  - 直接删除  
  - 轻提示：已移至“最近删除”

- 真正的 Alert 只在：  
  - 永久删除  
  - 或系统权限问题时出现

Apple 的逻辑是：  
> **优先通过系统结构解决问题，而不是通过文案提醒。**

---

### 2.3 Microsoft：打断是可以接受的，只要它能省时间

Microsoft 接受更多 Dialog / Message，只要它能：

- 减少后续错误
- 帮用户快速理解当前状态

#### 案例：关闭未保存文档（Office）

- 标题：Do you want to save your changes?  
- 正文：If you don’t save, your changes will be lost.  
- 按钮：Save / Don’t Save / Cancel  

👉 这是一个**教学 + 决策并存**的弹窗。

---

## 三、深化二：Dialog 文案结构的本质差异（同一场景对照）

### 场景：退出编辑页面，存在未保存内容

### Material 写法
- 标题：放弃未保存的更改？  
- 正文：你所做的更改将不会被保存。  
- 按钮：放弃更改 / 继续编辑  

特点：
- 冷静
- 不提建议
- 只陈述事实

---

### Apple 写法
- 标题：Discard Changes  
- （可能没有正文）  
- 按钮：Discard / Cancel  

特点：
- 极简
- 假设用户知道后果
- 文案几乎只起“标记作用”

---

### Microsoft 写法
- 标题：Do you want to save your changes?  
- 正文：If you close now, you’ll lose your recent edits.  
- 按钮：Save / Don’t Save / Cancel  

特点：
- 教学性强
- 面向不熟练用户
- 冗余但安全

---

## 四、深化三：错误文案（Error）在三大体系中的角色

### Material：恢复控制感

#### 示例
> 无法提交表单。请检查网络连接后再试。

- 明确问题
- 给下一步
- 不解释系统

---

### Apple：陈述事实

#### 示例
> Unable to connect to the network.

- 极短
- 不给建议
- 假设用户知道怎么处理

---

### Microsoft：提供解决路径

#### 示例
> We couldn’t save your changes.  
> Check your internet connection and try again.

- 解释 + 建议
- 更像“帮助文档内嵌”

---

## 五、深化四：空状态（Empty state）的态度差异

### Material
> 这里还没有文件。上传一个开始使用。

- 引导
- 行动明确

### Apple
> No Photos

- 几乎不引导
- 强依赖界面与图标

### Microsoft
> You don’t have any files yet.  
> Create a new file to get started.

- 解释 + 引导
- 面向新手

---

## 六、一个可以直接落地的「体系选择指南」

当你在写 UX 文案前，可以先问自己三个问题：

1. 用户是否需要在此刻做出“重要决策”？  
   → 是：偏 Material  
2. 界面本身是否已经足够自解释？  
   → 是：偏 Apple  
3. 用户是否可能不知道下一步怎么做？  
   → 是：偏 Microsoft  

---

## 七、终极总结（分享收尾用）

> Material 教我们如何 **承担信息责任**  
> Apple 教我们如何 **减少存在感**  
> Microsoft 教我们如何 **帮助用户把事做完**

**真正成熟的 UX 文案能力，是在三者之间自由切换。**
