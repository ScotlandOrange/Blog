# GitHub Pages 设置指南 / GitHub Pages Setup Guide

## 问题 / Problem

当访问 https://scotlandorange.github.io/Blog/ 时显示：
> "There isn't a GitHub Pages site here."

When visiting https://scotlandorange.github.io/Blog/, it shows:
> "There isn't a GitHub Pages site here."

## 原因 / Root Cause

GitHub Pages 功能未在仓库设置中启用。虽然 GitHub Actions 工作流已正确配置，但由于 Pages 功能未启用，部署会失败。

GitHub Pages feature is not enabled in the repository settings. Although the GitHub Actions workflow is correctly configured, deployment fails because the Pages feature is disabled.

## 解决方案 / Solution

### 步骤 1: 启用 GitHub Pages / Step 1: Enable GitHub Pages

1. 访问仓库设置页面 / Visit repository settings page:
   ```
   https://github.com/ScotlandOrange/Blog/settings/pages
   ```

2. 在 "Build and deployment" 部分 / In the "Build and deployment" section:
   - **Source** (来源): 选择 "GitHub Actions" / Select "GitHub Actions"
   - 这将允许 GitHub Actions 工作流自动部署网站 / This will allow the GitHub Actions workflow to automatically deploy the site

### 步骤 2: 触发部署 / Step 2: Trigger Deployment

启用 GitHub Pages 后，有两种方式触发部署 / After enabling GitHub Pages, there are two ways to trigger deployment:

**选项 A: 推送到 master 分支 / Option A: Push to master branch**
```bash
# 对 master 分支进行任何更改后推送
# Make any changes to master branch and push
git push origin master
```

**选项 B: 手动触发工作流 / Option B: Manually trigger workflow**
1. 访问 / Visit: https://github.com/ScotlandOrange/Blog/actions
2. 选择 "Build and Deploy Sphinx Documentation" 工作流 / Select "Build and Deploy Sphinx Documentation" workflow
3. 点击 "Run workflow" 按钮 / Click "Run workflow" button
4. 选择 "master" 分支 / Select "master" branch
5. 点击绿色的 "Run workflow" 按钮 / Click green "Run workflow" button

### 步骤 3: 验证部署 / Step 3: Verify Deployment

1. 等待工作流完成（通常需要 1-2 分钟）/ Wait for workflow to complete (usually takes 1-2 minutes)
2. 访问 / Visit: https://scotlandorange.github.io/Blog/
3. 您应该能看到 Sphinx 文档网站 / You should see the Sphinx documentation site

## 工作流说明 / Workflow Description

本仓库已配置 GitHub Actions 工作流 (`.github/workflows/sphinx-build.yml`)，它会：

This repository has a configured GitHub Actions workflow (`.github/workflows/sphinx-build.yml`) that will:

1. ✅ 自动安装依赖 / Automatically install dependencies
2. ✅ 使用 Sphinx 构建 HTML 文档 / Build HTML documentation using Sphinx
3. ✅ 创建 `.nojekyll` 文件（确保 GitHub Pages 正确显示）/ Create `.nojekyll` file (ensures GitHub Pages displays correctly)
4. ✅ 上传构建产物 / Upload build artifact
5. ✅ 部署到 GitHub Pages / Deploy to GitHub Pages

**触发条件 / Trigger Conditions:**
- 推送到 `master` 分支时自动运行 / Automatically runs on push to `master` branch
- 可以手动触发 / Can be manually triggered
- Pull Request 时仅构建不部署（用于测试）/ Only builds on Pull Request (for testing, no deployment)

## 故障排查 / Troubleshooting

### 问题: 工作流失败，显示 "Not Found" 错误
### Issue: Workflow fails with "Not Found" error

**症状 / Symptom:**
```
Error: Failed to create deployment (status: 404)
Ensure GitHub Pages has been enabled
```

**解决方案 / Solution:**
确保已按照上述步骤 1 启用 GitHub Pages 并选择 "GitHub Actions" 作为来源。

Make sure you have enabled GitHub Pages following Step 1 above and selected "GitHub Actions" as the source.

### 问题: 网站显示但样式丢失
### Issue: Site displays but styling is missing

**症状 / Symptom:**
网站显示纯文本，无 CSS 样式 / Site shows plain text without CSS styling

**解决方案 / Solution:**
检查 `.nojekyll` 文件是否存在。本项目的 Sphinx 配置（`docs/source/conf.py`）已包含 `sphinx.ext.githubpages` 扩展，会自动创建此文件。

Check if `.nojekyll` file exists. This project's Sphinx configuration (`docs/source/conf.py`) includes the `sphinx.ext.githubpages` extension, which automatically creates this file.

### 问题: 更改未显示在网站上
### Issue: Changes not showing on site

**解决方案 / Solution:**
1. 确认更改已推送到 `master` 分支 / Confirm changes are pushed to `master` branch
2. 检查 GitHub Actions 工作流是否成功完成 / Check if GitHub Actions workflow completed successfully
3. 等待几分钟后刷新浏览器（可能有缓存）/ Wait a few minutes and refresh browser (may be cached)
4. 尝试硬刷新: Ctrl+Shift+R (Windows/Linux) 或 Cmd+Shift+R (Mac) / Try hard refresh: Ctrl+Shift+R (Windows/Linux) or Cmd+Shift+R (Mac)

## 本地开发 / Local Development

如果您想在本地预览文档 / If you want to preview documentation locally:

```bash
# 安装依赖 / Install dependencies
pip install -r requirements.txt

# 构建文档 / Build documentation
make html

# 查看构建结果 / View built documentation
# 在浏览器中打开 / Open in browser: docs/build/html/index.html
```

## 相关链接 / Related Links

- [GitHub Pages 官方文档](https://docs.github.com/en/pages)
- [GitHub Actions for Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site#publishing-with-a-custom-github-actions-workflow)
- [Sphinx 文档](https://www.sphinx-doc.org/)
- [sphinx-rtd-theme](https://sphinx-rtd-theme.readthedocs.io/)
