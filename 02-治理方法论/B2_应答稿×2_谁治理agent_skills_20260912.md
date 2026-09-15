---
title: "B2 · 应答稿 ×2：谁来治理 agent skills？"
summary: "A recent wave of discussion asks an uncomfortable question: *agent skills spread faster than anyone can review them — **who governs them?***"
domain: "AI治理/A³法则/AI造AI方法论"
source: "github:zhaoxinghua09-cell/medxpert-ai-gov-kb"
version: "1.0"
updated: "2026-09-15"
tags: ["AI治理", "A3法则", "生命周期治理", "证据门禁", "记忆工程", "自进化", "可追溯", "AI造AI"]
type: "doc"
---

# B2 · 应答稿 ×2：谁来治理 agent skills？

> 生成：2026-09-12 ｜ 线别：曝光度与竞争力提升线 · Wave 2 · **B2**
> 场合：回应正在发生的公共讨论（如 *"Now Who Governs Them?"* 一类关于 agent skills 生态失控的提问）
> 锚词策略：**统一用「生命周期治理」降门槛**，不用生造词开场；生造词只在正文中段作为"命名"出现。
> 口径纪律：不宣称首创；对我方只作定位陈述。

---

## 稿一（英文 · dev.to）：Who Governs the Skills?

### Who Governs the Skills?

A recent wave of discussion asks an uncomfortable question: *agent skills spread faster than anyone can review them — **who governs them?***

The honest answer today is: **mostly nobody, and that's a structural problem, not a moral one.**

#### Why "review at the door" doesn't scale

Most ecosystems handle this with a marketplace review gate: a skill gets submitted, someone checks it, it goes live. That works when you have a few dozen skills. It breaks at a few thousand, and it breaks *worse* when skills can call each other.

Three structural failures show up:

1. **Point-in-time review ≠ ongoing governance.** A skill that was safe at review can become risky after an update, a dependency change, or a new permission.
2. **No portable record.** Even when a platform audits a skill, that record usually can't leave the platform. Move it, and the governance evidence is gone.
3. **No accountability chain.** When a chain of skills produces a bad outcome, there is often no way to say *who* contributed *what*.

#### What a lifecycle view changes

Instead of asking *"is this skill allowed?"* once, ask the same question **across its life**:

| Stage | Question | What must exist |
|---|---|---|
| **At birth** | Who made it, who owns it, what can it touch? | a registry entry: identity, creator, governance owner, declared scope |
| **While running** | What did it actually do? | evidence: action log, data touched, human-oversight record |
| **On change** | Should this update be allowed? | a gate: trigger → assessment → release → review |
| **At retirement** | What happens to its data and permissions? | a retirement record and revocation path |

This is not exotic. It is simply **lifecycle governance** — the same discipline that regulated industries (medical devices, aviation, finance) already apply to things that can hurt people.

#### The part most tooling misses

If you want this to work in the real world, three requirements are non-negotiable:

- **Offline capability.** Many deployments cannot send data off-machine. A governance tool that requires cloud access is unusable in exactly the places governance matters most.
- **Portable evidence.** The record must be exportable and verifiable outside the platform that created it.
- **Human-owned gates.** High-stakes permission expansion should not be a machine's decision. Machines request; humans authorize.

#### A modest proposal

We — MedXpert × SynomosAI — work on exactly this, under the name **Evidence-Gated AI Lifecycle Governance** (the Chinese given name is 凡自治之物 — *every self-governing thing*, with the three-beat mnemonic **registry · evidence · gates**).

We are **not** claiming to be the definition. Standards bodies and regulators define the rules; our work sits deliberately one layer down: **the implementation layer (How)** — plus a concrete instantiation drawn from medical-device regulation, and a cross-domain template.

If you are building a skill ecosystem, the useful question is not *"do we need governance?"* — it's:

> **Can you answer, for any skill, these four questions: who owns it, what did it do, was its last change reviewed, and what happens when it retires?**

If any of the four is "we don't know", the gap is the lifecycle, not the review.

