```mermaid
flowchart TD
    A[输入：无标签目标领域语料库\n+种子查询] --> B[阶段1：自动生成示例集]
    B --> B1[1. 使用BM25检索 Top-N 候选文档]
    B1 --> B2[2. 使用MonoT5对 Top-N rerank]
    B2 --> B3[3. 选取最高得分 passage\n作为 pseudo-expansion]
    B3 --> B4[4. 构建 (query, expansion) 示例数据集]
    
    B4 --> C[阶段2：Few-Shot 查询扩展]
    C --> C1[1. 为新测试查询选取4个示例]
    C1 --> C1a[静态示例] 
    C1 --> C1b[随机采样]
    C1 --> C1c[Embedding 相似度选择]
    C1 --> C1d[Cluster 多样性选择]

    C1a & C1b & C1c & C1d --> C2[2. 构造Few-Shot Prompt 输入LLM]
    C2 --> C3[3. LLM 生成扩展查询（Expanded Passage）]
    
    C3 --> D[阶段3：检索评估]
    D --> D1[将扩展结果作为查询，使用 BM25 检索]
    D1 --> D2[与原始查询结果对比]
    D2 --> D3[评估 Recall@1K、nDCG@10 等指标]

    style A fill:#f9f,stroke:#333,stroke-width:1px
    style D fill:#bbf,stroke:#333,stroke-width:1px

```