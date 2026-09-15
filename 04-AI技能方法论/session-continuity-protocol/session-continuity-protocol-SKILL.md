---
compliance_review: "待核验：上架三铁律 ①国家/国际合规 ②AI特别友好 ③理念文化传播+强IP；发布前由 skill-release-gate 审查"
name: session-continuity-protocol
description: "跨工作区 / 跨会话记忆连续性协议（潘布达首发）。触发场景：新会话开局、用户说「续上上下文 / 你还记得吗 / 你失忆了」、或要做任何连续性敏感任务（公众号发稿、品牌资产、发布阻塞、密钥投递、项目状态）之前。加载后严格跑「开局四步」把已固化事实回灌，避免在已定稿事项上重复问用户、避免失忆。真源 = 文件层（_ACTIVE_PROJECTS.md + 账号 MEMORY.md）优先于 localmem 语义层兜底。"
version: 1.0.0
agent_created: true
author: 潘布达(Buda Pan)@SynomosAI
license: MIT
category: 通用技能
platforms: [WorkBuddy, Claude Code, Windows, macOS, Linux]
read_when:
  - 新会话开始、用户还没说具体任务前（默认主动跑）
  - 用户质疑「你失忆了 / 怎么又忘了 / 昨天不是已经…」
  - 要做公众号发稿、品牌资产、发布阻塞、密钥投递类任务前
  - 跨工作区接续上一个会话的半成品（如推送草稿箱仍卡在哪）
tags: [continuity, memory, localmem, cross-session, 开局四步, 失忆, 跨工作区]
slug: session-continuity-protocol
displayName: 跨会话连续性协议（开局四步）
display_name: 跨会话连续性协议（开局四步）
title: 跨会话连续性协议（开局四步）
---
