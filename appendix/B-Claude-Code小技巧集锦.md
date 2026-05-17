# 附录 B：Claude Code 小技巧集锦

> 书里没讲到的实用小技巧，每个都能帮你节省 5-30 分钟。
> 这些技巧来自社区贡献和日常实战，会持续更新。

---

## 🚀 效率提升技巧

### 技巧 1：用 CLAUDE.md 记住项目上下文

**场景**：每次新会话都要重新解释项目结构，烦不烦？

**解决方案**：在项目根目录创建 `CLAUDE.md`，Claude Code 会自动读取。

```markdown
# CLAUDE.md

## 项目概述
这是一个用 Next.js + TypeScript + Prisma 的电商后台管理系统。

## 常用命令
- 启动开发服务器：`npm run dev`
- 构建：`npm run build`
- 运行测试：`npm test`
- 数据库迁移：`npx prisma migrate dev`

## 代码规范
- 使用 ESLint + Prettier
- 组件用函数式 + Hooks
- 状态管理用 Zustand
- API 请求用 SWR

## 项目结构
- `src/app/` - Next.js App Router 页面
- `src/components/` - 可复用组件
- `src/lib/` - 工具函数和配置
- `prisma/schema.prisma` - 数据模型
```

**效果**：新会话开头说"继续开发"，Claude Code 就知道你在干什么了。

---

### 技巧 2：用 Shift + Tab 切换建议模式

**场景**：Claude Code 给的建议太多，你只想要代码，不要解释。

**解决方案**：按 `Shift + Tab` 在计算建议和代码建议之间切换。

| 模式 | 说明 |
|------|------|
| **计算建议** | Claude Code 解释它在做什么（默认） |
| **代码建议** | 只显示代码块，解释更少 |

**快捷键**：`Shift + Tab` 在两者之间切换。

---

### 技巧 3：用 /cost 查看 Token 消耗

**场景**：生怕用超了，不知道这轮对话花了多少钱。

**解决方案**：输入 `/cost` 查看当前会话的 Token 消耗和费用估算。

```
你：/cost

Claude Code 响应：
Token 消耗：
- 输入：12,345 tokens
- 输出：6,789 tokens
- 总计：19,134 tokens

费用估算（Claude 3.5 Sonnet）：
- 输入：$0.037
- 输出：$0.102
- 总计：$0.139
```

**技巧**：如果 Token 快用完（200K 上下文限制），用 `/clear` 开启新会话。

---

### 技巧 4：用 /compact 压缩上下文

**场景**：会话太长，Token 快满了，但还没做完。

**解决方案**：输入 `/compact`，Claude Code 会总结之前的对话，释放上下文空间。

```
你：/compact

Claude Code：[总结之前的对话]
已压缩上下文，释放了约 50K tokens。
你可以继续工作了。
```

**注意**：压缩后会丢失一些细节，但在大项目里很有用。

---

### 技巧 5：用 Escape 中断生成

**场景**：Claude Code 开始胡说八道，或者你在测试指令，发现方向错了。

**解决方案**：按 `Escape` 立即中断生成。

**技巧**：
- 中断后可以继续对话，Claude Code 会基于已生成的内容继续
- 如果想完全重来，输入 `/clear` 开启新会话

---

## 🎯 指令编写技巧

### 技巧 6：用"角色扮演"提高代码质量

**场景**：生成的代码不符合你的代码风格或质量标准。

**解决方案**：在指令开头指定"角色"，让 Claude Code 按特定风格写代码。

```
你：
作为一个有 10 年经验的高级 TypeScript 开发者，帮我重构 src/utils/helpers.ts：
- 使用函数式编程范式
- 优先使用组合而非继承
- 添加完整的 JSDoc 注释
- 确保每个函数单一职责
```

**效果**：生成的代码质量明显更高，更符合资深开发者的风格。

---

### 技巧 7：用"分步执行"处理大任务

