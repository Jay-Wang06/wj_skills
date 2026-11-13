---
name: commit-message
description: >-
  根据已暂存或未暂存的 diff 起草简洁的 git commit message，强调 why 而非 what。在用户要求写 commit 说明、协助提交，或总结暂存改动以便提交时使用。
---

# Commit Message

根据真实 diff 写清晰的提交说明。除非用户明确要求，否则不要执行 commit。

## 工作流

1. **查看改动**（尽量并行）：
   - `git status`
   - `git diff --staged`（主依据）；若无暂存则用 `git diff`，并说明文案假定会暂存这些文件
   - `git log -5 --oneline`（对齐仓库风格：Conventional Commits 或自由格式、语言、长度）
2. **按下方格式起草**。
3. **自检**：
   - 变更集中无密钥（`.env`、凭证、token）——有则警告
   - 文案与 diff 一致；不要编造 diff 里没有的功能
   - 优先一次逻辑提交；若混杂多个意图，建议拆分，并只起草主提交文案（除非用户要全部）

## 文案格式

近期 log 若用 Conventional Commits 则沿用；否则模仿本仓库既有风格。

```
<type>(<可选 scope>): <祈使语气短摘要>

<可选正文：1～3 行说明 why / 影响>
```

**摘要规则**

- 祈使语气：用 "add" / "fix" / "rename"，不用 "added" / "fixes"（中文仓库可用「添加」「修复」等对应说法）
- 约 ≤ 72 字符；句末不加句号
- 强调 **为什么 / 意图**，不要列文件清单
- 语言与仓库近期提交一致（中文或英文）

**常用 type**：`feat`、`fix`、`refactor`、`docs`、`test`、`chore`、`perf`、`build`、`ci`

**正文**——仅在有用时写：

- 动机、取舍或用户可见影响
- 破坏性变更：`BREAKING CHANGE: …`
- 不要重复摘要；不要堆 `git status`

## 示例

**输入**：新增 JWT 登录接口 + 中间件  
**输出**：
```
feat(auth): add JWT-based login

Validate tokens on protected routes so unauthenticated
requests fail closed at the edge.
```

**输入**：报表日期时区错误  
**输出**：
```
fix(reports): use UTC when formatting report dates
```

**输入**：重命名 helper，行为不变  
**输出**：
```
refactor: rename loadConfig helpers for clarity
```

## 若用户要求执行提交

仅在此时：

1. 暂存相关文件（`git add …`）——跳过密钥文件并警告
2. 用 HEREDOC/stdin 传 message（不要用 `-i`）；Windows PowerShell 优先：
   ```powershell
   git commit -m @"
   <message>
   "@
   ```
   若 shell 支持也可用 bash 风格 HEREDOC
3. 提交后跑 `git status` 确认
4. 除非用户明确要求，绝不 `push`、`--amend` 或跳过 hook 的参数

## 约束

- 不要改 git config。
- 只要求文案时不要 commit。
- 暂存为空且工作区干净时如实说明——不要编造 message。
