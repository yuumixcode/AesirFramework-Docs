# AesirFramework-Docs

**AesirFramework 官方文档站点** —— Aesir Architecture / Aesir Modules 的公开文档仓库。

- 站点地址:https://yuumixcode.github.io/AesirFramework-Docs/
- 框架源码:https://github.com/yuumixcode/AesirFramework

## 技术栈

- [Zensical](https://zensical.org/)(Rust 静态站生成器,Material for MkDocs 继任者)
- 内容:Markdown(`docs/`),模板:MiniJinja
- 部署:GitHub Pages(GitHub Actions,见 `.github/workflows/deploy.yml`)

## 本地开发

```bash
pip install zensical
zensical serve        # 本地预览,默认 http://localhost:8000
zensical build        # 构建到 site/
zensical build --strict  # 严格模式(CI 用)
```

## 目录结构

```
docs/
├── index.md                # 落地页
├── architecture/           # Aesir Architecture 文档
├── modules/                # Aesir Modules 文档
├── faq.md / support.md
└── stylesheets/extra.css   # 站点自定义样式
```

## 文档维护约定

- 提交信息风格:`docs: 中文单行主题`
- 内容语言:中文(站点语言配置 `zh`)
- 内容来源:从框架主仓库各包 `Documentation/` 与包 README 核查整理,版本口径与主仓库 package.json 保持一致(当前 0.17.0)
- 事实核查基线:安装 URL、角色矩阵、三档渐进、API 名称均以包内 README 为准;包内文档更新后同步本站

MIT License © 2026 Runestone Yuumix