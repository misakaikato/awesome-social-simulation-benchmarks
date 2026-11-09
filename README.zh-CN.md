# Awesome Social Simulation Benchmarks

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![Link check](https://github.com/misakaikato/awesome-social-simulation-benchmarks/actions/workflows/links.yml/badge.svg)](https://github.com/misakaikato/awesome-social-simulation-benchmarks/actions/workflows/links.yml)
[![License: CC0-1.0](https://img.shields.io/badge/license-CC0--1.0-lightgrey.svg)](LICENSE)
[![PRs welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

[English](README.md) · **简体中文**

评测 LLM 驱动的社会模拟所需的基准与真人对照数据，按**验证哪一层**分类，不按发表时间排。

"benchmark"这个词在这个领域指三件不同的事，跨层比较结果是引错数字最常见的方式：

- **L1 个体保真度**：一个 agent 扮一个真人，答案对不对得上那个真人。
- **L2 交互与社交智能**：多个 agent 互动，过程和结果好不好。
- **L3 宏观涌现与现实对齐**：一群 agent 跑起来，群体现象对不对得上真实社会的统计规律。

每个条目都有**数据**一列，写的是能不能拿到真人对照数据、以什么条件拿。挑对照物的时候要看的就是这个，按时间排的列表不记录它。

## 目录

- [L1 个体保真度](#l1-个体保真度)
- [L2 交互与社交智能](#l2-交互与社交智能)
- [L3 宏观涌现与现实对齐](#l3-宏观涌现与现实对齐)
- [真人对照数据](#真人对照数据)
- [复现与科研流程](#复现与科研流程)
- [通用评测基础设施](#通用评测基础设施)
- [相关索引](#相关索引)
- [收录标准](#收录标准)
- [领域现状](#领域现状)
- [参与贡献](#参与贡献)

## L1 个体保真度

| 名字 | 数据 | 说明 |
|---|---|---|
| [When Synthetic Users Fail: A Cross-Domain Benchmark of LLM-Simulated Human Survey Responses](https://arxiv.org/abs/2607.26348) · [代码](https://github.com/ZihanChen1995/when-synthetic-users-fail-a-cross-domain-benchmark-of-llm-simulated-human-survey-responses) | GSS/WVS 评测数据、缓存模型输出和分析代码；完整 WVS 微观数据须按 WVSA 条款另行获取 | 在两个真人调查领域中，将四个 LLM 与非 LLM 基线比较，评测个体问卷回答保真度及人口学特征与态度关系的夸大。 |
| [SimBench](https://arxiv.org/abs/2510.17516) · [数据](https://huggingface.co/datasets/pitehu/SimBench) | 20 个数据集统一格式，HF 可下 | 这一层目前唯一的统一基准，45 个模型跑分，最好的只有 40.80/100 |
| [LLM Agents Grounded in Self-Reports](https://arxiv.org/abs/2411.10109) · [代码](https://github.com/joonspk-research/genagents) | 1052 人深度访谈 + GSS 应答（受限申请） | 原名 "Generative Agent Simulations of 1,000 People"；复现真人 GSS 答案达到真人两周后自我一致性的 85% |
| [OpinionQA](https://arxiv.org/abs/2303.17548) | Pew ATP，1498 题 × 约 9.1 万题-人群对 | 按 9 个人口学维度比对意见分布，群体对齐的事实标准 |
| [GlobalOpinionQA](https://arxiv.org/abs/2306.16388) | WVS + Pew Global Attitudes | 跨国意见分布，测模型默认站在谁的视角说话 |
| [CoMPosT](https://arxiv.org/abs/2310.11501) | 评测方法，无独立数据 | 量化 persona 模拟的"漫画化"；做 L1 之前先读这个失败模式 |
| [Homo Silicus](https://arxiv.org/abs/2301.07543) | 经典经济学实验复刻 | 最早把 LLM 当经济主体跑实验的范式论文 |

## L2 交互与社交智能

| 名字 | 数据 | 说明 |
|---|---|---|
| [SOTOPIA](https://arxiv.org/abs/2310.11667) · [代码](https://github.com/sotopia-lab/sotopia) | 90 个社交场景 + 人类标注 | 目标达成、关系、社会规范等 7 个维度打分，有人评做锚 |
| [SOTOPIA-S4](https://arxiv.org/abs/2504.16122) | 同上 | 上面那套的工程化版：pip 包 + REST + Web，评测维度可自定义 |
| [AgentSense](https://arxiv.org/abs/2410.19346) | 从戏剧剧本抽取的社交场景 | 交互式场景测社交智能 |
| [MultiAgentBench / MARBLE](https://arxiv.org/abs/2503.01935) · [代码](https://github.com/ulab-uiuc/MARBLE) | 协作与竞争任务 + 里程碑 KPI | 同时测协作质量与协调拓扑（星/链/树/图） |
| [Melting Pot](https://arxiv.org/abs/2107.06857) · [代码](https://github.com/google-deepmind/meltingpot) | 50+ substrates，256 个测试场景 | MARL 社会困境的老牌评测集，重点是泛化到陌生同伴 |
| [Concordia](https://github.com/google-deepmind/concordia) | 场景与主持人框架 | Melting Pot 的 LLM 版，配套有 Concordia Contest |
| [AvalonBench](https://github.com/jonathanmli/Avalon-LLM) | Avalon 对局 | 隐藏信息、结盟、欺骗的最小闭环 |
| [SocialGrid](https://arxiv.org/abs/2604.16022) | 具身多智能体网格环境 | 规划能力与社会推理分开计分 |
| [Can Agents Read the Room?](https://arxiv.org/abs/2606.15152) | 多模态社交场景 | 视觉社交智能 |
| [LLMs Can't Handle Peer Pressure](https://arxiv.org/abs/2508.18321) | 多轮群体互动 | 同伴压力下的信念更新，当失败案例集用价值最高 |

## L3 宏观涌现与现实对齐

这一层最薄，多数条目只能在自己的框架里跑。

| 名字 | 数据 | 说明 |
|---|---|---|
| [OASIS](https://arxiv.org/abs/2411.11581) · [代码](https://github.com/camel-ai/oasis) | 百万 agent 社媒模拟，对照真实平台现象 | 信息传播、群体极化、从众效应；最接近宏观对齐的开源实现 |
| [AgentSociety](https://github.com/tsinghua-fib-lab/AgentSociety) | 城市级社会模拟平台，自带实验与评测 | v2 支持 Ray 并行与实验回放 |
| [MiroBench](https://arxiv.org/abs/2606.14715) | 真实世界讨论记录 | 直接用真实讨论当 ground truth，这层里少见 |
| [Shachi](https://arxiv.org/abs/2509.21862) | 模块化 ABM 框架 | 面向涌现集体行为，组件可控可消融 |
| [Validating Generative ABM of Social Norm Enforcement](https://arxiv.org/abs/2507.22049) | 已有实验复现 + 新预测 | 少数走完"先复现已知结果再做未见预测"全流程的工作 |
| [ABM 验证的分层框架](https://dl.acm.org/doi/10.1145/3769857) | 方法论，无数据 | ACM TOMACS 2026；这层共识还在形成，先用它给自己的验证定级 |

## 真人对照数据

调查项目与数据档案，对照得自己拿它们搭。

| 名字 | 数据 | 说明 |
|---|---|---|
| [LLMs can predict the results of social science experiments](https://www.nature.com/articles/s41586-026-10742-x) | 70 个预注册实验，476 个处理效应，105165 名被试 | 模拟应答与真实处理效应相关 r=0.85，未发表研究 r=0.90；目前最适合当 L1 到 L3 之间桥梁的档案 |
| [GSS](https://gss.norc.org/) | 美国综合社会调查，1972 至今 | 长时序态度数据，genagents 验证用的就是它 |
| [Pew American Trends Panel](https://www.pewresearch.org/american-trends-panel/) | 面板调查原始数据 | OpinionQA 的上游 |
| [World Values Survey](https://www.worldvaluessurvey.org/) | 跨国价值观调查 | 跨文化对照的默认选择 |
| [ANES](https://electionstudies.org/) | 美国全国选举研究 | 政治态度与投票行为 |
| [ICPSR](https://www.icpsr.umich.edu/) · [OSF](https://osf.io/) · [Harvard Dataverse](https://dataverse.harvard.edu/) | 社科数据与复现包归档 | 找特定实验的原始数据从这三个入口进 |

## 复现与科研流程

| 名字 | 数据 | 说明 |
|---|---|---|
| [ReplicatorBench](https://arxiv.org/abs/2602.11354) · [代码](https://github.com/CenterForOpenScience/llm-benchmarking) | 复现任务 | 把复现拆成信息抽取、代码生成、结果解读三段分别计分 |

## 通用评测基础设施

跟社会模拟无关，看的是它们怎么组织任务、怎么发布结果。

| 名字 | 说明 |
|---|---|
| [lm-evaluation-harness](https://github.com/EleutherAI/lm-evaluation-harness) | 任务注册与统一跑分的事实标准写法 |
| [HELM](https://crfm.stanford.edu/helm/) · [代码](https://github.com/stanford-crfm/helm) | 多维度评测与结果站点的组织方式 |
| [Croissant](https://mlcommons.org/croissant/) | MLCommons 的数据集元数据标准，记录条目元信息时可以照它写 |

## 相关索引

| 名字 | 说明 |
|---|---|
| [awesome-llm-social-simulation](https://github.com/Wanying-He/awesome-llm-social-simulation) | 按论文时间线收，覆盖面最广 |
| [FudanDISC/SocialAgent](https://github.com/FudanDISC/SocialAgent) | 社交 agent 资源合集 |
| [LLM-Agent-Benchmark-List](https://github.com/zhangxjohn/LLM-Agent-Benchmark-List) | 通用 agent 基准清单，非社会模拟专门 |
| [awesome-LLM-game-agent-papers](https://github.com/git-disl/awesome-LLM-game-agent-papers) | 游戏与博弈类 agent，L2 的补充 |

## 收录标准

- 有公开地址，且链接可达。
- 数据一列要说清楚拿到手的是什么：真人对照数据、合成场景，还是只有评测代码。
- 能归进三层中的一层。三层都归不进去，说明该加一层，在 PR 里说明。

## 领域现状

L1 已被 SimBench 统一，L2 拥挤且同质化，L3 薄且各绑各的框架。带真人宏观对照数据的 L3 基准目前只有个位数，且没有一个是框架无关的。

## 参与贡献

欢迎补条目、纠错、改进描述，见 [CONTRIBUTING.md](CONTRIBUTING.md)。只写一种语言也可以提，维护者会补另一边。
