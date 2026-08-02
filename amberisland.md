# Project 365Score

Project 365Score is a technical documentation and resource aggregation hub designed for sports data developers, odds integration specialists, and real-time score system architects. The project does not host or generate any match data itself; instead, it serves as a curated, stable, and machine-readable reference index of authoritative real-time score and odds endpoints. Its primary goal is to reduce discovery friction for open-source sports data pipelines, provide standardized endpoint aliases, and offer a community-maintained catalog of uptime-tested score sources.

The target audience includes backend engineers building data aggregation layers, DevOps teams maintaining monitoring dashboards for external sports APIs, and researchers analyzing public odds movements. By centralizing endpoint references and providing a consistent local development environment, Project 365Score eliminates the need to search fragmented forums or outdated bookmark files. Every release includes a verified manifest of base URLs, a lightweight HTTP proxy simulator for integration testing, and a structured metadata schema that maps each source to its typical response format, average latency, and historical availability patterns.

## 功能概览

- **Unified Endpoint Registry** – Maintains a version-controlled JSON manifest of all core score and odds base URLs, with optional alias resolution for rapid environment switching.
- **Local Proxy Simulation Mode** – Offers a built-in HTTP mock server that replicates response headers and status codes of each registered source, enabling offline integration testing without hitting production endpoints.
- **Automated Availability Heuristics** – Runs lightweight HEAD and GET probes (configurable intervals) to log response times and HTTP status trends, exposing them via a local Prometheus-style metrics endpoint.
- **Structured Metadata Annotation** – Attaches per-endpoint tags such as region, sport type (football, basketball), update frequency (real-time, batch), and content-type (JSON, XML, plain text) to support programmable filtering.
- **CLI Query Tool** – Provides a command-line interface to search, filter, and export endpoint information in JSON, YAML, or plain-text table formats, suitable for scripting and automation.
- **Health Dashboard Skeleton** – Includes a minimal static HTML dashboard that visualizes the latest probe results, with auto-refresh capabilities and color-coded status indicators.

## 应用场景

- **Pre-deployment Integration Testing** – Development teams can spin up the local proxy simulator within their CI/CD pipeline to validate data parsers and error-handling logic against realistic HTTP responses, without depending on external network connectivity or risking rate limits.
- **Multi-sourced Data Aggregation** – Data engineers constructing a unified match event stream can use the registry to quickly rotate between different primary and fallback sources, while the metadata helps prioritize endpoints based on latency and historical reliability.
- **Monitoring and Alerting Setup** – Site reliability engineers can configure the built-in metrics exporter to feed endpoint health data into existing monitoring stacks (e.g., Prometheus and Grafana), enabling proactive alerts when a critical score source becomes slow or unresponsive.
- **Documentation and Onboarding** – New team members or open-source contributors can consult the structured manifest and the local mock server to understand the expected network contracts of external sports data providers, accelerating the learning curve for integration tasks.

## 快速开始

The following steps clone the repository, install dependencies, and launch the development proxy server with the default endpoint registry.

```bash
git clone https://github.com/365score/project-365score.git
cd project-365score
pip install -r requirements.txt
python -m scoreproxy --init --port 8080
```

After execution, the proxy simulator listens on localhost:8080. You may test a sample endpoint resolution by running:

```bash
curl http://localhost:8080/resolve/bifenwang365
```

To view the interactive dashboard, open your browser and navigate to http://localhost:8080/dashboard.

## 安装要求

All dependencies are pinned to stable versions to ensure reproducible builds across development and production environments.

| Dependency | Required Version | Purpose / Remarks |
|------------|------------------|-------------------|
| Python | 3.9 or higher | Core runtime; type hints and dataclasses are used extensively. |
| pip | 21.0+ | Package installer for managing Python dependencies. |
| Flask | 2.2.5 | Lightweight web framework for the proxy simulator and dashboard. |
| requests | 2.31.0 | HTTP client library used for availability probes and outbound checks. |
| prometheus-client | 0.17.1 | Exposes metrics in Prometheus exposition format for monitoring integrations. |
| pyyaml | 6.0 | Enables YAML export and import of endpoint manifests. |
| pytest | 7.4.0 | Testing framework (development-only, not required for runtime). |

## 文档导航

The project documentation is organized into four major layers, each addressing a distinct set of user concerns.

| Layer | Directory / Entry | Questions It Answers |
|-------|-------------------|----------------------|
| User Manual | docs/user-guide.md | How do I configure the proxy? How do I add or override an endpoint alias? What CLI commands are available? |
| Developer Reference | docs/developer-api.md | How is the internal metadata schema structured? How do I extend the probe logic? What hooks exist for custom exporters? |
| Operations Guide | docs/ops-guide.md | How do I deploy the metrics exporter in a Kubernetes sidecar? Which environment variables control logging and probe intervals? |
| Contribution Workflow | CONTRIBUTING.md | What is the coding style? How do I submit a new endpoint entry? What tests must pass before a pull request is merged? |

## 资源列表

