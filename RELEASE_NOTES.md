# v0.1.0 - Initial release

`resume-jd-optimizer-cn` 是一个面向中国大陆求职者的 JD 驱动型中文简历优化 Skill。它不是通用简历润色 Prompt，而是先解析目标岗位要求，再将要求映射到用户可验证的真实经历，帮助发现材料缺口、重构表达并准备面试追问。

本项目帮助提高简历表达质量、岗位匹配度和面试自洽性，但不保证通过 ATS、获得面试或录用。

## 核心能力

- 解析岗位 JD：识别硬性条件、核心职责、技能、业务场景、关键词和权重。
- 诊断简历缺口：区分已覆盖、弱覆盖、未覆盖和不建议硬凑的要求。
- 追问真实素材：围绕业务背景、个人贡献、方法、结果和证据来源提出具体问题。
- 生成 JD 定制版简历与 ATS 纯文本版。
- 生成 HR 快速阅读摘要、Boss 直聘开场白和猎头介绍。
- 生成针对数字、归因、决策和个人贡献的面试追问。
- 使用 JD 匹配、ATS、HR、面试准备和可信度五套评分规则。
- 支持应届、社招、转行和多 JD 独立版本管理。
- 检查编造、夸大、关键词堆砌、AI 模板腔和面试自洽风险。

## 安装方式

本项目是 AI Skill / Prompt Engineering 工程包，不是需要启动服务的传统软件。

### Codex

```bash
mkdir -p ~/.codex/skills
git clone https://github.com/coinluu/resume-jd-optimizer-cn.git \
  ~/.codex/skills/resume-jd-optimizer-cn
```

在新会话中调用 `$resume-jd-optimizer-cn`，并提供脱敏后的简历与目标 JD。

### ChatGPT / 自定义 GPT

1. 将 `SKILL.md` 放入 Project Instructions 或自定义 GPT Instructions。
2. 上传 `docs/`、`rubrics/` 和 `templates/` 中需要的参考文件。
3. 在请求中明确要求读取并严格执行 `SKILL.md`。

### Cursor、Claude 或其他 Agent

将 `SKILL.md` 作为 System Instruction，并按阶段加载 `prompts/`、`rubrics/` 和 `templates/`。

完整步骤见 [安装与接入指南](https://github.com/coinluu/resume-jd-optimizer-cn/blob/main/docs/installation.md)。

## 使用示例

```text
请严格执行 resume-jd-optimizer-cn / SKILL.md。

目标 JD：
[粘贴完整 JD]

现有简历：
[粘贴脱敏后的简历]

补充背景：
- 是否转行：
- 已确认数据或区间：
- 作品链接：
- 历史投递反馈：

请先分析 JD 与简历差距。
信息不足时先追问，不要编造。
在事实确认前，不要生成最终简历。
```

完整产品经理、数据分析师和转行 AI 产品经理案例见
[示例文档](https://github.com/coinluu/resume-jd-optimizer-cn/blob/main/docs/examples.md)。

## 隐私与真实性提醒

- 上传简历前删除姓名、电话、邮箱、身份证、住址和其他身份信息。
- 不要提交客户名称、合同、源代码、访问令牌或未公开经营数据。
- 最终简历只能使用用户原始材料或用户明确确认的事实。
- 不编造公司、项目、证书、工具、数据、AI、RAG 或 Agent 经历。
- 不把“参与”改成“主导”，不把团队结果全部归给个人。
- 若用户要求造假，Skill 会停止最终版生成和评分，并提供真实替代方案。

详细规则见
[隐私与真实性声明](https://github.com/coinluu/resume-jd-optimizer-cn/blob/main/docs/privacy-and-truthfulness.md)。

## 已知限制

- 项目无法验证用户输入事实是否真实，最终内容仍需用户逐项确认。
- ATS、HR 和面试评分用于结构化诊断，不代表真实招聘结果。
- 不同公司、岗位和招聘平台的筛选标准存在差异。
- 当前以 Markdown 与纯文本输入输出为主，尚未提供 PDF / DOCX 自动解析。
- 岗位参考以常见中国大陆招聘场景为主，部分行业覆盖仍有限。
- AI 平台的文件数量、上下文长度和知识库能力可能影响执行完整度。

## 下一步 Roadmap

- 增加金融、制造、医疗、游戏和跨境岗位参考。
- 增加更多匿名化真实回归案例，以及应届生、实习和中高年限专项样例。
- 完善空窗、短期经历和跨行业转岗风险表达。
- 提供结构化事实底稿 Schema 和多 JD 版本差异检查工具。
- 增加链接、评分权重、必需文件和测试覆盖自动校验。
- 探索 PDF / DOCX 文本解析与 ATS 结构检查，同时保留人工复核。

完整计划见 [Roadmap](https://github.com/coinluu/resume-jd-optimizer-cn/blob/main/ROADMAP.md)。