**场景**：让 Claude Code 做太大的任务，它容易遗漏细节或者跑偏。

**解决方案**：把大任务拆成小步骤，一步步来。

**错误示例**（太笼统）：
```
你：帮我重构整个项目，用上最佳实践。
```

**正确示例**（分步执行）：
```
你：
第一步：分析 src/ 目录下所有文件，找出代码坏味道（过长函数、重复代码、复杂条件判断），列出清单。
我确认后，我们再做第二步。

（Claude Code 列出清单）

你：
第二步：按优先级重构清单里的前 3 个问题，每次重构后告诉我改了什么、为什么这样改。
```

**技巧**：每完成一步，检查一下结果，确认没问题再继续。这样可以及时纠正方向。

---

### 技巧 8：用"示例驱动"生成精确代码

**场景**：用自然语言描述需求，Claude Code 理解有偏差。

**解决方案**：给 1-2 个示例，让 Claude Code 照着写。

```
你：
我要给每个 API 接口添加请求日志。格式如下：

示例 1（GET 请求）：
[2025-05-17 10:23:45] GET /api/users - 200 - 45ms

示例 2（POST 请求）：
[2025-05-17 10:24:12] POST /api/orders - 201 - 123ms - body: { "userId": 123, "amount": 456 }

请给所有 API 接口添加这种格式的日志。
```

**效果**：生成的代码完全符合你的预期，不需要反复修改。

---

### 技巧 9：用"对比表格"做技术选型

**场景**：犹豫用哪个库/框架，让 Claude Code 帮你分析。

**解决方案**：要求用对比表格列出优缺点。

```
你：
我要给项目添加状态管理，纠结用 Zustand 还是 Redux Toolkit。

请做一个对比表格，考虑：
- 学习曲线
- 代码量
- 性能
- TypeScript 支持
- 生态系统
- 适合团队规模（5 人）

然后给我推荐。
```

**效果**：Claude Code 会给出客观的分析，帮你做决策。

---

### 技巧 10：用"反向提问"让 Claude Code 帮你理清需求

**场景**：你自己的需求都没想清楚，Claude Code 生成的代码肯定不对。

**解决方案**：让 Claude Code 先问你问题，搞清楚需求再动手。

```
你：
我想添加一个"权限管理"功能，但还没想清楚具体要怎么做。

请你先问我 5 个问题，帮我理清需求。然后再生成代码。
```

**Claude Code 可能会问**：
1. 权限是基于角色（RBAC）还是基于资源（ABAC）？
2. 权限粒度到哪里？接口级？字段级？
3. 前端是否需要动态渲染（根据用户权限显示/隐藏按钮）？
4. 权限数据存储在哪里？数据库？JWT？Redis？
5. 是否需要权限继承（比如"管理员"自动继承"用户"的权限）？

**效果**：回答完这 5 个问题，你自己都清楚要做什么了，Claude Code 生成的代码也会更精准。

---

## 🔧 调试与排错技巧

### 技巧 11：用"最小复现"定位 Bug

**场景**：代码报错了，但项目太大，不知道哪里出问题。

**解决方案**：让 Claude Code 帮你创建一个最小复现示例。

```
你：
我的代码报这个错：[错误信息]

请你创建一个最小复现示例（单独的文件，不依赖项目其他部分），帮我定位问题。
```

**效果**：把复杂问题简化成 50 行以内的代码，很容易找到根因。

---

### 技巧 12：用"Git Bisect"自动找引入 Bug 的提交

**场景**：代码上周还好好的，这周挂了。不知道哪个提交引入的 Bug。

**解决方案**：让 Claude Code 帮你用 `git bisect` 二分查找。

```
你：
这个 Bug（描述 Bug 现象）是最近引入的，请帮我用 git bisect 找出是哪个提交引入的。

我知道上周还是好的，最早可能是 abc1234 这个提交之后引入的。
```

