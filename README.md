# AgentBench

![](./assets/cover.jpg)
<p align="center">
   <a href="https://llmbench.ai" target="_blank">🌐 Website</a> | <a href="https://twitter.com/thukeg" target="_blank">🐦 Twitter</a> | <a href="mailto:agentbench@googlegroups.com">✉️ Google Group</a> | <a href="https://arxiv.org/abs/2308.03688" target="_blank">📃 Paper </a> | <a href="README_cn.md">🌏中文文档</a>
</p> 

<p align="center">
👋 Join our <a href="https://join.slack.com/t/agentbenchcol-huw1944/shared_invite/zt-20ixabcuv-31cFLBAkqGQxQkJqrWVEVg" target="_blank">Slack</a>  for <i>Q & A</i> or <i><b>collaboration</b> on next version of AgentBench</i>!
</p>

## 📌Introducing AgentBench v0.2🎉

You are now browsing AgentBench v0.2. If you wish to use the older version, you can revert to [v0.1](https://github.com/THUDM/AgentBench/tree/v0.1).

Based on [v0.1](https://github.com/THUDM/AgentBench/tree/v0.1), we:
- Updated the framework architecture for easier use and extension
- Adjusted some task settings
- Added test results for more models
- Released the full data for the Dev and Test sets

# AgentBench: Evaluating LLMs as Agents

https://github.com/THUDM/AgentBench/assets/129033897/656eed6e-d9d9-4d07-b568-f43f5a451f04

**AgentBench** is the first benchmark designed to evaluate **LLM-as-Agent** across a diverse spectrum of different
environments. It encompasses 8 distinct environments to provide a more comprehensive evaluation of the LLMs' ability to
operate as autonomous agents in various scenarios. These environments include 5 freshly created domains, namely

- Operating System (OS)
- Database (DB)
- Knowledge Graph (KG)
- Digital Card Game (DCG)
- Lateral Thinking Puzzles (LTP)

as well as 3 recompiled from published datasets:

- House-Holding (HH) ([ALFWorld](https://github.com/alfworld/alfworld))
- Web Shopping (WS) ([WebShop](https://github.com/princeton-nlp/webshop))
- Web Browsing (WB) ([Mind2Web](https://github.com/OSU-NLP-Group/Mind2Web))

![](./assets/agentbench.png)

## Table of Contents

- [Dataset Summary](#dataset-summary)
- [Leaderboard](#leaderboard)
- [Quick Start](#quick-start)
- [Next Steps](#next-steps)
- [Citation](#citation)

## Dataset Summary

We offer two splits for each dataset: Dev and Test. The multi-turn interaction requires an LLMs to generate around 4k
and 13k times respectively.

![](./assets/statistics.png)

## Leaderboard

Here is the scores on test set (standard) results of AgentBench.

![](./assets/leaderboard.png)

While LLMs begin to manifest their proficiency in LLM-as-Agent, gaps between models and the distance towards practical
usability are significant.

![](./assets/intro.png)

## Prerequisites

Install the dependencies.

```bash
pip install -r requirements.txt
```

Also, ensure that Docker is properly installed. And locally, you have images for `mysql` and `ubuntu`.

## Quick Start

This section will guide you on how to quickly use gpt-3.5-turbo-0613 as an agent to launch the `dbbench-std`, `os-std`,
and `kg-std` tasks.
For the specific framework structure, please refer to [Framework Introduction](docs/Introduction_en.md).
For more detailed configuration and launch methods, please check [Configuration Guide](docs/Config_en.md)
and [Program Entrance Guide](docs/Entrance_en.md).

### Configure the Agent

Fill in your OpenAI API Key at the correct location in `configs/agents/openai-chat.yaml`.

You can try using `python -m src.client.agent_test` to check if your Agent is configured correctly.

### Start the task server

Starting the task worker involves specific tasks. Manual starting might be cumbersome; hence, we provide an automated
script.

The assumption for this step is that ports from 5000 to 5015 are available.

```bash
python -m src.start_task -a
```

This will launch five task_workers each for `dbbench-std`, `os-std`, and `kg-std` tasks and automatically connect them
to the controller on port 5000.

### Start the assigner

This step is to actually start the tasks.

If everything is correctly configured so far, you can now initiate the task tests.

```bash
python -m src.assigner
```

## Next Steps

If you wish to launch more tasks or use other models, you can refer to the content
in [Configuration Guide](docs/Config_en.md) and [Program Entrance Guide](docs/Entrance_en.md).

For the environment of the remaining five tasks, you will need to download the Docker images we provide.

```
longinyu/agentbench-ltp
longinyu/agentbench-webshop
longinyu/agentbench-mind2web
longinyu/agentbench-card_game
longinyu/agentbench-alfworld
```

The resource consumption of a single task_worker for the eight tasks is roughly as follows; consider this when
launching:

| Task Name | Start-up Speed | Memory Consumption |
|-----------|----------------|--------------------|
| webshop   | ~3min          | ~15G               |
| mind2web  | ~5min          | ~1G                |
| db        | ~20s           | < 500M             |
| alfworld  | ~10s           | < 500M             |
| card_game | ~5s            | < 500M             |
| ltp       | ~5s            | < 500M             |
| os        | ~5s            | < 500M             |
| kd        | ~5s            | < 500M             |

## Citation

```
@article{liu2023agentbench,
  title   = {AgentBench: Evaluating LLMs as Agents},
  author  = {Xiao Liu and Hao Yu and Hanchen Zhang and Yifan Xu and Xuanyu Lei and Hanyu Lai and Yu Gu and Hangliang Ding and Kaiwen Men and Kejuan Yang and Shudan Zhang and Xiang Deng and Aohan Zeng and Zhengxiao Du and Chenhui Zhang and Sheng Shen and Tianjun Zhang and Yu Su and Huan Sun and Minlie Huang and Yuxiao Dong and Jie Tang},
  year    = {2023},
  journal = {arXiv preprint arXiv: 2308.03688}
}
```
