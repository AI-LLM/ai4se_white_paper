# GenAI/LLM 生成软件的过程质量标准与研究报告

> 报告日期：2026年3月27日

---

## 1. 概述

随着大语言模型（LLM）和生成式人工智能（GenAI）在软件开发中的广泛应用，如何从**过程**角度评价 AI 生成代码的质量和可信度，已成为行业前沿的核心议题。传统的软件工程过程质量标准假设代码由人类在可理解、可追溯、可审计的过程中编写，而 AI 生成代码打破了这些基本假设，带来了全新的过程挑战。

目前，针对 GenAI 生成软件的过程质量标准和研究仍处于早期阶段，尚未形成如传统软件工程般成熟的体系，但已涌现出若干重要的标准框架、方法论和学术研究。

---

## 2. GenAI 生成代码带来的根本性过程挑战

### 2.1 自一致性陷阱（Self-Consistent Artifact Problem）

AI 能够同时生成代码、测试和文档，三者之间完全一致——但可能全部是错的。标准 QA 流程无法发现此类问题，因为测试验证的是 AI 的理解，而非开发者的需求。这是传统过程标准完全没有考虑过的场景。[^1]

### 2.2 结构性缺陷

研究表明，LLM 生成的代码比人工代码存在显著更多的缺陷，包括 30–41% 更多的技术债务和 39% 更高的认知复杂度。[^2] 一项系统性研究确认，所有被评估的模型都会产出问题，没有任何模型能一致性地生成无缺陷的代码，缺陷类型涵盖影响可维护性的代码异味、影响运行时可靠性的 bug，以及严重的安全漏洞。[^3]

### 2.3 安全性未随模型进步而改善

Veracode 的 2025 年 GenAI 代码安全报告发现，45% 的代码样本未通过安全测试并引入了 OWASP Top 10 安全漏洞。更令人担忧的是，虽然模型在生成功能正确的代码方面不断改进，但在安全性方面的表现基本没有提升，无论模型大小或训练方法如何演进。[^4]

---

## 3. 已有的标准和框架

### 3.1 ISO/IEC 42001 — AI 管理系统标准

ISO/IEC 42001 是全球首个 AI 管理系统（AIMS）标准，于 2023 年 12 月发布，为组织建立、实施、维护和持续改进人工智能管理系统提供了要求和指导。[^5] 其核心关注点包括：

- 风险管理与 AI 系统影响评估
- 系统生命周期管理
- 第三方供应商监督
- 治理与问责

该标准与 EU AI Act 紧密关联，帮助组织展示对 AI 法案的合规性。[^6] 对于使用 LLM 生成代码的组织而言，ISO/IEC 42001 提供了将 AI 工具纳入过程治理的框架，但它是通用的 AI 管理标准，并非专门针对代码生成场景。

2025 年 4 月，ISO 又发布了 **ISO/IEC 42005:2025** 作为补充标准，提供 AI 系统影响评估的结构化指导。[^7]

### 3.2 SENAR 方法论 — AI 原生软件开发方法论

SENAR（v1.2，2026 年 3 月发布）是首个专门为 AI 辅助软件开发设计的过程方法论，定位为开放标准且永久免费。[^1] 其核心过程要求包括：

- **需求先于代码**：AI 接收的是结构化上下文（目标、验收标准、范围边界），而非模糊的提示。
- **人工独立验证**：验证对照验收标准进行，而非"看起来对"就行。每个验收标准独立对照需求检查，而非对照 AI 的输出。AI 生成的测试不算数。
- **死胡同文档化**：用一句话记录"方案 X 失败，原因是 Y"，防止跨会话重复同样的失败。
- **模型版本即供应链管理**：模型版本变更等同于编译器版本变更，必须重新校准基线、重新验证质量门禁。SENAR 将 AI 模型治理视为供应链管理问题。
- **九项度量指标**：包括首次通过率（First-Pass Success Rate）、缺陷逃逸率（Defect Escape Rate）、吞吐量、交付周期等。