**Claude Code 会**：
1. 运行 `git bisect start`
2. 标记当前版本有 Bug：`git bisect bad`
3. 标记已知好版本：`git bisect good abc1234`
4. 自动切换到中间提交，让你测试
5. 重复直到找到引入 Bug 的提交

**效果**：从几十个提交里找 Bug，从手动 1 小时降到自动 5 分钟。

---

### 技巧 13：用"日志注入"调试异步代码

**场景**：异步代码执行顺序看不懂，不知道哪里卡住了。

**解决方案**：让 Claude Code 在关键位置注入日志，可视化执行流程。

```
你：
这段异步代码（贴代码）的执行顺序我理解不了。

请在每个 async/await、Promise.then、setTimeout 前后添加日志，格式为：
[时间戳] [函数名] 即将执行...
[时间戳] [函数名] 执行完成

然后我运行一下，把日志发给你分析。
```

**效果**：通过日志时间线，异步执行顺序一目了然。

---

### 技巧 14：用"类型体操"调试 TypeScript 类型错误

**场景**：TypeScript 类型报错，但错误信息看不懂。

**解决方案**：让 Claude Code 帮你"拆类型"，逐个排查。

```
你：
这个 TypeScript 类型错误我看不懂：

[错误信息]

请帮我：
1. 把复杂的类型定义拆成简单的中间类型
2. 用 // @ts-check 逐行检查哪里类型不匹配
3. 给出修复方案（保持类型安全，不要 any）
```

**效果**：TypeScript 类型错误从"看天书"变成"一步步推理"。

---

### 技巧 15：用"快照测试"捕获意外变更

**场景**：重构代码后，不知道有没有改坏什么东西。

**解决方案**：让 Claude Code 帮你添加快照测试（Snapshot Testing）。

```
你：
我准备重构 src/components/UserTable.tsx，请帮我添加快照测试。

要求：
1. 渲染组件，生成 DOM 快照
2. 快照存到 __snapshots__/ 目录
3. 重构后运行测试，如果 DOM 结构变了，测试失败
4. 如果我确认改动是合理的，运行更新快照命令
```

**效果**：重构代码的"安全网"，防止意外破坏现有功能。

---

## 📦 项目配置技巧

### 技巧 16：用"模板项目"快速启动新项目

**场景**：每次新建项目都要从头配置，浪费时间。

**解决方案**：让 Claude Code 帮你创建一个"模板项目"，以后直接复制。

```
你：
帮我创建一个 Next.js + TypeScript + Tailwind + Prisma 的模板项目，要求：
1. 配置好 ESLint + Prettier
2. 配置好 GitHub Actions CI/CD
3. 添加 README.md 说明如何使用和定制
4. 所有可配置项用环境变量或配置文件
5. 推送到 GitHub 作为模板仓库（勾选 Template 选项）

以后新建项目直接 clone 这个模板，5 分钟搞定。
```

**效果**：新项目从"从零开始 2 天"降到"clone 模板 5 分钟"。

---

### 技巧 17：用".env.example"管理环境变量

**场景**：新同事拉代码后，不知道要配置哪些环境变量。

**解决方案**：让 Claude Code 帮你生成 `.env.example` 和启动脚本。

```
你：
我的项目需要很多环境变量（数据库、Redis、第三方 API 等）。

请帮我：
1. 生成 .env.example，每个变量加注释说明用途和默认值
2. 写个脚本 check-env.js，启动时检查必需的环境变量是否都配置了
3. 如果缺少必需变量，给出明确错误提示和文档链接
```

**.env.example 示例**：
```bash
# 数据库
DATABASE_URL=postgresql://user:pass@localhost:5432/mydb

# Redis
REDIS_URL=redis://localhost:6379

# 第三方 API
OPENAI_API_KEY=sk-...  # 从 https://platform.openai.com 获取

# 可选：Sentry 错误监控
SENTRY_DSN=https://...  # 可选，不配置也能运行
```

