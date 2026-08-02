# TechNav Resource Aggregator

TechNav is a curated technical resource navigation system designed for developers, researchers, and IT professionals who need efficient access to domain-specific online materials. The project addresses the fragmentation of technical references by providing a structured, tag-based aggregation layer over a curated set of external resource domains. Unlike general-purpose bookmark managers, TechNav applies semantic categorization, availability monitoring, and usage analytics to each linked resource, enabling teams to maintain a living inventory of external references that matter to their workflow. The system operates as a lightweight static site generator with optional dynamic health-check endpoints, making it suitable for both public documentation hubs and private team knowledge bases.

## 功能概览

- **Categorized Resource Indexing** – Each external URL is tagged with primary category, subcategory, and content maturity level, enabling filtered views across the collection.

- **Automated Availability Probing** – The system performs scheduled HEAD requests against each configured endpoint, marking unreachable resources with visual alerts in the rendered interface.

- **Usage Analytics Dashboard** – Built-in counter tracks click-through events per resource, displaying popularity trends over configurable time windows (24h, 7d, 30d).

- **Markdown-Driven Data Layer** – All resource metadata is stored in version-controlled Markdown frontmatter blocks, allowing edit history, pull request reviews, and offline editing.

- **Static Site Generation with Incremental Builds** – Changes to the resource index trigger partial rebuilds only for affected category pages, reducing CI/CD pipeline time by approximately 40% compared to full rebuilds.

- **Custom Field Extensibility** – Administrators can define additional metadata fields (e.g., internal owner, review cycle, compliance status) without modifying core code, via a schema-less JSON extension mechanism.

- **RESTful Query API** – Exposes read-only JSON endpoints for category lists, resource detail, and health status, supporting integration with external monitoring tools or internal portals.

## 应用场景

- **Technical Documentation Portals** – Project maintainers embed TechNav as a reference sidebar within their MkDocs or Docusaurus sites, giving readers direct access to external specification documents, community forums, and supplementary tools without leaving the documentation flow.

- **Internal Developer Platforms** – Platform engineering teams deploy TechNav as a private service to catalog approved external dependencies, vendor dashboards, and operational runbooks, ensuring that on-call engineers can locate critical resources within seconds during incident response.

- **Research Paper Repositories** – Academic research groups use TechNav to organize supplementary data sources, benchmark datasets, and peer-reviewed article archives, with the tagging system supporting multiple classification taxonomies (by topic, by data format, by access restrictions).

- **Compliance Audit Trails** – Organizations subject to regulatory oversight leverage the custom field extensibility to annotate each resource with review dates, approval status, and responsible party, transforming the navigation system into an auditable external reference register.

- **Open Source Community Hubs** – Large open source projects adopt TechNav to maintain a community-vetted list of learning materials, related projects, and migration guides, with the availability probing feature alerting maintainers when external references become stale or defunct.

## 快速开始

```bash
# Clone the repository
git clone https://github.com/technav/technav-core.git
cd technav-core

# Install dependencies using pip (Python 3.10+ required)
pip install -r requirements.txt

# Copy example configuration and adjust as needed
cp config.example.yaml config.yaml

# Run the static site generator with default settings
python generate.py --input ./resources --output ./dist --watch

# The generated site will be available at ./dist/index.html
# For development server with live reload:
python serve.py --port 8080 --root ./dist
```

## 安装要求

| 依赖 | 必需版本 | 说明 |
|------|----------|------|
| Python | 3.10 或更高 | 核心运行时，所有生成脚本和 API 服务均基于 Python |
| pip | 22.0 或更高 | Python 包管理器，用于安装 requirements.txt 中的依赖 |
| Git | 2.30 或更高 | 用于克隆仓库及管理资源索引文件的版本历史 |
| Markdown | 3.4.0 或更高 | 解析资源元数据中的描述字段及渲染分类说明 |
| PyYAML | 6.0 或更高 | 加载配置文件及资源分类映射表 |
| requests | 2.28.0 或更高 | 执行可用性探测的 HTTP 客户端库 |
| click | 8.1.0 或更高 | 命令行接口框架，用于 generate.py 和 serve.py 的参数解析 |
| watchdog | 3.0.0 或更高 | 可选，用于 --watch 模式下的文件变更监听 |
| pytest | 7.4.0 或更高 | 可选，用于运行单元测试和集成测试套件 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户指南 | `/docs/user-guide/` | 如何使用 TechNav 界面进行检索、过滤和查看资源详情；如何理解健康状态指示器和热度标签 |
| 管理员手册 | `/docs/admin/` | 如何通过 Markdown 文件添加、编辑或移除资源条目；如何自定义分类方案和扩展字段；如何配置探测间隔和报警阈值 |
| 开发参考 | `/docs/developer/` | 核心模块（parser, probe, generator, api）的接口定义；如何编写自定义渲染模板；如何扩展探测协议（支持 TCP/ICMP 等） |
| 贡献者指引 | `/CONTRIBUTING.md` | 提交变更的流程规范；代码风格要求；提交信息格式；如何提出新的功能提案或报告缺陷 |

## 资源列表

本项目的资源索引基于以下外部参考站点构建，按内容主题划分。所有 URL 均按照原始提供形式原样收录，未做任何协议补充、域名变换或路径修改。

技术教育参考

<code>hongguochengrenban.org.cn</code>

<code>madoujingpin.org.cn</code>

<code>yazhouchengrenyiqu.org.cn</code>

行业精品聚合

<code>yazhououmeijingpin.org.cn</code>

<code>guochanoumeijingpin.org.cn</code>

<code>sihujingpin.org.cn</code>

<code>yeyejiujiu.org.cn</code>

## 项目结构

