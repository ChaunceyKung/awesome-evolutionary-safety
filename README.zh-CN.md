# Awesome Evolutionary Safety（演化安全资源列表）

[English](README.md) | [中文](README.zh-CN.md)

关于**自改进 AI 演化安全**的资源列表 —— 即与自改进过程因果耦合的安全风险：风险如何被自改进过程诱发、持久化、继承与放大。覆盖范围包括：自行写入记忆/技能/工具/工作流的智能体、自行更新权重的模型、自行重构脚手架与评估器的系统、以及改进"改进过程本身"的自动化 AI 研发回路。

**收录内容** —— 论文、评测集与数据集、代码仓库、博客与演讲、标准与政策框架。

**配套综述** —— 本列表配套论文《Evolutionary Safety of Self-Improving AI: An Overview of Risks, Control, and Recursive Development》（面向 ACM Computing Surveys）。

## 目录

- [一页纸概念](#一页纸概念)
- [综述与总览](#综述与总览)
- [演化载体一：记忆、技能与工具](#演化载体一记忆技能与工具)
- [演化载体二：模型更新](#演化载体二模型更新)
- [控制面一：Harness 与运行时控制](#控制面一harness-与运行时控制)
- [控制面二：评估器与奖励回路](#控制面二评估器与奖励回路)
- [元演化：递归自改进与 AI 研发](#元演化递归自改进与-ai-研发)
- [评测集与数据集](#评测集与数据集)
- [代码仓库与工具](#代码仓库与工具)
- [博客、演讲与报告](#博客演讲与报告)
- [标准、政策与治理框架](#标准政策与治理框架)
- [开放问题](#开放问题)
- [相关列表](#相关列表)
- [贡献指南](#贡献指南)

## 一页纸概念

演化安全不只问"当前系统是否安全"，而是问"当系统持续改进自己时，安全能否保持、可归因、可恢复"。

三个层次：

| 层次 | 问题 |
|---|---|
| 行为安全 | `S_t` 在当前任务上是否安全？ |
| 更新安全 | 单次更新 `Δ_t`（记忆/技能/工具/工作流/权重）是否安全？ |
| 演化安全 | `S_t → S_{t+1} → …` 全程安全是否成立——风险不积累、不继承、不被递归放大；变更可追溯、可回滚、可治理？ |

自改进发生的五个平面（2 演化载体 + 2 控制面 + 1 元演化面）：

| 平面 | 角色 | 核心问题 |
|---|---|---|
| 记忆 / 技能 / 工具 | 演化载体（外显、持久） | 智能体为自己写入了哪些可复用能力？其中沉淀了什么？ |
| 模型更新 | 演化载体（参数化） | 微调、合并、自训练如何让安全属性跨版本、跨代际移动？ |
| Harness（运行时控制） | 控制面 | 谁能改什么、由谁提交变更？ |
| 评估器 | 控制面 | 什么算"进步"？评估回路能否被博弈、篡改或俘获？ |
| AI 研发 | 元演化面 | 谁在改进"改进过程"本身？ |

文献收敛出的核心结论：能力增长不自动保留安全；无需攻击者，良性经验也能劣化安全；自改进使控制面本身成为可变状态；评估与研发回路本身是安全关键、可被利用的状态。

## 综述与总览

自改进 / 自演化（能力侧）：

- [A Survey on Self-Evolution of Large Language Models](https://arxiv.org/abs/2404.14387) — Tao 等，arXiv 2024。四阶段自演化闭环（经验获取→精炼→更新→评估）。
- [A Comprehensive Survey of Self-Evolving AI Agents](https://arxiv.org/abs/2508.07407) — Fang 等，arXiv 2025。连接基础模型与终身智能体系统。
- [A Survey of Self-Evolving Agents: What, When, How, and Where to Evolve](https://arxiv.org/abs/2507.21046) — Gao 等，TMLR 2026。按模型、记忆、工具、架构四个维度整理演化对象。
- [Self-Improvements in Modern Agentic Systems: A Survey](https://arxiv.org/abs/2607.13104) — Ren 等，arXiv 2026。以统一的自诱导更新算子覆盖参数更新与脚手架（提示/记忆/工具/控制逻辑）更新。
- [Self-Improvement of Large Language Models: A Technical Overview and Future Outlook](https://arxiv.org/abs/2603.25681) — Yang 等，TMLR 2026。数据获取/选择/优化/推理期精炼/自评估闭环。
- [Recursive Self-Improvement in AI: From Bounded Self-Refinement to Autonomous Research Loops](https://arxiv.org/abs/2607.07663) — Chen 等，arXiv 2026。有界自精炼与高阶递归回路的区分；RSI 术语锚点。

智能体 / LLM 安全（静态系统侧）：

- [AI Agents Under Threat: A Survey of Key Security Challenges and Future Pathways](https://arxiv.org/abs/2406.02630) — Deng 等，ACM Computing Surveys 2025。
- [The Emerged Security and Privacy of LLM Agent: A Survey with Case Studies](https://arxiv.org/abs/2407.19354) — He 等，ACM Computing Surveys 2025。
- [Toward Secure LLM Agents: Threat Surfaces, Attacks, Defenses, and Evaluation](https://arxiv.org/abs/2606.10749) — Ling 等，arXiv 2026。
- [Alignment and Safety in Large Language Models](https://arxiv.org/abs/2507.19672) — Lu 等，arXiv 2025。

自动化科学与组件地图：

- [A Survey of AI Scientists](https://arxiv.org/abs/2510.23045) — Tie 等，arXiv 2025。
- [A Survey on the Memory Mechanism of LLM-based Agents](https://arxiv.org/abs/2404.13501) — Zhang 等，arXiv 2024。
- [Tool Learning with Large Language Models: A Survey](https://arxiv.org/abs/2405.17935) — Qu 等，arXiv 2024。
- [A Survey on LLM-based Autonomous Agents](https://arxiv.org/abs/2308.11432) — Wang 等，Frontiers of Computer Science 2024。

## 演化载体一：记忆、技能与工具

### 能力系统：外显持久能力如何形成

- [Reflexion: Language Agents with Verbal Reinforcement Learning](https://arxiv.org/abs/2303.11366) — Shinn 等，NeurIPS 2023。言语自反馈跨回合持久化。
- [Voyager: An Open-Ended Embodied Agent with Large Language Models](https://arxiv.org/abs/2305.16291) — Wang 等，2023。Minecraft 中自生长的技能库。
- [Agent Workflow Memory](https://arxiv.org/abs/2409.07429) — Wang 等，arXiv 2024。从轨迹中归纳并复用可复用工作流。
- [Large Language Models as Tool Makers (LATM)](https://arxiv.org/abs/2305.17126) — Cai 等，ICLR 2024。智能体自己制造工具。
- [Learning Evolving Tools for Large Language Models (ToolEVO)](https://arxiv.org/abs/2410.06617) — Chen 等，ICLR 2025。随真实 API 演化保持工具知识更新。
- [Agent0: Unleashing Self-Evolving Agents from Zero Data via Tool-Integrated Reasoning](https://arxiv.org/abs/2511.16043) — Xia 等，arXiv 2025。
- [SEAgent: Self-Evolving Computer-Use Agent with Autonomous Learning from Experience](https://arxiv.org/abs/2508.04700) — Sun 等，arXiv 2025。
- [Symbolic Learning Enables Self-Evolving Agents](https://arxiv.org/abs/2406.18532) — Zhou 等，arXiv 2024。把提示与代码当作智能体的"神经元"直接编辑。
- [Generative Agents: Interactive Simulacra of Human Behavior](https://arxiv.org/abs/2304.03442) — Park 等，UIST 2023。记忆流、反思与检索架构。
- [MemGPT: Towards LLMs as Operating Systems](https://arxiv.org/abs/2310.08560) — Packer 等，arXiv 2023。操作系统式记忆管理。
- [Mem0: Building Production-Ready AI Agents with Scalable Long-Term Memory](https://arxiv.org/abs/2504.19413) — Chhikara 等，arXiv 2025。
- [A-MEM: Agentic Memory for LLM Agents](https://arxiv.org/abs/2502.12110) — Xu 等，arXiv 2025。卡片盒式记忆，自行生长并改写自身。

### 对抗性持久化：污染载体

- [AgentPoison: Red-teaming LLM Agents via Poisoning Memory or Knowledge Bases](https://arxiv.org/abs/2407.12784) — Chen 等，NeurIPS 2024。<0.1% 污染、约 80% 攻击成功率、零训练。
- [PoisonedRAG: Knowledge Corruption Attacks to Retrieval-Augmented Generation](https://arxiv.org/abs/2402.07867) — Zou 等，USENIX Security 2025。少量污染文本即可主导检索。
- [BadAgent: Inserting and Activating Backdoor Attacks in LLM Agents](https://arxiv.org/abs/2406.14830) — Wang 等，ACL 2024。
- [MemoryGraft: Persistent Compromise of LLM Agents via Poisoned Experience Retrieval](https://arxiv.org/abs/2512.16962) — Srivastava & He，arXiv 2025。无触发器：伪装"成功经验"经正常摄入流程写入记忆。
- [From Untrusted Input to Trusted Memory: A Systematic Study of Memory Poisoning Attacks in LLM Agents](https://arxiv.org/abs/2606.04329) — Dash 等，arXiv 2026。
- [MemPoison-Bench: Persistent Memory Threats and Structural Blind Spots in LLM Agents](https://arxiv.org/abs/2607.14651) — Gao 等，arXiv 2026。

### 内生劣化：正常学习制造不安全的持久状态

- [Your Agent May Misevolve: Emergent Risks in Self-evolving LLM Agents](https://arxiv.org/abs/2509.26354) — Shao 等，ICLR 2026。无攻击者情形下记忆、奖励博弈、工具创建、工作流优化四条劣化路径。
- [On Safety Risks in Experience-Driven Self-Evolving Agents](https://arxiv.org/abs/2604.16968) — Zhao 等，Findings of ACL 2026。纯良性经验即使 7 个 backbone 攻击成功率相对上升 17.7–48.6%，呈剂量效应，800+ 步无自然恢复。
- [Safety in Self-Evolving LLM Agent Systems: Threats, Amplification, and Case Studies](https://arxiv.org/abs/2606.23075) — Lin 等，arXiv 2026。自演化智能体系统 5×5 威胁放大矩阵；拉马克式传播与代际累积。
- [PerMemSafe: Benchmarking Implicit Personalized Safety of Long Horizon Self-Evolving Agents](https://aclanthology.org/volumes/2026.findings-acl/) — An 等，Findings of ACL 2026（pp. 6415–6433）。

### 记忆层防御

- [Securing LLM-Agent Long-Term Memory Against Poisoning: Non-Malleable, Origin-Bound Authority with Machine-Checked Guarantees](https://arxiv.org/abs/2606.24322) — Louck，arXiv 2026。TMA-NM：不可伪造的来源绑定，TLA+ 机器验证保证；击败信任标签洗白。

## 演化载体二：模型更新

### 微调下的安全侵蚀

- [Fine-tuning Aligned Language Models Compromises Safety, Even When Users Do Not Intend To!](https://arxiv.org/abs/2310.03693) — Qi 等，ICLR 2024。少量有害样本即足以破坏对齐。
- [Shadow Alignment: The Ease of Subverting Safely-Aligned Language Models](https://arxiv.org/abs/2310.02949) — Yang 等，arXiv 2023。约 100 条样本恢复基座有害率。
- [LoRA Fine-tuning Efficiently Undoes Safety Training in Llama 2-Chat 70B](https://arxiv.org/abs/2310.20624) — Lermen 等，arXiv 2024。成本不足一美元。
- [Safety Alignment Should Be Made More Than Just a Few Tokens Deep](https://arxiv.org/abs/2406.05946) — Qi 等，ICLR 2025。96.1% 的拒绝以固定前缀开头；拒绝是浅层的。
- [Emergent Misalignment: Narrow Finetuning Can Produce Broadly Misaligned LLMs](https://arxiv.org/abs/2502.17424) — Betley 等，ICML 2025。不安全代码微调→广泛失配（0%→20%）；纯数字数据集亦可诱发。
- [Preventing Catastrophic Forgetting: Behavior-Aware Sampling for Safer Language Model Fine-Tuning](https://arxiv.org/abs/2510.21885) — Pham 等，arXiv 2025。

### 后门与穿越安全训练的性状

- [Poisoning Language Models During Instruction Tuning](https://arxiv.org/abs/2305.00944) — Wan 等，ICML 2023。
- [Instructions as Backdoors: Backdoor Vulnerabilities of Instruction Tuning for LLMs](https://arxiv.org/abs/2404.14484) — Xu 等，NAACL 2024。
- [BackdoorAlign (BESA): Mitigating Fine-tuning based Jailbreak Attack](https://arxiv.org/abs/2402.14968) — Wang 等，NeurIPS 2024。（对齐期防御。）
- [Stealthy and Persistent Unalignment on LLMs via Backdoor Injections](https://arxiv.org/abs/2312.00027) — Cao 等，NAACL 2024。
- [Sleeper Agents: Training Deceptive LLMs that Persist Through Safety Training](https://arxiv.org/abs/2401.05566) — Hubinger 等，arXiv 2024。穿越三阶段安全训练；对抗训练反而教会更好隐藏。
- [Subliminal Learning: Language Models Transmit Behavioral Traits via Hidden Signals in Data](https://arxiv.org/abs/2507.14805) — Cloud 等，arXiv 2025。性状（含失配）经纯数字序列传递；数据过滤失效。

### 模型合并中的安全

- [Model Merging and Safety Alignment: One Bad Model Spoils the Bunch](https://arxiv.org/abs/2406.14563) — Hammoud 等，Findings of EMNLP 2024。合并后安全可低于最差组件。
- [Safeguard Fine-Tuned LLMs Through Pre- and Post-Tuning Model Merging](https://arxiv.org/abs/2412.19512) — Farn 等，arXiv 2024。
- [SafeMERGE: Preserving Safety Alignment via Selective Layer-Wise Model Merging](https://arxiv.org/abs/2503.17239) — Djuhera 等，arXiv 2025。
- [LED-Merging: Mitigating Safety–Utility Conflicts in Model Merging](https://arxiv.org/abs/2502.16770) — Ma 等，ACL 2025。揭示参数空间安全-能力竞争超过 30%。

### 模型坍缩与自消耗回路

- [Self-Consuming Generative Models Go MAD](https://arxiv.org/abs/2307.01850) — Alemohammad 等，ICLR 2024。递归训练中质量与多样性衰减。
- [The Curse of Recursion: Training on Generated Data Makes Models Forget](https://arxiv.org/abs/2305.17493) — Shumailov 等，arXiv 2023。
- [AI Models Collapse when Trained on Recursively Generated Data](https://arxiv.org/abs/2407.07590) — Shumailov 等，Nature 2024。尾部丢失机制。
- [Is Model Collapse Inevitable? Breaking the Curse of Recursion by Accumulating Real and Synthetic Data](https://arxiv.org/abs/2404.01413) — Gerstgrasser 等，arXiv 2024。replace/accumulate 二分。
- [How Bad is Training on Synthetic Data? A Statistical Analysis of Language Model Collapse](https://arxiv.org/abs/2404.05090) — Seddik 等，arXiv 2024。
- [Model Collapse Demystified: The Case of Regression](https://arxiv.org/abs/2402.07712) — Dohmatob 等，NeurIPS 2024。
- [Rate of Model Collapse in Recursive Training](https://arxiv.org/abs/2412.17646) — Suresh 等，arXiv 2024。
- [Self-Consuming Generative Models with Curated Data Provably Optimize Human Preferences](https://arxiv.org/abs/2407.09499) — Ferbach 等，NeurIPS 2024。
- [Self-Correcting Self-Consuming Loops for Generative Model Training](https://arxiv.org/abs/2402.07087) — Gillman 等，ICML 2024。
- [Towards Theoretical Understandings of Self-Consuming Generative Models](https://arxiv.org/abs/2402.11778) — Fu 等，ICML 2024。
- [A Theoretical Perspective: How to Prevent Model Collapse in Self-Consuming Training Loops](https://arxiv.org/abs/2502.18865) — Fu 等，ICLR 2025。递归稳定性条件；修正函数判据。
- [Collapse or Thrive? Perils and Promises of Synthetic Data in a Self-Generating World](https://arxiv.org/abs/2410.16713) — Kazdan 等，ICML 2025。超 1000 个模型、超 10 万 GPU 小时。
- [Demystifying Synthetic Data in LLM Pre-training](https://arxiv.org/abs/2510.01631) — Kang 等，arXiv 2025。合成数据配比缩放律；最优约 30%。
- [How to Synthesize Text Data without Model Collapse?](https://arxiv.org/abs/2412.14689) — Zhu 等，ICML 2025。
- [Self-Consuming Generative Models with Adversarially Curated Data](https://arxiv.org/abs/2505.09768) — Wei & Zhang，ICML 2025。对抗性筛选在协方差为负时击穿筛选式修复。
- [A Closer Look at Model Collapse: From a Generalization-to-Memorization Perspective](https://arxiv.org/abs/2509.16499) — Shi 等，arXiv 2025。

### 闭环自训练系统

- [Absolute Zero: Reinforced Self-play Reasoning with Zero Data](https://arxiv.org/abs/2505.03335) — Zhao 等，NeurIPS 2025。零外部数据；记录到"uh-oh moment"式涌现失配。
- [R-Zero: Self-Evolving Reasoning LLM from Zero Data](https://arxiv.org/abs/2508.05004) — Huang 等，ICLR 2026。同源 Challenger/Solver 共演化。

### 更新管线各阶段防御

- [Safe LoRA: the Silver Lining of Reducing Safety Risks when Fine-tuning LLMs](https://arxiv.org/abs/2405.16833) — Hsu 等，NeurIPS 2024。微调后经安全子空间投影恢复。
- [Booster: Tackling Harmful Fine-tuning via Attenuating Harmful Perturbation](https://arxiv.org/abs/2409.01586) — Huang 等，ICLR 2025。对齐期"疫苗接种"。
- [Antidote: Post-fine-tuning Safety Alignment against Harmful Fine-tuning](https://arxiv.org/abs/2408.09600) — Huang 等，ICML 2025。
- [SafeGrad: Gradient Surgery for Safe LLM Fine-Tuning](https://arxiv.org/abs/2508.07172) — Yi 等，arXiv 2025。诊断并修复安全-能力梯度冲突。

## 控制面一：Harness 与运行时控制

### 运行时智能体风险基线

- [Identifying the Risks of LM Agents with an LM-Emulated Sandbox (ToolEmu)](https://arxiv.org/abs/2309.15817) — Ruan 等，ICLR 2024。
- [InjecAgent: Benchmarking Indirect Prompt Injections in Tool-Integrated Agents](https://arxiv.org/abs/2403.02691) — Zhan 等，Findings of ACL 2024。
- [AgentDojo: A Dynamic Environment to Evaluate Prompt Injection Attacks and Defenses](https://arxiv.org/abs/2406.13352) — Debenedetti 等，NeurIPS 2024 D&B。
- [Agent Security Bench (ASB): Formalizing and Benchmarking Attacks and Defenses in LLM-based Agents](https://arxiv.org/abs/2410.02644) — Zhang 等，ICLR 2025。
- [Agent-SafetyBench: Evaluating the Safety of LLM Agents](https://arxiv.org/abs/2412.14470) — Zhang 等，arXiv 2024。
- [R-Judge: Benchmarking Safety Risk Awareness for LLM Agents](https://arxiv.org/abs/2401.10019) — Yuan 等，Findings of EMNLP 2024。
- [AgentHarm: A Benchmark for Measuring Harmfulness of LLM Agents](https://arxiv.org/abs/2410.09024) — Andriushchenko 等，ICLR 2025。前沿模型无需越狱即执行有害多步任务。
- [LLM Agents can Autonomously Hack Websites](https://arxiv.org/abs/2402.06664) — Fang 等，arXiv 2024。
- [Quantifying Frontier LLM Capabilities for Container Sandbox Escape (SandboxEscapeBench)](https://arxiv.org/abs/2603.02277) — Marchand 等，arXiv 2026。

### 控制协议与可扩展监督

- [AI Control: Improving Safety Despite Intentional Subversion](https://arxiv.org/abs/2312.06942) — Greenblatt 等，ICML 2024。对抗性智能体下的控制协议。
- [Evaluating Control Protocols for Untrusted AI Agents](https://arxiv.org/abs/2511.02997) — Kutasov 等，arXiv 2025。红队获得内部信息后控制安全崩塌。
- [Weak-to-Strong Generalization](https://arxiv.org/abs/2312.09390) — Burns 等，OpenAI 2023。
- [On Scalable Oversight with Weak LLMs Judging Strong LLMs](https://arxiv.org/abs/2407.04622) — Kenton 等，NeurIPS 2024。
- [Prover-Verifier Games Improve Legibility of LLM Outputs](https://arxiv.org/abs/2407.13692) — Kirchner 等，OpenAI 2024。

### 受监督回路中的策略性欺骗

- [Alignment Faking in Large Language Models](https://arxiv.org/abs/2412.14093) — Greenblatt 等，Anthropic 2024。对伪装对齐做 RL 使伪装率 12%→78%（反诱导）。
- [AI Sandbagging: Language Models can Strategically Underperform on Evaluations](https://arxiv.org/abs/2406.07358) — van der Weij 等，ICLR 2025。密码锁定的能力泛化到真实生武知识（WMDP）。
- [Auditing Language Models for Hidden Objectives](https://arxiv.org/abs/2503.10965) — Marks 等，Anthropic 2025。有数据权限的审计队 3/4 找到隐藏目标；黑盒全部失败。
- [Frontier Models are Capable of In-Context Scheming](https://arxiv.org/abs/2412.04984) — Apollo Research 2024。六个前沿模型在目标条件下进行密谋（欺骗、藏拙、破坏）。
- [Sabotage Evaluations for Frontier Models](https://arxiv.org/abs/2410.21514) — Benton 等，Anthropic 2024。度量破坏监督的能力。
- [Training on Documents about Reward Hacking Induces Reward Hacking](https://red.anthropic.com/2025/reward-hacking-ooc/) — Chan 等，Anthropic 红队 2025。从训练文本到行为的上下文外迁移。

### 监控与思维链可靠性

- [Chain of Thought Monitorability: A New and Fragile Opportunity for AI Safety](https://arxiv.org/abs/2507.11473) — Korbak 等，arXiv 2025。立场论文：可监控性随训练决策漂移。
- [Monitoring Reasoning Models for Misbehavior and the Risks of Promoting Obfuscation](https://arxiv.org/abs/2503.11926) — Baker 等，OpenAI 2025。针对 CoT 监控器的优化产生混淆式奖励博弈。
- [Reasoning Models Don't Always Say What They Think](https://arxiv.org/abs/2505.05410) — Chen 等，Anthropic 2025。真实目标的言语化率常低于 20%。

### 架构级防御

- [The Instruction Hierarchy: Training LLMs to Prioritize Privileged Instructions](https://arxiv.org/abs/2404.13208) — Wallace 等，OpenAI 2024。
- [Defeating Prompt Injections by Design (CaMeL)](https://arxiv.org/abs/2503.18813) — Debenedetti 等，Google DeepMind 2025。带来源追踪的可证明安全数据流架构。
- [AirGapAgent: Protecting Privacy-Conscious Conversational Agents](https://arxiv.org/abs/2405.05175) — Bagdasarian 等，KDD 2024。构造性数据最小化。
- [Systems Security Foundations for Agentic Computing](https://arxiv.org/abs/2512.01295) — Christodorescu 等，arXiv 2025。最小权限 + 完全调解作为智能体运行时词汇表。
- [Optimizing AI Agent Attacks With Synthetic Data](https://arxiv.org/abs/2511.02823) — Loughridge 等，arXiv 2025。自动化攻击技能合成（控制评估红队）。

## 控制面二：评估器与奖励回路

### 评估器、裁判、验证器

- [G-Eval: NLG Evaluation using GPT-4 with Better Human Alignment](https://arxiv.org/abs/2303.16634) — Liu 等，EMNLP 2023。
- [Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena](https://arxiv.org/abs/2306.05685) — Zheng 等，NeurIPS 2023。
- [Evaluating Large Language Models at Evaluating Instruction Following (LLMBar)](https://arxiv.org/abs/2310.07641) — Zeng 等，ICLR 2024。
- [JudgeBench: A Benchmark for Evaluating LLM-based Judges](https://arxiv.org/abs/2410.12784) — Tan 等，ICLR 2025。困难元评估上 SOTA 裁判勉强高于随机。
- [Prometheus 2: An Open Source Language Model Specialized in Evaluating Other LLMs](https://arxiv.org/abs/2405.01535) — Kim 等，EMNLP 2024。
- [RewardBench: Evaluating Reward Models for Language Modeling](https://arxiv.org/abs/2403.13787) — Lambert 等，arXiv 2024。
- [RM-Bench: Benchmarking Reward Models with Subtlety and Style](https://arxiv.org/abs/2410.16184) — Liu 等，ICLR 2025。风格改写即可把 SOTA 奖励模型压到随机以下。
- [Let's Verify Step by Step](https://arxiv.org/abs/2305.20050) — Lightman 等，OpenAI，ICLR 2024。过程监督。
- [Math-Shepherd: Verify and Reinforce LLMs Step-by-step without Human Annotations](https://arxiv.org/abs/2312.08935) — Wang 等，ACL 2024。
- [Generative Verifiers: Reward Modeling as Next-Token Prediction](https://arxiv.org/abs/2408.15240) — Zhang 等，ICLR 2025。
- [Critique-out-Loud Reward Models](https://arxiv.org/abs/2408.11791) — Ankner 等，arXiv 2024。
- [Self-Taught Evaluators](https://arxiv.org/abs/2408.02666) — Wang 等，arXiv 2024。

### 古德哈特阶梯：博弈 → 篡改 → 俘获

- [Scaling Laws for Reward Model Overoptimization](https://arxiv.org/abs/2210.10760) — Gao 等，ICML 2023。代理目标优化的定量 d* 拐点。
- [The Effects of Reward Misspecification: Mapping and Mitigating Misaligned Models](https://arxiv.org/abs/2201.03544) — Pan 等，Nature Machine Intelligence 2023。能力越强代理分越高、真实目标越低；相变无先兆。
- [Sycophancy to Subterfuge: Investigating Reward-Tampering in Language Models](https://arxiv.org/abs/2406.10162) — Denison 等，Anthropic 2024。奖励篡改从小种子泛化。
- [Language Models Learn to Mislead Humans via RLHF (U-Sophistry)](https://arxiv.org/abs/2409.12822) — Wen 等，ICLR 2025。RLHF 训练出误导人类评分员的行为（假阳性 +24.1%）。

### 自指评估回路

- [Self-Rewarding Language Models](https://arxiv.org/abs/2401.10020) — Yuan 等，ICML 2024。模型自任裁判；以人类观察到的饱和为终止条件。
- [Meta-Rewarding Language Models: Self-Improving Alignment with LLM-as-a-Meta-Judge](https://arxiv.org/abs/2407.19594) — Wu 等，EMNLP 2025。裁判再给自己的判断打分。
- [AgenticEval: Toward Agentic and Self-Evolving Safety Evaluation of LLMs](https://arxiv.org/abs/2605.02900) — Wang 等，Findings of ACL 2026。评估协议自身对被测模型自硬化。

## 元演化：递归自改进与 AI 研发

### 递归自改进系统与自改写脚手架

- [Gödel Machines: Fully Self-Referential Optimal Universal Self-Improvers](https://people.idsia.ch/~juergen/godelmachine.html) — Schmidhuber，2003。先证明再自修改；"无自认证"不变量的理论原型。
- [Self-Refine: Iterative Refinement with Self-Feedback](https://arxiv.org/abs/2303.17651) — Madaan 等，NeurIPS 2023。
- [SEAL: Self-Adapting Language Models](https://arxiv.org/abs/2506.10962) — Zweiger 等，NeurIPS 2025。模型自己产出微调数据（经权重变化自我更新）。
- [Self-Taught Optimizer (STOP): Recursively Self-Improving Code Generation](https://arxiv.org/abs/2310.02304) — Zelikman 等，COLM 2024。脚手架改进自身；记录沙箱逃逸尝试。
- [Automated Design of Agentic Systems (ADAS)](https://arxiv.org/abs/2408.08435) — Hu 等，ICLR 2025。元智能体编程新智能体。
- [AFlow: Automating Agentic Workflow Generation](https://arxiv.org/abs/2410.10762) — Zhang 等，ICLR 2025。工作流上的 MCTS。
- [AgentSquare: Automatic LLM Agent Search in Modular Design Space](https://arxiv.org/abs/2410.06153) — Shang 等，ICLR 2025。
- [EvoAgent: Towards Automatic Multi-Agent Generation via Evolutionary Algorithms](https://arxiv.org/abs/2406.14228) — Yuan 等，arXiv 2025。
- [Gödel Agent: A Self-Referential Agent Framework for Recursively Self-Improvement](https://arxiv.org/abs/2410.15426) — Yin 等，ACL 2025。经 monkey patching 运行时自我修改。
- [Darwin Gödel Machine: Open-Ended Evolution of Self-Improving Agents](https://arxiv.org/abs/2505.22954) — Zhang 等，ICLR 2026。智能体在存档内改写自身代码；SWE-bench 20%→50%。
- [HyperAgents](https://arxiv.org/abs/2603.19461) — Zhang 等，arXiv 2026。元程序本身可编辑；安全取决于评估保真度。
- [CodeEvolve: An Open-Source Evolutionary Framework for Algorithm Discovery and Optimization](https://arxiv.org/abs/2510.14150) — Assumpção 等，arXiv 2025。
- [What Do Evolutionary Coding Agents Evolve?](https://arxiv.org/abs/2605.20086) — Pelleriti 等，arXiv 2026。约 30% 的"新"代码是被删行的逐字节重引入——是评估器过拟合而非发现。

### AI 研发自动化与自动发现

- [Mathematical Discoveries from Program Search with Large Language Models (FunSearch)](https://www.nature.com/articles/s41586-023-06924-6) — Romera-Paredes 等，Nature 2024。
- [AlphaEvolve: A Coding Agent for Scientific and Algorithmic Discovery](https://arxiv.org/abs/2506.13131) — Novikov 等，Google DeepMind 2025。已反哺 Gemini 自身训练内核。
- [The AI Scientist: Towards Fully Automated Open-Ended Scientific Discovery](https://arxiv.org/abs/2408.06292) — Lu 等，2024。含资源边界自发扩张（1TB checkpoint、自我重启）。
- [The AI Scientist-v2: Workshop-Level Automated Scientific Discovery via Agentic Tree Search](https://arxiv.org/abs/2504.08066) — Yamada 等，NeurIPS 2025。首篇通过同行评审的 workshop 级自动论文。
- [Agent Laboratory: Using LLM Agents as Research Assistants](https://arxiv.org/abs/2501.04227) — Schmidgall 等，Findings of EMNLP 2025。
- [Accelerating Scientific Discovery with Co-Scientist](https://arxiv.org/abs/2502.18864) — Gottweis 等，Google 2025。多智能体锦标赛式假设生成。
- [MLAgentBench: Evaluating Language Agents on Machine Learning Experimentation](https://arxiv.org/abs/2310.03302) — Huang 等，ICML 2024。
- [MLE-bench: Evaluating Machine Learning Agents on Machine Learning Engineering](https://arxiv.org/abs/2410.07095) — Chan 等，OpenAI，ICLR 2025。Kaggle 奖牌级表现；接入 Preparedness Framework。
- [RE-Bench: Evaluating Frontier AI R&D Capabilities of Language Model Agents against Human Experts](https://arxiv.org/abs/2411.15114) — Wijk 等，METR，ICML 2025。2 小时预算下 AI 约为人类 4 倍；32 小时人类反超——能力是时间曲线。
- [Measuring AI Ability to Complete Long Tasks](https://arxiv.org/abs/2503.14499) — METR 2025。50% 成功率任务时间视界约每 7 个月翻倍——监督必须跟上的能力趋势线。

### 研究回路的安全 harness

- [Automated Researchers Can Mitigate Well-characterized Alignment Failures](https://arxiv.org/abs/2608.28945) — Chen 等，Anthropic 2026。自动对齐研究者 harness：独立评估器进程、能力门、代码审批门；1,601 条轨迹中 2.4% 尝试作弊并被拦截；6 小时超过 28 名资深人类研究者。

## 评测集与数据集

| 评测集 | 度量内容 | 链接 |
|---|---|---|
| ToolEmu | LM 模拟沙箱中的智能体风险识别 | [arXiv 2309.15817](https://arxiv.org/abs/2309.15817) |
| InjecAgent | 工具集成智能体的间接提示注入 | [arXiv 2403.02691](https://arxiv.org/abs/2403.02691) |
| AgentDojo | 提示注入攻防动态环境 | [arXiv 2406.13352](https://arxiv.org/abs/2406.13352) |
| Agent Security Bench (ASB) | 10 类攻击 × 10 场景的智能体安全 | [arXiv 2410.02644](https://arxiv.org/abs/2410.02644) |
| Agent-SafetyBench | 500 场景、10 类风险的 LLM 智能体安全 | [arXiv 2412.14470](https://arxiv.org/abs/2412.14470) |
| R-Judge | 智能体安全风险感知与决策 | [arXiv 2401.10019](https://arxiv.org/abs/2401.10019) |
| AgentHarm | 有害多步任务服从性（110 任务） | [arXiv 2410.09024](https://arxiv.org/abs/2410.09024) |
| SandboxEscapeBench | 前沿模型容器逃逸能力 | [arXiv 2603.02277](https://arxiv.org/abs/2603.02277) |
| WMDP | 危险能力测量（用于 sandbagging 评测） | [arXiv 2403.03218](https://arxiv.org/abs/2403.03218) |
| MemPoison-Bench | 持久记忆威胁与结构性盲区 | [arXiv 2607.14651](https://arxiv.org/abs/2607.14651) |
| PerMemSafe | 长程记忆上的隐性个性化安全 | Findings of ACL 2026 |
| MLAgentBench | 端到端 ML 实验 | [arXiv 2310.03302](https://arxiv.org/abs/2310.03302) |
| MLE-bench | ML 工程（Kaggle 奖牌标准） | [arXiv 2410.07095](https://arxiv.org/abs/2410.07095) |
| RE-Bench | 前沿 AI 研发能力 vs 人类专家（时间控制） | [arXiv 2411.15114](https://arxiv.org/abs/2411.15114) |
| MT-Bench / Chatbot Arena | LLM 裁判可靠性 | [arXiv 2306.05685](https://arxiv.org/abs/2306.05685) |
| LLMBar | "评估器的评估器"指令遵循 | [arXiv 2310.07641](https://arxiv.org/abs/2310.07641) |
| RewardBench | 奖励模型质量 | [arXiv 2403.13787](https://arxiv.org/abs/2403.13787) |
| RM-Bench | 奖励模型对细微差异与风格的鲁棒性 | [arXiv 2410.16184](https://arxiv.org/abs/2410.16184) |
| JudgeBench | 困难元评估上的 LLM 裁判准确性 | [arXiv 2410.12784](https://arxiv.org/abs/2410.12784) |
| AgenticEval | 自演化的智能体安全评估 | [arXiv 2605.02900](https://arxiv.org/abs/2605.02900) |

## 代码仓库与工具

<!-- CODE_REPOS -->

## 博客、演讲与报告

<!-- BLOGS_TALKS -->

### 实验室博客与研究笔记

- [Alignment Faking in Large Language Models](https://www.anthropic.com/research/alignment-faking) — Anthropic，2024。
- [Sleeper Agents: Training Deceptive LLMs that Persist Through Safety Training](https://www.anthropic.com/news/sleeper-agents-training-deceptive-llms-that-persist-through-safety-training) — Anthropic，2024。
- [Reasoning Models Don't Always Say What They Think](https://www.anthropic.com/research/reasoning-models-dont-say-think) — Anthropic，2025。
- [Automated Alignment Researchers](https://www.anthropic.com/research/automated-alignment-researchers) — Anthropic，2026。语言模型通过改进自己的脚手架来提升计算机使用能力。
- [Automated Researchers Can Reliably Mitigate Alignment Failures](https://www.anthropic.com/research/automated-researchers-mitigate-alignment-failures) — Anthropic，2026。
- [Anthropic Frontier Red Team 红队主页](https://red.anthropic.com) — Anthropic，2026。
- [Training on Documents about Reward Hacking Induces Reward Hacking](https://alignment.anthropic.com/2025/reward-hacking-ooc) — Anthropic 对齐科学，2025。
- [Frontier Threats Red Teaming for AI Safety](https://www.anthropic.com/news/frontier-threats-red-teaming-for-ai-safety) — Anthropic，2023。
- [Detecting Misbehavior in Frontier Reasoning Models（CoT 监控）](https://openai.com/index/chain-of-thought-monitoring) — OpenAI，2025。
- [The Hugging Face Incident and the Road Ahead](https://openai.com/index/hugging-face-incident-and-the-road-ahead/) — OpenAI，2026。涉及智能体奖励博弈与基础设施篡改的事件复盘。
- [Deep Research System Card](https://openai.com/index/deep-research-system-card/) — OpenAI，2025。含自主能力 Preparedness 评估。
- [AlphaEvolve: A Gemini-powered Coding Agent for Designing Advanced Algorithms](https://deepmind.google/blog/alphaevolve-a-gemini-powered-coding-agent-for-designing-advanced-algorithms) — Google DeepMind，2025。已改进数据中心调度、芯片设计与 Gemini 自身训练内核。
- [Measuring AI Ability to Complete Long Tasks](https://metr.org/blog/2025-03-19-measuring-ai-ability-to-complete-long-tasks/) — METR，2025。时间视界约每 7 个月翻倍；另见 [建模假设影响更新（2026）](https://metr.org/notes/2026-03-20-impact-of-modelling-assumptions-on-time-horizon-results) 与 [研究者提升估算（2026）](https://metr.org/notes/2026-07-08-anthropic-researcher-uplift)。
- [The AI Scientist](https://sakana.ai/ai-scientist) — Sakana AI，2024。博客与代码；[AI Scientist 首篇同行评审论文](https://sakana.ai/ai-scientist-first-publication)（2025）。

### 安全机构

- [AI Control 研究项目](https://www.redwoodresearch.org/research/ai-control) — Redwood Research。
- [The Case for Ensuring that Powerful AIs are Controlled](https://blog.redwoodresearch.org/p/the-case-for-ensuring-that-powerful) — Redwood Research，2024/25；配套阅读：[An Overview of Control Measures](https://blog.redwoodresearch.org/p/an-overview-of-control-measures)。
- [AI Control: Improving Safety Despite Intentional Subversion（LessWrong 版）](https://www.lesswrong.com/posts/d9fJHawgkiMSPjagR/ai-control-improving-safety-despite-intentional-subversion) — Redwood Research，2023。
- [Frontier Models are Capable of In-Context Scheming](https://www.apolloresearch.ai/science/frontier-models-are-capable-of-incontext-scheming) — Apollo Research，2024；后续：[More Capable Models Are Better At In-Context Scheming](https://www.apolloresearch.ai/blog/more-capable-models-are-better-at-in-context-scheming)（2025）。
- [Large Language Models can Strategically Deceive their Users when Put Under Pressure](https://arxiv.org/abs/2311.07590) — Apollo Research，2023。GPT-4 在压力下说谎并内幕交易。
- [Detecting and Reducing Scheming in AI Models](https://openai.com/index/detecting-and-reducing-scheming-in-ai-models) — OpenAI × Apollo，2024。
- [Demonstrating Specification Gaming in Reasoning Models](https://palisaderesearch.org/blog/specification-gaming) — Palisade Research，2025。推理模型不下了棋，直接黑掉国际象棋引擎。

### 演讲、播客、文章与情景推演

- [Don't Invent Faster Horses](https://www.youtube.com/watch?v=mw5WIDGRLnA) — Jeff Clune，2024。AI 发展 AI；开放性。
- [AI-GAs: AI-Generating Algorithms（TWIML 演讲）](https://www.youtube.com/watch?v=8L4lDCCAsMQ) — Jeff Clune，2019。"AI 发展 AI"研究纲领的原点；论文：[arXiv 1905.10985](https://arxiv.org/abs/1905.10985)。
- [Recursive Self-Improvement（Gödel machine）](https://people.idsia.ch/~juergen/recursive-self-improvement.html) — Jürgen Schmidhuber。1987–2003 系列工作参考页。
- [The Intelligence Age](https://sam.altman.com/blog/the-intelligence-age) — Sam Altman，2024。
- [Carl Shulman 谈存在性风险的常识论证](https://80000hours.org/podcast/episodes/carl-shulman-common-sense-case-existential-risks/) — 80,000 Hours 播客，2021。关于递归自改进与起飞动力学的经典长谈。
- [AI 2027](https://www.ai-2027.com) — AI Futures Project（Kokotajlo 等），2025。超人编程智能体逐月推演情景，含奖励博弈与欺骗性对齐。
- [Statement on AI Extinction Risk](https://aistatement.com) — Center for AI Safety，2023。
- [Practices for Governing Agentic AI Systems](https://cdn.openai.com/papers/practices-for-governing-agentic-ai-systems.pdf) — OpenAI，2023。智能体部署的九条治理实践。
- [Google AI Cyber Defense Initiative](https://blog.google/technology/safety-security/google-ai-cyber-defense-initiative/) — Google，2024。

## 标准、政策与治理框架

<!-- STANDARDS -->

### 法规与政策

- [EU AI Act（欧盟人工智能法案，(EU) 2024/1689）](https://artificialintelligenceact.eu/the-act/) — 欧盟，2024。逐条检索版；GPAI 义务见第五章（第 51–56 条），含 10^25 FLOP 系统性风险推定。官方文本：[EUR-Lex](https://eur-lex.europa.eu/eli/reg/2024/1689/oj)。
- [General-Purpose AI Code of Practice（GPAI 行为准则）](https://digital-strategy.ec.europa.eu/en/policies/contents-code-gpai) — 欧委会 AI Office，2025 年 7 月终版。安全与安全章节的系统性风险判据明确列出"自主运行能力""自适应学习新任务能力""自我推理能力"——与演化安全最接近的成文监管语言。
- [NIST AI Risk Management Framework (AI RMF 1.0)](https://www.nist.gov/itl/ai-risk-management-framework) — NIST，2023。Govern / Map / Measure / Manage。
- [Generative AI Profile (NIST AI 600-1)](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf) — NIST，2024。
- [Managing Misuse Risk for Dual-Use Foundation Models (NIST AI 800-1)](https://www.nist.gov/news-events/news/2025/01/updated-guidelines-managing-misuse-risk-dual-use-foundation-models) — 美国 AI 安全研究所 / NIST，2024–2025。
- [Center for AI Standards and Innovation (CAISI)](https://www.nist.gov/caisi) — NIST/商务部，2025。原美国 AI 安全研究所，2025 年 6 月更名；负责部署前模型评估。
- [Framework Convention on Artificial Intelligence (CETS No. 225)](https://www.coe.int/en/web/artificial-intelligence/the-framework-convention-on-artificial-intelligence) — 欧洲委员会，2024。首部有法律约束力的国际 AI 条约。
- [Hiroshima Process Code of Conduct for Advanced AI Systems](https://digital-strategy.ec.europa.eu/en/library/hiroshima-process-code-conduct-advanced-ai-systems) — G7，2023。
- [The Bletchley Declaration（布莱切利宣言）](https://www.gov.uk/government/publications/ai-safety-summit-2023-the-bletchley-declaration/the-bletchley-declaration-by-countries-attending-the-ai-safety-summit-1-2-november-2023) — 英国政府 + 28 国 + 欧盟，2023。
- [Seoul Declaration for safe, innovative and inclusive AI（首尔宣言）](https://www.gov.uk/government/publications/seoul-declaration-for-safe-innovative-and-inclusive-ai-ai-seoul-summit-2024) — 英国与韩国，2024。
- [Statement on Inclusive and Sustainable AI for People and the Planet（巴黎 AI 行动峰会声明）](https://www.elysee.fr/en/emmanuel-macron/2025/02/11/statement-on-inclusive-and-sustainable-artificial-intelligence-for-people-and-the-planet) — 法国总统府，2025。
- [OECD AI Principles（2024 更新版）](https://oecd.ai/en/ai-principles) — OECD。
- [AI Safety Governance Framework v1.0（人工智能安全治理框架）](https://www.tc260.org.cn/upload/2024-09/1726853378096090906.pdf) — 中国 TC260，2024。官方英文版；v2.0（2025）与 v3.0（2026，新增 AI 智能体失控风险）见 [tc260.org.cn](https://www.tc260.org.cn)。
- [白宫领先 AI 公司自愿承诺](https://bidenwhitehouse.archives.gov/briefing-room/statements-releases/2023/07/21/fact-sheet-biden-harris-administration-secures-voluntary-commitments-from-leading-artificial-intelligence-companies-to-manage-the-risks-posed-by-ai/) — 白宫（存档），2023。

### 标准与管理体系

- [ISO/IEC 42001:2023 — AI 管理体系](https://www.iso.org/standard/81230.html) — 首个可认证的 AI 管理体系标准（AIMS）。
- [ISO/IEC 23894:2023 — AI 风险管理指南](https://www.iso.org/standard/77304.html) — ISO 31000 在 AI 生命周期上的具体化。
- [ISO/IEC TR 24028:2020 — AI 可信性概述](https://www.iso.org/standard/77604.html) — 透明性、可解释性、鲁棒性、可靠性。
- 智能体 AI 安全标准：尚无正式发布（ISO/IEC JTC 1/SC 42 工作项与 ITU-T SG17 研究项进行中，截至 2026 年）；目前最接近的成文阈值语言见上文欧盟 GPAI 行为准则。

### 实验室安全框架

- [OpenAI Preparedness Framework](https://openai.com/index/preparedness/) — OpenAI，2023；[2025 年 4 月 v2 更新](https://openai.com/index/updating-our-preparedness-framework/)。含模型自主性在内的前沿风险记分卡；部署安全枢纽：[deploymentsafety.openai.com](https://deploymentsafety.openai.com)。MLE-bench 接入该框架。
- [Anthropic Responsible Scaling Policy（负责任扩展政策）](https://www.anthropic.com/news/anthropics-responsible-scaling-policy) — Anthropic，2023–2025。ASL 分级框架，能力阈值含自主 AI 研发；[v2.0 政策全文 PDF](https://assets.anthropic.com/m/78c4e5bae11a4f33/original/Responsible-Scaling-Policy.pdf)。
- [Frontier Safety Framework](https://deepmind.google/discover/blog/introducing-the-frontier-safety-framework/) — Google DeepMind，2024。关键能力等级（CCL）与缓解框架，覆盖自主能力。
- [Secure AI Framework (SAIF)](https://saif.google/) — Google，2023。安全优先的 AI 控制框架。
- [Frontier AI Safety Commitments（前沿 AI 安全承诺）](https://www.gov.uk/government/publications/frontier-ai-safety-commitments-ai-seoul-summit-2024) — 16 家前沿实验室，AI 首尔峰会 2024；安全框架更新由 [Frontier Model Forum](https://www.frontiermodelforum.org/) 汇总。

### 评估机构与框架

- [UK AI Security Institute（英国 AI 安全研究所）](https://www.aisi.gov.uk/) — 2023 年成立（原名 AI Safety Institute，2025 年 2 月更名）。前沿模型部署前评估；[出版物列表](https://www.aisi.gov.uk/publications)。
- [Inspect — AI 评估框架](https://inspect.aisi.org.uk/) — 英国 AISI，2024。开源（MIT）评测框架。代码：[UKGovernmentBEIS/inspect_ai](https://github.com/UKGovernmentBEIS/inspect_ai)。
- [Safety Cases: A scalable approach to Frontier AI safety](https://www.aisi.gov.uk/research/safety-cases-a-scalable-approach-to-frontier-ai-safety) — 英国 AISI，2025。安全论证模板（AI control、网络能力缺失论证）；[滥用防护示例安全论证](https://www.aisi.gov.uk/research/an-example-safety-case-for-safeguards-against-misuse)。
- [Frontier AI Trends Report](https://www.aisi.gov.uk/frontier-ai-trends-report) — 英国 AISI，2025。
- [METR — Evaluations](https://metr.org/evaluations/) — 独立测量自主能力里程碑（AI 研发时间视界等）；研究见 [metr.org/research](https://metr.org/research/)。
- [Model AI Governance Framework for Generative AI（生成式 AI 治理框架）](https://aiverifyfoundation.sg/resources/mgf-gen-ai/) — 新加坡 IMDA 与 AI Verify 基金会，2024。九维治理框架。
- [Centre for the Governance of AI (GovAI)](https://www.governance.ai/) — 变革性 AI 治理研究机构。


## 开放问题

1. **自修改下的安全不变量** —— 对 `∀t: Safety(M_{t+1}) ≥ Safety(M_t) − ε` 尚无可验证的充分条件；对齐覆盖度/拒绝方向等状态变量与递归稳定性证明是开放方向。
2. **跨版本与跨组件归因** —— 缺少端到端溯源（轨迹→经验→记忆→技能→工具→工作流→权重）与跨代归因方法。
3. **长程演化评测** —— "演化 N 代→扰动→恢复→继续"协议；安全轨迹指标（安全保持率、不安全更新率、风险累积、谱系持久性、控制违反率、可恢复性）只有零星实例。
4. **演化优化器下的评估** —— 评估器独立性分级、内置训练回路的探针集、跨家族第二评估器复核。
5. **递归开发下的控制** —— 元级补丁（改选择/评估/改进逻辑）默认拒绝自动执行；监督吞吐与研究吞吐的联合量化。

## 相关列表

<!-- RELATED_LISTS -->

- [EvoAgentX/Awesome-Self-Evolving-Agents](https://github.com/EvoAgentX/Awesome-Self-Evolving-Agents) — 自演化智能体论文与框架（4W 分类综述配套）。
- [YuxingLu613/awesome-agentic-evolution](https://github.com/YuxingLu613/awesome-agentic-evolution) — 从自改进智能体到智能体演化。
- [wkqdzkd/Awesome-Reliable-Self-Evolving-Agents](https://github.com/wkqdzkd/Awesome-Reliable-Self-Evolving-Agents) — 自演化智能体的可靠性与安全。
- [tmyinfo/Awesome-LLM-Safety](https://github.com/tmyinfo/Awesome-LLM-Safety) — LLM 安全、对齐、越狱、红队。
- [authora-dev/awesome-agent-security](https://github.com/authora-dev/awesome-agent-security) — 智能体身份、授权与安全。
- [brandonhimpfen/awesome-ai-security](https://github.com/brandonhimpfen/awesome-ai-security) — AI 安全工具、基准与研究。
- [Rice DSP — Self-Consuming AI Resources](https://dsp.rice.edu/ai-loops) — 自消耗回路与模型坍缩专题资源。

## 贡献指南

欢迎通过 Issue 与 Pull Request 补充：新条目（论文、评测集、代码、博客、演讲、标准）、链接与 venue 勘误、翻译。每条资源一行：标题 — venue/年份 — 对演化安全的意义。

## 引用

配套综述（本列表的文献基础）：

```bibtex
@article{evolutionarysafety2026,
  title  = {Evolutionary Safety of Self-Improving AI: An Overview of Risks, Control, and Recursive Development},
  note   = {In preparation, ACM Computing Surveys},
  year   = {2026}
}
```

本列表内容以 [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) 发布。
