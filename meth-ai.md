# AI应用方法论

生成式AI正在重塑软件产品的需求定义与设计范式。**传统软件工程中"确定性规格驱动开发"的核心假设在AI应用中不再成立**——输出是概率性的、能力是涌现的、用户期望是模糊的。本方法论综合了Google PAIR、Anthropic、OpenAI、Microsoft HAX等业界领先框架，以及2024-2025年最新学术研究，为生成式AI应用（LLM对话产品、AI Agent、RAG系统、传统应用AI增强、开发框架AI化等）提供系统性的需求分析与设计指导。其核心洞见是：**AI应用的需求与设计必须从"规格驱动"转向"目标驱动+评估驱动"的双轮模式**，在持续迭代中发现能力边界、校准用户期望、构建信任闭环。

---

## 一、需求分析

相较于传统软件，AI应用的需求没那么具体，存在更大的未知程度。可以基于**目标**来进行分析、定义。

### 1.1 AI应用需求分析与传统软件的核心差异

一项涵盖**126篇研究**的系统性综述（Habiba et al., 2024）指出，当前的需求工程方法不足以适应AI系统的构建。两者的根本差异体现在以下维度：

| 维度 | 传统软件 | AI应用 |
|------|---------|--------|
| 确定性 | 相同输入产生相同输出 | 概率性输出，准确率以百分比衡量 |
| 规格来源 | 规格说明驱动系统行为 | 数据定义系统行为，规格只描述目标 |
| 行为可预测性 | 可测试、可预期 | 上下文依赖，涌现行为不可完全预知 |
| 需求稳定性 | 确定后相对稳定 | 持续演化——模型迭代改变系统行为 |
| 质量属性 | 性能、可靠性、安全性 | +可解释性、公平性、幻觉率、伦理合规 |
| 数据角色 | 数据被系统处理 | 数据*塑造*系统能力，是核心约束条件 |

其中最关键的范式转变是：**在传统软件中，需求定义功能边界；在AI应用中，需求定义目标与约束，而能力边界需要在开发和评估中逐步发现**。中文社区将此总结为"用户在接入AI之前无法预估自己的期望"——用户意图与模型能力之间存在高度非对称性。

这种不确定性要求需求分析从"我要系统做什么"转向"我希望达到什么目标，可接受的偏差范围是什么"。OpenAI在其2025年发布的hallucination研究中也揭示了根源：语言模型产生幻觉，部分原因在于标准的训练和评估流程奖励了猜测而非承认不确定性（OpenAI, 2025a）——这意味着需求定义必须显式地将不确定性管理纳入范围。

### 1.2 基于目标的需求定义方法论

#### 目标分析框架

基于KAOS（Keep All Objectives Satisfied）目标建模方法，结合2025年最新的AI需求工程研究（Alrajeh et al., 2025），建议将AI应用需求组织为以下**六类目标**：

**目标A：已知工作自动化（效率目标）**
- A1 减少人工劳动——可量化：节省时间、降低成本
- A2 降低重复性任务的错误率
- A3 提升处理吞吐量与速度
- 需求操作化：定义AI模型与人工审核者的职责分配，设定准确率阈值，明确自动化边界

**目标B：分析、预测未知问题（智能目标）**
- B1 非结构化数据中的模式发现
- B2 带置信度评分的预测分析
- B3 异常检测与预警
- 需求操作化：软目标（softgoal）定义"可接受的预测准确度"，障碍分析识别"误报率"风险

**目标C：在使用过程中学习（适应目标）**
- C1 通过反馈回路纠正错误
- C2 个性化适配用户偏好
- C3 性能随时间持续改进——需设定可度量的基线
- 需求操作化：建模人机协作的反馈闭环，定义学习周期与效果衡量标准

**目标D：安全与合规（约束目标）**
- Maintain[伦理行为]、Avoid[有害输出]、Maintain[法规合规]
- 这是AI应用独有的"硬约束"目标类，传统软件中通常不需要此层级的显式建模

**目标E：可解释性与信任（体验目标）**
- Achieve[用户理解AI决策]、Maintain[透明度]、Achieve[适当的信任校准]
- 信任过高或过低都是问题——目标是"校准的信任"（calibrated trust）

**目标F：优雅降级（韧性目标）**
- Maintain[无AI时的服务可用性]、Avoid[AI失败时的死胡同]
- Google PAIR明确指出：当系统不确定或无法完成请求时，确保存在不依赖AI的默认用户体验（Google PAIR）

#### 目标与数据的双向约束关系

