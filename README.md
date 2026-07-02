# DeepKLT-TRD

第三方开源软件的原样转存备份仓，为 DeepKLT 主项目提供依赖兜底。

## 为什么有这个仓库

DeepKLT 依赖若干第三方开源工具（播放器、在线音源 CLI 等）。这些工具大多托管在公网（npm / GitHub），存在**删库 / 下架 / 断网 / 版本漂移**等风险。一旦上游不可用，主项目的构建与运行会断链。

本仓库把这些**刚需依赖原样转存**一份，作为极端情况下的安装兜底，确保任何时候都能把环境重建起来。

## 原则

1. **不修改源码**——所有内容与上游保持一致（含版本）。
2. **遵循原始协议**——保留每个软件的原始 LICENSE（及 NOTICE），版权归原作者所有。
3. **只备份、不维护**——不接 issue、不改 bug，更新只跟随上游版本。

## 备份清单

| 软件 | 用途 | 协议 | 上游 | 本仓位置 | 安装方式 |
|---|---|---|---|---|---|
| mpv 0.41.0 | 音频播放后端（DeepKLT 音频 MCP 依赖） | LGPL-2.1+ | https://github.com/mpv-player/mpv | `src/mpv-0.41.0.tar.gz` | `dnf install mpv`（推荐，主环境）；上游失效时解压本仓 tarball 自行编译 |
| @music163/ncm-cli | 网易云音乐在线播放 CLI | MIT | https://www.npmjs.com/package/@music163/ncm-cli | `src/ncm-cli/`（待存） | `npm install -g @music163/ncm-cli`（需 Node.js ≥18）；上游失效时从本仓 tgz 安装 |
| NetEase/skills | ncm-cli 的 AI Agent 技能定义 | Apache-2.0 | https://github.com/NetEase/skills | `src/netease-skills/`（待存） | `npx skills add` 或 `git clone` 本仓副本 |

## 目录结构

```
DeepKLT-TRD/
├── README.md
└── src/
    ├── mpv-0.41.0.tar.gz      # 已存
    ├── ncm-cli/               # 待存（npm 包源码 + tgz）
    └── netease-skills/        # 待存（git 仓库镜像）
```

每个子目录**必须自带上游的 LICENSE（及 NOTICE）文件**，备份时连同一起复制，不得删改。

## 极端情况下的安装

优先用上表"安装方式"列的官方命令。仅当官方渠道失效时：

- **tarball**（如 mpv）：`tar xf src/xxx.tar.gz` → 按上游 `INSTALL` / 文档编译安装
- **npm 包**（如 ncm-cli）：`npm install -g src/ncm-cli/<pkg>.tgz`
- **git 仓库**（如 skills）：`git clone <本仓> src/netease-skills && cd src/netease-skills`

## 版权与法律

本仓库是第三方开源软件的**原样转存（mirror）**，行使的是各开源协议（MIT / Apache-2.0 / LGPL 等）明确赋予的再分发权利。

- 所有软件保持源码原样，不做任何修改，版权归原作者所有。
- 每个软件保留其原始 LICENSE（及 NOTICE）——这是相应协议的强制义务。
- 本仓库不主张对第三方代码的任何权利，也不代表与原作者或其商标有任何关联或背书。
- 商标（如"网易云音乐"）归各自所有者。

如某项备份的 LICENSE 缺失、标注有误，或有版权疑虑，请开 issue 指出，会立即补齐或移除。

> 本 README 非法律意见；商业化或大规模分发前建议咨询专业律师。
