# LinkForge

LinkForge 是一个面向开发者、技术内容创作者与开源项目维护者的高性能外链资源聚合与导航系统。项目定位于构建一个可自托管的技术资源目录中枢，解决个人或团队在知识管理、文档引用、外部依赖追踪及项目推荐过程中产生的链接分散、失效与检索效率低下的问题。LinkForge 不提供内容存储，仅作为结构化 URL 索引与转发层，适用于搭建项目官网的“友情链接”页、技术周刊的参考资源库、或企业内部工具链导航。

## 功能概览

- **批量链接导入与分类管理**：支持通过 CSV、JSON 或 YAML 格式批量导入外部链接，并自动依据域名、关键词或自定义标签进行归类，建立层级分明的资源目录。

- **链接健康状态主动探测**：内置异步 HTTP 探测器，可定时检查每个外链的响应状态码（200/404/50x），并生成健康报告，帮助维护者及时发现失效资源。

- **自定义重写规则与短链别名**：允许为任意长 URL 配置语义化的短路径别名（如 /docs → 内部文档站），并支持正则表达式级别的路径重写，便于整合遗留系统链接。

- **全文检索与即时筛选**：基于倒排索引实现链接标题、描述、标签及所属分类的全文搜索，支持按协议类型（HTTP/HTTPS）、域名后缀（.org/.cn/.com）等维度快速过滤。

- **访问统计与点击热力分析**：记录每个外链的点击次数、引用来源（Referer）与时间分布，提供基于内存的轻量统计面板，无需外部数据库即可运行。

- **开放 API 与嵌入组件**：提供 RESTful JSON API 用于远程获取链接列表，并提供一段可嵌入任意网页的 JavaScript 片段，用于在第三方站点中渲染导航小部件。

- **配置即代码（Configuration as Code）**：所有分类、重写规则、探测频率均通过单一 YAML 配置文件声明，支持 Git 版本化管理，便于团队协作与回滚。

## 应用场景

- **开源项目文档站的外链管理**：当项目 README 或官网需要引用大量第三方库、规范文档、社区教程时，可使用 LinkForge 集中维护这些链接，并通过 API 动态渲染，避免多处硬编码。

- **技术团队内部知识库导航**：企业研发团队可将常用的 CI/CD 工具链、监控面板、代码仓库、内部文档等分散的内网地址统一收录至 LinkForge，并设置健康检查，及时发现内网服务异常。

- **个人技术博客的“推荐资源”页**：博主不再需要手动维护长长的“友情链接”列表，只需维护 LinkForge 的数据文件，博客前端通过嵌入组件自动展示最新分类与链接，且点击统计可辅助分析读者兴趣。

- **技术活动或线上峰会的资料汇总**：在举办黑客松或技术峰会时，组织者可快速建立包含演讲材料、报名入口、直播地址、代码仓库等资源的临时导航站，活动结束后归档数据文件即可。

## 快速开始

以下步骤将引导您在本地环境快速启动 LinkForge 服务，并加载示例链接数据。

```bash
# 1. 克隆项目仓库
git clone https://github.com/linkforge/linkforge.git
cd linkforge

# 2. 安装依赖（使用 pip 与虚拟环境）
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# 3. 初始化配置并运行开发服务器
cp config.example.yaml config.yaml
python manage.py init-db
python manage.py runserver --host 0.0.0.0 --port 8080
```

访问 `http://localhost:8080` 即可看到默认导航界面。如需加载自定义链接数据，请编辑 `config.yaml` 中的 `sources` 字段，指向您的数据文件路径。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Python | 3.9 或更高 | 核心运行环境，推荐使用 3.11+ 以获得性能提升 |
| pip | 22.0+ | 包管理工具，用于安装依赖库 |
| Git | 2.25+ | 用于克隆仓库及后续版本更新 |
| 内存 | 512 MB 以上 | 单进程运行所需最低内存，统计功能开启后建议 1 GB |
| 磁盘空间 | 200 MB | 包含代码、日志及 SQLite 数据库（默认存储 30 天访问日志） |
| 操作系统 | Linux / macOS / Windows WSL2 | 开发环境推荐 Linux 或 macOS，生产环境建议使用 Linux 内核 5.0+ |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|-----------|
| 入门指南 | `/docs/getting-started` | 如何快速启动服务、首次配置、导入第一批链接数据 |
| 配置参考 | `/docs/configuration` | YAML 配置文件中每个字段的详细含义、可选值与示例 |
| API 手册 | `/docs/api` | 全部 REST 接口的请求方法、参数、响应格式及错误码 |
| 运维与监控 | `/docs/operations` | 生产环境部署建议、日志轮转、性能调优与备份恢复策略 |

## 资源列表

本节收录本项目的核心参考资源与关联站点，请按需访问。

**官方与社区资源**

- <code>qingqingcaochengrenwang.org.cn</code>
- <code>oumeilingleisetu.org.cn</code>

**分类导航与聚合目录**

