# Blog

[![GitHub Pages](https://img.shields.io/badge/Website-GitHub%20Pages-blue?style=flat-square&logo=github)](https://scotlandorange.github.io/Blog/)

记录技术开发文档

## 📖 网站访问

**在线访问**: [https://scotlandorange.github.io/Blog/](https://scotlandorange.github.io/Blog/)

## 简介

这是一个基于 Sphinx 的技术博客，用于记录和分享技术开发文档。文档会自动构建并部署到 GitHub Pages。

## 文档结构

```
docs/
├── source/          # 源文档目录
│   ├── conf.py     # Sphinx 配置文件
│   ├── index.rst   # 主页
│   └── *.rst       # 其他文档页面
└── build/          # 构建输出目录（自动生成）
```

## 本地开发

### 安装依赖

```bash
pip install -r requirements.txt
```

### 构建文档

使用 Makefile:
```bash
make html
```

或直接使用 sphinx-build:
```bash
sphinx-build -b html docs/source docs/build/html
```

### 查看文档

构建完成后，在浏览器中打开 `docs/build/html/index.html`

## 添加新文档

1. 在 `docs/source/` 目录下创建新的 `.rst` 文件
2. 在 `docs/source/index.rst` 中的 `toctree` 指令里添加新文件的引用
3. 提交更改到仓库

## CI/CD

本项目使用 GitHub Actions 自动构建和部署：

- **触发条件**: 当代码推送到 `main` 分支时
- **构建**: 自动使用 Sphinx 构建 HTML 文档
- **部署**: 自动部署到 GitHub Pages

要启用 GitHub Pages:
1. 进入仓库的 Settings -> Pages
2. 在 "Source" 部分选择 "GitHub Actions"

## 许可证

MIT License
