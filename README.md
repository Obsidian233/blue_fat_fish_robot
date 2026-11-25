# Blue Fat Fish Robot

ROBOMINI 2027 机器人对抗赛（机甲杯）团队仓库，按 **机械、电控、算法** 三个方向组织，统一保存接口约定、测试记录、过程媒体与提交材料。

> ⚠️ 本仓库是**公开仓库**：<https://github.com/crion99/blue_fat_fish_robot>。
> 请勿提交密码、Token、密钥、个人隐私或未经授权的第三方资料，具体要求见 [CONTRIBUTING.md](CONTRIBUTING.md)。

## 仓库状态

- [x] 目录骨架、README 与协作规范（2026-11-24）
- [x] 上传前配置：`.gitignore`、`.gitattributes`、`.editorconfig`、PR 模板
- [ ] 机械：兑矿车 / 固定发射架
- [ ] 电控：遥控解包、串口、动力控制、远程演示
- [ ] 算法：灯效识别、相机、位姿解算、仿真击打
- [ ] 中期考核材料汇总到 `submission/`

## 快速开始

```bash
git clone https://github.com/crion99/blue_fat_fish_robot.git
cd blue_fat_fish_robot
git switch -c <方向>/<任务>        # 例如 elec/remote-unpack
```

开发前请阅读 [CONTRIBUTING.md](CONTRIBUTING.md)：分支与提交规范、大文件策略、隐私红线、Git 命令速查。

## 目录结构

```text
.
├── docs/                   # 规则、需求、总体方案、接口约定与会议记录
│   ├── rules/              # 赛事规则、制作规范、中期考核要求
│   ├── architecture/       # 整车方案、系统框图、模块职责
│   ├── interfaces/         # 机械/电控/算法接口、坐标系、通信协议
│   └── meetings/           # 会议纪要（按日期归档）
├── mechanical/             # 机械：兑矿车、固定发射架、CAD 与加工图纸
├── electrical/             # 电控：遥控解包、串口、舵机/电机控制与整车联调
├── algorithm/              # 算法：相机、灯效识别、位姿解算与仿真击打
├── tests/                  # 跨方向测试方案、测试记录与数据
├── media/                  # 过程照片、演示视频与截图（photos/、demo/、screenshots/）
├── submission/             # 中期考核最终提交材料
├── .github/                # Pull Request 模板
├── .editorconfig           # 编辑器编码与缩进约定
├── .gitattributes          # 换行与二进制文件处理
├── .gitignore              # 构建产物、临时文件与敏感配置
└── CONTRIBUTING.md         # 团队协作规范
```

## 中期考核目标

- [ ] **机械**：兑矿车（底盘、资源拾取/存储、资源兑换）完成可加工装配；固定发射架为选交项。
- [ ] **电控**：遥控器对频与协议解包、串口通信、角度控制、速度控制、远程控制演示、Git 管理。
- [ ] **算法**：识别能量机关待激活/已激活灯效、实时相机画面、靶位姿与瞄准转角解算、仿真环境分阶段击打。
- [ ] 整理三个方向的展示视频、技术文档、代码/模型文件及仓库地址。

## 协作约定

1. 每个方向在自己的目录内开发，不要把临时文件、编译产物和个人环境配置提交进仓库。
2. 重要接口、坐标系、通信协议和参数变更，及时同步到 `docs/interfaces/`。
3. 使用功能分支 + Pull Request 合并到 `main`，提交信息遵循 [CONTRIBUTING.md](CONTRIBUTING.md) 第 3 节。
4. CAD 源文件、导出图纸、固件源码、算法源码和演示材料分开放置。
5. 大文件遵循 [CONTRIBUTING.md](CONTRIBUTING.md) 第 5 节：单文件超过 100MB 禁止入库，演示视频只放精简版。
6. 最终交付前检查 `submission/README.md` 中的清单。

## 仓库配置

| 文件 | 作用 |
| --- | --- |
| `.gitignore` | 忽略构建产物、临时文件、个人配置与敏感文件 |
| `.gitattributes` | 统一换行为 LF，标记 CAD / 媒体 / Office 等二进制文件 |
| `.editorconfig` | 统一编码（UTF-8 无 BOM）与缩进 |
| `CONTRIBUTING.md` | 分支、提交信息、大文件、安全红线与 Git 速查 |
| `.github/PULL_REQUEST_TEMPLATE.md` | PR 自检模板 |

## 时间节点

根据当前提供的考核通知，中期考核材料提交窗口为 **2026-11-16 00:00 至 2026-12-20 23:59**。请以赛事官方通知为准。
