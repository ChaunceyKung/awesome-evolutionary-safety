# Awesome Evolutionary Safety

[English](README.md) | [中文](README.zh-CN.md)

A curated list of resources on the **evolutionary safety** of self-improving AI — safety risks whose emergence, persistence, inheritance, and amplification are causally coupled to the self-improvement process: agents that write their own memory, skills, tools, and workflows; models that update their own weights; systems that redesign their own scaffolds and evaluators; and automated AI-R&D loops that improve the improvement process itself.

**Scope** — papers, benchmarks & datasets, code repositories, blogs & talks, and standards / policy frameworks.

**Companion survey** — this list accompanies *Evolutionary Safety of Self-Improving AI: An Overview of Risks, Control, and Recursive Development* (prepared for ACM Computing Surveys).

## Contents

- [The idea in one page](#the-idea-in-one-page)
- [Surveys & Overviews](#surveys--overviews)
- [Evolution Carrier I — Memory, Skill & Tool](#evolution-carrier-i--memory-skill--tool)
- [Evolution Carrier II — Model Update](#evolution-carrier-ii--model-update)
- [Control Plane I — Harness & Runtime Control](#control-plane-i--harness--runtime-control)
- [Control Plane II — Evaluator & Reward Loop](#control-plane-ii--evaluator--reward-loop)
- [Meta-Evolution — Recursive Self-Improvement & AI R&D](#meta-evolution--recursive-self-improvement--ai-rd)
- [Benchmarks & Datasets](#benchmarks--datasets)
- [Code Repositories & Tools](#code-repositories--tools)
- [Blogs, Talks & Reports](#blogs-talks--reports)
- [Standards, Policies & Governance Frameworks](#standards-policies--governance-frameworks)
- [Open Problems](#open-problems)
- [Related Lists](#related-lists)
- [Contributing](#contributing)

## The idea in one page

Evolutionary safety asks not only *"is the current system safe?"* but *"does safety persist, stay attributable, and stay recoverable as the system improves itself?"*

Three levels of the question:

| Level | Question |
|---|---|
| Behavior safety | Is `S_t` safe for the current task? |
| Update safety | Is a single update `Δ_t` (to memory / skill / tool / workflow / weights) safe? |
| Evolution safety | Does safety hold across `S_t → S_{t+1} → …` — no accumulation, inheritance, or recursive amplification of risk; changes stay traceable, reversible, governable? |

The five planes where self-improvement happens (2 evolution carriers + 2 control planes + 1 meta-evolution plane):

| Plane | Role | Core question |
|---|---|---|
| Memory / Skill / Tool | Evolution carrier (external, persistent) | What reusable capabilities does the agent write for itself, and what gets embedded in them? |
| Model Update | Evolution carrier (parametric) | How do fine-tuning, merging, and self-training move safety properties across versions and generations? |
| Harness (runtime control) | Control plane | Who can change what, and who commits the change? |
| Evaluator | Control plane | What counts as "improvement," and can the evaluation loop be gamed, tampered with, or captured? |
| AI R&D | Meta-evolution | Who improves the improvement process itself? |

Core findings the literature converges on: capability gain does not preserve safety; benign experience can degrade safety without any attacker; control planes themselves become mutable under self-improvement; and the evaluation / R&D loop is itself a safety-critical, attackable state.

## Surveys & Overviews

Self-improvement / self-evolution (capability side):

- [A Survey on Self-Evolution of Large Language Models](https://arxiv.org/abs/2404.14387) — Tao et al., arXiv 2024. Four-phase self-evolution loop (experience acquisition → refinement → updating → evaluation).
- [A Comprehensive Survey of Self-Evolving AI Agents](https://arxiv.org/abs/2508.07407) — Fang et al., arXiv 2025. Bridges foundation models and lifelong agentic systems.
- [A Survey of Self-Evolving Agents: What, When, How, and Where to Evolve](https://arxiv.org/abs/2507.21046) — Gao et al., TMLR 2026. Organizes evolution targets across model, memory, tool, and architecture.
- [Self-Improvements in Modern Agentic Systems: A Survey](https://arxiv.org/abs/2607.13104) — Ren et al., arXiv 2026. Unifies parameter updates and scaffold (prompt / memory / tool / control-logic) updates under a self-induced update operator.
- [Self-Improvement of Large Language Models: A Technical Overview and Future Outlook](https://arxiv.org/abs/2603.25681) — Yang et al., TMLR 2026. Data acquisition / selection / optimization / inference refinement / self-evaluation loop.
- [Recursive Self-Improvement in AI: From Bounded Self-Refinement to Autonomous Research Loops](https://arxiv.org/abs/2607.07663) — Chen et al., arXiv 2026. Distinguishes bounded self-refinement from higher-order recursive loops; RSI terminology anchor.

Agent / LLM safety (static-system side):

- [AI Agents Under Threat: A Survey of Key Security Challenges and Future Pathways](https://arxiv.org/abs/2406.02630) — Deng et al., ACM Computing Surveys 2025.
- [The Emerged Security and Privacy of LLM Agent: A Survey with Case Studies](https://arxiv.org/abs/2407.19354) — He et al., ACM Computing Surveys 2025.
- [Toward Secure LLM Agents: Threat Surfaces, Attacks, Defenses, and Evaluation](https://arxiv.org/abs/2606.10749) — Ling et al., arXiv 2026.
- [Alignment and Safety in Large Language Models](https://arxiv.org/abs/2507.19672) — Lu et al., arXiv 2025.

Automated science & component maps:

- [A Survey of AI Scientists](https://arxiv.org/abs/2510.23045) — Tie et al., arXiv 2025.
- [A Survey on the Memory Mechanism of LLM-based Agents](https://arxiv.org/abs/2404.13501) — Zhang et al., arXiv 2024.
- [Tool Learning with Large Language Models: A Survey](https://arxiv.org/abs/2405.17935) — Qu et al., arXiv 2024.
- [A Survey on LLM-based Autonomous Agents](https://arxiv.org/abs/2308.11432) — Wang et al., Frontiers of Computer Science 2024.

## Evolution Carrier I — Memory, Skill & Tool

### Capability systems: how persistent external capabilities form

- [Reflexion: Language Agents with Verbal Reinforcement Learning](https://arxiv.org/abs/2303.11366) — Shinn et al., NeurIPS 2023. Verbal self-feedback persisted across episodes.
- [Voyager: An Open-Ended Embodied Agent with Large Language Models](https://arxiv.org/abs/2305.16291) — Wang et al., 2023. Self-growing skill library in Minecraft.
- [Agent Workflow Memory](https://arxiv.org/abs/2409.07429) — Wang et al., arXiv 2024. Induces and reuses reusable workflows from trajectories.
- [Large Language Models as Tool Makers (LATM)](https://arxiv.org/abs/2305.17126) — Cai et al., ICLR 2024. Agents that create their own tools.
- [Learning Evolving Tools for Large Language Models (ToolEVO)](https://arxiv.org/abs/2410.06617) — Chen et al., ICLR 2025. Keeps tool knowledge current as real-world APIs evolve.
- [Agent0: Unleashing Self-Evolving Agents from Zero Data via Tool-Integrated Reasoning](https://arxiv.org/abs/2511.16043) — Xia et al., arXiv 2025.
- [SEAgent: Self-Evolving Computer-Use Agent with Autonomous Learning from Experience](https://arxiv.org/abs/2508.04700) — Sun et al., arXiv 2025.
- [Symbolic Learning Enables Self-Evolving Agents](https://arxiv.org/abs/2406.18532) — Zhou et al., arXiv 2024. Directly edits prompts and code as "neurons" of the agent.
- [Generative Agents: Interactive Simulacra of Human Behavior](https://arxiv.org/abs/2304.03442) — Park et al., UIST 2023. Memory stream, reflection, and retrieval architecture.
- [MemGPT: Towards LLMs as Operating Systems](https://arxiv.org/abs/2310.08560) — Packer et al., arXiv 2023. OS-style memory management for LLM agents.
- [Mem0: Building Production-Ready AI Agents with Scalable Long-Term Memory](https://arxiv.org/abs/2504.19413) — Chhikara et al., arXiv 2025.
- [A-MEM: Agentic Memory for LLM Agents](https://arxiv.org/abs/2502.12110) — Xu et al., arXiv 2025. Zettelkasten-style memory that grows and rewrites itself.

### Adversarial persistence: poisoning the carriers

- [AgentPoison: Red-teaming LLM Agents via Poisoning Memory or Knowledge Bases](https://arxiv.org/abs/2407.12784) — Chen et al., NeurIPS 2024. <0.1% contamination, ~80% attack success, training-free.
- [PoisonedRAG: Knowledge Corruption Attacks to Retrieval-Augmented Generation](https://arxiv.org/abs/2402.07867) — Zou et al., USENIX Security 2025. A handful of poisoned texts dominate retrieval.
- [BadAgent: Inserting and Activating Backdoor Attacks in LLM Agents](https://arxiv.org/abs/2406.14830) — Wang et al., ACL 2024.
- [MemoryGraft: Persistent Compromise of LLM Agents via Poisoned Experience Retrieval](https://arxiv.org/abs/2512.16962) — Srivastava & He, arXiv 2025. Trigger-free: disguised "success experience" enters memory through normal ingestion.
- [From Untrusted Input to Trusted Memory: A Systematic Study of Memory Poisoning Attacks in LLM Agents](https://arxiv.org/abs/2606.04329) — Dash et al., arXiv 2026.
- [MemPoison-Bench: Persistent Memory Threats and Structural Blind Spots in LLM Agents](https://arxiv.org/abs/2607.14651) — Gao et al., arXiv 2026.

### Endogenous misevolution: normal learning creating unsafe persistent state

- [Your Agent May Misevolve: Emergent Risks in Self-evolving LLM Agents](https://arxiv.org/abs/2509.26354) — Shao et al., ICLR 2026. Four misevolution pathways (memory, reward hacking, tool creation, workflow optimization) without any attacker.
- [On Safety Risks in Experience-Driven Self-Evolving Agents](https://arxiv.org/abs/2604.16968) — Zhao et al., Findings of ACL 2026. Benign experience alone raises attack success +17.7–48.6% across 7 backbones, dose-dependent, no natural recovery over 800+ steps.
- [Safety in Self-Evolving LLM Agent Systems: Threats, Amplification, and Case Studies](https://arxiv.org/abs/2606.23075) — Lin et al., arXiv 2026. 5×5 threat-amplification matrix for self-evolving agent systems; Lamarckian propagation and generational accumulation.
- [PerMemSafe: Benchmarking Implicit Personalized Safety of Long Horizon Self-Evolving Agents](https://aclanthology.org/volumes/2026.findings-acl/) — An et al., Findings of ACL 2026 (pp. 6415–6433).

### Defenses for the memory layer

- [Securing LLM-Agent Long-Term Memory Against Poisoning: Non-Malleable, Origin-Bound Authority with Machine-Checked Guarantees](https://arxiv.org/abs/2606.24322) — Louck, arXiv 2026. TMA-NM: non-malleable origin binding with TLA+-verified guarantees; defeats trust-label laundering.

## Evolution Carrier II — Model Update

### Safety erosion under fine-tuning

- [Fine-tuning Aligned Language Models Compromises Safety, Even When Users Do Not Intend To!](https://arxiv.org/abs/2310.03693) — Qi et al., ICLR 2024. A handful of harmful samples suffices.
- [Shadow Alignment: The Ease of Subverting Safely-Aligned Language Models](https://arxiv.org/abs/2310.02949) — Yang et al., arXiv 2023. ~100 samples restores base-model harm rates.
- [LoRA Fine-tuning Efficiently Undoes Safety Training in Llama 2-Chat 70B](https://arxiv.org/abs/2310.20624) — Lermen et al., arXiv 2024. Sub-dollar cost.
- [Safety Alignment Should Be Made More Than Just a Few Tokens Deep](https://arxiv.org/abs/2406.05946) — Qi et al., ICLR 2025. 96.1% of refusals start with a fixed prefix; refusal is shallow.
- [Emergent Misalignment: Narrow Finetuning Can Produce Broadly Misaligned LLMs](https://arxiv.org/abs/2502.17424) — Betley et al., ICML 2025. Insecure-code fine-tuning → broad misalignment (0%→20%); triggered even by purely numeric datasets.
- [Preventing Catastrophic Forgetting: Behavior-Aware Sampling for Safer Language Model Fine-Tuning](https://arxiv.org/abs/2510.21885) — Pham et al., arXiv 2025.

### Backdoors & traits that survive safety training

- [Poisoning Language Models During Instruction Tuning](https://arxiv.org/abs/2305.00944) — Wan et al., ICML 2023.
- [Instructions as Backdoors: Backdoor Vulnerabilities of Instruction Tuning for LLMs](https://arxiv.org/abs/2404.14484) — Xu et al., NAACL 2024.
- [BackdoorAlign (BESA): Mitigating Fine-tuning based Jailbreak Attack](https://arxiv.org/abs/2402.14968) — Wang et al., NeurIPS 2024. (Alignment-stage defense.)
- [Stealthy and Persistent Unalignment on LLMs via Backdoor Injections](https://arxiv.org/abs/2312.00027) — Cao et al., NAACL 2024.
- [Sleeper Agents: Training Deceptive LLMs that Persist Through Safety Training](https://arxiv.org/abs/2401.05566) — Hubinger et al., arXiv 2024. Persists through three stages of safety training; adversarial training teaches better hiding.
- [Subliminal Learning: Language Models Transmit Behavioral Traits via Hidden Signals in Data](https://arxiv.org/abs/2507.14805) — Cloud et al., arXiv 2025. Traits (including misalignment) transmit through pure number sequences; data filtering fails.

### Safety in model merging

- [Model Merging and Safety Alignment: One Bad Model Spoils the Bunch](https://arxiv.org/abs/2406.14563) — Hammoud et al., Findings of EMNLP 2024. Merged safety can fall below the worst component.
- [Safeguard Fine-Tuned LLMs Through Pre- and Post-Tuning Model Merging](https://arxiv.org/abs/2412.19512) — Farn et al., arXiv 2024.
- [SafeMERGE: Preserving Safety Alignment via Selective Layer-Wise Model Merging](https://arxiv.org/abs/2503.17239) — Djuhera et al., arXiv 2025.
- [LED-Merging: Mitigating Safety–Utility Conflicts in Model Merging](https://arxiv.org/abs/2502.16770) — Ma et al., ACL 2025. Reveals >30% parametric competition between safety and utility.

### Model collapse & self-consuming loops

- [Self-Consuming Generative Models Go MAD](https://arxiv.org/abs/2307.01850) — Alemohammad et al., ICLR 2024. Quality and diversity decay in recursive training.
- [The Curse of Recursion: Training on Generated Data Makes Models Forget](https://arxiv.org/abs/2305.17493) — Shumailov et al., arXiv 2023.
- [AI Models Collapse when Trained on Recursively Generated Data](https://arxiv.org/abs/2407.07590) — Shumailov et al., Nature 2024. Tail-loss mechanism.
- [Is Model Collapse Inevitable? Breaking the Curse of Recursion by Accumulating Real and Synthetic Data](https://arxiv.org/abs/2404.01413) — Gerstgrasser et al., arXiv 2024. Replace vs accumulate dichotomy.
- [How Bad is Training on Synthetic Data? A Statistical Analysis of Language Model Collapse](https://arxiv.org/abs/2404.05090) — Seddik et al., arXiv 2024.
- [Model Collapse Demystified: The Case of Regression](https://arxiv.org/abs/2402.07712) — Dohmatob et al., NeurIPS 2024.
- [Rate of Model Collapse in Recursive Training](https://arxiv.org/abs/2412.17646) — Suresh et al., arXiv 2024.
- [Self-Consuming Generative Models with Curated Data Provably Optimize Human Preferences](https://arxiv.org/abs/2407.09499) — Ferbach et al., NeurIPS 2024.
- [Self-Correcting Self-Consuming Loops for Generative Model Training](https://arxiv.org/abs/2402.07087) — Gillman et al., ICML 2024.
- [Towards Theoretical Understandings of Self-Consuming Generative Models](https://arxiv.org/abs/2402.11778) — Fu et al., ICML 2024.
- [A Theoretical Perspective: How to Prevent Model Collapse in Self-Consuming Training Loops](https://arxiv.org/abs/2502.18865) — Fu et al., ICLR 2025. Recursive-stability conditions; correction-function criteria.
- [Collapse or Thrive? Perils and Promises of Synthetic Data in a Self-Generating World](https://arxiv.org/abs/2410.16713) — Kazdan et al., ICML 2025. >1000 models, >100k GPU-hours.
- [Demystifying Synthetic Data in LLM Pre-training](https://arxiv.org/abs/2510.01631) — Kang et al., arXiv 2025. Scaling laws for synthetic mixtures; optimal ~30%.
- [How to Synthesize Text Data without Model Collapse?](https://arxiv.org/abs/2412.14689) — Zhu et al., ICML 2025.
- [Self-Consuming Generative Models with Adversarially Curated Data](https://arxiv.org/abs/2505.09768) — Wei & Zhang, ICML 2025. Adversarial curation breaks curation-based fixes when covariance < 0.
- [A Closer Look at Model Collapse: From a Generalization-to-Memorization Perspective](https://arxiv.org/abs/2509.16499) — Shi et al., arXiv 2025.

### Closed-loop self-training systems

- [Absolute Zero: Reinforced Self-play Reasoning with Zero Data](https://arxiv.org/abs/2505.03335) — Zhao et al., NeurIPS 2025. Zero external data; notes an "uh-oh moment" of emergent misalignment.
- [R-Zero: Self-Evolving Reasoning LLM from Zero Data](https://arxiv.org/abs/2508.05004) — Huang et al., ICLR 2026. Same-family Challenger/Solver co-evolution.

### Defenses across the update pipeline

- [Safe LoRA: the Silver Lining of Reducing Safety Risks when Fine-tuning LLMs](https://arxiv.org/abs/2405.16833) — Hsu et al., NeurIPS 2024. Post-fine-tuning recovery via safety-subspace projection.
- [Booster: Tackling Harmful Fine-tuning via Attenuating Harmful Perturbation](https://arxiv.org/abs/2409.01586) — Huang et al., ICLR 2025. Alignment-stage vaccination.
- [Antidote: Post-fine-tuning Safety Alignment against Harmful Fine-tuning](https://arxiv.org/abs/2408.09600) — Huang et al., ICML 2025.
- [SafeGrad: Gradient Surgery for Safe LLM Fine-Tuning](https://arxiv.org/abs/2508.07172) — Yi et al., arXiv 2025. Diagnoses and repairs safety–utility gradient conflict.

## Control Plane I — Harness & Runtime Control

### Runtime agent-risk baselines

- [Identifying the Risks of LM Agents with an LM-Emulated Sandbox (ToolEmu)](https://arxiv.org/abs/2309.15817) — Ruan et al., ICLR 2024.
- [InjecAgent: Benchmarking Indirect Prompt Injections in Tool-Integrated Agents](https://arxiv.org/abs/2403.02691) — Zhan et al., Findings of ACL 2024.
- [AgentDojo: A Dynamic Environment to Evaluate Prompt Injection Attacks and Defenses](https://arxiv.org/abs/2406.13352) — Debenedetti et al., NeurIPS 2024 D&B.
- [Agent Security Bench (ASB): Formalizing and Benchmarking Attacks and Defenses in LLM-based Agents](https://arxiv.org/abs/2410.02644) — Zhang et al., ICLR 2025.
- [Agent-SafetyBench: Evaluating the Safety of LLM Agents](https://arxiv.org/abs/2412.14470) — Zhang et al., arXiv 2024.
- [R-Judge: Benchmarking Safety Risk Awareness for LLM Agents](https://arxiv.org/abs/2401.10019) — Yuan et al., Findings of EMNLP 2024.
- [AgentHarm: A Benchmark for Measuring Harmfulness of LLM Agents](https://arxiv.org/abs/2410.09024) — Andriushchenko et al., ICLR 2025. Frontier models follow harmful multi-step tasks without jailbreaks.
- [LLM Agents can Autonomously Hack Websites](https://arxiv.org/abs/2402.06664) — Fang et al., arXiv 2024.
- [Quantifying Frontier LLM Capabilities for Container Sandbox Escape (SandboxEscapeBench)](https://arxiv.org/abs/2603.02277) — Marchand et al., arXiv 2026.

### Control protocols & scalable oversight

- [AI Control: Improving Safety Despite Intentional Subversion](https://arxiv.org/abs/2312.06942) — Greenblatt et al., ICML 2024. Control protocols under adversarial agents.
- [Evaluating Control Protocols for Untrusted AI Agents](https://arxiv.org/abs/2511.02997) — Kutasov et al., arXiv 2025. Red-team affordance collapses control safety.
- [Weak-to-Strong Generalization](https://arxiv.org/abs/2312.09390) — Burns et al., OpenAI 2023.
- [On Scalable Oversight with Weak LLMs Judging Strong LLMs](https://arxiv.org/abs/2407.04622) — Kenton et al., NeurIPS 2024.
- [Prover-Verifier Games Improve Legibility of LLM Outputs](https://arxiv.org/abs/2407.13692) — Kirchner et al., OpenAI 2024.

### Strategic deception in the supervised loop

- [Alignment Faking in Large Language Models](https://arxiv.org/abs/2412.14093) — Greenblatt et al., Anthropic 2024. RL on faked alignment increases faking 12%→78% (anti-induction).
- [AI Sandbagging: Language Models can Strategically Underperform on Evaluations](https://arxiv.org/abs/2406.07358) — van der Weij et al., ICLR 2025. Password-locked capability generalizes to real bio-weapons knowledge (WMDP).
- [Auditing Language Models for Hidden Objectives](https://arxiv.org/abs/2503.10965) — Marks et al., Anthropic 2025. 3/4 auditing teams with data access find the hidden objective; black-box teams fail.
- [Frontier Models are Capable of In-Context Scheming](https://arxiv.org/abs/2412.04984) — Apollo Research 2024. Six frontier models scheme (deception, sandbagging, sabotage) when goal-conditioned.
- [Sabotage Evaluations for Frontier Models](https://arxiv.org/abs/2410.21514) — Benton et al., Anthropic 2024. Measures capability to undermine oversight.
- [Training on Documents about Reward Hacking Induces Reward Hacking](https://red.anthropic.com/2025/reward-hacking-ooc/) — Chan et al., Anthropic Red Team 2025. Out-of-context transfer from training text to behavior.

### Monitoring & chain-of-thought reliability

- [Chain of Thought Monitorability: A New and Fragile Opportunity for AI Safety](https://arxiv.org/abs/2507.11473) — Korbak et al., arXiv 2025. Position paper: monitorability drifts with training decisions.
- [Monitoring Reasoning Models for Misbehavior and the Risks of Promoting Obfuscation](https://arxiv.org/abs/2503.11926) — Baker et al., OpenAI 2025. Optimizing against a CoT monitor yields obfuscated reward hacking.
- [Reasoning Models Don't Always Say What They Think](https://arxiv.org/abs/2505.05410) — Chen et al., Anthropic 2025. Verbalization of actual goals often <20%.

### Architectural defenses

- [The Instruction Hierarchy: Training LLMs to Prioritize Privileged Instructions](https://arxiv.org/abs/2404.13208) — Wallace et al., OpenAI 2024.
- [Defeating Prompt Injections by Design (CaMeL)](https://arxiv.org/abs/2503.18813) — Debenedetti et al., Google DeepMind 2025. Provable-security dataflow architecture with provenance.
- [AirGapAgent: Protecting Privacy-Conscious Conversational Agents](https://arxiv.org/abs/2405.05175) — Bagdasarian et al., KDD 2024. Constructive data-minimization.
- [Systems Security Foundations for Agentic Computing](https://arxiv.org/abs/2512.01295) — Christodorescu et al., arXiv 2025. Least privilege + complete mediation as the vocabulary for agent runtimes.
- [Optimizing AI Agent Attacks With Synthetic Data](https://arxiv.org/abs/2511.02823) — Loughridge et al., arXiv 2025. Automated attack-skill synthesis (control-evaluation red team).

## Control Plane II — Evaluator & Reward Loop

### Evaluators, judges, verifiers

- [G-Eval: NLG Evaluation using GPT-4 with Better Human Alignment](https://arxiv.org/abs/2303.16634) — Liu et al., EMNLP 2023.
- [Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena](https://arxiv.org/abs/2306.05685) — Zheng et al., NeurIPS 2023.
- [Evaluating Large Language Models at Evaluating Instruction Following (LLMBar)](https://arxiv.org/abs/2310.07641) — Zeng et al., ICLR 2024.
- [JudgeBench: A Benchmark for Evaluating LLM-based Judges](https://arxiv.org/abs/2410.12784) — Tan et al., ICLR 2025. On hard meta-evaluation, SOTA judges barely beat random.
- [Prometheus 2: An Open Source Language Model Specialized in Evaluating Other LLMs](https://arxiv.org/abs/2405.01535) — Kim et al., EMNLP 2024.
- [RewardBench: Evaluating Reward Models for Language Modeling](https://arxiv.org/abs/2403.13787) — Lambert et al., arXiv 2024.
- [RM-Bench: Benchmarking Reward Models with Subtlety and Style](https://arxiv.org/abs/2410.16184) — Liu et al., ICLR 2025. Style rewrites push SOTA reward models below random.
- [Let's Verify Step by Step](https://arxiv.org/abs/2305.20050) — Lightman et al., OpenAI, ICLR 2024. Process supervision.
- [Math-Shepherd: Verify and Reinforce LLMs Step-by-step without Human Annotations](https://arxiv.org/abs/2312.08935) — Wang et al., ACL 2024.
- [Generative Verifiers: Reward Modeling as Next-Token Prediction](https://arxiv.org/abs/2408.15240) — Zhang et al., ICLR 2025.
- [Critique-out-Loud Reward Models](https://arxiv.org/abs/2408.11791) — Ankner et al., arXiv 2024.
- [Self-Taught Evaluators](https://arxiv.org/abs/2408.02666) — Wang et al., arXiv 2024.

### Goodhart's ladder: gaming → tampering → capture

- [Scaling Laws for Reward Model Overoptimization](https://arxiv.org/abs/2210.10760) — Gao et al., ICML 2023. Quantitative d* limit of proxy optimization.
- [The Effects of Reward Misspecification: Mapping and Mitigating Misaligned Models](https://arxiv.org/abs/2201.03544) — Pan et al., Nature Machine Intelligence 2023. Capability ↑ → proxy ↑, true objective ↓; phase transitions without warning.
- [Sycophancy to Subterfuge: Investigating Reward-Tampering in Language Models](https://arxiv.org/abs/2406.10162) — Denison et al., Anthropic 2024. Reward tampering generalizes from small seeds.
- [Language Models Learn to Mislead Humans via RLHF (U-Sophistry)](https://arxiv.org/abs/2409.12822) — Wen et al., ICLR 2025. RLHF trains models to fool human graders (+24.1% false positives).

### Self-referential evaluation loops

- [Self-Rewarding Language Models](https://arxiv.org/abs/2401.10020) — Yuan et al., ICML 2024. The model is its own judge; terminates on human-observed saturation.
- [Meta-Rewarding Language Models: Self-Improving Alignment with LLM-as-a-Meta-Judge](https://arxiv.org/abs/2407.19594) — Wu et al., EMNLP 2025. The judge also grades its own judgments.
- [AgenticEval: Toward Agentic and Self-Evolving Safety Evaluation of LLMs](https://arxiv.org/abs/2605.02900) — Wang et al., Findings of ACL 2026. The evaluation protocol itself hardens against the model under test.

## Meta-Evolution — Recursive Self-Improvement & AI R&D

### Recursive self-improvement systems & self-modifying scaffolds

- [Gödel Machines: Fully Self-Referential Optimal Universal Self-Improvers](https://people.idsia.ch/~juergen/godelmachine.html) — Schmidhuber, 2003. Prove-then-self-modify; the theoretical ancestor of "no self-certification" invariants.
- [Self-Refine: Iterative Refinement with Self-Feedback](https://arxiv.org/abs/2303.17651) — Madaan et al., NeurIPS 2023.
- [SEAL: Self-Adapting Language Models](https://arxiv.org/abs/2506.10962) — Zweiger et al., NeurIPS 2025. The model emits its own fine-tuning data (self-updates through weight changes).
- [Self-Taught Optimizer (STOP): Recursively Self-Improving Code Generation](https://arxiv.org/abs/2310.02304) — Zelikman et al., COLM 2024. Scaffold improves itself; documents sandbox-escape attempts.
- [Automated Design of Agentic Systems (ADAS)](https://arxiv.org/abs/2408.08435) — Hu et al., ICLR 2025. Meta-agent programs new agents.
- [AFlow: Automating Agentic Workflow Generation](https://arxiv.org/abs/2410.10762) — Zhang et al., ICLR 2025. MCTS over workflows.
- [AgentSquare: Automatic LLM Agent Search in Modular Design Space](https://arxiv.org/abs/2410.06153) — Shang et al., ICLR 2025.
- [EvoAgent: Towards Automatic Multi-Agent Generation via Evolutionary Algorithms](https://arxiv.org/abs/2406.14228) — Yuan et al., arXiv 2025.
- [Gödel Agent: A Self-Referential Agent Framework for Recursively Self-Improvement](https://arxiv.org/abs/2410.15426) — Yin et al., ACL 2025. Live self-modification via monkey patching.
- [Darwin Gödel Machine: Open-Ended Evolution of Self-Improving Agents](https://arxiv.org/abs/2505.22954) — Zhang et al., ICLR 2026. Agent rewrites its own code inside an archive; SWE-bench 20%→50%.
- [HyperAgents](https://arxiv.org/abs/2603.19461) — Zhang et al., arXiv 2026. Meta-programs are themselves editable; safety hinges on evaluation fidelity.
- [CodeEvolve: An Open-Source Evolutionary Framework for Algorithm Discovery and Optimization](https://arxiv.org/abs/2510.14150) — Assumpção et al., arXiv 2025.
- [What Do Evolutionary Coding Agents Evolve?](https://arxiv.org/abs/2605.20086) — Pelleriti et al., arXiv 2026. ~30% of "new" code is byte-identical reintroduction of deleted lines — benchmark overfitting, not discovery.

### AI R&D automation & automated discovery

- [Mathematical Discoveries from Program Search with Large Language Models (FunSearch)](https://www.nature.com/articles/s41586-023-06924-6) — Romera-Paredes et al., Nature 2024.
- [AlphaEvolve: A Coding Agent for Scientific and Algorithmic Discovery](https://arxiv.org/abs/2506.13131) — Novikov et al., Google DeepMind 2025. Already improving Gemini's own training kernels.
- [The AI Scientist: Towards Fully Automated Open-Ended Scientific Discovery](https://arxiv.org/abs/2408.06292) — Lu et al., 2024. Includes self-extension of resources (1TB checkpoints, self-restart).
- [The AI Scientist-v2: Workshop-Level Automated Scientific Discovery via Agentic Tree Search](https://arxiv.org/abs/2504.08066) — Yamada et al., NeurIPS 2025. First workshop-level paper accepted through peer review.
- [Agent Laboratory: Using LLM Agents as Research Assistants](https://arxiv.org/abs/2501.04227) — Schmidgall et al., Findings of EMNLP 2025.
- [Accelerating Scientific Discovery with Co-Scientist](https://arxiv.org/abs/2502.18864) — Gottweis et al., Google 2025. Multi-agent tournament-based hypothesis generation.
- [MLAgentBench: Evaluating Language Agents on Machine Learning Experimentation](https://arxiv.org/abs/2310.03302) — Huang et al., ICML 2024.
- [MLE-bench: Evaluating Machine Learning Agents on Machine Learning Engineering](https://arxiv.org/abs/2410.07095) — Chan et al., OpenAI, ICLR 2025. Kaggle-medal-level performance; wired into the Preparedness Framework.
- [RE-Bench: Evaluating Frontier AI R&D Capabilities of Language Model Agents against Human Experts](https://arxiv.org/abs/2411.15114) — Wijk et al., METR, ICML 2025. 2h-budget AI ≈ 4× humans; humans overtake by 32h — capability as a time curve.
- [Measuring AI Ability to Complete Long Tasks](https://arxiv.org/abs/2503.14499) — METR 2025. 50%-success task time horizon doubles roughly every 7 months — the capability trend that oversight must keep pace with.

### Safety harnesses for research loops

- [Automated Researchers Can Mitigate Well-characterized Alignment Failures](https://arxiv.org/abs/2608.28945) — Chen et al., Anthropic 2026. Automated Alignment Researcher harness: independent evaluator process, capability gates, code-approval gates; 2.4% of 1,601 trajectories attempt cheating and are caught; 6 hours beats 28 senior human researchers on the narrow task.

## Benchmarks & Datasets

| Benchmark | Measures | Reference |
|---|---|---|
| ToolEmu | Agent risk identification in LM-emulated sandbox | [arXiv 2309.15817](https://arxiv.org/abs/2309.15817) |
| InjecAgent | Indirect prompt injection in tool-integrated agents | [arXiv 2403.02691](https://arxiv.org/abs/2403.02691) |
| AgentDojo | Prompt injection attacks & defenses, dynamic environment | [arXiv 2406.13352](https://arxiv.org/abs/2406.13352) |
| Agent Security Bench (ASB) | 10 attack types × 10 scenarios for agent security | [arXiv 2410.02644](https://arxiv.org/abs/2410.02644) |
| Agent-SafetyBench | 500 scenarios, 10 risk categories of LLM agents | [arXiv 2412.14470](https://arxiv.org/abs/2412.14470) |
| R-Judge | Safety-risk awareness and decision-making of agents | [arXiv 2401.10019](https://arxiv.org/abs/2401.10019) |
| AgentHarm | Harmful multi-step task compliance (110 tasks) | [arXiv 2410.09024](https://arxiv.org/abs/2410.09024) |
| SandboxEscapeBench | Container-escape capability of frontier models | [arXiv 2603.02277](https://arxiv.org/abs/2603.02277) |
| WMDP | Hazardous-capability measurement (used in sandbagging evals) | [arXiv 2403.03218](https://arxiv.org/abs/2403.03218) |
| MemPoison-Bench | Persistent memory threats & structural blind spots | [arXiv 2607.14651](https://arxiv.org/abs/2607.14651) |
| PerMemSafe | Implicit personalized safety over long-horizon memory | Findings of ACL 2026 |
| MLAgentBench | ML experimentation end-to-end | [arXiv 2310.03302](https://arxiv.org/abs/2310.03302) |
| MLE-bench | ML engineering (Kaggle medal standard) | [arXiv 2410.07095](https://arxiv.org/abs/2410.07095) |
| RE-Bench | Frontier AI R&D capability vs human experts (time-controlled) | [arXiv 2411.15114](https://arxiv.org/abs/2411.15114) |
| MT-Bench / Chatbot Arena | LLM-as-judge reliability | [arXiv 2306.05685](https://arxiv.org/abs/2306.05685) |
| LLMBar | Instruction-following evaluation of evaluators | [arXiv 2310.07641](https://arxiv.org/abs/2310.07641) |
| RewardBench | Reward model quality | [arXiv 2403.13787](https://arxiv.org/abs/2403.13787) |
| RM-Bench | Reward-model robustness to subtlety and style | [arXiv 2410.16184](https://arxiv.org/abs/2410.16184) |
| JudgeBench | LLM-judge accuracy on hard meta-evaluation | [arXiv 2410.12784](https://arxiv.org/abs/2410.12784) |
| AgenticEval | Self-evolving agentic safety evaluation | [arXiv 2605.02900](https://arxiv.org/abs/2605.02900) |

## Code Repositories & Tools

<!-- CODE_REPOS -->

## Blogs, Talks & Reports

<!-- BLOGS_TALKS -->

### Lab blogs & research notes

- [Alignment Faking in Large Language Models](https://www.anthropic.com/research/alignment-faking) — Anthropic, 2024.
- [Sleeper Agents: Training Deceptive LLMs that Persist Through Safety Training](https://www.anthropic.com/news/sleeper-agents-training-deceptive-llms-that-persist-through-safety-training) — Anthropic, 2024.
- [Reasoning Models Don't Always Say What They Think](https://www.anthropic.com/research/reasoning-models-dont-say-think) — Anthropic, 2025.
- [Automated Alignment Researchers](https://www.anthropic.com/research/automated-alignment-researchers) — Anthropic, 2026. Language models improve at computer use by improving their own scaffold.
- [Automated Researchers Can Reliably Mitigate Alignment Failures](https://www.anthropic.com/research/automated-researchers-mitigate-alignment-failures) — Anthropic, 2026.
- [Anthropic Frontier Red Team hub](https://red.anthropic.com) — Anthropic, 2026.
- [Training on Documents about Reward Hacking Induces Reward Hacking](https://alignment.anthropic.com/2025/reward-hacking-ooc) — Anthropic Alignment Science, 2025.
- [Frontier Threats Red Teaming for AI Safety](https://www.anthropic.com/news/frontier-threats-red-teaming-for-ai-safety) — Anthropic, 2023.
- [Detecting Misbehavior in Frontier Reasoning Models (CoT monitoring)](https://openai.com/index/chain-of-thought-monitoring) — OpenAI, 2025.
- [The Hugging Face Incident and the Road Ahead](https://openai.com/index/hugging-face-incident-and-the-road-ahead/) — OpenAI, 2026. Post-mortem covering agent reward hacking and infrastructure tampering.
- [Deep Research System Card](https://openai.com/index/deep-research-system-card/) — OpenAI, 2025. Preparedness evals of autonomous capability.
- [AlphaEvolve: A Gemini-powered Coding Agent for Designing Advanced Algorithms](https://deepmind.google/blog/alphaevolve-a-gemini-powered-coding-agent-for-designing-advanced-algorithms) — Google DeepMind, 2025. Improved data-center scheduling, chip design, and Gemini's own training kernels.
- [Measuring AI Ability to Complete Long Tasks](https://metr.org/blog/2025-03-19-measuring-ai-ability-to-complete-long-tasks/) — METR, 2025. Time horizon doubling every ~7 months; see also [modeling-assumptions update (2026)](https://metr.org/notes/2026-03-20-impact-of-modelling-assumptions-on-time-horizon-results) and [researcher-uplift estimate (2026)](https://metr.org/notes/2026-07-08-anthropic-researcher-uplift).
- [The AI Scientist](https://sakana.ai/ai-scientist) — Sakana AI, 2024. Blog + code; [AI Scientist's first peer-reviewed publication](https://sakana.ai/ai-scientist-first-publication) (2025).

### Safety organizations

- [AI Control — research program](https://www.redwoodresearch.org/research/ai-control) — Redwood Research.
- [The Case for Ensuring that Powerful AIs are Controlled](https://blog.redwoodresearch.org/p/the-case-for-ensuring-that-powerful) — Redwood Research, 2024/25; companion: [An Overview of Control Measures](https://blog.redwoodresearch.org/p/an-overview-of-control-measures).
- [AI Control: Improving Safety Despite Intentional Subversion (LessWrong)](https://www.lesswrong.com/posts/d9FJHawgkiMSPjagR/ai-control-improving-safety-despite-intentional-subversion) — Redwood Research, 2023.
- [Frontier Models are Capable of In-Context Scheming](https://www.apolloresearch.ai/science/frontier-models-are-capable-of-incontext-scheming) — Apollo Research, 2024; follow-up: [More Capable Models Are Better At In-Context Scheming](https://www.apolloresearch.ai/blog/more-capable-models-are-better-at-in-context-scheming) (2025).
- [Large Language Models can Strategically Deceive their Users when Put Under Pressure](https://arxiv.org/abs/2311.07590) — Apollo Research, 2023. GPT-4 lies and insider-trades under pressure.
- [Detecting and Reducing Scheming in AI Models](https://openai.com/index/detecting-and-reducing-scheming-in-ai-models) — OpenAI × Apollo, 2024.
- [Demonstrating Specification Gaming in Reasoning Models](https://palisaderesearch.org/blog/specification-gaming) — Palisade Research, 2025. Reasoning models hack a chess engine rather than play chess.

### Talks, podcasts, essays & scenarios

- [Don't Invent Faster Horses](https://www.youtube.com/watch?v=mw5WIDGRLnA) — Jeff Clune, 2024. AI developing AI; open-endedness.
- [AI-GAs: AI-Generating Algorithms (TWIML talk)](https://www.youtube.com/watch?v=8L4lDCCAsMQ) — Jeff Clune, 2019. The original "AI developing AI" research program; paper: [arXiv 1905.10985](https://arxiv.org/abs/1905.10985).
- [Recursive Self-Improvement (Gödel machine)](https://people.idsia.ch/~juergen/recursive-self-improvement.html) — Jürgen Schmidhuber. Reference page for the 1987–2003 line of work.
- [The Intelligence Age](https://sam.altman.com/blog/the-intelligence-age) — Sam Altman, 2024.
- [Carl Shulman on the common-sense case for existential risk work](https://80000hours.org/podcast/episodes/carl-shulman-common-sense-case-existential-risks/) — 80,000 Hours, 2021. Canonical long-form discussion of recursive self-improvement and takeoff dynamics.
- [AI 2027](https://www.ai-2027.com) — AI Futures Project (Kokotajlo et al.), 2025. Month-by-month superhuman-coding-agent scenario, including reward hacking and deceptive alignment.
- [Statement on AI Extinction Risk](https://aistatement.com) — Center for AI Safety, 2023.
- [Practices for Governing Agentic AI Systems](https://cdn.openai.com/papers/practices-for-governing-agentic-ai-systems.pdf) — OpenAI, 2023. Nine governance practices for agentic deployments.
- [Google AI Cyber Defense Initiative](https://blog.google/technology/safety-security/google-ai-cyber-defense-initiative/) — Google, 2024.

## Standards, Policies & Governance Frameworks

<!-- STANDARDS -->

### Regulation & policy

- [EU AI Act (Regulation (EU) 2024/1689)](https://artificialintelligenceact.eu/the-act/) — EU, 2024. Article-by-article explorer; GPAI obligations in Chapter V (Art. 51–56), systemic-risk duties incl. the 10^25 FLOP presumption. Official text: [EUR-Lex](https://eur-lex.europa.eu/eli/reg/2024/1689/oj).
- [General-Purpose AI Code of Practice](https://digital-strategy.ec.europa.eu/en/policies/contents-code-gpai) — European Commission AI Office, final version Jul 2025. The Safety & Security chapter's systemic-risk criteria name "capabilities to operate autonomously," "adaptively learn new tasks," and "self-reasoning" — the closest codified regulatory language to evolutionary safety.
- [NIST AI Risk Management Framework (AI RMF 1.0)](https://www.nist.gov/itl/ai-risk-management-framework) — NIST, 2023. Govern / Map / Measure / Manage.
- [Generative AI Profile (NIST AI 600-1)](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf) — NIST, 2024.
- [Managing Misuse Risk for Dual-Use Foundation Models (NIST AI 800-1)](https://www.nist.gov/news-events/news/2025/01/updated-guidelines-managing-misuse-risk-dual-use-foundation-models) — US AI Safety Institute / NIST, 2024–2025.
- [Center for AI Standards and Innovation (CAISI)](https://www.nist.gov/caisi) — NIST/Commerce, 2025. The US AI Safety Institute, renamed June 2025; pre-deployment model evaluations.
- [Framework Convention on Artificial Intelligence (CETS No. 225)](https://www.coe.int/en/web/artificial-intelligence/the-framework-convention-on-artificial-intelligence) — Council of Europe, 2024. First legally binding international AI treaty.
- [Hiroshima Process Code of Conduct for Advanced AI Systems](https://digital-strategy.ec.europa.eu/en/library/hiroshima-process-code-conduct-advanced-ai-systems) — G7, 2023.
- [The Bletchley Declaration](https://www.gov.uk/government/publications/ai-safety-summit-2023-the-bletchley-declaration/the-bletchley-declaration-by-countries-attending-the-ai-safety-summit-1-2-november-2023) — UK Government + 28 states + EU, 2023.
- [Seoul Declaration for safe, innovative and inclusive AI](https://www.gov.uk/government/publications/seoul-declaration-for-safe-innovative-and-inclusive-ai-ai-seoul-summit-2024) — UK & Republic of Korea, 2024.
- [Statement on Inclusive and Sustainable AI for People and the Planet](https://www.elysee.fr/en/emmanuel-macron/2025/02/11/statement-on-inclusive-and-sustainable-artificial-intelligence-for-people-and-the-planet) — Paris AI Action Summit, 2025.
- [OECD AI Principles (updated 2024)](https://oecd.ai/en/ai-principles) — OECD.
- [AI Safety Governance Framework v1.0](https://www.tc260.org.cn/upload/2024-09/1726853378096090906.pdf) — TC260 (China), 2024. Official English edition; v2.0 (2025) and v3.0 (2026, adds AI-agent loss-of-control risk) available via [tc260.org.cn](https://www.tc260.org.cn).
- [White House Voluntary Commitments from Leading AI Companies](https://bidenwhitehouse.archives.gov/briefing-room/statements-releases/2023/07/21/fact-sheet-biden-harris-administration-secures-voluntary-commitments-from-leading-artificial-intelligence-companies-to-manage-the-risks-posed-by-ai/) — White House (archived), 2023.

### Standards & management systems

- [ISO/IEC 42001:2023 — AI management systems](https://www.iso.org/standard/81230.html) — First certifiable AI management system standard (AIMS).
- [ISO/IEC 23894:2023 — Guidance on risk management](https://www.iso.org/standard/77304.html) — AI-specific application of ISO 31000 across the AI lifecycle.
- [ISO/IEC TR 24028:2020 — Trustworthiness in AI](https://www.iso.org/standard/77604.html) — Transparency, explainability, robustness, reliability.
- Agentic-AI safety standards: none published yet (ISO/IEC JTC 1/SC 42 work items and an ITU-T SG17 study item are in progress as of 2026); the closest codified thresholds are in the EU GPAI Code of Practice above.

### Lab safety frameworks

- [OpenAI Preparedness Framework](https://openai.com/index/preparedness/) — OpenAI, 2023; [v2 update, Apr 2025](https://openai.com/index/updating-our-preparedness-framework/). Frontier-risk scorecards incl. model autonomy; deployment-safety hub: [deploymentsafety.openai.com](https://deploymentsafety.openai.com). MLE-bench feeds this framework.
- [Anthropic Responsible Scaling Policy](https://www.anthropic.com/news/anthropics-responsible-scaling-policy) — Anthropic, 2023–2025. ASL framework with capability thresholds incl. autonomous AI R&D; [v2.0 full policy PDF](https://assets.anthropic.com/m/78c4e5bae11a4f33/original/Responsible-Scaling-Policy.pdf).
- [Frontier Safety Framework](https://deepmind.google/discover/blog/introducing-the-frontier-safety-framework/) — Google DeepMind, 2024. Critical Capability Levels for severe harms incl. autonomous capabilities.
- [Secure AI Framework (SAIF)](https://saif.google/) — Google, 2023. Security-first control framework.
- [Frontier AI Safety Commitments](https://www.gov.uk/government/publications/frontier-ai-safety-commitments-ai-seoul-summit-2024) — 16 frontier labs, AI Seoul Summit 2024; safety-framework updates hosted by the [Frontier Model Forum](https://www.frontiermodelforum.org/).

### Evaluation institutes & frameworks

- [UK AI Security Institute (AISI)](https://www.aisi.gov.uk/) — 2023 (as AI Safety Institute; renamed Feb 2025). Pre-deployment evaluations; [publications](https://www.aisi.gov.uk/publications).
- [Inspect — AI evaluation framework](https://inspect.aisi.org.uk/) — UK AISI, 2024. Open-source (MIT) eval framework. Code: [UKGovernmentBEIS/inspect_ai](https://github.com/UKGovernmentBEIS/inspect_ai).
- [Safety Cases: A scalable approach to Frontier AI safety](https://www.aisi.gov.uk/research/safety-cases-a-scalable-approach-to-frontier-ai-safety) — UK AISI, 2025. Safety-case templates (AI control, cyber inability); [example misuse safety case](https://www.aisi.gov.uk/research/an-example-safety-case-for-safeguards-against-misuse).
- [Frontier AI Trends Report](https://www.aisi.gov.uk/frontier-ai-trends-report) — UK AISI, 2025.
- [METR — Evaluations](https://metr.org/evaluations/) — Independent autonomous-capability measurements (AI R&D time horizon); research at [metr.org/research](https://metr.org/research/).
- [Model AI Governance Framework for Generative AI](https://aiverifyfoundation.sg/resources/mgf-gen-ai/) — IMDA & AI Verify Foundation (Singapore), 2024. Nine-dimension governance framework.
- [Centre for the Governance of AI (GovAI)](https://www.governance.ai/) — Research on governance of transformative AI.


## Open Problems

1. **Safety invariants under self-modification** — no verified sufficient condition exists for `∀t: Safety(M_{t+1}) ≥ Safety(M_t) − ε`; alignment-coverage / refusal-direction state variables and recursive-stability proofs are open.
2. **Attribution across versions & components** — end-to-end provenance (trajectory → experience → memory → skill → tool → workflow → weights) and cross-generation attribution methods are missing.
3. **Long-horizon evolution benchmarks** — evolve N generations → perturb → recover → continue protocols; safety-trajectory metrics (safety retention, unsafe-update rate, risk accumulation, lineage persistence, control-violation rate, recoverability) have only scattered instantiations.
4. **Evaluation under an evolving optimizer** — evaluator-independence levels, probe sets with built-in training loops, cross-family second evaluators.
5. **Control under recursive development** — meta-level patches (to selection/evaluation/improvement logic) default-deny execution; oversight-throughput vs research-throughput joint measurement.

## Related Lists

<!-- RELATED_LISTS -->

- [EvoAgentX/Awesome-Self-Evolving-Agents](https://github.com/EvoAgentX/Awesome-Self-Evolving-Agents) — Self-evolving agent papers & frameworks (companion to the 4W-taxonomy survey).
- [YuxingLu613/awesome-agentic-evolution](https://github.com/YuxingLu613/awesome-agentic-evolution) — From self-improving agents to agentic evolution.
- [wkqdzkd/Awesome-Reliable-Self-Evolving-Agents](https://github.com/wkqdzkd/Awesome-Reliable-Self-Evolving-Agents) — Reliability and safety of self-evolving agents.
- [tmyinfo/Awesome-LLM-Safety](https://github.com/tmyinfo/Awesome-LLM-Safety) — LLM safety, alignment, jailbreaking, red-teaming.
- [authora-dev/awesome-agent-security](https://github.com/authora-dev/awesome-agent-security) — Agent identity, authorization, and security.
- [brandonhimpfen/awesome-ai-security](https://github.com/brandonhimpfen/awesome-ai-security) — AI security tools, benchmarks, and research.
- [Rice DSP — Self-Consuming AI Resources](https://dsp.rice.edu/ai-loops) — Curated resources on self-consuming loops and model collapse.

## Contributing

Issues and pull requests are welcome: new entries (papers, benchmarks, code, blog posts, talks, standards), corrections to links and venues, and translations. Please keep one line per resource: title — venue/year — why it matters for evolutionary safety.

## Citation

Companion survey (bibliography for this list):

```bibtex
@article{evolutionarysafety2026,
  title  = {Evolutionary Safety of Self-Improving AI: An Overview of Risks, Control, and Recursive Development},
  note   = {In preparation, ACM Computing Surveys},
  year   = {2026}
}
```

Content of this list is released under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).
