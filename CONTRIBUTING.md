# 贡献指南

感谢你帮助改进 `resume-jd-optimizer-cn`。项目优先接受能够提升真实性、可执行性和国内招聘适配度的贡献。

## 可以贡献什么

- 匿名化的真实求职案例和回归测试。
- 新岗位类型、指标词典或国内招聘语境。
- 更准确的 JD 解析、追问和风险检查规则。
- ATS、HR、面试和可信度评分改进。
- 文档、安装说明、示例和错别字修复。

## 隐私要求

提交前必须删除或替换：

- 姓名、电话、邮箱、住址和身份证信息。
- 真实客户名称、合同信息和未公开经营数据。
- 能识别个人或公司的敏感项目细节。

推荐使用“某电商公司”“客户 A”“约 20%”等脱敏表达。

## 提交 Issue

1. 选择合适的 Issue 模板。
2. 描述输入、预期行为和实际行为。
3. 提供最小可复现案例。
4. 明确说明案例已经脱敏。

不要在公开 Issue 中上传完整真实简历。

## 提交 Pull Request

1. Fork 仓库并创建主题分支。
2. 只修改与问题直接相关的文件。
3. 为规则变化增加或更新 `tests/test_cases.md`。
4. 若新增失败风险，更新 `tests/failure_modes.md`。
5. 检查内部链接、Markdown 格式和真实性边界。
6. 在 PR 中说明修改原因、验证方式和潜在风险。

建议分支名：

```text
docs/quickstart-improvement
feat/role-taxonomy-finance
fix/no-jd-routing
test/keyword-stuffing-case
```

## 设计原则

- 不以增加篇幅为目标。
- 不新增无法验证的效果承诺。
- 不鼓励编造、夸大或关键词堆砌。
- 优先复用现有工作流和文件结构。
- 规则必须能通过具体测试场景验证。

## 本地验证

安装 Node.js 后运行：

```bash
npx --yes markdownlint-cli2@0.18.1 "**/*.md" "#.git/**"
```

若本机有 Skill 校验器，也应验证 `SKILL.md` 的 frontmatter 和命名规则。

## License

提交贡献即表示你同意贡献内容按本项目的 [MIT License](LICENSE) 发布。
