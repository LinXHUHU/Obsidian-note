# Git 使用技巧

## 一、Git Stash

`git stash` 是一个非常有用的 Git 命令，它可以临时存储你的工作进度，让你能够快速切换到其他分支进行工作，而不用担心当前的工作状态。下面是一些使用 `git stash` 的技巧和最佳实践：

### 1. 常用命令
- **创建 stash**：
  - `git stash`: 自动保存当前工作区的状态和索引到 stash 中。
  - `git stash save <message>`: 添加一条 stash 并附带消息说明。
  - `git stash push`: 同 `git stash save`，但是可以连续使用多次来保存多个 stash。
  - `git stash drop`: 删除最新的 stash。
  - `git stash list`: 列出所有 stash。

- **应用 stash**：
  - `git stash apply`: 将最新的 stash 应用到当前工作区，保留 stash。
  - `git stash pop`: 将最新的 stash 应用到当前工作区并删除该 stash。
  - `git stash apply <stash>`: 应用特定的 stash。
  - `git stash pop <stash>`: 应用并删除特定的 stash。

- **清除 stash**：
  - `git stash clear`: 清除所有 stash。
  - `git stash drop <stash>`: 删除特定的 stash。

### 2. 实际应用场景
- **切换分支**：当你正在开发一个特性，但突然需要修复另一个分支上的紧急 bug 时，可以使用 `git stash` 临时保存当前的工作状态，然后切换到 bug 修复分支，修复 bug 后再回到原来的特性分支继续工作。
  
  ```bash
  git stash
  git checkout <bug-fix-branch>
  # 修复 bug
  git commit
  git push
  git checkout <original-feature-branch>
  git stash pop
  ```
  
- **合并冲突**：当你在合并分支时遇到冲突，可以先使用 `git stash` 保存当前的工作状态，解决冲突后再恢复工作状态。
  
  ```bash
  git stash
  git merge <other-branch>
  # 解决冲突
  git commit
  git stash pop
  ```
  
- **提交前清理**：当你即将提交更改，但还有一些未完成的改动不想提交时，可以使用 `git stash` 保存这些改动，然后提交已完成的工作。
  
  ```bash
  git stash
  git add .
  git commit -m "Completed feature X"
  git stash pop
  ```

### 3. 更高级的用法
- **stash 特定文件**：如果你想仅保存特定文件的更改，可以使用 `--patch` 选项。
  
  ```bash
  git stash save --patch
  ```
  
- **stash 未跟踪文件**：默认情况下，`git stash` 不会保存未跟踪的文件。如果你想要保存这些文件，可以使用 `--include-untracked` 选项。
  
  ```bash
  git stash save --include-untracked
  ```
  
- **stash 未添加的改动**：如果你只想保存那些已经被修改但还没有被 `git add` 的文件，可以使用 `--keep-index` 选项。
  
  ```bash
  git stash save --keep-index
  ```

### 4. 常见问题
- **如何查看 stash 的内容**：
  - `git stash show`: 显示最新 stash 的 diff。
  - `git stash show <stash>`: 显示特定 stash 的 diff。
  - `git stash show -p <stash>`: 显示特定 stash 的详细 diff。

- **如何恢复 stash 中的文件**：
  - `git stash apply <stash>`: 将特定 stash 中的文件恢复到工作区。
  - `git stash pop <stash>`: 将特定 stash 中的文件恢复到工作区并删除该 stash。

- **如何将 stash 应用到另一个分支**：
  - `git checkout <branch>`: 切换到目标分支。
  - `git stash apply <stash>`: 将特定 stash 应用到当前分支。





## 二、Git Tag 最佳实践

### 1. 使用语义版本控制
遵循 [语义版本控制规范](https://semver.org/)，使用 `MAJOR.MINOR.PATCH` 的形式来命名版本号：
- **MAJOR** 当你做出不兼容的 API 修改时。
- **MINOR** 当你添加功能到公共 API 时。
- **PATCH** 当你做出向后兼容的 bug 修复时。

例如：
```bash
git tag v1.0.0
```

### 2. 创建带有注释的标签
使用带有注释的标签，这样可以包含创建者的名称、电子邮件、日期和标签消息。这是创建标签的标准方式：
```bash
git tag -a v1.0.0 -m "Initial public release"
```

### 3. 签名标签
对于重要的版本，考虑使用 GPG 签名的标签来增加安全性：
```bash
git tag -s v1.0.0 -m "Initial public release"
```

### 4. 使用有意义的消息
在创建标签时，提供有意义的消息来描述版本或里程碑的重要变化。这有助于其他人理解每个版本的意义。

### 5. 创建标签时指向正确的提交
确保在创建标签时指向正确的提交。通常，这应该是最后一次提交，即最新的一次更改。
```bash
git tag v1.0.0
```

### 6. 保持标签的顺序
尽量不要在已经存在的标签之间插入新的标签。这会导致混乱，并可能使其他用户难以追踪版本历史。

### 7. 避免重命名或删除已发布的标签
一旦发布了标签，避免重命名或删除它。这可能导致其他用户的仓库出现混乱。

### 8. 推送标签到远程仓库
将标签推送到远程仓库，让团队成员和其他贡献者知道新版本的发布。
```bash
git push origin v1.0.0
```

### 9. 定期清理本地标签
定期清理不再需要的本地标签，保持仓库整洁。
```bash
git tag -d v0.1.0
```

### 10. 使用标签进行版本控制
在文档和发布说明中引用特定的标签，帮助用户和贡献者追踪版本历史。

### 11. 创建里程碑标签
除了版本标签之外，还可以创建里程碑标签来标记重要的项目阶段或里程碑。

### 12. 使用标签进行发布
在每次发布新版本时，创建一个带有版本号的标签，并将其推送到远程仓库。

### 13. 遵循一致的命名约定
保持标签命名的一致性，这有助于简化标签管理和查找。

### 14. 为重要的版本创建标签
只对重要的版本创建标签，避免过度使用标签，否则会使标签列表变得杂乱无章。

### 15. 保持标签列表的可读性
使用 `git tag` 命令列出所有标签，并定期整理和排序这些标签，使其易于阅读。

### 16. 避免使用临时标签
避免创建临时性的标签，除非你打算最终删除它们。临时标签可能会导致混淆。

### 17. 使用标签进行自动化
考虑将标签集成到自动化工作流程中，例如 CI/CD 流程，以自动触发部署或测试。

### 18. 给以前的提交打tag

这个操作一般不建议，因为需要保持tag的顺序

``````
git tag <tag-name> <commit-hash>
``````





