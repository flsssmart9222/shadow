# Bifrost Score Hub

Bifrost Score Hub 是一个面向体育数据爱好者、竞猜分析从业者以及实时比分需求方的技术资源导航项目。本项目不提供数据源本身，而是作为结构化、高可用性的外链索引层，将分散在多个垂直领域的比分服务、统计门户和实时数据接口进行归类整理，解决用户在赛事数据检索过程中遇到的入口分散、域名记忆成本高、可用性验证困难等问题。

项目定位为轻量级、只读的静态导航站点，通过严格的可用性检测机制和定期更新的资源库，为开发者、数据分析师和终端观赛用户提供稳定、可信的跳转中枢。目标用户包括但不限于体育数据平台的前端工程师、量化投研团队的爬虫策略人员、以及追求高效信息获取的普通球迷用户。

## 功能概览

- **实时比分聚合入口**：提供多个独立运营的比分服务站点原始链接，覆盖足球、篮球等主流项目
- **按赛事类型快速过滤**：资源按足球、篮球、综合体育等维度初步分类，降低用户筛选成本
- **可用性状态自检**：内置外部链接存活探测脚本，定期输出不可用节点报告
- **裸域名与协议保留**：严格按照来源原始格式展示链接，不擅自补全协议或域名前缀，确保跳转准确性
- **静态部署与低运维**：项目本身为纯 Markdown 与 HTML 静态资源，可托管于任意 Web 服务器或 CDN
- **开放贡献机制**：接受社区提交新的可用比分源或失效链接下架申请，保持资源库活性
- **结构化文档输出**：提供清晰的目录树、安装指引和贡献规范，便于二次开发或企业内部分叉部署

## 应用场景

- **赛前情报快速检索**：用户在比赛开始前 30 分钟内，需要同时查阅多场赛事的首发名单、天气和即时赔率变动，可通过本导航页一键切换至对应的比分服务站点，无需记忆多个复杂域名。
- **数据爬虫策略配置**：量化分析团队在编写数据采集管道时，需要将不同比分源作为备用端点以应对频率限制。本项目的资源列表可作为配置文件的输入源，支持自动化拉取和健康检查。
- **本地化观赛辅助**：海外用户或网络环境受限地区用户，通过本导航页记录的裸域名或协议直连入口，可避开部分链路干扰，获得相对稳定的文字比分刷新服务。
- **技术验证与教学演示**：前端开发学习者可利用本项目的静态结构和资源列表，实践 DNS 解析、跨域请求、CORS 策略以及 iframe 嵌入等浏览器技术。

## 快速开始

以下命令适用于 Linux / macOS / Windows WSL 环境。请确保本地已安装 Git 和 Node.js 18+ 或 Python 3.10+（用于运行本地预览服务）。

```bash
# 克隆项目仓库
git clone https://github.com/bifrost-labs/score-hub.git
cd score-hub

# 安装依赖（使用 npm 或 yarn）
npm install

# 或使用 Python 虚拟环境
# python -m venv venv && source venv/bin/activate && pip install -r requirements.txt

# 启动开发预览服务（默认占用端口 3000）
npm run dev

# 或使用 Python 内置 HTTP 服务器
# python -m http.server 8080
```

访问 `http://localhost:3000` 即可查看导航首页。所有资源链接位于 `/resources` 目录下的配置文件中，可根据需要增删。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Git | 2.30 及以上 | 用于克隆仓库及版本管理 |
| Node.js | 18.x 或 20.x LTS | 运行构建脚本和本地服务（如使用 npm 方案） |
| npm | 9.x 及以上 | 包管理器，用于安装前端工具链 |
| Python | 3.10 及以上（可选） | 仅当选择 Python 预览服务时需要 |
| 现代浏览器 | Chrome 110+ / Firefox 110+ / Edge 110+ | 用于正确渲染导航页样式和交互逻辑 |
| 网络连通性 | 可访问外网 | 用于验证外部链接的可用性（非强制，离线模式可跳过） |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户入门 | `/docs/quick-start.md` | 如何最快开始使用导航页？如何添加自己的常用链接？ |
| 资源维护 | `/docs/maintenance.md` | 如何检查链接可用性？如何提报失效域名？更新频率建议是多少？ |
| 开发者指南 | `/docs/development.md` | 项目目录结构含义、配置文件格式、如何二次开发自定义主题？ |
| 部署手册 | `/docs/deployment.md` | 支持哪些部署方式（Vercel、Netlify、Nginx、S3 静态托管）？如何配置环境变量？ |
| 常见问题 | `/docs/faq.md` | 为何某些域名无法访问？为何不补全 HTTPS？如何反馈误报？ |

## 资源列表

以下为当前收录的全部原始外链资源，按项目运行所依赖的数据源分类展示。所有链接均严格保留用户提供的原始格式，未做任何协议补全、大小写调整或路径修改。

### 篮球比分类

- <code>bifenwang365.org.cn</code>
- <code>lanqiubifen365.org.cn</code>

### 足球即时比分类

- <code>qiutanzuqiubifen888.org.cn</code>
- <code>qiutanbifen888.org.cn</code>