**效果**：新同事拉代码后，复制 `.env.example` 为 `.env`，按注释填完就能跑。

---

### 技巧 18：用"Git Hooks"自动检查代码质量

**场景**：团队成员提交代码时，有人不跑测试，有人不格式化，代码质量参差不齐。

**解决方案**：让 Claude Code 帮你配置 Git Hooks（用 Husky + lint-staged）。

```
你：
帮我配置 Git Hooks：

1. 安装 husky 和 lint-staged
2. pre-commit 钩子：只对暂存的文件运行 ESLint 和 Prettier
3. commit-msg 钩子：检查提交信息是否符合 Conventional Commits 规范
4. pre-push 钩子：运行单元测试，如果有失败阻止推送

给出完整配置和说明。
```

**效果**：
- 提交代码前自动格式化
- 提交信息不规范不让提交
- 测试没过不让推送
- 团队代码质量自动统一

---

### 技巧 19：用"Docker Compose"一键启动开发环境

**场景**：新同事要装数据库、Redis、消息队列... 配环境就要半天。

**解决方案**：让 Claude Code 帮你写 `docker-compose.dev.yml`，一键启动所有依赖。

```
你：
帮我写 docker-compose.dev.yml，包含：
- PostgreSQL（数据库）
- Redis（缓存）
- RabbitMQ（消息队列）
- MailHog（测试邮件）

要求：
1. 数据持久化（卷挂载）
2. 端口映射不冲突（用 5432、6380、15673、8025）
3. 添加 docker-compose.override.yml 方便本地定制
4. 写 README 说明如何启动和停止
```

**效果**：新同事只需要装 Docker，然后 `docker compose up -d`，5 分钟环境就准备好了。

---

### 技巧 20：用"Makefile"统一常用命令

**场景**：项目有很多脚本（启动、构建、测试、部署...），记不住，文档也散。

**解决方案**：让 Claude Code 帮你写 `Makefile`，统一入口。

```makefile
# Makefile
.PHONY: dev build test deploy

# 启动开发服务器
dev:
\tnpm run dev

# 构建生产版本
build:
\tnpm run build

# 运行测试
test:
\tnpm test

# 部署到生产环境
deploy:
\t@read -p "确认部署到生产环境？(y/N) " confirm && \
\tif [ "$$confirm" = "y" ]; then \
\t\tnpm run deploy; \
\tfi
```

**使用**：
```bash
make dev      # 启动开发服务器
make build    # 构建
make test     # 测试
make deploy   # 部署（会让你确认）
```

**效果**：常用命令一个 `make` 搞定，新同事不用翻文档。

---

## 🎨 代码生成技巧

### 技巧 21：用"测试用例驱动"生成代码

**场景**：先写代码再写测试，容易漏掉边界情况。

**解决方案**：让 Claude Code 先写测试用例，再生成代码。

```
你：
我要实现一个函数：给定一个数组，返回去重后的数组（保持原顺序）。

请按 TDD 流程：
1. 先写测试用例（包含普通情况、边界情况、异常情况）
2. 运行测试，确认失败（红灯）
3. 生成实现代码
4. 运行测试，确认通过（绿灯）
5. 重构（如果有必要）
```

**效果**：生成的代码质量更高，边界情况都考虑到了。

---

### 技巧 22：用"类型定义优先"生成 TypeScript 代码

**场景**：直接让 Claude Code 生成代码，类型定义可能不规范。

**解决方案**：让 Claude Code 先写类型定义（interface/type），再生成实现。

```
你：
我要做一个用户管理系统，请：

1. 先定义 TypeScript 类型（User、CreateUserDTO、UpdateUserDTO、UserRole 等）
2. 定义 API 接口（请求/响应类型）
3. 定义数据库模型（Prisma schema）
4. 根据以上类型定义，生成实现代码

确保类型在整个系统中保持一致。
```

**效果**：类型从头到尾一致，不会出现"这里叫 User，那里叫 UserInfo"的尴尬。

