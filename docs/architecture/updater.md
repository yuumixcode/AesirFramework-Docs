# 包内更新器

Aesir Architecture 内置面向 **unitypackage 安装方式**的包内更新器:无需重新下载导入,编辑器内一键完成版本检测、备份与更新。

!!! warning "管辖范围"
    更新器只管辖 `Assets/Runestone/` 下的代码导入副本(unitypackage 安装)。**Git URL(UPM)安装的副本不在管辖内**,请用 Package Manager 更新;**开发仓库(存在 `.git`)切勿点更新** —— Release 内容会覆盖本地源码(窗口已内置警告)。

## 使用

菜单 `Tools → Aesir → Check for Updates` 打开更新窗口:

1. 扫描 `Assets/Runestone/*/package.json` 识别本地安装的 Aesir 包与版本
2. 检测最新 Release 版本
3. 点击更新,自动完成全流程(无需手动干预)

## 更新流程

```
检测新版本 → 下载 unitypackage → 自动备份 → 差集清理残留 → 静默导入 → 登记安装清单
```

| 步骤 | 行为 |
|------|------|
| 下载 | 从 GitHub Release 拉取 `<包目录名>-v<版本>.unitypackage` |
| 备份 | 更新前自动备份 `Assets/Runestone` 到项目根 `.aesir-backup/`(时间戳前缀命名,保留最近 3 份) |
| 残留清理 | 按「上次安装清单 − 新版清单」精确差集删除(仅限本包目录内;无历史清单则跳过,不误伤用户新增文件) |
| 导入 | `AssetDatabase.ImportPackage` 静默导入 |
| 清单登记 | 逐包合并登记 `.aesir/installed-manifest.json`;更新中途域重载时,已导入包的状态保证正确落盘 |

## 版本检测三级兜底(大陆友好)

版本检测按以下顺序尝试,首个成功即返回:

1. **jsDelivr CDN** —— 四个域名(cdn / testingcf / gcore / fastly,5 秒超时)拉取仓库内 `.github/update-info.json`;大陆连通性好、无限流
2. **GitHub Releases API** —— 未认证 60 次/时/IP(按出口 IP 计数)
3. **`releases/latest` 302 重定向探测** —— 读取 Location 头获得版本号,完全绕开 API 限流

unitypackage 下载始终走 GitHub Release 直链(jsDelivr 不代理 Release 资产)。

!!! note "检测延迟"
    jsDelivr 对分支引用的缓存最长约 12 小时 —— 新发布的版本最长约 12 小时后才经 CDN 被检测到(窗口 HelpBox 已注明)。

## 设计参考

实现参考 QFramework PackageKit(版本记录随包走 + 先删后导),增强点为**自动备份**与**精确差集清理**。

## 继续阅读

- [快速开始](getting-started.md) —— 三种安装方式对比
- [FAQ](../faq.md) —— 更新器常见问题
