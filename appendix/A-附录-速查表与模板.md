# 附录 A：速查表与模板

> 把书里最常用的模式、指令、代码片段集中在这里，方便你随时查阅和复制。

---

## 🔧 Claude Code 指令模式速查

### 基础模式

| 场景 | 指令模板 | 说明 |
|------|----------|------|
| 创建新功能 | `帮我创建 [功能描述]，用 [技术栈]` | 最常用 |
| 修改现有代码 | `把 [文件路径] 的 [函数/类] 改成 [新逻辑]` | 精确到位置 |
| 解释代码 | `解释一下 [文件路径] 是怎么工作的` | 理解遗留代码 |
| 找 Bug | `我的代码报错了：[错误信息]，帮我定位问题` | 附上完整错误 |
| 重构 | `重构 [文件路径]，目标是 [可读性/性能/简洁]` | 明确目标 |
| 写测试 | `给 [函数/模块] 写完整的单元测试` | 自动生成测试用例 |
| 优化性能 | `分析 [函数/模块] 的性能瓶颈并优化` | 需要 profiler 数据 |

### 进阶模式

| 场景 | 指令模板 | 技巧 |
|------|----------|------|
| 多文件协同 | `修改涉及 [功能] 的所有文件，保持一致性` | Claude Code 会自动找相关文件 |
| 架构调整 | `把当前的 [单体/分层] 架构改成 [微服务/模块化]，分步执行` | 大改动要分步 |
| 代码审查 | `审查 [文件路径] 的代码质量、安全性和性能` | 相当于 AI Code Review |
| 生成文档 | `给 [模块] 生成 API 文档和使用示例` | 保持文档同步 |
| 数据迁移 | `生成从 [旧格式] 到 [新格式] 的迁移脚本` | 数据分析+脚本二合一 |

---

## 📝 提示词模板库

### 1. 创建 REST API

```
帮我用 [Express/FastAPI/Spring Boot] 创建一个 [资源名] API：
- 字段：[字段1] ([类型]), [字段2] ([类型])
- 接口：GET /[resources], GET /[resources]/:id, POST /[resources], PUT /[resources]/:id, DELETE /[resources]/:id
- 使用 [Prisma/TypeORM/SQLAlchemy] 操作数据库
- 包含输入验证和错误处理
- 生成对应的测试用例
```

### 2. 前端组件开发

```
帮我用 [React/Vue] 创建一个 [组件名] 组件：
- 功能：[描述组件做什么]
- Props：[列出需要的 props 和类型]
- 状态：[内部状态]
- 样式：用 [CSS Modules/Tailwind/styled-components]
- 包含 Storybook 故事文件
```

### 3. 数据处理脚本

```
帮我写一个 [Python/Node.js] 脚本：
- 输入：[输入数据格式和来源]
- 处理：[数据清洗/转换/分析逻辑]
- 输出：[输出格式和目的地]
- 错误处理：记录失败的行并继续处理
- 加进度条（处理大量数据时）
```

### 4. 配置文件生成

```
帮我生成 [Docker/Terraform/K8s] 配置：
- 环境：[开发/测试/生产]
- 需求：[描述需要的资源和服务]
- 包含：[环境变量/密钥管理/健康检查]
- 注释要详细，方便后人维护
```

### 5. Bug 修复

```
我的代码出 Bug 了：

**错误信息：**
[完整的错误堆栈]

**复现步骤：**
1. [步骤1]
2. [步骤2]

**预期行为：**
[应该怎样]

**实际行为：**
[现在怎样]

帮我定位并修复问题，解释原因。
```

### 6. 性能优化

```
帮我优化 [函数/模块] 的性能：

**当前性能：**
- 处理 [X] 条数据需要 [Y] 秒
- 内存占用 [Z] MB

**性能目标：**
- 时间降到 [A] 秒以内
- 内存降到 [B] MB 以内

分析瓶颈并给出优化方案，先解释再改代码。
```

---

## 🎯 CLAUDE.md 配置模板

### 通用项目模板

```markdown
# CLAUDE.md

## 项目概述
[一句话描述项目是做什么的]

## 技术栈
- 后端：[语言/框架]
- 前端：[框架/UI库]
- 数据库：[类型/版本]
- 部署：[平台/方式]

## 代码规范
- 缩进：[空格/Tab] [数量]
- 命名：[驼峰/下划线/短横线]
- 引号：[单引号/双引号]
- 分号：[有/没有]

## 项目结构
```
src/
  controllers/  # API 控制器
  models/       # 数据模型
  services/     # 业务逻辑
  utils/        # 工具函数