---

### 技巧 23：用"组件库"生成统一风格的前端代码

**场景**：每次让 Claude Code 生成组件，风格不统一（有的用 CSS Modules，有的用 styled-components）。

**解决方案**：让 Claude Code 先创建一个小型组件库，以后再生成组件时引用它。

```
你：
帮我创建一个小型组件库（基于 React + TypeScript + Tailwind）：

基础组件：
- Button（按钮，支持 variant、size、loading）
- Input（输入框，支持前缀、后缀、错误状态）
- Modal（模态框，支持自定义头部和底部）
- Table（表格，支持排序、筛选、分页）

要求：
1. 统一使用 Tailwind 样式
2. 统一的 Props 设计规范
3. 完整的 TypeScript 类型定义
4. 添加 Storybook 文档

以后生成新组件时，优先使用这个组件库的组件。
```

**效果**：所有页面风格统一，新组件开发速度加快（复用基础组件）。

---

### 技巧 24：用"代码模板"生成重复代码

**场景**：Redux 的 reducer、React 的 CRUD 页面... 每次写都差不多，但又要改很多地方。

**解决方案**：让 Claude Code 帮你创建代码生成器（用 Plop.js 或自定义脚本）。

```
你：
我要频繁创建新的 Redux slice（每个功能模块一个）。

请帮我：
1. 用 Plop.js 创建一个代码生成器
2. 模板包含：slice.ts、types.ts、thunks.ts、selectors.ts
3. 运行 plop 时问我要生成哪个模块，自动填充文件名、函数名、类型名
4. 生成后自动添加到 store 的 rootReducer

以后新增模块，运行 plop 填个名字就搞定。
```

**效果**：重复性代码从"复制粘贴改 10 分钟"降到"运行命令 30 秒"。

---

### 技巧 25：用"迁移脚本"自动升级依赖

**场景**：依赖库大版本升级（比如 React 17 → 18，Next.js 13 → 14），手动改代码要疯。

**解决方案**：让 Claude Code 帮你写迁移脚本，自动改代码。

```
你：
我的项目要从 Next.js 13（pages router）升级到 Next.js 14（app router）。

请帮我：
1. 分析需要改的所有文件（pages/** → app/**）
2. 生成迁移脚本（用 jscodeshift 或 ast-grep）
3. 脚本自动把 getServerSideProps 改成 async Server Component
4. 把 API routes 改成 Route Handlers
5. 运行迁移脚本，然后我手动检查一遍

给出完整方案和回滚方案。
```

**效果**：大版本升级从"手动改 3 天"降到"跑脚本 + 检查 3 小时"。

---

## 🌐 MCP 高级技巧

### 技巧 26：用"MCP 组合"实现复杂工作流

**场景**：单个 MCP 能做的事情有限，但组合起来就能实现复杂工作流。

**示例**：自动生成周报（Git + 数据库 + 文件系统 MCP）

```bash
你：帮我生成本周技术周报：
1. 用 Git MCP 查看本周的所有提交，按功能模块分组
2. 用数据库 MCP 查询本周新增的 bug 数量和已修复数量
3. 生成 Markdown 格式周报，保存到桌面
```

**进阶示例**：线上故障排查（日志 + 数据库 + 搜索 MCP）

```bash
你：API 响应变慢了，帮我排查：
1. 用文件系统 MCP 读取最近 1 小时的 Nginx 访问日志
2. 找出响应时间超过 5 秒的请求，按端点分组
3. 用数据库 MCP 查询这些端点的数据库查询时间
4. 用搜索 MCP 搜索"[数据库/框架名] 性能优化"，找出可能的优化方向
5. 生成排查报告和改进建议
```

**效果**：把需要在 5 个工具之间来回切换的工作，压缩到一个对话里完成。

---

### 技巧 27：用"自定义 MCP 服务器"扩展能力

