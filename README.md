# wj_skills

一组通用的 Cursor Agent Skills，与具体业务项目无关，可在任意仓库中复用。

每个 skill 是一个目录，内含 `SKILL.md`。按需复制到个人 skills 目录（如 `~/.cursor/skills/`）或项目的 `.cursor/skills/` 后即可使用。

## Skills 一览

| Skill | 做什么 |
|-------|--------|
| [explain-diff](explain-diff/) | 用人话解释代码 diff：改了什么、影响范围、风险与建议验证 |
| [debug-playbook](debug-playbook/) | 系统化排错：复现 → 假设 → 证据验证 → 最小修复 → 回归 |
| [commit-message](commit-message/) | 根据 diff 起草简洁 commit message（强调 why；默认只出文案不提交） |
| [ask-before-code](ask-before-code/) | 动手前先澄清需求：阻塞问题、范围、薄计划，避免做错方向 |
| [rewrite-clear](rewrite-clear/) | 把含糊的需求/邮件/笔记改写成清晰、可执行的表述 |
| [changelog-user](changelog-user/) | 把 commit/PR 转成面向用户的更新说明（What's New） |

## 各 skill 说明

### explain-diff

把 git diff 或粘贴的 patch 整理成便于评审的说明：按意图分组、标出影响半径与风险，并给出建议验证项。不主动改代码，也不默认做完整 code review。

**适用**：解释 diff、总结改动、理解 PR 补丁。

### debug-playbook

按固定流程排错，用证据说话：先复现或界定范围，再列可证伪假设并验证，最后做最小修复并做回归检查。

**适用**：粘贴 stacktrace、报 bug、排查「坏了 / 不工作」。

### commit-message

根据暂存或未暂存 diff 起草提交说明，对齐仓库既有风格（如 Conventional Commits），强调意图而非文件列表。仅在用户明确要求时才执行 `git commit`。

**适用**：写 commit 文案、协助提交。

### ask-before-code

在需求含糊或存在多种设计时，先用少量阻塞问题划清目标与范围，再给出薄计划，确认后再动手。小而明确的改动可跳过。

**适用**：实现新功能、非琐碎改动且验收标准不清。

### rewrite-clear

把含糊文字改成别人能照着做的表述，并标出缺口；不编造截止日期、负责人或验收标准。

**适用**：澄清需求措辞、整理邮件/纪要、把凌乱笔记变成可执行说明。

### changelog-user

把技术向的 commit/PR 改写成用户能看懂的更新说明：讲结果、藏实现，按新增/改进/修复等分类，破坏性变更附应对方式。

**适用**：写 changelog、release notes、What's New。

## 使用方式

在对话中点名 skill（例如「用 explain-diff 讲讲这段改动」），或确保 skill 已安装到 Cursor 可发现的路径，以便按 `description` 自动匹配场景。
