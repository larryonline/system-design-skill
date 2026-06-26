[:us: English Version](README.md)

# 场景驱动的系统抽象与边界治理方法论

> 用真实场景发现问题，用共通性提炼抽象，用语义归属划清解释权，用边界治理控制复杂度，最终形成稳定、清晰、可审查的设计基线。

基于场景驱动的系统抽象与边界治理方法论，以 Claude Code Skill 形式交付。适用于复杂系统的早期与中期设计——场景复杂、需求来源多样、容易出现功能堆叠和职责膨胀、需要从大量用例中提炼稳定抽象的场合。

## 安装

### 方式一：克隆到本地 skills 目录

```bash
mkdir -p ~/.claude/skills
git clone https://github.com/larryonline/system-design-skill.git ~/.claude/skills/system-design
```

### 方式二：让 Claude Code 自动安装

对 Claude Code 说：

```
请帮我安装 system-design skill，从 https://github.com/larryonline/system-design-skill 克隆到本地 skills 目录
```

## 触发方式

讨论以下话题时 skill 会自动激活：

- 系统设计、架构设计、模块划分
- 边界治理、抽象设计、接口定义
- 技术方案评审、系统重构

不适用于纯代码实现、bug 修复、简单功能添加。

## 目录结构

```
├── SKILL.md                        # Skill 应用骨架
├── references/                     # 方法论细节，按需加载
│   ├── methodology-full.md         # 12 层方法论完整版
│   ├── layers-1-4.md               # 场景 → 边界
│   ├── layers-5-8.md               # 抽象 → 失败
│   ├── layers-9-12.md              # 工程 → 版本化
│   ├── checklist.md                # 通用设计检查清单
│   ├── aesthetics.md               # 设计审美偏好
│   └── coverage-regression.md      # 用例覆盖与回归机制
```

## 三种工作模式

| 模式 | 信号 | 行为 |
|------|------|------|
| 交互式引导 | 从零设计新系统 | 逐层引导场景收集、边界治理、抽象设计，生成用例表 + 设计基线 |
| 自动分析评审 | 评审已有设计 | 对照检查清单输出符合点、风险点、建议 |
| 聚焦分析 | 只看特定层 | 深入特定粒度（边界/抽象/接口），不做全面覆盖 |

## 输出物

交互式引导模式下生成两个文件：

- `docs/<系统名称>-use-cases.md` — 全量用例表，设计输入基线，9 列格式（UC-ID、场景名称、触发者、输入、系统行为、输出、消费方、路径类型、频率）
- `docs/<系统名称>-system-design.md` — 设计基线，7 个设计面（场景分析 → 系统定位与边界 → 核心抽象 → 接口契约 → 运行语义与失败模型 → 工程约束与角色 → 扩展治理与版本化）

用例表变更后自动回归审查设计基线各章节是否仍覆盖全量用例。