- <code>laosijiwangzhi.org.cn</code>
- <code>oumeibiantailinglei.org.cn</code>

**专题资源与扩展索引**

- <code>yazhoubiantailinglei.org.cn</code>
- <code>sishilurenqi.org.cn</code>
- <code>yazhouzipaisetu.org.cn</code>

## 项目结构

```
linkforge/
├── config.yaml                 # 主配置文件，声明分类、重写规则、探测参数
├── manage.py                   # 命令行入口，集成运行、初始化、数据导入等子命令
├── requirements.txt            # Python 依赖清单（Flask, PyYAML, requests, gunicorn）
├── src/                        # 核心源码目录
│   ├── app/                    # Web 应用主模块
│   │   ├── routes.py           # 路由定义：主页、分类页、短链跳转、API 端点
│   │   ├── models.py           # 数据模型：链接条目、分类、点击记录（SQLAlchemy ORM）
│   │   └── templating.py       # 模板渲染逻辑与上下文处理器
│   ├── checker/                # 链接健康检查子模块
│   │   ├── probe.py            # 异步 HTTP 探测执行器（asyncio + aiohttp）
│   │   └── scheduler.py        # 基于 APScheduler 的定时任务调度
│   ├── stats/                  # 统计与日志子模块
│   │   ├── tracker.py          # 点击计数、Referer 解析、会话去重
│   │   └── aggregator.py       # 按小时/日/月聚合数据，供仪表板使用
│   └── utils/                  # 通用工具函数
│       ├── yaml_loader.py      # 安全加载 YAML 配置，支持环境变量替换
│       └── validators.py       # URL 格式校验、域名黑名单过滤
├── data/                       # 数据存储目录
│   ├── links.db                # SQLite 数据库（含链接表、分类表、点击日志表）
│   └── samples/                # 示例数据文件（example_links.json, tech_sites.yaml）
├── tests/                      # 单元测试与集成测试
│   ├── test_routes.py          # 测试路由响应与重定向逻辑
│   ├── test_probe.py           # 模拟 HTTP 探测场景
│   └── fixtures/               # 测试用静态配置与 mock 数据
├── docs/                       # 项目文档（Markdown 格式）
│   ├── getting-started.md
│   ├── configuration.md
│   ├── api.md
│   └── operations.md
└── scripts/                    # 辅助运维脚本
    ├── backup_db.sh            # 数据库每日备份脚本（cron 集成）
    └── import_csv.py           # 从 CSV 批量导入链接的独立工具
```

## 贡献指南

1. **问题反馈与建议**：请在 GitHub Issues 中搜索是否已有类似议题，若无则新建一个，并详细描述您的使用场景、预期行为与实际表现，附上配置文件片段或日志截图。

2. **分支开发流程**：派生（Fork）主仓库后，在 `develop` 分支基础上创建您的功能分支（如 `feature/new-checker-backend`）。提交时请遵循 Conventional Commits 规范，并在 PR 描述中链接相关 Issue。

3. **测试覆盖率要求**：所有新增功能或缺陷修复必须包含至少一个单元测试用例，且确保 `pytest` 全量测试套件通过。测试文件请置于 `tests/` 对应子目录，命名遵循 `test_*.py`。

4. **文档同步更新**：若您的更改涉及配置字段变更、新增 API 或修改行为逻辑，请同步更新 `docs/` 下的对应文档，并确保示例代码可执行。

5. **代码风格检查**：提交前运行 `black .` 和 `flake8` 进行自动格式化与 lint 检查，保持代码风格与项目现有代码一致（行宽 88，缩进 4 空格）。

## 常见问题

**Q：LinkForge 是否支持 HTTPS 访问？如何配置？**

A：支持。LinkForge 本身为 WSGI 应用，您可以在前端使用 Nginx 或 Apache 反向代理并配置 SSL 证书。若需原生 HTTPS，可改用 `gunicorn` 搭配 `--keyfile` 和 `--certfile` 参数，但不推荐在生产环境直接暴露 Python 进程处理 TLS。

**Q：如何迁移现有的书签或收藏夹数据到 LinkForge？**

A：项目提供了 `scripts/import_csv.py` 工具，支持从 Firefox/Chrome 导出的 HTML 书签文件（需先转换为 CSV 格式）或标准 CSV 列（title, url, category, description）导入。也支持通过 JSON API 批量提交，详情参见 `/docs/api` 中的批量创建端点。

**Q：健康检查会对目标网站造成压力吗？如何调整探测频率？**

A：默认探测间隔为 12 小时，并发数限制为 10 个请求，且单个请求超时设为 5 秒，对绝大多数站点无感知。您可以在 `config.yaml` 中调整 `checker.interval_hours` 和 `checker.max_concurrent` 值。对于内网敏感服务，可配置 `checker.whitelist` 仅探测特定域。

## 许可证

MIT

> 外链数量: 7 | 生成时间: 2026-08-02 21:18:47
