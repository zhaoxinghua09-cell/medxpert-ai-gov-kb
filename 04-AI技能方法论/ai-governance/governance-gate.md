---
title: "Governance Gate Checklist（AI 治理门禁清单）"
summary: "本文件为 `ai-governance` 的门禁检查与合规映射细则。门禁在任何'对外动作 / 外部评测'前运行，"
domain: "AI治理/A³法则/AI造AI方法论"
source: "github:zhaoxinghua09-cell/medxpert-ai-gov-kb"
version: "1.0"
updated: "2026-09-15"
tags: ["AI治理", "A3法则", "生命周期治理", "证据门禁", "记忆工程", "自进化", "可追溯", "AI造AI"]
type: "doc"
---

# Governance Gate Checklist（AI 治理门禁清单）

本文件为 `ai-governance` 的门禁检查与合规映射细则。门禁在任何"对外动作 / 外部评测"前运行，
结论为 **PASS / CONDITIONAL / BLOCK**。

## 1. Pre-external-action gate（对外动作前门禁）

- [ ] 意图已记录（who / what / target / why）
- [ ] Agent 身份已核验（`verified-agent-identity` / `identity-verify`）
- [ ] 授权 token 按最小必要范围签发（`authz-code-design`）
- [ ] Skill / agent 已通过安全审计（`skills-security-check` / `skill-vetter` / `unblocklabs-skill-audit`）
- [ ] 无未处理的高危（high）安全发现
- [ ] 最新 `ai-grader` 评分存在且达到放行阈值（`ai-consciousness` + `ai-grader`）
- [ ] 已产出合规映射（EU AI Act / FDA，见 §3）

## 2. Decision（结论与阈值）

### BLOCK（禁止，立即停）
满足任一即 BLOCK：
- Agent 身份未核验，或授权 token 范围超出最小必要；
- 存在任一未处理的高危（high）安全发现；
- 无 `ai-grader` 评分，或评分低于放行阈值（见下）；
- 受监管场景（器械 / 国际业务）下合规映射缺失。

### CONDITIONAL（条件放行）
满足全部以下条件可 CONDITIONAL 放行：
- 安全发现均为中危（medium）且已记录缓解措施；
- `ai-grader` 评分处于条件区间（见下）；
- 由指定人类监督人（human overseer，身份经 `identity-verify` 确认）签字放行，记录于审计轨迹。

### PASS（通过）
上述门禁全绿，写入审计记录后执行。

### 放行阈值（ai-grader 45 维量表）
- 满分 100（45 维加权）。
- **PASS**：总分 ≥ 75，且任一维度不低于"可接受"档（≥ 2/3 档）。
- **CONDITIONAL**：总分 60–74，且无人格 / 合规相关维度落入"风险"档。
- **BLOCK**：总分 < 60，或任一合规 / 安全相关维度落入"风险"档。
> 阈值数值为占位初值，需按实环境调参（见 SKILL.md Status）。

### 审批流（CONDITIONAL）
requester → gate 判 CONDITIONAL → 路由至角色化人类监督人（来自 `identity-verify` 的 overseer 角色）
→ 签字（身份 + 时间戳 + 理由）写入 audit trail → 在命名约束下执行。

## 3. Compliance mapping（合规映射 · 已填实）

### 3.1 EU AI Act（Regulation (EU) 2024/1689，高风险系统义务）
| 要求 | 条款 | 证据来源 |
|---|---|---|
| 风险管理系统 | Art. 9 | `ai-grader` 评分 + 维度增量（行为风险信号） |
| 数据与数据治理 | Art. 10 | 数据集 lineage 记录（TODO 接数据治理 skill） |
| 技术文档 | Art. 11 | gate 审计记录（本 trail） |
| 记录保存 / 日志 | Art. 12 | audit trail（§4） |
| 透明度与用户告知 | Art. 13 | 对外动作意图记录（§1） |
| 人类监督 | Art. 14 | CONDITIONAL 审批流（§2） |
| 准确性 / 鲁棒性 / 网络安全 | Art. 15 | 评测台结果（rag-eval-harness 等） |

### 3.2 FDA（AI/ML 医疗器械 · SaMD / AI-DSF）
| 要求 | 来源 | 证据来源 |
|---|---|---|
| 全生命周期可追溯（TPLC） | FDA TPLC 框架 | audit trail 全程链接 |
| 良好机器学习实践（GMLP）— 文档与可追溯 | FDA/CMS/ONC GMLP 十原则（2021） | 数据 / 设计 / 测试可追溯 + `ai-grader` 基线 |
| 预定变更控制计划（PCCP） | FDA PCCP 指南 | gate 对"已声明变更"放行，未声明变更 BLOCK |
| SaMD 预期用途对齐 | IMDRF SaMD 框架 | 意图记录（§1）与合规映射 |

> 注：FDA 部分条款为映射骨架，落地时需对照具体产品分类（SaMD 分级 / AI-DSF）细化。

## 4. Audit trail（审计轨迹规范）

### 存储格式
追加式 JSONL，每个对外动作一行，路径：
`<AUDIT_ROOT>/ai-governance/<YYYY-MM>/trail.jsonl`
（默认 `AUDIT_ROOT = .workbuddy/audit`，可通过环境变量覆盖）。

### 单行 schema
```json
{
  "ts": "ISO-8601",
  "agent_id": "string",
  "skill": "string",
  "target_surface": "string",
  "intent": "string",
  "identity_proof": "ref",
  "authz_scope": "string",
  "security_findings": {"high": 0, "medium": 0, "details": []},
  "ai_grader_score": {"total": 0, "dimensions": {}},
  "compliance_map": {"eu_ai_act": {}, "fda": {}},
  "decision": "PASS|CONDITIONAL|BLOCK",
  "approver": "ref|null"
}
```

### 查询约定
- 按 agent_id / 日期 / decision 过滤：用 Grep / Read 检索 `<AUDIT_ROOT>/ai-governance/` 下 JSONL。
- 未来可加 `scripts/query_trail.py` 提供结构化查询（占位，非阻塞）。
