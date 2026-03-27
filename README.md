# AISMM

## 定义研究的问题、范围和目的

1️⃣最近的技术进展

比谁看到的更多更全面？

总结成功经验和规律？还没有“经验”经过长时间考验可以称之为“成功”。比如Claude code的设计被外界做各种解读，[实际都是为了以最简单的方式开始探索](https://www.youtube.com/watch?v=PQU9o_5rHC4)，无从衡量模型还是设计因素贡献更大。

针对特定人群的认知提升？

2️⃣在具体问题上用具体AI方案能做到什么效果

[机器学习适用性（Suitability for Machine Learning, SML）指标](reference/SML-report.md)没有及时更新的具体的AI方案①，O*NET也没有针对特定软件类型的操作粒度②。
分类细化②——SWE Task Network & Taxonomy，可以对应到评测数据集，对①进行Eval。

3️⃣从流程角度评价AI（为主）生成的软件的质量

类似CMMI（能力成熟度模型集成）评价人类组织，现在要评价AI或人类+AI。ISO/IEC 12207 与 15288（生命周期过程）扩展到包含AI的过程。

[Node.js 19000行的PR问题](https://mp.weixin.qq.com/s/-68vDfR-SSCXnu6w_jUkEA)实际上是这个标准问题。

## 分类分析框架
```mermaid
block-beta
  columns 7
    A<["方法论"]>(right):1
    block:groupB:3
      columns 2
      m1(("<a href='https://github.com/AI-LLM/ai4se_white_paper/blob/main/meth-nonai.md'>1</a>")) space
      B1["新抽象层"]:1
      B2["新角色"]:1
    end
    block:groupC:3
      columns 2
      m2(("<a href='https://github.com/AI-LLM/ai4se_white_paper/blob/main/meth-ai.md'>2</a>")) space
      C21["通用基础模型"]
      C22["垂直模型"]
      C11["数据+'算法+数据结构'"]
      C12["Harness engineering"]
    end
    D<["<a href='https://ai-llm.github.io/ai4se_white_paper/taxonomy/index.html'>分类法</a>"]>(right)
    block:groupE:3
      E2["非AI系统软件"]:1
      E1["Non-AI Cloud App"]:2
    end
    block:groupF:3
      F1["AI应用软件"]:2
      F2["AlphaX"]:1
    end
    G<["基本UI智能"]>(right):1
    H["代码检索、解释"]:3
    I["代码补全、编辑"]:3
    comment1["类比文本终端到IDE的改进"]
    style comment1 fill:rgb(0,0,0,0),stroke:rgb(0,0,0,0),stroke-width:0
    K["摘要"]:2
    J["模式匹配"]:2
    L["转译"]:2
    style groupB fill:#4a90d9,color:#fff
    style groupE fill:#4a90d9,color:#fff
    style groupC fill:#00bcd4,color:#fff
    style groupF fill:#00bcd4,color:#fff
```

## AI4SE White Paper

依据初步讨论达成以下共识：
- 本次白皮书的内容，重点放在对相应的范式、技术、工具和案例等 进行调研、分析和总结; 
- 文章中可以适当提出一些价值主张，但是对于不确定的发展趋势、未经试验的想法和观点等，暂时不在白皮书中做深入探讨。

白皮书的草稿暂时使用 gitbook 进行组织：
- [gitbook.md](gitbook.md) 中是 gitbook 的安装和配置过程；如果只是文章撰写，不编译和发布则无需安装和配置 gitbook；
- SUMMARY.md 是书籍的目录，gitbook 会按照该文件生成相应的章节 markdown 文件, 修改目录大纲直接编辑 SUMMARY.md；
- 根据大纲生成 markdown 文件后，直接编辑对应章节的 markdown 文件完成内容编写；
- 如果要生成并发布电子书，参考 gitbook.md 配置 gitbook 工具；
