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





## 二、Git Tag