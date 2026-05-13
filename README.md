# 日报编写

一个用于**把测试日报按固定结构直接写入飞书文档**的 Agent Skill。

## 这个 skill 解决什么问题

适合这种场景：
- 每天把测试工作整理成日报
- 日报需要按**自然周**归档
- 日报需要按**日期**落到对应位置
- 最新周要放在最上面
- 同一周内最新日期要放在最上面
- 同一天多条任务要合并到同一个日期下面
- 用户已经提供了固定的飞书日报文档，希望后续默认直接写入

这个 skill 的目标不是只“生成一段日报文案”，而是：
- 读取现有飞书文档结构
- 识别周标题 / 日标题
- 依据测试时间定位正确插入位置
- 按固定规则写入
- 严格不编造缺失内容

## 主要能力

- 根据测试时间自动计算所属自然周
- 以周为一级标题、日期为二级标题组织日报
- 周级倒序：最新周在最上面
- 日级倒序：同一周内最新日期在最上面
- 同日多任务合并到同一日期标题下
- 支持默认飞书日报文档直写
- 发现结构错位时先修结构，再追加内容

## 触发场景

以下表达通常会触发这个 skill：
- 写测试日报
- 补测试日报
- 按模板写到飞书文档
- 直接写入默认飞书日报文档
- 按测试时间插到正确周
- 优化日报模板
- 形成日报约束词
- 生成测试日报 skill

## 推荐提示词

最推荐的固定触发句：

```text
请按测试日报模板，直接写入默认飞书日报文档。
```

推荐输入模板：

```text
请按测试日报模板，直接写入默认飞书日报文档。

测试时间：YYYY-MM-DD

任务1：
- 项目：
- 所属模块：
- 测试任务：
- 耗时：
- 当前状态：
- 备注：

今日主要内容：
- 

当前问题/风险：
- 

当前阻塞：
- 

明日计划：
- 

工作产出：
- 
```

## 当前核心约束

1. 以**测试时间**为唯一日期基准，不以执行当天为准。
2. 按**自然周（周一到周日）**归档为一级标题。
3. 一级标题（周）按时间**倒序**排列，最新周在最上面。
4. 二级标题（日期）按时间**倒序**排列，最新日期在最上面。
5. 同一天多条任务必须合并到同一个日期标题下。
6. 缺失信息不编造。
7. 用户确认过日报飞书文档后，后续默认直接写入该文档。
8. 如果文档现有结构与规则冲突，先修正文档结构，再继续写入。

## 默认日报文档

当前默认日报文档：
- `https://ihqz5dyhwa.feishu.cn/docx/HUomdMnauo1hqdxPYulcFF9xngc`

## 仓库结构

```text
feishu-daily-report-writer/
├── SKILL.md
├── README.md
└── .gitignore
```

## 主维护规则

- 主维护目录：`C:\Users\zhangxincheng\.openclaw\workspace\repos\feishu-daily-report-writer`
- 运行投放目录：`C:\Users\zhangxincheng\.openclaw\workspace\skills\feishu-daily-report-writer`
- 所有功能修改、规则修改、README 更新，**只在主维护目录进行**
- 确认无误后，再同步到运行投放目录
- 禁止同时手改两份，避免版本漂移

一句话记忆：
- **repo 是主库，skills 是投放副本**

## 推荐工作流

1. 在 `repos/feishu-daily-report-writer` 中修改
2. 本地验证内容
3. 同步到 `skills/feishu-daily-report-writer`
4. 提交 git
5. push 到 GitHub
6. 需要发版时打 tag

## 版本查看方式

- 仓库地址：`https://github.com/mikeqiu66/feishu-daily-report-writer`
- tags 页面：`https://github.com/mikeqiu66/feishu-daily-report-writer/tags`
- 主分支：`main`
- 当前首版标签：`v0.1.0`

## 后续维护建议

建议使用下面这套提交前缀：

- `feat:` 新功能或规则增强
- `fix:` 修复插入逻辑、排序逻辑、归属错误
- `docs:` 更新 README / 提示词 / 说明文档
- `refactor:` 重构 skill 结构但不改外部行为

示例：

```text
feat: support reverse chronological week/day ordering
fix: correct weekly title placement for monday entries
docs: add recommended prompt templates
refactor: simplify insertion workflow description
```

## 建议的版本节奏

- `v0.1.0`：首版可用
- `v0.2.0`：补强触发条件与提示词模板
- `v0.3.0`：补强周倒序 / 日倒序 / 同日合并规则
- `v1.0.0`：规则稳定，可长期复用