2025年KAOS应用于ML系统的最新研究揭示了一个AI需求工程的独特发现：**数据需求约束目标的细化选择，而目标的分解又反过来塑造数据质量期望**（Alrajeh et al., 2025）。这意味着AI应用的需求分析不是线性的，而是目标定义与数据评估之间的迭代往复过程。

### 1.3 AI应用特有的需求维度

传统软件的需求维度（功能/非功能/约束）在AI应用中需要扩展为以下**六大维度**：

**数据需求**是AI应用最根本的差异点。Enterprise Knowledge建议：AI项目的范围主要由两个因素驱动——用例和可用数据（Enterprise Knowledge, 2024）。具体包括数据质量（完整性、准确性、一致性、时效性）、数据量（最小训练数据阈值、持续采集策略）、隐私合规（GDPR/个人信息保护法）、偏见检测（代表性采样、公平性指标）以及数据血缘追踪。

**模型能力需求**需要用AI特有的指标定义。Filev（2025）在InfoWorld上提出了AI Agent非功能性需求的实用框架：**F1分数**（如要求最低0.85）、**幻觉率**（事实性错误频率）、**延迟指标**（首Token时间、末Token时间、端到端执行延迟）、**单次查询成本**（Token消耗、API调用费用）、**用户满意度评分**以及**对抗测试结果**。他精辟地指出：构建AI体验的团队需要评估模型做了什么和它表现如何——功能性基准检查有用性和准确性，但不衡量体验的速度和流畅度。

**交互设计需求**方面，Microsoft HAX Toolkit从150余条AI设计建议中提炼出**18条可在UI层面观察和验证的具体指南**，覆盖首次交互、使用过程、出错时和长期使用四个阶段（Amershi et al., 2019）。关键原则是：交互需求必须具体到可测试，而非停留在"建立信任"这样的抽象层面。

**可解释性需求**应区分三个层次：全局理解（系统整体工作原理）、局部理解（具体决策的解释）、功能理解（能力范围和使用方式）。需求规格应明确每个场景需要哪个层次的解释。

**安全与伦理需求**采用Microsoft的分层安全栈模型：用户体验层→系统消息与接地层→安全系统层→模型层，六大原则为公平性、可靠性与安全性、隐私与安全、包容性、透明度、问责制（Microsoft HAX Toolkit）。

**信任与反馈需求**是AI应用独有的长期体验维度。研究显示AI系统的开发速度往往快于用户的接受准备度，导致低信任（Tpmap, 2024）。信任发展遵循一个闭环：用户信任→影响依赖方式→产生结果→反馈调整信任。初始阶段**过度信任**很常见，随后经历校正。需求应显式定义信任建立的机制和节奏。

### 1.4 处理模糊需求与涌现能力

Wei et al.（2022）对涌现能力的形式化定义为：如果一个能力在小模型中不存在、但在大模型中出现，则称其为涌现能力。Georgetown CSET的分析指出这些能力是被发现的而非被设计的（CSET, 2022）——这对需求工程构成根本性挑战：**你无法为尚未发现的能力编写需求规格**。

应对策略包括以下几个层面：

**能力单元分解法**。中文社区（CSDN, 2025）提出将AI产品需求从传统的"功能分解"转变为"能力单元分解"——每个能力单元回答三个问题：能否回应？如何回应？回应准确度如何？这种方法将模糊的AI能力锚定为可评估的单元。

**原型驱动的需求获取（PRE4AIM）**。Yildirim et al.（2024）发布的这一方法包含四个阶段：准备（识别AI项目和利益相关方）→价值探索（理解需求，参与者表达了对可靠性和结果信任的关切，并显示出需要保持控制）→方案发现（探索解决方案和质量控制需求）→迭代原型。核心原则是通过**涌现式设计**和**原型演示设定现实期望**。

**能力发现框架**。综合研究建议采用五步流程：探索阶段（跨模型规模运行对比实验）→验证阶段（可复现测试、分阶段发布、评估生产稳定性）→风险评估（识别有害涌现行为、部署防护栏）→集成阶段（监控性能、追踪回归、构建持续评估套件）→治理（记录行为和限制、维持利益相关方一致）。

**迭代式KPI定义**。McKinsey（2024）观察到生成式AI产品的功能定义、原型开发和测试全部在并行且前所未有地快速进行。AI项目的KPI定义本身就是一个迭代过程——初始KPI包含假设，需要在实践中逐步验证和更新。

### 1.5 用户体验需求的特殊性

