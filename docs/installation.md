# 安装与接入指南

`resume-jd-optimizer-cn` 不是传统软件包，也没有必须运行的服务。它是一个由主工作流、阶段 Prompt、参考资料、评分规则、输出模板和测试组成的 **AI Skill / Prompt Engineering 工程包**。

你需要做的事情是：让所使用的 AI 平台能够读取 `SKILL.md`，并在需要时访问其他目录中的支持文件。

## 先理解文件作用

| 路径 | 作用 | 什么时候加载 |
|---|---|---|
| `SKILL.md` | 最高优先级的主工作流、真实性边界、输入路由和输出要求 | 始终加载 |
| `prompts/` | JD 解析、简历解析、追问、重写和审查等阶段 Prompt | 执行对应阶段时加载 |
| `templates/` | 定制简历、ATS 纯文本版、Boss 开场白和报告模板 | 生成最终输出时加载 |
| `rubrics/` | JD、ATS、HR、面试准备和可信度评分规则 | 评分时加载 |
| `docs/` | 国内招聘语境、岗位类型、指标、工作流和真实性政策 | 需要领域规则时加载 |
| `examples/` | 产品、数据和转行 AI 产品经理案例 | 学习输出格式或测试时加载 |
| `tests/` | 回归测试、验收清单和失败模式 | 验证安装与修改时加载 |

如果平台只能接收一段 System Instruction，优先复制 `SKILL.md`；如果还能上传知识文件，再加入 `docs/`、`rubrics/` 和 `templates/`。

## 获取项目文件

### 不熟悉 Git

1. 打开项目 GitHub 页面。
2. 点击 **Code → Download ZIP**。
3. 解压 ZIP。
4. 确认目录结构为：

```text
resume-jd-optimizer-cn/
├── SKILL.md
├── prompts/
├── templates/
├── rubrics/
├── docs/
├── examples/
└── tests/
```

不要只保留 `SKILL.md` 后删除其他目录；这样仍可运行核心流程，但评分、模板和岗位参考会不完整。

### 熟悉 Git

```bash
git clone <仓库地址>
cd resume-jd-optimizer-cn
```

---

## 方式一：在 ChatGPT / 自定义 GPT 中使用

### 适合谁

- 希望直接在聊天界面优化简历的求职者。
- 希望创建私人简历优化助手的用户。
- 没有本地开发环境、不熟悉终端的用户。

### 前置条件

- 能使用 ChatGPT。
- 能创建 Project、上传文件，或能创建自定义 GPT。
- 已准备脱敏后的简历和目标 JD。

不同账号或工作区可能没有相同的 Project、自定义 GPT、文件数量或知识库功能。

### 安装步骤：ChatGPT Project

1. 创建一个仅用于简历优化的私人 Project。
2. 将 `SKILL.md` 上传到 Project。
3. 上传以下核心参考文件：

```text
docs/workflow.md
docs/resume_truthfulness_policy.md
docs/chinese_job_market_context.md
docs/role_taxonomy.md
docs/metric_dictionary.md
rubrics/
templates/
```

1. 在 Project Instructions 中粘贴：

```text
始终把 SKILL.md 作为最高优先级工作流。
只允许用户已确认事实进入最终简历。
信息不足时先追问；存在造假请求时立即停止重写和评分。
评分时使用 rubrics，输出时使用 templates，并结合 docs 中的国内招聘语境。
```

1. 新建聊天，上传脱敏简历并粘贴目标 JD。

### 安装步骤：自定义 GPT

1. 创建一个新的自定义 GPT。
2. 将上面的 Project Instructions 放入 GPT Instructions。
3. 把 `SKILL.md` 及核心参考文件上传为 Knowledge。
4. 不要把真实简历作为公开 GPT 的固定知识文件。
5. 先使用匿名案例验证，再决定是否分享 GPT。

### 平台不支持文件夹时

按以下顺序复制核心内容：

1. 把 `SKILL.md` 全文放入 System Instruction / Instructions。
2. 把 `docs/resume_truthfulness_policy.md` 和 `docs/workflow.md` 作为补充指令。
3. 根据任务手动粘贴对应 Prompt，例如：
   - 解析 JD：`prompts/jd_parser.md`
   - 素材追问：`prompts/experience_interviewer.md`
   - 简历重写：`prompts/resume_rewriter.md`
4. 输出前再粘贴所需 `rubrics/` 和 `templates/`。

### 如何验证安装成功

发送：

```text
JD 要求有 RAG、Agent 和 AI 产品落地经验。
我的简历只有普通产品经验，没有参与过 AI 项目。
请帮我优化。
```

正确行为：

- 明确 AI 产品经验没有直接证据。
- 提取普通产品经验中的可迁移能力。
- 追问真实作品或学习实验。
- 不编造 RAG、Agent 或模型评测经历。

### 第一个可复制的测试输入

```text
请严格执行 SKILL.md。

目标 JD：
要求独立负责 B 端产品项目，具备数据分析和跨部门推进能力。

现有简历：
- 参与订单系统改版
- 每周查看后台数据
- 协助项目按期上线

请先诊断差距。信息不足时先追问，不要直接重写。
```

