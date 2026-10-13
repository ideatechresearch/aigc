# AIGC（历史归档）

> [!IMPORTANT]
> **本仓库已基本归档。** 这里保留 AIGC 早期的应用代码、可公开的实验痕迹与数据处理思路，主要用于历史追溯。后续研究、可复现脚本和当前维护内容请前往 **[dooven-prime/aigc-lite](https://github.com/dooven-prime/aigc-lite)**。

`aigc-lite` 是重新梳理边界后的当前项目，不是本仓库代码的原地兼容升级。新需求、问题和贡献请优先在 `aigc-lite` 提出；这里原则上只接受影响归档准确性或安全性的修订。

## 归档范围

此仓库从 [patent_invest](https://github.com/ideatechresearch/patent_invest) 的 `aigc/` 子目录独立出来，保留早期 FastAPI 服务、Agent 与模型调用、企业和文档分析、任务调度及 HTTP/MCP 接口的源码快照。为形成干净的公开历史，新仓库从经过检查的源码重新开始提交；旧仓库的原始提交历史没有复制过来。

真实密钥、本地 YAML、数据库、日志、运行数据、私有部署配置和含敏感信息的临时脚本没有迁入。**不要将本仓库当作可直接部署的生产版本。** 若曾在旧历史中使用真实密钥，应由持有人评估并轮换；删除当前文件不等于清除旧 Git 历史。

魔方、遗传学等 Rime 代码也不再内嵌。AIGC 对 `rime.allele.Allele` 的注册是可选的；早期独立源码见 [ideatechresearch/rime](https://github.com/ideatechresearch/rime)，并以该项目的归档说明为准。

## 历史运行参考

以下仅供复现早期实现，不代表当前受维护的安装流程。需要 Python 3.10+ 以及按所用功能配置 MySQL、Redis 等服务。

```bash
git clone https://github.com/ideatechresearch/aigc.git
cd aigc
python -m venv .venv
pip install -r requirements.txt
python main.py
```

启动前需由部署环境提供 `AIGC_SECRET_KEY`、`AIGC_DATABASE_URI` 和 `AIGC_ASYNC_DATABASE_URI`，或在本地未跟踪的 `config.yaml` 中配置对应字段。`AIGC_REDIS_HOST` 默认为 `localhost`；`redis_aigc` 仅适用于存在该服务名的 Docker 网络，不能作为普通 Windows 本机的默认地址。其他模型密钥与外部服务地址按需提供，切勿提交真实配置。

应用入口是 `main.py`，历史默认端口为 7000。此次归档只做了字节编译和公开文件检查，未对外部数据库、模型服务及端到端流程做运行验收。