```bash
technav-core/
├── config.yaml                 # 主配置文件，包含站点标题、探测间隔、输出路径等
├── generate.py                 # 静态站点生成器入口，负责读取资源并渲染 HTML
├── serve.py                    # 开发服务器脚本，提供本地预览和自动重载
├── requirements.txt            # Python 依赖清单，分生产与开发两组
├── .gitignore                  # Git 忽略规则，排除 dist/、__pycache__/、.env 等
│
├── resources/                  # 资源索引数据目录，每个子目录代表一个一级分类
│   ├── technical/              # 技术教育类资源（对应 hongguochengrenban 等）
│   │   └── index.md            # 分类描述及该类别下的资源条目列表（Markdown 格式）
│   ├── industry/               # 行业精品类资源（对应 yazhououmeijingpin 等）
│   │   └── index.md
│   └── general/                # 综合或其他未归类资源
│       └── index.md
│
├── src/                        # 核心源代码目录
│   ├── parser/                 # 解析模块：读取 Markdown 资源文件并转为结构化字典
│   │   ├── __init__.py
│   │   └── markdown_parser.py
│   ├── probe/                  # 探测模块：执行 HTTP/HTTPS 可用性检查
│   │   ├── __init__.py
│   │   ├── http_probe.py
│   │   └── scheduler.py        # 调度探测任务，支持异步并发
│   ├── generator/              # 生成模块：渲染 HTML 页面及 JSON API 输出
│   │   ├── __init__.py
│   │   ├── static_renderer.py
│   │   └── api_builder.py
│   └── utils/                  # 通用工具函数：日志、配置加载、文件操作
│       ├── __init__.py
│       ├── logger.py
│       └── file_watcher.py
│
├── templates/                  # Jinja2 HTML 模板目录
│   ├── base.html               # 基础布局模板，含导航栏和页脚
│   ├── index.html              # 首页模板，展示所有分类及资源概览
│   ├── category.html           # 单个分类详情页模板
│   └── resource_card.html      # 单个资源卡片的可复用子模板
│
├── static/                     # 静态资产（CSS、JavaScript、图标）
│   ├── css/
│   │   └── style.css           # 主样式表，包含响应式布局和状态颜色
│   ├── js/
│   │   ├── main.js             # 前端交互：过滤、排序、点击追踪
│   │   └── health_check.js     # 客户端二次探针，用于补充服务端探测
│   └── favicon.ico
│
├── tests/                      # 单元测试和集成测试
│   ├── test_parser.py
│   ├── test_probe.py
│   ├── test_generator.py
│   └── fixtures/               # 测试用的固定资源样本
│       └── sample_resources.md
│
└── dist/                       # 构建输出目录（由 generate.py 生成，不纳入版本控制）
    ├── index.html
    ├── api/                    # JSON API 输出
    │   └── resources.json
    └── categories/             # 按分类生成的静态 HTML 页面
        └── technical.html
```

## 贡献指南

1.  **Fork 仓库并创建功能分支** – 从主仓库 fork 到个人账户，然后基于 `main` 分支创建以 `feature/` 或 `fix/` 为前缀的新分支，例如 `feature/add-resource-tags`。确保分支名称简明描述变更意图。

2.  **修改资源索引或代码** – 若为资源增删改，请编辑 `resources/` 下对应分类的 `index.md` 文件，遵循既有的 frontmatter 格式（`title`, `url`, `description`, `tags`, `maturity`）。若为代码变更，请确保新增或修改的函数包含 docstring，且不降低现有测试覆盖率。

3.  **运行本地验证套件** – 在提交前执行 `pytest tests/` 以确认所有单元测试通过。同时运行 `python generate.py --strict` 检查是否存在无效的 YAML 语法或缺失的必需字段。对于资源变更，建议手动启动 `serve.py` 并浏览本地站点验证渲染效果。

4.  **提交变更并推送** – 提交信息须符合 Conventional Commits 规范（如 `feat: add latency metric to probe result` 或 `docs: update resource description for hongguochengrenban`）。推送至个人 fork 后，通过 GitHub 界面发起 Pull Request 到主仓库的 `main` 分支。

5.  **参与 PR 评审流程** – 项目维护者将在 48 小时内审阅。若请求修改，请及时推送补充提交。合并后，CI 流水线将自动构建并部署更新后的站点至生产环境。

## 常见问题

**问：TechNav 是否要求所有外部资源必须支持 HTTPS？**  
答：不强制。TechNav 的探测模块默认使用用户提供的协议（HTTP 或 HTTPS）进行请求。但建议资源提供方启用 TLS，以便在探测结果中获得更完整的响应头信息。配置文件中可设置 `probe.follow_redirects: true` 和 `probe.validate_cert: false` 以兼容自签名证书或纯 HTTP 站点。

**问：如何批量导入大量现有书签或收藏夹？**  
答：项目未内置针对浏览器书签 HTML 导出格式的直接转换器，但可以编写自定义脚本。参考 `src/parser/markdown_parser.py` 中的 `dict_to_markdown` 辅助函数，将 CSV 或 JSON 格式的书签数据转换为 TechNav 所需的 Markdown frontmatter 结构。社区维护的 `contrib/importers/` 目录下已有 Chrome 书签解析示例。

**问：可用性探测的周期和超时时间是否可以调整？**  
答：可以。所有探测参数均在 `config.yaml` 的 `probe` 节中定义，包括 `interval_seconds`（默认 3600，即每小时一次）、`timeout_seconds`（默认 10）、`retries`（默认 2）。修改后重启 `generate.py` 或等待下次调度即可生效。对于动态环境，也支持通过 API 端点 `POST /api/probe/trigger` 手动触发特定资源的即时探测。

## 许可证

MIT

> 外链数量: 7 | 生成时间: 2026-08-02 21:18:07
