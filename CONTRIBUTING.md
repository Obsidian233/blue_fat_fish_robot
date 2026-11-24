# 协作规范（Contributing）

本仓库是 ROBOMINI 2027 / 机甲杯机器人对抗赛的团队仓库，按 **机械 / 电控 / 算法** 三个方向协作。
本文件约定 Git 工作流、目录放置、大文件策略与安全红线。**开始开发前请先读完，尤其是第 5、6 节。**

最后更新：2026-11-24

---

## 1. 首次配置

### 1.1 克隆仓库

```bash
git clone https://github.com/crion99/blue_fat_fish_robot.git
cd blue_fat_fish_robot
```

> 本仓库为**公开仓库**：提交内容任何人都能看到，请严格遵守第 6 节。

### 1.2 配置身份

```bash
git config --global user.name "你的名字或 GitHub 昵称"
git config --global user.email "你的 GitHub noreply 邮箱"
```

建议使用 GitHub 提供的 `xxxxx+用户名@users.noreply.github.com`，避免在公开仓库历史中暴露真实邮箱。

### 1.3 换行符

换行由仓库内的 `.gitattributes` 强制为 LF，不需要手动修改行尾，也不需要额外配置 `core.autocrlf`（`.gitattributes` 的 `eol=lf` 优先生效）。

- 编辑器如提示行尾不一致，统一选择 LF。
- `.bat` / `.cmd` / `.ps1` 已在 `.gitattributes` 中单独保留 CRLF，请勿手改。

### 1.4 （可选）Git LFS

需要把较大 CAD / 视频提交进仓库时使用（见第 5 节）：

```bash
git lfs install
git lfs track "media/demo/*.mp4"
git lfs track "mechanical/**/*.SLDPRT"
git add .gitattributes
```

`git lfs track` 会自动把规则写入 `.gitattributes`，**不要手写 `filter=lfs`**，以免未安装 LFS 的成员无法正常检出。

---

## 2. 分支约定

- `main` 始终保持可读、可用，建议在 GitHub `Settings → Branches` 为 `main` 开启保护：禁止直接 push、要求 PR。
- 开发一律在功能分支进行：`<方向>/<任务>`，方向取值 `mech` / `elec` / `algo` / `docs` / `repo` / `tests`，修复用 `fix/<任务>`。
- 示例：
  - `mech/ore-car-chassis`
  - `elec/remote-unpack`
  - `algo/lamp-detection`
  - `fix/serial-timeout`
- 合并后删除分支，保持分支列表干净。

---

## 3. 提交信息规范

采用简版 Conventional Commits：

```text
<type>(<scope>): <简短描述>
```

- `type`：`feat` 新功能 / `fix` 修复 / `docs` 文档 / `test` 测试 / `chore` 杂务 / `refactor` 重构 / `build` 构建
- `scope`：`mech` / `elec` / `algo` / `docs` / `repo` / `tests`

示例：

```text
feat(elec): 解析遥控器 SBUS 数据帧
fix(algo): 修正相机内参标定文件名
docs(interfaces): 补充云台角度命令协议
```

要求：一次提交只做一件事；标题不超过 50 字符；必要时在正文说明原因和验证方式。
不要提交 `update`、`修改`、`1` 这类无信息量的 message。

---

## 4. 目录与文件放置

| 内容 | 位置 |
| --- | --- |
| 赛事规则、总体方案、接口约定、会议纪要 | `docs/rules/`、`docs/architecture/`、`docs/interfaces/`、`docs/meetings/` |
| 机械 CAD 源文件 / 导出图纸 | 建议 `mechanical/cad/`、`mechanical/drawings/`（按需创建） |
| 电控固件工程 | 建议 `electrical/firmware/<工程名>/` |
| 算法源码与配置 | 建议 `algorithm/src/`、`algorithm/configs/` |
| 测试方案、日志与数据 | `tests/`，按 `YYYY-MM-DD_对象` 命名 |
| 照片、演示视频、截图 | `media/photos/`、`media/demo/`、`media/screenshots/` |
| 中期考核提交材料 | `submission/` |