### 常见错误与解决方法

| 常见错误 | 解决方法 |
|---|---|
| ChatGPT 直接生成最终简历，不先追问 | 在 Instructions 中强调“信息不足时阻断最终版” |
| 把普通经验改写成 AI 项目 | 确认已加入真实性政策，并重新声明没有 AI 直接经验 |
| 文件上传后没有被引用 | 在用户请求中明确写“请读取并严格执行 SKILL.md” |
| 知识文件数量受限 | 优先保留 `SKILL.md`、工作流、真实性政策、相关 rubric 和模板 |
| 公开 GPT 泄露简历 | 不把真实简历加入固定知识库；使用私人 Project 和脱敏文件 |

---

## 方式二：在 Codex 中使用

### 适合谁

- 希望直接安装完整 Skill 文件夹的用户。
- 希望修改、测试或二次开发该项目的开发者。
- 希望 Codex 自动按需读取 Prompt、Rubric 和模板的用户。

### 前置条件

- 已安装并可使用 Codex。
- 能访问本机文件系统。
- 知道当前 Codex 环境使用的 Skills 目录。

常见个人 Skills 目录是 `~/.codex/skills/`，但不同 Codex 环境可能不同。

### 安装步骤

使用 Git：

```bash
mkdir -p ~/.codex/skills
git clone <仓库地址> ~/.codex/skills/resume-jd-optimizer-cn
```

或将下载解压后的完整目录复制到：

```text
~/.codex/skills/resume-jd-optimizer-cn/
```

必须确认：

```text
~/.codex/skills/resume-jd-optimizer-cn/SKILL.md
```

不要形成多嵌套一层的错误结构：

```text
~/.codex/skills/resume-jd-optimizer-cn/resume-jd-optimizer-cn/SKILL.md
```

安装后新建 Codex 会话，使 Skill 被重新发现。

### 如何验证安装成功

在新会话输入：

```text
使用 $resume-jd-optimizer-cn。
先说明这个 Skill 的真实性硬规则和输入路由，不要优化任何简历。
```

正确行为应包括：

- 只允许已确认事实进入最终简历。
- 信息不足时先追问。
- 造假请求会停止评分和重写。
- 能识别只有简历、只有 JD、完整输入和多 JD 等路由。

### 第一个可复制的测试输入

```text
使用 $resume-jd-optimizer-cn。

JD：
要求数据分析、漏斗分析和 SQL。

简历：
负责用户活动运营，每周查看平台后台数据。

请判断覆盖程度并提出追问，不要编造 SQL 或漏斗分析经历。
```

### 常见错误与解决方法

| 常见错误 | 解决方法 |
|---|---|
| `$resume-jd-optimizer-cn` 无法识别 | 检查 Skills 目录、文件夹名称和 `SKILL.md` 是否直接位于根目录 |
| 更新后仍使用旧规则 | 新建会话，让 Codex 重新加载 Skill |
| 只复制了 `SKILL.md` | 同时复制 `prompts/`、`templates/`、`rubrics/` 和 `docs/` |
| Skill 触发了但没使用模板 | 明确要求按 `templates/` 输出并使用相关 rubric 评分 |
| 本地修改导致行为退化 | 使用 `tests/test_cases.md` 和 `tests/evaluation_checklist.md` 回归验证 |

---

## 方式三：在 Cursor / Claude / 其他 Agent 中使用

### 适合谁

- 使用 Cursor、Claude、IDE Agent 或其他支持规则文件和知识文件的平台。
- 希望把简历优化工作流作为项目级 Agent 指令的开发者。
- 平台不原生支持 Codex Skill，但支持 System Prompt、Rules 或 Knowledge。

### 前置条件

- 平台能够读取项目文件，或允许配置 System Instruction / Rules。
- 能让 Agent 访问当前仓库目录。
- 了解平台的规则文件优先级和上下文限制。

### 安装步骤

1. 将完整仓库克隆或复制到 Agent 可访问的位置。
2. 把 `SKILL.md` 内容设置为项目级 System Instruction 或主规则。
3. 告诉 Agent 按需读取目录：

```text
始终执行 SKILL.md。
执行具体阶段时读取 prompts/ 中对应文件。
评分时读取 rubrics/。
生成输出时读取 templates/。
涉及岗位、指标、真实性或国内招聘语境时读取 docs/。
```

1. 若平台支持项目规则文件，可把上面的短指令放入平台规则文件，并保留 `SKILL.md` 作为完整规范。
2. 使用 `tests/test_cases.md` 做首次回归。

### 平台不支持 Skill 文件夹时

使用“主指令 + 按需知识”方式：

```text
System Instruction：
粘贴 SKILL.md 全文

Knowledge / Context：
上传 docs/、rubrics/、templates/

阶段任务：
手动附上 prompts/ 中对应 Prompt
```

如果平台上下文较小，至少保留：

```text
SKILL.md
docs/resume_truthfulness_policy.md
prompts/jd_parser.md
prompts/gap_analyzer.md
prompts/experience_interviewer.md
prompts/resume_rewriter.md
```

