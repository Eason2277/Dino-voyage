# Dinosaur Science App — 项目总览

本项目在现有的 Next.js 全栈架构上实现一个恐龙科普应用。文档旨在帮助未来的开发者与 AI 阅读器快速理解项目结构、技术栈、设计决策以及后续扩展点。

## 1. 概要
- 项目名：appz
- 目标：基于现有的 Next.js 全栈架构实现一个面向大众的恐龙科普应用，包含知识科普、交互题、图文展示等功能。
- 架构风格：前后端同构的 Next.js 应用（App Router 风格），使用 TypeScript&Tailwind CSS，采用静态/服务端混合渲染策略。

## 2. 技术栈
- 前端/服务端框架：Next.js (16.2.2) + React (19.2.4)
- 语言与类型：TypeScript
- 样式：Tailwind CSS
- 质量保障：ESLint（eslint-config-next）、tailwindcss，@types/* 作为开发依赖
- 构建/运行：npm run dev / npm run build / npm run start

注：当前仓库的依赖中未看到 explicit 的数据库驱动或测试框架，后续可结合需要引入数据库和端到端测试工具。

## 3. 架构概览
- 客户端/服务端：基于 Next.js App Router 的单体应用，前端页面和 API 路由均在同一个代码库内。
- 路由与入口：主页入口通常在 app/page.tsx，其他路由遵循 App Router 的约定（如 app/dinosaurs/page.tsx、app/quiz/page.tsx 等，具体路径需以实际代码为准）。
- 数据与内容：初步实现通常使用本地数据源（JSON/静态文件）或简单 API 层暴露数据，后续可接入数据库或远端 API。
- 安全与部署：官方建议通过 Vercel 等平台进行部署，Next.js 与 Vercel 集成良好。

## 4. 目录结构与关键入口（基于当前仓库的典型约定，具体实现请以实际代码为准）
- app/：Next.js App Router 入口目录，包含路由、服务端组件、客户端组件。
- app/page.tsx：站点主页入口。 
- app/api/：若存在，会包含 API 路由（如 dinosaurs、quiz 等资源），提供前端数据获取能力。
- app/styles/，或 app/globals.css：全局样式（Tailwind 引导样式）。
- components/：可复用组件。
- data/：若使用本地数据源，可能存放 JSON 数据文件。
- tests/：若存在测试，放在此目录（若暂无，后续可添加）。

> 说明：当前文档基于 README 与 tsconfig、package.json 的信息推断架构要点。实际代码结构以仓库实际目录为准，请以文件树为准后续补充完善。

## 5. 数据模型与 API 初版契约（建议草案）
- Dinosaur: { id, name, era, description, image, facts: string[] }
- Fact: { id, dinosaurId, text }
- QuizQuestion: { id, prompt, options: string[], answerIndex }
- UserProgress: { userId, visitedDinosaurs: string[], quizScores: number[] }

- API（初版草案，具体实现以实际 API 路由为准）
  - GET /api/dinosaurs -> Dinosaur[]
  - GET /api/dinosaurs/:id -> Dinosaur
  - GET /api/quiz -> QuizQuestion[]
  - POST /api/quiz/submit -> { score, answers }
  - GET /api/progress/:userId -> UserProgress

## 6. 本地开发与运行
- 安装依赖：
  - 你应具有 Node.js 环境，推荐版本与项目对齐（见 package.json 的依赖版本）。
- 启动开发服务器：
  - npm run dev
  - 浏览器访问 http://localhost:3000
- 构建与部署：
  - npm run build
  - npm run start

## 7. 部署考量
- 官方推荐在 Vercel 上部署，Next.js 与 Vercel 的整合较完善，部署流程简单且高效。
- 如需自建服务器，请确保 Node.js 版本、环境变量和数据库（若接入）的配置在生产环境中正确传递。

## 8. 对 AI 的快速阅读要点（读者指南）
- 关注要点：app/page.tsx 入口、app/api 目录下的数据端点、data/数据源结构、tailwind 配置、tsconfig 的路径别名。
- 关注数据契约与 API 合同（GET /api/dinosaurs、GET /api/quiz 等），AI 可以据此生成数据流图、接口文档、测试用例。
- 识别未实现的领域以便规划扩展：数据库接入、用户认证、国际化、无障碍访问等。
- 审核代码风格与约定：TypeScript、React 组件分层、服务器组件与客户端组件的适用场景、Tailwind 的样式组织。

## 9. 未来改进方向
- 增加正式的数据库层（如 SQLite/PostgreSQL）及 ORM 方案，替代静态数据源。
- 增加端到端测试（Playwright / Cypress）以及单元测试（Jest/Vitest）。
- 完善 API 文档与类型定义，生成 API 参考文档（如 OpenAPI/Swagger 风格草案）。
- 引入 GitHub Actions 等 CI/CD 流程，自动化测试与部署。

## 10. 变更历史与版本计划
- 本文件用于帮助新成员快速理解代码库与开发方向。
- 如需对某部分进行变更，请在后续迭代中补充相应章节并更新此文档。

---

文档生成时间: 自动化补充/维护中，请在后续迭代中持续更新。
- 关键入口点（基于当前代码）
  - app/layout.tsx：定义全局布局、字体（Geist）和全局样式引入，作为应用的根布局入口。
  - app/page.tsx：主页入口组件，当前示例展示一个简单的欢迎页，演示 App Router 的入口点在此文件。
  - app/globals.css：全局样式，包含 Tailwind 的引入和颜色/字体变量定义，便于全局一致的 UI 风格。
  - 其他资源：鉴于该仓库尚未包含 next.config.js 的显式文件，下一步若有自定义构建配置，请在 docs 中补充具体项。
