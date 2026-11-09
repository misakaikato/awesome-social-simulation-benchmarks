# Awesome Social Simulation Benchmarks

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![Link check](https://github.com/misakaikato/awesome-social-simulation-benchmarks/actions/workflows/links.yml/badge.svg)](https://github.com/misakaikato/awesome-social-simulation-benchmarks/actions/workflows/links.yml)
[![License: CC0-1.0](https://img.shields.io/badge/license-CC0--1.0-lightgrey.svg)](LICENSE)
[![PRs welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

**English** · [简体中文](README.zh-CN.md)

Benchmarks and human ground-truth data for evaluating LLM-driven social simulation, sorted by **which layer of validation they support** rather than by publication date.

The word "benchmark" means three different things in this field. Comparing results across layers is how people end up citing an unrelated number:

- **L1 — Individual fidelity.** One agent plays one real person. Does it answer the way that person answered?
- **L2 — Interaction and social intelligence.** Several agents interact. Is the interaction any good?
- **L3 — Emergent macro alignment.** A population runs. Do the collective patterns match real-world statistical regularities?

Every entry carries a **Data** column saying whether real human comparison data is obtainable, and on what terms. That is what you need when you pick something to validate against, and a date-sorted list does not record it.

## Contents

- [L1 Individual Fidelity](#l1-individual-fidelity)
- [L2 Interaction and Social Intelligence](#l2-interaction-and-social-intelligence)
- [L3 Emergent Macro Alignment](#l3-emergent-macro-alignment)
- [Human Ground-Truth Data](#human-ground-truth-data)
- [Replication and Research Workflow](#replication-and-research-workflow)
- [General Evaluation Infrastructure](#general-evaluation-infrastructure)
- [Related Indexes](#related-indexes)
- [Inclusion Criteria](#inclusion-criteria)
- [State of the Field](#state-of-the-field)
- [Contributing](#contributing)

## L1 Individual Fidelity

| Name | Data | Notes |
|---|---|---|
| [When Synthetic Users Fail: A Cross-Domain Benchmark of LLM-Simulated Human Survey Responses](https://arxiv.org/abs/2607.26348) · [code](https://github.com/ZihanChen1995/when-synthetic-users-fail-a-cross-domain-benchmark-of-llm-simulated-human-survey-responses) | GSS/WVS evaluation data, cached model outputs, and analysis code; full WVS microdata require separate access under WVSA terms | Tests individual survey-response fidelity and demographic over-determination across four LLMs and two human-survey domains against non-LLM baselines. |
| [SimBench](https://arxiv.org/abs/2510.17516) · [dataset](https://huggingface.co/datasets/pitehu/SimBench) | 20 datasets unified, downloadable from HF | The only unified benchmark at this layer. 45 models scored; the best reaches 40.80/100 |
| [LLM Agents Grounded in Self-Reports](https://arxiv.org/abs/2411.10109) · [code](https://github.com/joonspk-research/genagents) | 1,052 in-depth interviews + GSS responses (restricted access) | Formerly "Generative Agent Simulations of 1,000 People". Agents match participants' GSS answers at 85% of the participants' own two-week self-consistency |
| [OpinionQA](https://arxiv.org/abs/2303.17548) | Pew ATP, 1,498 questions across ~91k question-subgroup pairs | Opinion distributions compared across 9 demographic traits. The de facto standard for group alignment |
| [GlobalOpinionQA](https://arxiv.org/abs/2306.16388) | WVS + Pew Global Attitudes | Cross-national opinion distributions; measures whose default perspective a model speaks from |
| [CoMPosT](https://arxiv.org/abs/2310.11501) | Method, no standalone dataset | Quantifies caricature in persona simulation. Read this failure mode before building anything at L1 |
| [Homo Silicus](https://arxiv.org/abs/2301.07543) | Classic economics experiments, re-run | The paper that started treating LLMs as economic subjects |

## L2 Interaction and Social Intelligence

| Name | Data | Notes |
|---|---|---|
| [SOTOPIA](https://arxiv.org/abs/2310.11667) · [code](https://github.com/sotopia-lab/sotopia) | 90 social scenarios + human annotations | Seven scoring dimensions including goal completion, relationship, and social rules, anchored to human judgment |
| [SOTOPIA-S4](https://arxiv.org/abs/2504.16122) | Same | The productized version: pip package, REST API, web UI, custom evaluation dimensions |
| [AgentSense](https://arxiv.org/abs/2410.19346) | Scenarios extracted from dramatic scripts | Interactive scenarios for social intelligence |
| [MultiAgentBench / MARBLE](https://arxiv.org/abs/2503.01935) · [code](https://github.com/ulab-uiuc/MARBLE) | Collaboration and competition tasks with milestone KPIs | Scores collaboration quality alongside coordination topology (star, chain, tree, graph) |
| [Melting Pot](https://arxiv.org/abs/2107.06857) · [code](https://github.com/google-deepmind/meltingpot) | 50+ substrates, 256 test scenarios | The established MARL social-dilemma suite. The point is generalization to unfamiliar co-players |
| [Concordia](https://github.com/google-deepmind/concordia) | Scenario and game-master framework | The LLM counterpart to Melting Pot, with the Concordia Contest built on it |
| [AvalonBench](https://github.com/jonathanmli/Avalon-LLM) | Resistance: Avalon matches | Minimal closed loop for hidden information, coalition forming, and deception |
| [SocialGrid](https://arxiv.org/abs/2604.16022) | Embodied multi-agent grid environments | Planning and social reasoning scored separately |
| [Can Agents Read the Room?](https://arxiv.org/abs/2606.15152) | Multimodal social scenarios | Visual social intelligence |
| [LLMs Can't Handle Peer Pressure](https://arxiv.org/abs/2508.18321) | Multi-round group interactions | Belief updating under peer pressure. Most valuable as a failure-case collection |

## L3 Emergent Macro Alignment

The thinnest layer. Most entries only run inside their own framework.

| Name | Data | Notes |
|---|---|---|
| [OASIS](https://arxiv.org/abs/2411.11581) · [code](https://github.com/camel-ai/oasis) | Million-agent social media simulation, compared against real platform phenomena | Information spread, group polarization, herd behavior. The closest thing to open macro alignment |
| [AgentSociety](https://github.com/tsinghua-fib-lab/AgentSociety) | City-scale simulation platform with built-in experiments and evaluation | v2 adds Ray-based parallelism and experiment replay |
| [MiroBench](https://arxiv.org/abs/2606.14715) | Transcripts of real-world discussions | Uses real discussions as ground truth, which is rare at this layer |
| [Shachi](https://arxiv.org/abs/2509.21862) | Modular ABM framework | Aimed at emergent collective behavior, with controllable and ablatable components |
| [Validating Generative ABM of Social Norm Enforcement](https://arxiv.org/abs/2507.22049) | Replication of known experiments plus novel predictions | One of the few that completes the loop from replication to out-of-sample prediction |
| [Hierarchical ABM Validation Framework](https://dl.acm.org/doi/10.1145/3769857) | Methodology, no data | ACM TOMACS 2026. Consensus at this layer is still forming; use it to declare your own validation tier |

## Human Ground-Truth Data

Survey programs and data archives. You build the comparison out of these yourself.

| Name | Data | Notes |
|---|---|---|
| [LLMs can predict the results of social science experiments](https://www.nature.com/articles/s41586-026-10742-x) | 70 pre-registered experiments, 476 treatment effects, 105,165 participants | Simulated responses correlate with real treatment effects at r=0.85, and r=0.90 on unpublished studies. The best available bridge between L1 and L3 |
| [GSS](https://gss.norc.org/) | US General Social Survey, 1972 to present | Long-horizon attitude data; the source genagents validates against |
| [Pew American Trends Panel](https://www.pewresearch.org/american-trends-panel/) | Raw panel survey data | Upstream of OpinionQA |
| [World Values Survey](https://www.worldvaluessurvey.org/) | Cross-national values survey | The default choice for cross-cultural comparison |
| [ANES](https://electionstudies.org/) | American National Election Studies | Political attitudes and voting behavior |
| [ICPSR](https://www.icpsr.umich.edu/) · [OSF](https://osf.io/) · [Harvard Dataverse](https://dataverse.harvard.edu/) | Social science data and replication package archives | Where to look for the raw data behind a specific experiment |

## Replication and Research Workflow

| Name | Data | Notes |
|---|---|---|
| [ReplicatorBench](https://arxiv.org/abs/2602.11354) · [code](https://github.com/CenterForOpenScience/llm-benchmarking) | Replication tasks | Scores extraction, code generation, and interpretation as three separate stages |

## General Evaluation Infrastructure

Unrelated to social simulation; relevant for how they organize tasks and publish results.

| Name | Notes |
|---|---|
| [lm-evaluation-harness](https://github.com/EleutherAI/lm-evaluation-harness) | The de facto pattern for task registration and unified scoring |
| [HELM](https://crfm.stanford.edu/helm/) · [code](https://github.com/stanford-crfm/helm) | How to organize multi-dimensional evaluation and publish results |
| [Croissant](https://mlcommons.org/croissant/) | MLCommons dataset metadata standard. Worth following when recording entry metadata |

## Related Indexes

| Name | Notes |
|---|---|
| [awesome-llm-social-simulation](https://github.com/Wanying-He/awesome-llm-social-simulation) | Sorted by publication timeline; the broadest coverage |
| [FudanDISC/SocialAgent](https://github.com/FudanDISC/SocialAgent) | Social agent resource collection |
| [LLM-Agent-Benchmark-List](https://github.com/zhangxjohn/LLM-Agent-Benchmark-List) | General agent benchmarks, not specific to social simulation |
| [awesome-LLM-game-agent-papers](https://github.com/git-disl/awesome-LLM-game-agent-papers) | Game and strategic agents; a supplement to L2 |

## Inclusion Criteria

- Publicly addressable, and the link resolves.
- The Data column states what you actually get: real human comparison data, synthetic scenarios, or evaluation code only.
- It fits one of the three layers. An entry that fits none of them means the taxonomy needs another layer; say so in the PR.

## State of the Field

L1 has been unified by SimBench. L2 is crowded and increasingly homogeneous. L3 is thin, and each entry is bound to its own framework. Benchmarks at L3 with real macro-level human comparison data still number in the single digits, and none of them are framework-agnostic.

## Contributing

Additions, corrections, and better descriptions are all welcome. See [CONTRIBUTING.md](CONTRIBUTING.md). Submitting in one language only is fine; a maintainer will fill in the other.