*Further reading: [lgd-theory](https://github.com/zhaoxinghua09-cell/lgd-theory) · DOI [10.5281/zenodo.22456647](https://doi.org/10.5281/zenodo.22456647). Knowledge synthesis and perspective, not legal or regulatory advice.*

---

## 稿二（中文 · 知乎）：技能生态失控了吗？——换个问法

### 技能生态"失控"了吗？先换个问法

最近有一个被反复讨论的问题：**agent skills 增长的速度，已经超过任何人能审查的速度——那到底谁来治理它们？**

坦率的回答是：**目前基本没人治理，而这是结构问题，不是道德问题。**

#### "入口审查"为什么不顶用

大多数生态用的是市场审核闸门：提交 → 人工看一眼 → 上架。几十个技能时可行；几千个时失效；而当技能可以互相调用时，失效得更彻底。

三个结构性失效：

1. **一次性审查 ≠ 持续治理。** 审核时安全的技能，在一次更新、一个依赖变更、一次权限扩张之后，可能就不再安全。
2. **记录带不走。** 就算平台审过，那份记录通常也出不了平台。换个环境，治理证据就没了。
3. **责任链断裂。** 一串技能协作产生了坏结果，往往说不清**谁贡献了什么**。

#### 换成"生命周期"视角，问题就清楚了

不要只问一次"这个技能允许吗"，而是**在它的整条命里反复问**：

| 阶段 | 问什么 | 必须有什么 |
|---|---|---|
| **出生时** | 谁做的、谁负责、能碰什么？ | 登记：身份、创造者、治理责任人、声明的权限范围 |
| **运行时** | 它实际做了什么？ | 证据：动作日志、触碰的数据、人工监督记录 |
| **变更时** | 这次更新该不该放行？ | 门禁：触发 → 评估 → 放行 → 复核 |
| **退役时** | 数据和权限怎么处置？ | 退役记录与吊销路径 |

这套东西并不新奇，它就是**生命周期治理**——医疗器械、航空、金融这些"出事会伤人"的行业，早就在用这套管东西。

#### 大多数工具漏掉的三件事

- **离线能力**：很多部署环境不允许数据出机器。要求联网的治理工具，恰恰在最需要治理的地方用不了。
- **证据可携带**：记录必须能导出、能在创建它的平台之外被验证。
- **门禁归人**：高风险权限扩张不该由机器自己决定。**机器申请，人来授权。**

#### 我们的位置

我们（MedXpert × SynomosAI）做的正是这一层，名字叫 **Evidence-Gated AI Lifecycle Governance**，中文主权词是「**凡自治之物**」——配口诀 **有籍 · 有证 · 有门禁**。

**我们不主张自己是定义者。** 规则由标准组织和监管机构定义；我们的位置刻意低一层：**实现层（How）**，加上一个来自医疗器械监管的具体实例化，以及一套可迁移的跨域母版。

如果你在做技能生态，真正该问的不是"要不要治理"，而是：

> **对任意一个技能，你能不能回答这四个问题：谁拥有它、它做过什么、它上次变更有没有被审过、它退役时会发生什么？**

四个里有一个答不上来，缺的是**链条**，不是审查。

*延伸阅读：[lgd-theory](https://github.com/zhaoxinghua09-cell/lgd-theory) · DOI [10.5281/zenodo.22456647](https://doi.org/10.5281/zenodo.22456647)。本文为知识梳理与视角陈述，不构成法律或合规意见。*

---

## 投放建议

| 稿 | 平台 | 时机 | 锚词 |
|---|---|---|---|
| 稿一（EN） | dev.to | 与 B1 英文版**同日或次日**发布，互指 | Evidence-Gated AI Lifecycle Governance |
| 稿二（CN） | 知乎 | 与 B1 中文版**间隔 2–3 天** | 生命周期治理 / 凡自治之物 |

**互动预案**：若被追问"这跟 ISO 42001 / GB/Z 185 什么关系"，统一答——**"对齐、不取代；我们补的是实现层"**（见总账 §五 口径铁律）。

---

*B2 交付件 v1.0 · 2026-09-12 · 曝光度与竞争力提升线 Wave 2*
© XLGD · MedXpert × SynomosAI