### 3.3 SENAI 研究框架 — 软件工程原生生成式 AI

SENAI 是 2025 年发表的一篇愿景论文，主张将软件工程知识整合到 LLM 中，使其超越单纯的功能正确性，在执行生成任务时能遵循软件工程原则和最佳实践。[^8] 其核心贡献包括：

- **丰富训练数据**：建议在训练中加入 UML 图、架构决策记录（ADR）等软件制品，而非仅有代码，让模型理解编码结构背后的意图。[^9]
- **Bloom 分类法评估框架**：提出用 Bloom 分类法评估 LLM 对软件工程知识的内化程度，不仅评估代码正确性，还评估模型在多大程度上能应用、分析和创造符合软件工程原则的代码。[^9]
- **强化学习对齐**：建议整合基于软件工程标准提供反馈的强化学习技术，引导模型更紧密地遵循最佳实践。[^9]

### 3.4 SE 3.0 愿景 — AI 原生软件工程

该研究提出从 AI 辅助的软件工程（SE 2.0）转向 AI 原生软件工程（SE 3.0），其特征是以意图为中心、以对话为导向的开发模式，人类开发者与 AI 队友协作。[^10] 它指出了当前 Copilot 模式的根本缺陷：

- 当前的 Copilot 基本上只能添加代码，而资深工程师经常使用设计模式和重构技术来精简代码、创建封装抽象、提高复用性。
- 提出的技术栈包括：Teammate.next（自进化个性化 AI 伙伴）、IDE.next（意图中心开发环境）、Compiler.next（多目标代码合成）、Runtime.next（SLA 感知执行）。

### 3.5 系统理论质量保障框架

该研究提出将 AI 使能的软件系统理解为动态系统——有状态的自适应系统，其行为依赖于先前输入、反馈和环境交互。从这个视角出发，质量保障变成了通过执行约束和设计稳健的反馈与控制机制来维持稳定性的问题。[^11] 这代表了一种根本性的范式转变：传统 QA 假设软件行为是确定性的，但 AI 生成的系统引入了非确定性和持续学习，需要全新的保障思维。

---

## 4. 过程质量的实践工具和方法

### 4.1 静态分析作为过程基线

静态分析工具在 LLM 驱动的开发范式中变得尤为重要，因为它们能提供一个一致的、客观的质量和安全基线，而这并非概率性生成模型的固有特征。随着 LLM 日益融入软件开发，静态分析工具的功能可能从质量和安全保障措施演变为负责任 AI 采用的组成部分。[^3]

代表性工具如 SonarQube 的 AI Code Assurance 功能，专门针对 AI 生成代码提供严格的质量门禁和安全检查。[^12]

### 4.2 多维评估协议

新兴的代码评估不再仅关注功能正确性，而是扩展到多个维度：

- **效率评估**：ENAMEL 等基准将 pass@k 指标推广到效率维度（eff@k），通过与人类专家参考方案对比来衡量执行性能。[^13]
- **安全与功能平衡**：SAFE@k 等指标鼓励在安全性不损害可用性的前提下给予部分评分。[^13]
- **许可证合规**：LiCoEval 评估 LLM 是否为与受版权保护代码高度相似的输出提供准确的许可信息。[^13]
- **演化感知评估**：评估协议需要管理多文件、依赖和演化感知的上下文，跟踪模型如何推理内部交叉引用和第三方 API。[^13]

### 4.3 "Vibe, Then Verify" 工作流

面对 AI 代码产出量的大幅增长，行业正在形成一种新的工作流模式：开发者可以自由地以 AI 为创意伙伴进行"vibe coding"，但同时需要一个严格的自动化框架来验证每一行代码是否符合标准。[^14]

---

## 5. 当前差距与建议

### 5.1 核心差距

传统过程标准（CMMI、ISO 12207 等）与 AI 生成代码的现实之间存在巨大鸿沟。这些标准假设人类全程可控、可追溯、可理解每一个决策。AI 生成代码从根本上破坏了这些假设。

