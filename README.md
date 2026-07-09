# Vue To‑Do Starter

一个面向新手的 Vue + Vite 待办事项示例，功能：添加、完成、编辑、删除，并使用 localStorage 保存数据。

## 运行

1. 安装依赖：

```bash
npm install
```

2. 启动开发服务器：

```bash
npm run dev
```

3. 打包：

```bash
npm run build
```

4. 预览构建：

```bash
npm run preview
```

## 开发者提示

- 第一次运行后在浏览器打开 `http://localhost:5173`（Vite 默认为 5173）。
- 本项目使用 Vue 3 `<script setup>`，如果你刚接触 Vue，可把逻辑逐步拆解来理解。

## Git & GitHub 建议流程（新手版）

1. 初始化仓库：

```bash
git init
git add .
git commit -m "feat: init vue todo starter"
```

2. 新建远程仓库并推送：

```bash
git branch -M main
git remote add origin <your-repo-url>
git push -u origin main
```

3. 如果想用分支创建功能：

```bash
git switch -c feat/add-filter
# 做改动
git add .
git commit -m "feat: add filter by status"
git push -u origin feat/add-filter
```

## 想法与扩展（练手）

- 添加按“全部/未完成/已完成”筛选；
- 添加任务优先级与排序；
- 持久化到后端（做一个简单的 REST API）；
- 加入单元测试（Vitest）并用 GitHub Actions 做 CI。
