# resume-screening

简历批量筛选与岗位匹配度评分技能。依据岗位评分模型对多份简历逐维度打分，输出候选人评分汇总表格。

## 目录结构

```
resume-screening/
├── SKILL.md                          # 唯一入口：角色、工作流、输出契约、约束
├── references/
│   ├── scoring-rubric.md             # 5 维度评分细则与硬性淘汰规则优先级
│   └── jobs/
│       ├── _index.md                 # 岗位索引（岗位名 → 文件路径 → 硬性规则）
│       └── 高级后端开发工程师.md      # 岗位评分模型原文
└── scripts/
    ├── extract_resume_text.py        # 简历文本提取（PDF / docx / txt / md）
    ├── calculate_match_score.py      # 分项分数 → 总分 / 初筛 / 面试建议
    └── summarize_batch.py            # 多份结果 JSON → Markdown 汇总表格
```

## 安装

将本目录整体放入以下任一位置：

| 作用域 | 路径 |
|--------|------|
| 用户级 | `~/.codebuddy/skills/resume-screening/` |
| 项目级 | `<项目根>/.codebuddy/skills/resume-screening/` |

## 依赖

按需安装，`extract_resume_text.py --check` 可查看当前环境缺什么。

```bash
pip install pypdf pdfplumber pdfminer.six pypdfium2   # PDF 解析（多引擎容错，至少装一个）
pip install python-docx                              # Word 简历解析
```

纯文本（`.txt` / `.md`）解析无需任何依赖。

## 使用

直接向助手提出请求，附上简历文件并指明岗位：

```
帮我评估这 5 份简历对「高级后端开发工程师」岗位的匹配度
```

## 评分模型

- 5 个维度各满分 20 分，总分 100 分
- 初筛通过标准：总分不低于 80 分
- 岗位模型中以 `{此项必备条件}：` 开头的行为硬性淘汰规则，优先于分数区间执行

## 新增岗位

1. 在 `references/jobs/` 新增 `<岗位名称>.md`，按 5 段标准结构编写：【核心底层要求】【岗位职责】【岗位必备条件】【岗位加分项】【实践经验描述标准】。
2. 在 `references/jobs/_index.md` 增行登记。无需改动 SKILL.md 与脚本。