上下文缺失是最普遍的问题。研究显示，在认为 AI 降低了代码质量的开发者中，44% 将原因归咎于上下文缺失；即使在认为 AI 改善了质量的开发者中，仍有 53% 希望获得更好的上下文理解。[^15]

### 5.2 实践建议

对于正在使用 AI 生成代码的组织，从过程质量角度需要特别关注以下方面：

1. **将 AI 视为不可信的供应商**：对其输出施加与外部采购代码同等甚至更严格的验收标准。
2. **建立独立于 AI 的验证机制**：AI 生成的测试不能用来验证 AI 生成的代码——这是自一致性陷阱的核心。验收标准必须在 AI 介入之前由人工制定。
3. **追踪 AI 生成代码的占比和质量数据**：建立与人工代码对比的度量基线，持续监控技术债务趋势和缺陷逃逸率。
4. **将模型版本变更纳入配置管理**：像对待编译器升级一样对待模型切换，重新校准基线并重新验证质量门禁。
5. **在 CI/CD 流水线中嵌入 AI 代码专用质量门禁**：利用静态分析工具对 AI 生成代码施加额外的安全和质量检查。
6. **文档化失败路径**：防止 AI 在不同会话中重复尝试已知失败的方案。

---

## 6. 参考资料

[^1]: SENAR — Methodology for AI-Native Software Development (v1.2, 2026). https://senar.tech/en/

[^2]: GenAI Code Quality – The Fundamental Flaws and How Bluffing Makes It Worse (Agile Pain Relief, 2026). https://agilepainrelief.com/blog/genai-code-quality-fundamental-flaws-and-how-bluffing-makes-it-worse/

[^3]: Assessing the Quality and Security of AI-Generated Code: A Quantitative Analysis (arXiv, 2025). https://arxiv.org/html/2508.14727v1

[^4]: Insights from 2025 GenAI Code Security Report (Veracode, 2025). https://www.veracode.com/blog/genai-code-security-report/

[^5]: ISO/IEC 42001:2023 — Artificial Intelligence Management Systems. https://www.iso.org/standard/42001

[^6]: EU AI Code of Practice: 2025 Guide + ISO 42001 Map (Elevate Consult, 2025). https://elevateconsult.com/insights/eu-ai-code-of-practice-iso-42001/

[^7]: Strengthening AI Governance and Supporting ISO/IEC 42001 — Understanding ISO/IEC 42005:2025 (AARC-360, 2025). https://www.aarc-360.com/understanding-iso-iec-42005-2025/

[^8]: SENAI: Towards Software Engineering Native Generative Artificial Intelligence (arXiv, 2025). https://arxiv.org/abs/2503.15282

[^9]: Literature Review of SENAI (The Moonlight, 2025). https://www.themoonlight.io/en/review/senai-towards-software-engineering-native-generative-artificial-intelligence

[^10]: Towards AI-Native Software Engineering (SE 3.0): A Vision and a Challenge Roadmap (arXiv, 2024). https://arxiv.org/abs/2410.06107

[^11]: Software Quality Assurance and AI: A Systems-Theoretic Approach to Reliability, Safety, and Security (MDPI, 2025). https://www.mdpi.com/2674-113X/4/4/30

[^12]: AI Code Assurance: Quality & Security in Generated Code (Sonar, 2024). https://www.sonarsource.com/solutions/ai/ai-code-assurance/

[^13]: LLM-Generated Code Evaluation (Emergent Mind, 2025). https://www.emergentmind.com/topics/llm-generated-code-evaluation

[^14]: AI Code Review: Scaling Quality and Security in the GenAI Era (Sonar, 2026). https://www.sonarsource.com/resources/library/what-is-ai-code-review/

[^15]: State of AI Code Quality in 2025 (Qodo, 2025). https://www.qodo.ai/reports/state-of-ai-code-quality/