**场景**：现有 MCP 服务器不满足需求，想接入内部系统（比如公司自研的项目管理工具）。

**解决方案**：让 Claude Code 帮你写自定义 MCP 服务器。

```
你：
我们公司有个内部项目管理系统（叫 ProjectHub），API 文档在 [链接]。

请帮我写一个 MCP 服务器，实现：
- 工具 1：list_my_projects（列出我参与的项目）
- 工具 2：get_project_tasks（获取项目的任务列表）
- 工具 3：create_task（创建新任务）
- 工具 4：update_task_status（更新任务状态）

然后配置到 Claude Code，我就能在对话里直接操作 ProjectHub 了。
```

**效果**：把公司内部系统接入 Claude Code，实现"对话即操作"。

---

### 技巧 28：用"MCP 缓存"提高响应速度

**场景**：MCP 调用数据库或 API 比较慢，每次都要等。

**解决方案**：让 Claude Code 帮你加一层缓存（用 Redis 或本地文件）。

```
你：
我这个 MCP 服务器（指向）每次查询都很慢（约 3 秒）。

请帮我加一层缓存：
1. 用 Redis 缓存查询结果（TTL 5 分钟）
2. 缓存 key 是查询参数的哈希值
3. 如果 Redis 不可用，降级到内存缓存
4. 添加 --no-cache 参数跳过缓存（调试时用）

给出完整代码。
```

**效果**：MCP 响应时间从 3 秒降到 50 毫秒（缓存命中时）。

---

## 🎓 学习技巧

### 技巧 29：用"代码阅读"学习优秀开源项目

**场景**：想学习优秀开源项目的代码，但手动读太慢。

**解决方案**：让 Claude Code 帮你"导读"开源项目。

```
你：
我想学习 Next.js 的源码，特别是路由系统。

请：
1. 克隆 Next.js 仓库（或让我指定本地路径）
2. 找出路由系统的核心文件
3. 用通俗的语言解释路由的工作原理（配流程图）
4. 指出值得学习的设计模式和技巧
5. 如果我要实现简化版路由，给我一个 200 行以内的示例
```

**效果**：从"茫然翻代码 2 天"到"理清思路 2 小时"。

---

### 技巧 30：用"对比学习"掌握多个框架

**场景**：想同时学 React 和 Vue，但容易搞混。

**解决方案**：让 Claude Code 帮你做对比表格 + 并行示例。

```
你：
我想同时学 React 和 Vue 3（Composition API）。

请给我 10 个常见场景的对比示例：
- 数据绑定
- 事件处理
- 条件渲染
- 列表渲染
- 组件通信
- 状态管理
- 生命周期
- 路由
- HTTP 请求
- 表单处理

每个场景并排显示 React 和 Vue 的代码，指出异同点。
```

**效果**：对比学习，记得更牢，不容易混淆。

---

## 🔐 安全技巧

### 技巧 31：用"安全扫描"检查代码漏洞

**场景**：代码写完了，但不知道有没有安全风险。

**解决方案**：让 Claude Code 帮你做安全审计。

```
你：
请帮我做安全审计：

1. 搜索代码中所有包含 password、secret、token、api_key 的地方
2. 检查是否有硬编码的敏感信息
3. 检查是否使用了已知有漏洞的依赖（查 npm audit）
4. 检查是否有 SQL 注入、XSS、CSRF 等常见漏洞
5. 生成安全报告，按严重程度排序（高/中/低）
```

**效果**：提前发现安全问题，避免上线后被攻击。

---

### 技巧 32：用"依赖锁定"防止供应链攻击

**场景**：npm 包可能被劫持（攻击者上传恶意版本），导致供应链攻击。

**解决方案**：让 Claude Code 帮你配置依赖锁定和完整性检查。

