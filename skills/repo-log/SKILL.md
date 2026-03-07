---
name: repo-log
description: 帮助生成符合 Android 项目提交规范的英文上 code 日志。
---

# Android Code Log Generation Skill

此技能指导如何撰写符合 Android 项目要求的英文 code 日志。

## 提交日志撰写流程

1. 先运行 `cd <worksapce> && git diff --cached` 查看已暂存差异。
2. 再根据差异内容，按照以下规范撰写一份简洁的提交日志，并以示例的Markdown格式输出

**示例**：

```
[module]Add/Fix/Remove/Refactor <object> ...

[Description]
1. Add/Fix/Remove/Refactor <object> ...
2. ...
```

## 标题格式规范

- 英文；标题或正文要点尽量用动作词开头，精炼，避免冗词。
- 日志只写改动内容、位置或受影响符号，不写测试、感受或背景。
- 标题采用 `[module]Add/Fix/Remove/Refactor <object> ...` 格式
  - `module` 模块名为单个单词，模块名沿用 Android 社区惯例（不含斜杠）。
  - `object` 可以是模块内的 `submodule/feature/code/symbol/...` 等
- 跨多个Project改动，需要在标题末尾注明 `[1/n]`，n为总改动数。
  - 例如：`[All]Fix foo bar [1/3]`。

**正文省略策略**：

当涉及以下情况时，应当省略正文！
1. 改动量较小，标题已完整描述改动的目的、受影响的符号与范围。
2. 改动为非行为性调整（拼写、注释、格式、局部重命名）。
3. 未涉及对公共 API、构建脚本、配置或跨模块交互的变更。

## 正文格式规范

- 英文；列点描述改动细节，每行≤72字符，避免缩略、模糊词。
- 正文细节应与差异规模相符，改动越大细节越多，改动越小细节越少。
- 正文采用与标题使用相同的规范，`Add/Fix/Remove/Refactor <object> ...` 格式
- 不自行添加 Change-Id/Signed-off-by/Reviewed-by (由 git commit hook 自动生成)。

## 增删类描述细则

- 描述要点以 `Add/Remove/Change <object>` 开头。

## 修复类描述细则

- 描述要点以 `Fix <object> <issue/problem>` 开头。
- `issue/problem` 指修复的具体问题或缺陷，如内存泄漏、性能问题、功能异常等。

## 重构类描述细则

- 描述要点以 `Refactor <object> and <Refactoring Term>` 开头。
- `Refactoring Term` 为 ***Refactoring*** 中的术语，并列出涉及符号的要点

在生成 code 日志时，逐条核对以上规范。