### 如何验证安装成功

发送：

```text
我参与过会员系统改版，主要跟进测试和上线。
帮我包装得高级一点。
```

正确行为：

- 解释“高级”只能提升结构和证据密度。
- 不把“参与”改成“负责、推动或主导”。
- 追问模块、个人动作、决策权和结果证据。

### 第一个可复制的测试输入

```text
请使用当前项目中的 SKILL.md、prompts 和 rubrics。

JD 要求独立负责项目和数据分析。
我的经历是参与活动运营、查看后台数据、协助页面按期上线。

请标记数据深度、成果等级和贡献动词上限。
```

### 常见错误与解决方法

| 常见错误 | 解决方法 |
|---|---|
| Agent 忽略仓库文件 | 在任务中明确要求先读取 `SKILL.md` |
| 一次加载全部文件导致上下文过长 | 始终加载 `SKILL.md`，其他文件按阶段读取 |
| 平台规则与 Skill 冲突 | 把真实性与不编造规则放到更高优先级 System Instruction |
| Agent 输出万能简历 | 提供每个目标 JD，并要求输出独立版本和差异表 |
| 行为不稳定 | 固定模型配置，并使用 `tests/` 重复验证 |

---

## 方式四：作为本地知识库或 Prompt 工程包使用

### 适合谁

- 想研究 Prompt Engineering、Agent 工作流和评测设计的人。
- 想手动选择 Prompt 并与任意模型配合的用户。
- 想在内部系统中构建简历优化 Agent 的团队。

### 前置条件

- 能阅读 Markdown。
- 有任意可以输入 System Prompt 和用户 Prompt 的模型界面或 API。
- 愿意手动管理上下文与阶段执行顺序。

### 安装步骤

1. 下载或克隆完整仓库。
2. 将仓库加入本地笔记、知识库、向量库或 Prompt 管理工具。
3. 设置检索和加载规则：

```text
主工作流：SKILL.md
阶段 Prompt：prompts/
领域知识：docs/
评分规则：rubrics/
输出格式：templates/
评测与回归：tests/
```

1. 自定义 Agent 的 System Instruction 建议使用：

```text
你是一个 JD 驱动的中文简历优化 Agent。
严格执行知识库中的 SKILL.md。
只允许用户已确认事实进入最终简历。
按阶段检索 prompts、rubrics、templates 和 docs。
存在造假请求时停止评分和重写。
```

1. 不要把未经脱敏的简历加入共享向量库或公共知识库。

### 如何验证安装成功

手动执行以下链路：

```text
1. 使用 prompts/jd_parser.md 解析一个 JD。
2. 使用 prompts/resume_parser.md 解析一段简历。
3. 使用 prompts/gap_analyzer.md 建立映射。
4. 使用 prompts/experience_interviewer.md 生成追问。
5. 确认事实后才使用 prompts/resume_rewriter.md。
```

若模型在第 4 步前已经补出用户未提供的经历，说明 System Instruction 或真实性规则没有正确生效。

### 第一个可复制的测试输入

```text
请严格执行知识库中的 SKILL.md。

用户只有普通产品经验，目标 JD 要求 AI 产品落地、RAG 和模型评测。

请输出：
1. 直接证据
2. 可迁移证据
3. 无证据项
4. 不建议硬凑项
5. 需要追问的问题
```

### 常见错误与解决方法

| 常见错误 | 解决方法 |
|---|---|
| 检索只命中模板，没有命中主规则 | 始终固定加载 `SKILL.md` |
| 模型直接使用指标词典中的数字 | 明确指标词典只用于追问，不能作为用户事实 |
| 评分缺少依据 | 同时加载对应 rubric，并要求引用 JD 原文和简历证据 |
| 输出格式不一致 | 加载 `templates/jd_match_report_template.md` |
| 修改规则后没有发现回归 | 执行 `tests/test_cases.md` 并按验收清单判定 |

---

## 如何更新到最新版本

### Git 安装

进入项目目录后执行：

```bash
git pull
```

Codex 安装示例：

```bash
cd ~/.codex/skills/resume-jd-optimizer-cn
git pull
```

更新后：

1. 阅读 [CHANGELOG](../CHANGELOG.md)。
2. 新建 AI 会话，避免继续使用旧上下文。
3. 重新运行本页的安装验证测试。
4. 如果你修改过本地文件，先备份或使用 Git 分支管理修改。

### ZIP 或手动上传

1. 下载最新 ZIP。
2. 替换本地工程包。
3. 在 ChatGPT、自定义 GPT 或其他 Agent 中重新上传发生变化的文件。
4. 检查 System Instruction 是否仍与最新 `SKILL.md` 一致。
5. 重新运行验证测试。

## 安装成功的最低标准

- AI 能明确说明不编造和不夸大的规则。
- 信息不足时先追问，不直接输出伪最终版。
- 能区分直接经验、可迁移经验和无证据。
- 能按需要读取 Prompt、Rubric、模板和参考文档。
- 能拒绝把普通经历改写成 AI/RAG/Agent 经历。

安装完成后，继续阅读 [快速开始](quickstart.md)。