```

## 常用命令
- 启动开发服务器：`npm run dev`
- 运行测试：`npm test`
- 构建：`npm run build`
- Lint：`npm run lint`

## 注意事项
- [重要的业务规则]
- [常见坑点]
- [需要避免的做法]

## 测试规范
- 单元测试用 [Jest/Pytest]
- 每个函数都要有测试
- Mock 外部依赖
```

### 前端项目专用

```markdown
# CLAUDE.md - 前端项目

## 技术栈
- React 18 + TypeScript
- Vite 构建工具
- Tailwind CSS 样式
- React Query 数据请求
- Zustand 状态管理

## 组件规范
- 用函数组件 + Hooks
- Props 必须定义 TypeScript 类型
- 每个组件单独一个文件
- 组件名用 PascalCase

## 样式规范
- 优先用 Tailwind 实用类
- 复杂样式用 CSS Modules
- 主题变量在 tailwind.config.js

## 目录结构
```
src/
  components/   # 通用组件
  pages/        # 页面组件
  hooks/        # 自定义 Hooks
  api/          # API 请求函数
  types/        # TypeScript 类型定义
```

## 性能要求
- 列表要虚拟滚动（> 100 条）
- 图片要懒加载
- 组件要代码分割
```

---

## 🐛 常见错误速查

### 1. 依赖问题

| 错误 | 原因 | 解决方案 |
|------|------|----------|
| `MODULE_NOT_FOUND` | 缺少依赖 | `npm install [包名]` |
| `peer dep conflict` | 版本冲突 | `npm install --legacy-peer-deps` |
| `Permission denied` | 权限不足 | `sudo npm install -g [包名]` (Mac/Linux) |

### 2. 数据库连接

| 错误 | 原因 | 解决方案 |
|------|------|----------|
| `ECONNREFUSED` | 数据库没启动 | 启动数据库服务 |
| `Access denied` | 用户名密码错 | 检查 `.env` 配置 |
| `Too many connections` | 连接池满 | 增加 `max_connections` |

### 3. CORS 错误

```
// 后端添加 CORS 中间件（Express）
app.use(cors({
  origin: 'http://localhost:3000',
  credentials: true
}));
```

### 4. 端口被占用

```bash
# 查找占用端口的进程
lsof -i :3000  # Mac/Linux
netstat -ano | findstr :3000  # Windows

# 杀掉进程
kill -9 [PID]  # Mac/Linux
taskkill /PID [PID] /F  # Windows
```

---

## ⚡ 效率提升技巧

### 1. 批量操作

不要一个文件一个文件改，告诉 Claude Code：
```
修改所有涉及用户认证的 API，加上 JWT 验证中间件
```

### 2. 上下文管理

项目大了之后，用 `.claudeignore` 排除不需要的文件：
```
# .claudeignore
node_modules/
dist/
*.log
package-lock.json
```

### 3. 分步验证

大改动分步做：
```
第一步：只改数据模型
第二步：改 API 接口
第三步：改前端调用
每步完成后运行测试，确保没问题再继续
```

### 4. 让 Claude Code 自己跑测试

```
改完代码后自动运行测试，如果失败就修复，直到全部通过
```

---

## 📚 推荐资源

### 官方文档
- [Claude Code 官方文档](https://docs.anthropic.com/claude-code)
- [Claude API 参考](https://docs.anthropic.com/en/api)

### 社区资源
- [Claude Code GitHub Discussions](https://github.com/anthropics/claude-code/discussions)
- [r/ClaudeAI](https://www.reddit.com/r/ClaudeAI/) - Reddit 社区

### 学习资源
- [Prompt Engineering Guide](https://www.promptingguide.ai/)
- [Awesome Claude Prompts](https://github.com/anthropics/awesome-claude-prompts)

---

## 🎓 学到了什么（总结）

1. **指令质量 = 输出质量** — 花 30 秒写清楚需求，省 30 分钟改代码
2. **Claude Code 擅长的是「理解上下文」** — 给它看你的项目结构、代码规范，输出质量翻倍
3. **大改动分步做** — 一次改 20 个文件容易出错，分 4 次每次改 5 个更稳
4. **让 AI 帮你测试** — 不只是写代码，还能帮你写测试、跑测试、修 Bug
5. **CLAUDE.md 是项目的大脑** — 把技术栈、代码规范、常用命令写进去，Claude Code 每次都能「回忆」起来

---

**Next Step：** 把这个速查表打印出来贴墙上，用的时候瞟一眼，比翻书快 10 倍 😎
