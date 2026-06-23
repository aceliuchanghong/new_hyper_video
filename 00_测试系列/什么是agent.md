# Agent

在强化学习里，我们习惯把 `agent` 理解为“玩家”：

> 它观察环境，选择动作，获得反馈，然后继续调整下一步行为。

到了大模型时代，`agent` 常被翻译成“智能体”。但这个词被用得太泛了，以至于很多东西都被包装成了 Agent。

所以先给出一个定义：

> **Agent 是一个能在环境中根据目标自主选择行动，并根据行动反馈继续调整下一步行为的闭环系统。**

在 LLM 工程语境下，可以更具体地说：

```
Agent = Model + Harness + Loop

Model 负责判断下一步做什么。
Harness 负责让模型能看见环境、调用工具、执行动作、接收反馈。
Loop 负责把反馈重新送回模型，直到任务完成。
```

## Agent 不是什么

`Agent` 这个词已经被一整个提示词水管工产业劫持了。

有一种常见幻觉：似乎只要把 LLM API 调用、if-else 分支、节点图、硬编码路由逻辑串在一起，就算是在“构建 Agent”。

不是的。

如果一个系统的流程是程序员提前写死的：

```text
用户输入
-> 分类
-> 进入固定分支
-> 调用固定工具
-> 生成固定格式输出
```

那它本质上是 workflow，不是 Agent。

它可能有 LLM，也可能调用工具，也可能画成复杂的节点图，但核心决策仍然来自代码，而不是模型在环境反馈中自主选择下一步行动。

这类系统更准确的名字是：

```text
过程式规则流水线
```


## 开发 Agent 到底是在开发什么

当一个人说“我在开发 Agent”时，他通常可能是在说两件完全不同的事。

### 1. 训练模型

第一种是真正意义上的 Agent 开发：

通过强化学习、微调、RLHF、RLAIF 或其他基于梯度的方法调整模型权重，让模型在真实任务中学会更好的行为策略。

这类工作关注的是：

```text
模型如何感知
模型如何推理
模型如何选择动作
模型如何从反馈中学习
模型如何形成更稳定的行为模式
```

它需要收集任务过程数据，也就是模型在真实领域中感知、推理、行动、失败、修正的完整序列，然后用这些数据塑造模型行为。

这是 DeepMind、OpenAI、Anthropic、腾讯 AI Lab 这类机构在做的事情。

这是最本义的 Agent 开发：**改变 Agent 的大脑。**

### 2. 构建 Harness

第二种是大多数工程师实际在做的事：

> **不是训练 Agent，而是构建 Agent Harness。**

Harness 可以理解为 Agent 的运行环境。

它让模型不只是“输出文本”，而是可以真正看见环境、调用工具、执行动作、接收反馈，并在权限边界内继续行动。

```
Harness = Tools + Knowledge + Observation + Action Interfaces + Permissions

    Tools:          文件读写、Shell、网络、数据库、浏览器
    Knowledge:      产品文档、领域资料、API 规范、风格指南
    Observation:    git diff、错误日志、浏览器状态、传感器数据
    Action:         CLI 命令、API 调用、UI 交互
    Permissions:    沙箱隔离、审批流程、信任边界
```

> **模型提供智能，Harness 提供身体，Loop 提供生命体征。**


## Agent Loop：最小闭环

一个工具型 LLM Agent 的最小模式，就是下面这个循环：

```text
User --> messages[] --> LLM --> response
                                  |
                        stop_reason == "tool_use"?
                       /                          \
                     yes                           no
                      |                             |
                execute tools                    return text
                append results
                loop back -----------------> messages[]
```


## Claude Code 是什么

Claude Code 是目前最优雅、最完整的 Agent Harness 实现之一。

它优秀的地方不在于某个单点技巧，而在于它清楚地知道自己不该做什么。

它没有试图替模型做所有判断。

它没有把任务强行塞进僵化的流程图。

它没有用一堆精心设计的决策树去冒充智能。

它做的是另一件事：

> 给模型提供足够好的工具、上下文、观察能力和权限边界，然后让模型在这个环境里工作。

把 Claude Code 剥到本质来看：

```
Claude Code = 一个 agent loop
            + 工具 (bash, read, write, edit, glob, grep, browser...)
            + 按需 skill 加载
            + 上下文压缩
            + 子 agent 派生
            + 带依赖图的任务系统
            + 异步邮箱的团队协调
            + worktree 隔离的并行执行
            + 权限治理
```

## 不同行业的 Agent，本质上都是 Harness 差异

```
庄园管理 agent  = 模型 + 物业传感器 + 维护工具 + 租户通信
农业 agent      = 模型 + 土壤/气象数据 + 灌溉控制 + 作物知识
酒店运营 agent  = 模型 + 预订系统 + 客户渠道 + 设施 API
医学研究 agent  = 模型 + 文献检索 + 实验仪器 + 协议文档
制造业 agent    = 模型 + 产线传感器 + 质量控制 + 物流系统
教育 agent      = 模型 + 课程知识 + 学生进度 + 评估工具
```

---

最终，Agent 不是一个提示词，也不是一个节点图，也不是一次 API 调用。

Agent 是一个闭环系统：

```text
它能看见环境。
它能理解目标。
它能选择动作。
它能执行动作。
它能观察反馈。
它能继续调整。
直到任务完成。
```

这才是 Agent。
