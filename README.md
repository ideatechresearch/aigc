# AIGC

从 `patent_invest` 拆出的 FastAPI 智能分析服务。项目包含模型调用、Agent 协作、企业与文档分析、任务调度及 HTTP/MCP 接口。这个仓库只发布应用代码；部署配置、密钥、数据库、日志和运行数据不随源码发布。

## 本地启动

需要 Python 3.10+，以及按实际使用的功能配置 MySQL、Redis 等外部服务。

```bash
git clone https://github.com/ideatechresearch/aigc.git
cd aigc
python -m venv .venv
pip install -r requirements.txt
python main.py
```

首次启动前，至少提供以下环境变量，或在本地未跟踪的 `config.yaml` 中提供对应的 `Config` 字段：

| 环境变量 | 用途 |
| --- | --- |
| `AIGC_SECRET_KEY` | 会话密钥 |
| `AIGC_DATABASE_URI` | SQLAlchemy 同步数据库地址 |
| `AIGC_ASYNC_DATABASE_URI` | SQLAlchemy 异步数据库地址 |
| `AIGC_REDIS_HOST` | Redis 主机；本机默认 `localhost` |

其他模型密钥、Qdrant 和外部服务地址按需配置。`redis_aigc` 只是特定 Docker 网络中的服务名，直接在 Windows 运行时通常不能解析；请使用本机或实际可达的 Redis 地址。不要提交真实配置或运行数据。

应用入口是 `main.py`，默认监听 7000 端口。FastAPI 文档位于 `/docs`。

## 代码结构

- `agents/`：模型、Agent、检索与提示词逻辑
- `router/`：HTTP 路由
- `service/`、`database.py`：外部服务与数据访问
- `config.py`：环境变量和本地 YAML 的配置入口
- `templates/`、`static/`：现有页面资源

## Rime 已独立

魔方、遗传学等 Rime 代码不再随 AIGC 发布。AIGC 只有一处可选的 `rime.allele.Allele` 工具注册；未安装兼容的独立 Rime 包时会跳过该能力，其他 AIGC 功能不依赖它。早期 Rime 源码见 [ideatechresearch/rime](https://github.com/ideatechresearch/rime)；该仓库已归档，请按其 README 选择当前维护的项目，不要将其历史代码复制回 AIGC。

## 发布说明

本仓库是从旧仓库的 `aigc/` 子目录整理出的独立源码快照，并选择性同步了本地 AIGC 的启动健壮性改动。旧仓库历史可能仍包含旧配置；从旧版本使用过的实际密钥应由其所有者评估并轮换。
