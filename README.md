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
- 站点为骨架阶段,页面内容陆续从框架各包 `Documentation/` 整理发布

MIT License © 2026 Runestone Yuumix