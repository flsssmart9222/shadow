# ResourceHub

ResourceHub 是一个面向开发者与技术研究人员的轻量级外链资源聚合与导航系统。项目定位为技术信息的中转枢纽，通过人工筛选与结构化组织，将分散于互联网各处的优质技术文档、社区讨论、工具站点与学术资源进行集中收录与分类展示。ResourceHub 不存储任何实质内容，仅提供链接索引与简要描述，帮助目标用户快速定位所需信息，降低信息检索成本，提升研究与开发效率。

本项目适用于需要频繁查阅多源技术资料的人群，包括但不限于运维工程师、后端开发者、安全研究人员以及学术论文写作者。通过统一的入口与清晰的分类逻辑，用户可在数秒内完成从需求到对应资源的跳转，无需在多个搜索引擎间反复切换。

## 功能概览

- **多层级分类导航** 资源按技术领域、内容类型与适用场景进行三级分类，支持快速筛选与定位。
- **外链健康状态监测** 系统定时对收录的 URL 进行可达性检查，自动标记异常链接并生成报告。
- **全文检索支持** 基于标题、标签与描述字段提供轻量级全文搜索，响应时间低于 200 毫秒。
- **标签体系与关联推荐** 每条资源可关联多个标签，系统依据标签共现频率自动推荐相关内容。
- **个人收藏与临时列表** 支持用户创建临时收藏列表，便于单次研究任务中的集中访问。
- **导入与导出机制** 提供 JSON 与 CSV 格式的资源列表导入导出接口，便于团队内部共享导航配置。
- **访问统计与热度排序** 记录每个外链的点击次数，支持按热度、添加时间与字母序三种排序方式。
- **响应式管理面板** 提供基于浏览器的管理界面，支持资源的增删改查与批量操作。

## 应用场景

- **技术文档快速查阅** 开发人员在调试第三方库或框架时，可通过 ResourceHub 快速跳转至对应官方文档或社区讨论帖，减少翻阅浏览器书签的时间。
- **学术研究文献索引** 研究人员在撰写论文或进行文献综述时，可将相关学术站点、数据集页面与工具仓库统一收录，形成个人研究门户。
- **运维故障排查参照** 运维工程师在遇到系统异常时，可通过本导航系统快速访问常用日志分析工具、错误码查询站点与系统调优指南。
- **团队知识库基础层** 技术团队可将 ResourceHub 作为内部知识库的入口层，统一存放团队常用的 CI/CD 工具、代码托管平台与监控面板地址。
- **开源项目依赖上游跟踪** 开源维护者可通过本系统集中管理项目所依赖的上游仓库、协议文本与版本发布页面，便于定期检查更新。

## 快速开始

以下步骤适用于 Linux 与 macOS 环境，Windows 用户建议使用 WSL2 或 Git Bash 执行。

```bash
# 步骤 1：克隆代码仓库
git clone https://github.com/resourcehub/resourcehub.git
cd resourcehub

# 步骤 2：安装依赖（使用 pip 与虚拟环境）
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# 步骤 3：初始化数据库并启动服务
python manage.py migrate
python manage.py loaddata initial_resources.json
python manage.py runserver 0.0.0.0:8000
```

启动成功后，访问 http://localhost:8000 即可进入导航主页。管理员后台位于 /admin，默认账号密码请参考 .env.example 文件中的配置说明。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|----------|----------|------|
| Python | 3.9 - 3.11 | 核心运行环境，3.12 及以上版本暂未完成兼容性测试 |
| Django | 4.2.x | Web 框架，用于路由、ORM 与管理界面 |
| SQLite | 3.35+ | 默认数据库，生产环境建议切换至 PostgreSQL 14+ |
| Redis | 6.0+ | 用于缓存搜索结果与临时收藏列表，非必需但强烈推荐 |
| Node.js | 18.x | 仅用于前端静态资源构建，运行时不需要 |
| gunicorn | 20.x | 生产环境 WSGI 服务器，开发环境可使用内置 runserver |
| python-dotenv | 1.0+ | 环境变量管理，用于区分开发与生产配置 |
| requests | 2.28+ | 用于外链健康状态检测的 HTTP 客户端 |
| beautifulsoup4 | 4.11+ | 用于解析资源页面的标题与描述（仅后台管理使用） |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | /docs/user-guide/ | 如何添加收藏、搜索资源、查看热度排行与导出列表 |
| 管理员手册 | /docs/admin-guide/ | 如何批量导入 URL、设置分类标签、查看健康检查日志 |
| 开发者指南 | /docs/developer-guide/ | 如何扩展资源解析器、自定义排序算法、接入外部 API |
| 部署运维 | /docs/deployment/ | 如何配置 PostgreSQL、Redis、使用 systemd 托管服务与 Nginx 反向代理 |
| API 参考 | /docs/api-reference/ | 资源查询、标签列表、统计信息的 RESTful 接口规范与示例 |
| 常见问题 | /docs/faq/ | 收录标准、更新频率、链接失效处理与数据备份策略 |

