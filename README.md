## AI4SE White Paper

```mermaid
block-beta
  columns 7

    A<["方法论"]>(right):1
    B["新抽象层"]:3
    C["算法+数据结构+数据"]:3
    D<["<a href='https://ai-llm.github.io/ai4se_white_paper/taxonomy/index.html'>分类法</a>"]>(right)
    E["cloud app"]:3
    F["AlphaX"]:3
    G<["基本UI智能"]>(right):1
    H["代码检索"]:3
    I["代码编辑"]:3
    comment1["类比文本终端到IDE的改进"]
    style comment1 fill:rgb(0,0,0,0),stroke:rgb(0,0,0,0),stroke-width:0
    K["摘要"]:2
    J["模式匹配"]:2
    L["转译"]:2
```

依据初步讨论达成以下共识：
- 本次白皮书的内容，重点放在对相应的范式、技术、工具和案例等 进行调研、分析和总结; 
- 文章中可以适当提出一些价值主张，但是对于不确定的发展趋势、未经试验的想法和观点等，暂时不在白皮书中做深入探讨。

白皮书的草稿暂时使用 gitbook 进行组织：
- [gitbook.md](gitbook.md) 中是 gitbook 的安装和配置过程；如果只是文章撰写，不编译和发布则无需安装和配置 gitbook；
- SUMMARY.md 是书籍的目录，gitbook 会按照该文件生成相应的章节 markdown 文件, 修改目录大纲直接编辑 SUMMARY.md；
- 根据大纲生成 markdown 文件后，直接编辑对应章节的 markdown 文件完成内容编写；
- 如果要生成并发布电子书，参考 gitbook.md 配置 gitbook 工具；