```
你：
我想防止供应链攻击，请帮我：

1. 启用 npm 的 package-lock.json（锁死版本）
2. 配置 .npmrc，禁止安装未知来源的包
3. 添加 preinstall 脚本，检查新依赖是否有恶意行为（比如访问敏感文件、发送网络请求）
4. 用 npm audit 和 snyk 定期扫描漏洞
5. 写个 README 章节，说明如何安全更新依赖

给出完整配置和说明。
```

**效果**：降低供应链攻击风险，依赖更新更安心。

---

## 🎁 附加技巧

### 技巧 33：用"Git Aliases"简化常用操作

**场景**：Git 命令太长，每次都要查文档。

**解决方案**：让 Claude Code 帮你配置 Git Aliases。

```
你：
请帮我配置 Git Aliases，简化这些操作：

- git s → git status
- git a → git add
- git c → git commit
- git p → git push
- git lg → git log --oneline --graph --all
- git undo → 撤销最后一次提交（保留修改）
- git amend → 修改最后一次提交（不修改提交信息）

配置到 ~/.gitconfig，全局生效。
```

---

### 技巧 34：用"Shell 别名"提高终端效率

**场景**：频繁使用的命令太长，懒得敲。

**解决方案**：让 Claude Code 帮你配置 Shell 别名（~/.zshrc 或 ~/.bashrc）。

```
你：
我常用这些命令，请帮我配置 Shell 别名：

- k → killall node（杀掉所有 node 进程）
- nrd → npm run dev
- nrb → npm run build
- nrt → npm run test
- cls → clear && ls（清屏并显示当前目录）
- myip → curl ifconfig.me（查看公网 IP）

配置到 ~/.zshrc，并添加注释说明。
```

---

### 技巧 35：用"README 模板"快速写文档

**场景**：每次写 README 都要从头开始，不知道写什么。

**解决方案**：让 Claude Code 帮你创建 README 模板。

```
你：
帮我创建一个 README 模板（README-TEMPLATE.md），包含：

- 项目标题和徽章（build passing、npm version、license 等）
- 项目描述（一句话 + 截图）
- 功能特性（bullets）
- 技术栈
- 快速开始（安装、配置、运行）
- 使用示例（代码块）
- API 文档（如果适用）
- 贡献指南
- 许可证

以后新项目直接复制这个模板，填内容就搞定。
```

---

## 📚 持续学习资源

### 官方资源

- **Claude Code 官方文档**：[https://docs.anthropic.com/claude-code](https://docs.anthropic.com/claude-code)
- **Claude Code GitHub**：[https://github.com/anthropics/claude-code](https://github.com/anthropics/claude-code)
- **Claude API 文档**：[https://docs.anthropic.com](https://docs.anthropic.com)

### 社区资源

- **r/ClaudeAI**（Reddit）：[https://reddit.com/r/ClaudeAI](https://reddit.com/r/ClaudeAI)
- **Claude Code Discord**：[邀请链接在官方文档]
- **Awesome Claude Code**（GitHub）：精选的工具和案例集合

### 推荐阅读

- **《The Pragmatic Programmer》**：编程哲学，同样适用于 AI 辅助编程
- **《Clean Code》**：如何写出 Claude Code 也能理解的优雅代码
- **《Refactoring》**：让 Claude Code 帮你重构的指导手册

---

## 小结

这 35 个小技巧，每一个都能帮你节省 5-30 分钟。

**记住**：
- 技巧是死的，人是活的。灵活运用，不要死记硬背。
- 如果某个技巧不适合你的项目，改改再用。
- 如果你发现了新技巧，欢迎贡献到这个附录（提交 PR）！

> 🎉 恭喜你读完了《Claude Code 案例指南》！现在去实战吧，用 Claude Code 做出点东西来！

---

**下一版预告**：
- 更多实战案例（来自社区贡献）
- 更多小技巧（目标是 50+ 个）
- 视频教程（B 站、YouTube）
- 配套练习题库（看完书不知道练什么？我们帮你准备了）

**保持关注**：[GitHub 仓库链接] | [微信公众号] | [Discord 社区]