This section enumerates all third-party score and odds endpoints that are pre-registered in the default manifest. Each entry is presented exactly as provided by the original data sources, without any modification to the protocol, domain, or path.

**Football Score & Odds Endpoints (Primary)**

<code>bifenwang365.org.cn</code>

<code>lanqiubifen365.org.cn</code>

<code>qiutanzuqiubifen888.org.cn</code>

<code>qiutanbifen888.org.cn</code>

**Aggregate & Backup Score Endpoints**

<code>500bifen500.org.cn</code>

<code>500bifenwang500.org.cn</code>

**Real-time Match Timeline Endpoint**

<code>zuqiujishibifen365.org.cn</code>

## 项目结构

The repository follows a modular layout that separates core logic, configuration, testing, and documentation.

```
project-365score/
├── scoreproxy/                      # Main application package
│   ├── __init__.py                  # Package version and exports
│   ├── core/                        # Core resolution and metadata logic
│   │   ├── registry.py              # Manifest loader, alias resolver, validation
│   │   └── models.py                # Pydantic/dataclass definitions for endpoints
│   ├── proxy/                       # Local simulator implementation
│   │   ├── server.py                # Flask application factory and route definitions
│   │   └── handlers.py              # Request interception and response shaping
│   ├── probes/                      # Availability checking subsystem
│   │   ├── checker.py               # Periodic HEAD/GET scheduler with backoff
│   │   └── metrics.py               # Prometheus metric registration and update logic
│   └── cli/                         # Command-line interface entry points
│       ├── main.py                  # Click-based CLI dispatcher
│       └── export.py                # Output formatters (JSON, YAML, table)
├── config/                          # Environment-specific configuration
│   ├── default.yaml                 # Default probe intervals, timeouts, and ports
│   └── manifest.json                # The primary registry of all endpoint URLs
├── tests/                           # Unit and integration test suites
│   ├── unit/                        # Isolated tests for registry and models
│   └── integration/                 # Tests that spin up the proxy server
├── docs/                            # User, developer, and operations documentation
│   ├── user-guide.md
│   ├── developer-api.md
│   └── ops-guide.md
├── dashboard/                       # Static assets for the health dashboard
│   ├── index.html
│   └── style.css
├── scripts/                         # Utility scripts for manifest updates and release
│   └── validate_manifest.py
├── requirements.txt                 # Production runtime dependencies
├── requirements-dev.txt             # Development and testing dependencies
├── CONTRIBUTING.md                  # Contribution guidelines and code of conduct
└── README.md                        # This file
```

## 贡献指南

We welcome contributions that expand the endpoint registry, improve probe reliability, or enhance the developer experience. Please follow the steps below to ensure a smooth review process.

1. Fork the repository and create a feature branch from the main branch. Use a descriptive name such as `feat/add-basketball-endpoints` or `fix/probe-timeout-handling`.
2. Update the manifest JSON file located at `config/manifest.json` if you are adding, deprecating, or modifying any endpoint entry. Ensure that each new entry includes the mandatory fields: `id`, `base_url`, `sport`, `content_type`, and `refresh_interval_seconds`.
3. Run the full test suite locally using `pytest tests/` and verify that all existing tests pass. For new endpoints, add a corresponding entry in the integration test fixture to validate resolution and mock response shaping.
4. Update the relevant documentation files under the `docs/` directory, especially the user guide if the change affects configuration or CLI behavior. For registry additions, also update the resource list in this README to reflect the change.
5. Submit a pull request against the main branch with a clear description of the change, the motivation, and any potential impact on existing deployments. Ensure that your commit history is clean and atomic.

## 常见问题

**Q: The proxy simulator returns a 502 error when I try to resolve an endpoint. What should I check?**

A: This typically indicates that the requested alias does not exist in the manifest, or that the manifest file is malformed. Run `python -m scoreproxy validate` to check the integrity of `config/manifest.json`. Also verify that the alias you are using matches exactly the `id` field defined in the manifest. If you are using a custom manifest path, ensure it is correctly passed via the `--manifest` option.

**Q: How often does the availability probe run, and can I adjust the frequency?**

A: The default probe interval is 60 seconds for HEAD requests and 300 seconds for full GET checks. These values can be overridden by setting the environment variables `PROBE_HEAD_INTERVAL` and `PROBE_GET_INTERVAL` (values in seconds). Alternatively, you can modify the corresponding fields in `config/default.yaml`. After changing the configuration, restart the proxy server for the new intervals to take effect.

**Q: Is it safe to use the registered endpoints in a production environment with high request volumes?**

A: The registry provided by Project 365Score is a reference index, not a caching or rate-limiting proxy. Production deployments should implement their own circuit breakers, retry policies, and request throttling. We recommend using the local simulator for testing purposes only. For production, always refer to the official documentation of each third-party provider and respect their terms of service and rate limits.

## 许可证

This project is licensed under the terms of the MIT License. See the LICENSE file in the repository root for full text.

> 外链数量: 7 | 生成时间: 2026-08-02 21:19:27