**容错与优雅降级**。Google PAIR指导原则要求：当AI功能失败时，不要创建死胡同（Google PAIR）。关键洞见是：如果用户的心智模型包含"系统会随时间学习"的概念，那么首次失败就变成了建立反馈关系的机会，而非灾难。需求应定义AI功能不可用时的完整备选路径。

**信任建立**需要六层机制：透明度（预先说明能力与局限）、置信度展示（系统不确定时明确告知）、渐进式披露（从简单到详细的分层解释）、来源引用（将输出锚定在可验证的信息上）、人机协作（关键决策保持人工监督）、一致性行为（使用熟悉的设计模式和清晰的语言）。

**反馈闭环**分为隐式反馈（用户行为自然暗示AI改进方向，如选择某首歌确认其相关性）和显式反馈（刻意评价，如点赞/点踩、纠正）。Google PAIR强调：不要只是感谢用户——要展示反馈将如何使他们受益；如果反馈并未真正连接到模型改进，不匹配的期望会造成困惑（Google PAIR）。

**心智模型管理**是AI应用UX需求中最关键但最易被忽视的维度。Google PAIR的研究框架发现：用户可能因"AI魔法"营销而高估产品的实际能力，从而为失望埋下伏笔。产品应在用户首次交互时就坦诚地说明产品能做什么和不能做什么，并通过**分阶段引导**（营销→首次使用→功能逐步展示）来校准心智模型（Google PAIR）。

### 1.6 非功能性需求的AI特殊考量

AI应用的非功能性需求维度远比传统软件复杂，建议按以下分类进行系统定义：

**性能类NFR**：首Token延迟（影响用户对"响应性"的感知）、端到端完成时间、并发用户处理能力、Token吞吐量。延迟容忍度随场景变化——交互式对话需要秒级响应，批处理分析可以接受分钟级。

**质量类NFR**：准确率/召回率/F1分数（可按场景分别定义阈值）、幻觉率（可通过事实核查评估）、一致性（同一问题多次回答不应自相矛盾）、完整性（是否覆盖所需信息的所有方面）。中文社区建议采用ICE框架（Impact影响力, Confidence置信度, Ease实施难度）对这些指标进行优先级排序（CSDN, 2025）。

**成本类NFR**：单次查询Token成本、月度API调用预算上限、成本与质量的权衡策略（不同场景可使用不同规格的模型）。

**安全类NFR**：有害响应率（将辱骂性或欺骗性响应转化为可量化的功能指标）、对抗性攻击抵御能力、PII泄露率、提示注入防御率（Filev, 2025）。

**运维类NFR**：可观测性（日志、监控、漂移检测）、可维护性（模型重训练流水线、版本管理）、模型可替换性（更换底层模型时的回归测试覆盖率）。


---

## 参考文献

### 学术研究

1. **Habiba, U.E., Haug, M., Bogner, J. & Wagner, S.** (2024). "How Mature is Requirements Engineering for AI-based Systems? A Systematic Mapping Study on Practices, Challenges, and Future Research Directions." *Requirements Engineering*, 29(4), 567-600.
   https://link.springer.com/article/10.1007/s00766-024-00432-3

2. **Wei, J., Tay, Y., Bommasani, R. et al.** (2022). "Emergent Abilities of Large Language Models." *Transactions on Machine Learning Research*.
   https://arxiv.org/abs/2206.07682

3. **Alrajeh, D. et al.** (2025). "Data-Dependent Goal Modeling for ML-Enabled Systems." *arXiv:2601.06237*.
   https://arxiv.org/abs/2601.06237

4. **Ahmad, K. et al.** (2023). "Requirements Engineering for Artificial Intelligence Systems: A Systematic Mapping Study." *Information and Software Technology*, 158.
   https://www.sciencedirect.com/science/article/abs/pii/S0950584923000307

5. **Yildirim, N. et al.** (2024a). "Requirements Elicitation for Prototype-driven AI (PRE4AIM)." *CEUR Workshop Proceedings*, Vol. 3959.
   https://ceur-ws.org/Vol-3959/PT-paper4.pdf

6. **Yildirim, N. et al.** (2024b). "Agent Design Pattern Catalogue: A Collection of Architectural Patterns for Foundation Model based Agents." *arXiv:2405.10467*.
   https://arxiv.org/html/2405.10467v2

7. **Amershi, S. et al.** (2019). "Guidelines for Human-AI Interaction." *CHI 2019*.
   https://www.microsoft.com/en-us/research/blog/guidelines-for-human-ai-interaction-design/