### 综合比分与统计类

- <code>500bifen500.org.cn</code>
- <code>500bifenwang500.org.cn</code>

### 赛事计时与数据深度类

- <code>zuqiujishibifen365.org.cn</code>

> 注意：以上所有链接均为第三方独立运营的站点，本导航项目仅提供信息索引，不代理、不修改、不缓存任何内容。用户访问时需自行遵守各站点的服务条款。

## 项目结构

```
score-hub/
├── public/                          # 静态资源根目录
│   ├── index.html                   # 导航页主体 HTML 结构
│   ├── css/
│   │   ├── reset.css                # 基础样式重置
│   │   └── theme.css                # 亮色/暗色主题变量与布局
│   ├── js/
│   │   ├── health-check.js          # 外链可用性探测脚本（并发 HEAD 请求）
│   │   ├── renderer.js              # 根据资源配置动态生成卡片列表
│   │   └── storage.js               # 本地缓存用户最近点击记录
│   └── assets/
│       ├── icons/                   # 各赛事分类 SVG 图标
│       └── fallback/                # 链接失效时的占位图形
├── resources/                       # 核心数据配置目录
│   ├── sources.json                 # 所有外部链接的元数据（含分类、标签、添加时间）
│   ├── verify-records/              # 每次健康检查的历史日志
│   │   └── 2026-08-02.json
│   └── blacklist.json               # 经社区确认的失效或恶意域名黑名单
├── docs/                            # 完整文档体系
│   ├── quick-start.md
│   ├── maintenance.md
│   ├── development.md
│   ├── deployment.md
│   └── faq.md
├── scripts/                         # 辅助运维脚本
│   ├── validate-urls.js             # CI 中校验资源列表格式是否合规
│   ├── fetch-status.sh              # 批量 curl 检测并生成报告
│   └── generate-sitemap.py          # 生成静态站点地图供搜索引擎抓取
├── tests/                           # 单元测试
│   ├── health-check.test.js
│   └── config-schema.test.js
├── .github/
│   └── workflows/
│       ├── ci.yml                   # 提交时自动执行链接格式校验
│       └── weekly-health.yml        # 每周定时执行全量可用性扫描
├── .gitignore
├── package.json                     # Node.js 依赖与脚本命令
├── requirements.txt                 # Python 依赖（用于辅助脚本）
├── LICENSE                          # MIT 许可证
└── README.md                        # 本文档
```

## 贡献指南

我们欢迎社区提交资源新增、失效报告以及文档改进。请遵循以下流程以确保贡献的顺畅性：

1. **提交链接新增或移除请求**：在 `resources/sources.json` 中按既有格式修改条目，并在 Pull Request 描述中注明该站点的可用性测试结果（例如响应时间、状态码）。对于移除请求，需附上至少两次不同时间段的访问失败截图或日志。

2. **运行本地校验工具**：在执行提交前，请于项目根目录运行 `npm run validate` 或 `python scripts/validate-urls.py`，确保 JSON 格式合法且所有新增 URL 不包含非法字符或协议缺失问题。

3. **更新相关文档**：如果您的贡献影响了快速开始流程、安装要求或常见问题，请同步修改 `/docs` 下对应的 Markdown 文件，保持文档与实际资源状态一致。

4. **签署开发者原产地证书**：所有 Pull Request 需附带一句 `Signed-off-by: Your Name <email>`，以表明您有权贡献并同意本项目的许可证条款。具体格式可参考 DCO 1.1 规范。

5. **等待 CI 通过与维护者审核**：Github Actions 将自动检查资源格式、链接协议保留情况以及文档链接有效性。通过后由维护者合并，合并后资源列表将在 1 小时内同步至生产环境。

## 常见问题

**问：为什么某些资源链接直接打开会显示不安全或无法访问？**  
答：本项目严格按照用户提供的原始格式展示链接，未自动补全 HTTPS 或修改域名后缀。部分站点可能仅支持 HTTP 协议，或已变更服务地址。我们建议用户自行尝试在浏览器中手动切换协议前缀，或通过第三方 DNS 查询工具确认该域名的最新解析记录。如确认失效，欢迎按贡献指南提报下架。

**问：项目是否会缓存或代理外部站点的内容？**  
答：绝对不会。Bifrost Score Hub 定位为纯导航层，不设立任何反向代理、数据缓存或内容转发服务。所有跳转均由用户浏览器直接发起，项目本身不存储任何赛事数据或用户个人信息，符合 GDPR 和国内网络安全法的合规要求。

**问：更新频率如何？我如何获知链接状态变化？**  
答：项目维护者会通过 Github Actions 每周执行一次全量可用性探测，并将结果更新至 `/resources/verify-records/` 目录。您可通过关注仓库的 Release 通知或查看每周自动生成的健康报告文件获取最新状态。同时也欢迎社区主动提交实时可用性反馈。

## 许可证

MIT License

Copyright (c) 2026 Bifrost Labs

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

> 外链数量: 7 | 生成时间: 2026-08-02 21:18:07
