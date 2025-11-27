# 同步到 GitHub 的步骤指南

在本地或容器中完成修改后，GitHub 仓库不会自动同步，需要手动提交并推送。下面提供分步说明，以及可以直接复制执行的命令模板。

## 1. 检查当前分支与远程
```bash
git status -sb      # 查看工作区是否有改动、当前分支
git remote -v       # 确认远程指向你的 GitHub 仓库
```
如需调整远程：
```bash
git remote set-url origin <你的仓库地址>
# 或首次添加远程
git remote add origin <你的仓库地址>
```

> Codex/容器环境没有自动推送，后续必须执行 `git push` 才会在 GitHub 可见。

## 2. 修改并自测
按需编辑代码，运行项目相关的测试或构建脚本（示例）：
```bash
npm test
npm run build
```

## 3. 查看并暂存改动
```bash
git status -sb      # 确认改动列表
git diff            # 逐行检查改动
git add <文件路径>  # 或使用 git add .
```

## 4. 提交
```bash
git commit -m "描述本次改动"
```
如提示未配置用户名/邮箱，可设置：
```bash
git config user.name "你的名字"
git config user.email "你的邮箱"
```

## 5. 推送到 GitHub
首次推送或新分支：
```bash
git push -u origin <分支名>
```
后续同分支更新：
```bash
git push
```

## 5+. 从 Codex/容器执行到 GitHub 生效的最短命令串
若已确认远程和分支无误，可直接复制下列命令（以当前分支为例）：
```bash
git status -sb
git add .
git commit -m "你的提交说明"
git push             # 首次推送用 git push -u origin <分支名>
git log --oneline -5 # 可选，确认本地最新提交
```
推送完成后，刷新 GitHub 对应分支即可看到最新提交。

## 6. 在 GitHub 上验证
- 打开仓库对应分支，确认最新 commit 出现。
- 若使用 PR 流程，查看 PR 是否包含刚推送的提交。

## 常见问题排查
- **看不到改动**：通常是未 `git commit` 或未 `git push`，或者推送到了错误远程/分支。
- **权限/凭据问题**：推送需要有效的 GitHub 凭据（如 PAT）。
- **分支不一致**：本地分支与 GitHub 浏览的分支不同，请在正确分支查看或推送。