### 业界设计指南

8. **Google PAIR** — People + AI Guidebook.
   https://pair.withgoogle.com/

9. **Anthropic** (2024). "Building Effective Agents."
   https://www.anthropic.com/research/building-effective-agents

10. **Anthropic** (2025a). "Demystifying Evals for AI Agents."
    https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents

11. **Anthropic** (2025b). "Effective Context Engineering for AI Agents."
    https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents

12. **OpenAI** (2025a). "Why Language Models Hallucinate."
    https://openai.com/index/why-language-models-hallucinate/

13. **OpenAI** (2025b). "A Practical Guide to Building Agents."
    https://openai.com/business/guides-and-resources/a-practical-guide-to-building-ai-agents/

14. **Microsoft** — HAX Toolkit: Guidelines for Human-AI Interaction.
    https://www.microsoft.com/en-us/haxtoolkit/ai-guidelines/

### 架构设计模式

15. **Fowler, M. / Thoughtworks** (2025). "Emerging Patterns in Building GenAI Products."
    https://martinfowler.com/articles/gen-ai-patterns/

16. **Google / InfoQ** (2026). "Google's Eight Essential Multi-Agent Design Patterns."
    https://www.infoq.com/news/2026/01/multi-agent-design-patterns/

17. **Databricks** — Agent System Design Patterns.
    https://docs.databricks.com/aws/en/generative-ai/guide/agent-system-design-patterns

18. **Microsoft Azure** — AI Agent Orchestration Patterns.
    https://learn.microsoft.com/en-us/azure/architecture/ai-ml/guide/ai-agent-design-patterns

19. **Lakshmanan, V. & Hapke, H.** (2024). *Generative AI Design Patterns: Solutions to Common Challenges*. O'Reilly Media.
    https://github.com/lakshmanok/generative-ai-design-patterns

20. **Koc, V.** (2024). "Generative AI Design Patterns: A Comprehensive Guide." *Medium / TDS Archive*.
    https://medium.com/data-science/generative-ai-design-patterns-a-comprehensive-guide-41425a40d7d0

### 评估驱动开发

21. **evaldriven.org** — Eval-Driven Development 社区宣言与方法论.
    https://evaldriven.org/

22. **Husain, H.** (2024). "LLM Evals: Everything You Need to Know."
    https://hamel.dev/blog/posts/evals-faq/

### UX与交互设计

23. **Nielsen Norman Group (NN/g)** (2024). "The UX of AI: Lessons from Perplexity."
    https://www.nngroup.com/articles/perplexity-henry-modisett/

24. **Nielsen Norman Group (NN/g)** — AI相关研究文章合集.
    https://www.nngroup.com/topic/ai/

25. **Salesforce** (2025). "6 UX Design Tips to Make AI Trustworthy and Easier to Use."
    https://www.salesforce.com/blog/6-ux-design-tips-trust-ai/

26. **Data Studios** (2026). "GitHub Copilot vs Cursor AI: 2026 Deep Comparison."
    https://www.datastudios.org/post/github-copilot-vs-cursor-ai-2026-deep-comparison-of-features-pricing-workflow-fit-and-developer

### 非功能性需求

27. **Filev, A.** (2025). "How to Write Nonfunctional Requirements for AI Agents." *InfoWorld*.
    https://www.infoworld.com/article/4061123/how-to-write-nonfunctional-requirements-for-ai-agents.html

### Prompt Engineering

28. **Gupta, A.** (2025). "Prompt Engineering in 2025: The Latest Best Practices."
    https://www.news.aakashg.com/p/prompt-engineering

29. **Symphonize** (2025). "What Business Leaders Should Know About Prompt Engineering."
    https://www.symphonize.com/tech-blogs/what-business-leaders-should-know-about-prompt-engineering

### 其他参考

30. **Enterprise Knowledge** (2024). "AI Beyond a Prototype."
    https://enterprise-knowledge.com/beyond-ai-prototypes/

31. **Georgetown CSET** (2022). "Emergent Abilities in Large Language Models: An Explainer."
    https://cset.georgetown.edu/article/emergent-abilities-in-large-language-models-an-explainer/

32. **CSDN** (2025). "AI产品的需求拆解与技术可行性评估方法论."
    https://blog.csdn.net/sinat_28461591/article/details/149131262

33. **Cloudflare / Anthropic Patterns** — Agent设计模式实现参考.
    https://github.com/cloudflare/agents/blob/main/guides/anthropic-patterns/README.md