## 资源列表

### 综合技术资源类

<code>oumeiguochanjingpin.org.cn</code>

<code>yazhouyikaerka.org.cn</code>

### 媒体与传播类

<code>yazhouchuanmei.org.cn</code>

### 技术福利与工具类

<code>chunshuifuli.org.cn</code>

### 理论与学术类

<code>wuyelilun.org.cn</code>

### 社区与活跃站点类

<code>ririganyeyecao.org.cn</code>

<code>oumeijingpinerqu.org.cn</code>

## 项目结构

```
resourcehub/
├── manage.py                      # Django 项目管理入口
├── requirements.txt               # Python 依赖列表
├── .env.example                   # 环境变量配置模板
├── resourcehub/                   # 项目主配置目录
│   ├── __init__.py
│   ├── settings/                  # 分环境配置子目录
│   │   ├── base.py                # 通用配置
│   │   ├── development.py         # 开发环境配置
│   │   └── production.py          # 生产环境配置
│   ├── urls.py                    # 主路由表
│   └── wsgi.py                    # WSGI 入口
├── apps/                          # 所有自定义应用
│   ├── resources/                 # 资源管理核心应用
│   │   ├── models.py              # Resource, Category, Tag 模型
│   │   ├── views.py               # 列表、详情、搜索、收藏视图
│   │   ├── admin.py               # 后台管理界面定制
│   │   ├── serializers.py         # RESTful API 序列化器
│   │   └── health_check.py        # 外链健康监测后台任务
│   ├── users/                     # 用户与收藏列表管理
│   │   ├── models.py              # 自定义用户模型与收藏关系
│   │   └── backends.py            # 邮箱与用户名双认证后端
│   └── stats/                     # 点击统计与热度计算
│       ├── models.py              # ClickLog 模型
│       └── middleware.py          # 请求拦截与异步落库中间件
├── static/                        # 编译后的前端静态文件
│   ├── css/                       # 响应式导航样式
│   └── js/                        # 搜索建议与收藏交互脚本
├── templates/                     # Django 模板文件
│   ├── base.html                  # 基础骨架模板
│   ├── resource_list.html         # 资源列表页
│   └── resource_detail.html       # 资源详情与关联推荐页
├── fixtures/                      # 初始数据固件
│   └── initial_resources.json     # 预置分类与示例资源
└── scripts/                       # 辅助运维脚本
    ├── import_csv.py              # CSV 批量导入工具
    └── export_markdown.py         # 生成当前资源列表的 Markdown 快照
```

## 贡献指南

1. 查阅 GitHub Issues 中的 "good first issue" 标签列表，选择未被指派的工单，在评论区声明认领。
2. 从 main 分支创建新的功能分支，分支命名格式为 feature/工单号-简述 或 fix/工单号-简述。
3. 本地开发时请确保使用 development 配置，并运行 pre-commit 钩子进行代码风格检查（Black + Flake8）。
4. 提交代码前需编写或更新对应的单元测试，确保测试覆盖率不低于 85%，所有测试用例通过。
5. 发起 Pull Request 至 main 分支，描述中需包含工单编号、变更摘要与手动测试步骤，至少一位项目维护者审核通过后合并。

## 常见问题

**问：ResourceHub 是否存储外链对应的页面内容或快照？**

答：不存储。ResourceHub 仅保存 URL 地址、标题、描述与分类标签，所有内容跳转均直接导向原始站点。系统不会对第三方内容进行缓存、转载或代理，外链健康检查仅验证 HTTP 状态码，不解析页面正文。

**问：收录资源的标准是什么？如何申请添加新链接？**

答：收录优先面向技术文档、开源工具、学术资源与公认的社区讨论站点。站点需保持稳定访问，内容无恶意代码或明显侵权争议。新链接可通过管理后台的 "建议添加" 表单提交，或直接联系项目维护者，审核周期通常为 3 个工作日。

**问：健康检查发现链接失效后会如何处理？**

答：系统连续三次检查失败（间隔 12 小时）后，会将资源标记为 "异常" 状态，并在管理面板中高亮显示。异常资源不会从数据库中删除，但会默认隐藏于前台列表。维护者定期复核后可手动更新 URL 或恢复为正常状态。

## 许可证

MIT License

Copyright (c) 2026 ResourceHub Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

> 外链数量: 7 | 生成时间: 2026-08-02 21:18:07