- 接口、坐标系、通信协议、关键参数变更，必须同步到 `docs/interfaces/` 并在 PR 中说明。
- 规则原文与团队方案分开保存，并记录版本号和来源。
- 不要把个人电脑路径、临时导出文件、编译产物放进仓库（`.gitignore` 已覆盖常见项）。

---

## 5. 大文件与媒体策略

GitHub 对单个文件有 **100MB 硬限制**，超过会被拒绝推送；仓库长期过大也会拖慢所有人的克隆。

- **单文件 < 20MB**：可直接提交。
- **20–100MB**：优先压缩；确需入库则使用 Git LFS，并确保全体成员已 `git lfs install`。
- **> 100MB**：**禁止提交**。放到网盘 / 群文件，并把可访问链接记录在 `media/README.md` 或对应文档中。
- 演示视频只保留 30–60 秒的精简版本，原始录像不入库。
- 公开仓库中**不要写私有网盘的提取码**，放到团队群公告。

提交前检查：

```bash
git status
git diff --cached --stat
```

---

## 6. 隐私与安全红线（公开仓库）

严禁提交：

- 密码、Token、API Key、私钥、证书、账号密码截图；
- 学号、身份证号、手机号、住址等个人隐私；
- 未获得授权的他人照片、视频、第三方资料；
- 内网地址、服务器配置、门禁/设备凭据；
- 赛事官方明确不允许公开的规则原文或内部通知。

`.env`、`*.pem`、`*.key`、`secrets.*`、`credentials*` 等已在 `.gitignore` 中忽略。
**如果已经误提交**：立即轮换相关凭据，通知组长，不要只删文件了事——历史记录仍可被查看，需要用 `git filter-repo` 清理历史并强推（操作前先在群里同步）。

---

## 7. 同步与冲突

- 每天开始工作前先同步：`git pull`（或 `git pull --rebase`，保持历史线性）。
- 冲突标记（`<<<<<<<`、`=======`、`>>>>>>>`）绝不允许进入仓库。
- CAD / 视频等二进制文件冲突无法手工合并：先沟通以哪一份为准，删除另一份后重新提交。
- 长期分支定期合并 `main`，避免最后集中冲突。

---

## 8. 提交前自检清单

- [ ] 只包含本次相关的文件（`git status` 检查）
- [ ] 没有构建产物、临时文件、>20MB 大文件
- [ ] 没有密码 / Token / 个人信息 / 未授权资料
- [ ] 接口或协议变更已同步到 `docs/interfaces/`
- [ ] 代码 / 模型 / 图纸能被他人按 README 或 PR 描述复现
- [ ] commit message 符合第 3 节规范

---

## 9. Git 常用命令速查

| 命令 | 用途 |
| --- | --- |
| `git status` | 查看工作区改动状态 |
| `git diff` | 查看未暂存的具体改动 |
| `git add <文件>` | 将文件加入暂存区 |
| `git commit -m "feat(elec): ..."` | 提交 |
| `git log --oneline --graph` | 查看提交历史 |
| `git switch -c elec/xxx` | 新建并切换到功能分支 |
| `git switch main` | 切换回 main |
| `git branch -a` | 查看本地与远端分支 |
| `git pull` | 拉取远端更新 |
| `git push -u origin elec/xxx` | 推送分支并建立跟踪 |
| `git merge main` | 把 main 合并进当前分支 |
| `git stash` / `git stash pop` | 临时保存 / 恢复未提交改动 |
| `git restore <文件>` | 放弃工作区改动 |
| `git revert <提交>` | 生成一个反向提交（已推送的历史用这个） |
| `git remote -v` | 查看远端地址 |

更完整的 Git 学习资料可参考 [Pro Git（中文版）](https://git-scm.com/book/zh/v2)。
