```mermaid
graph TD
    %% 用户输入查询
    A[fa:fa-user 用户输入查询] --> B[fa:fa-search 检索 & 生成 SERP 结果]

    %% 进入可解释性模块，提供两种选择方式
    B -->|自动选择（系统推荐）| C[fa:fa-cogs 可解释性自动决策]
    B -->|用户固定设置| D[fa:fa-sliders 用户手动选择展示方式]

    %% 自动选择方式（基于查询/文档特征 + 强化学习）
    C -->|提取查询 & 文档特征| E[fa:fa-brain 分析用户意图 & 文档结构]
    E -->|输入状态| F{fa:fa-robot RL 选择最佳可解释方式}

    %% 用户固定选择方式
    D -->|模式 1: 关键证据高亮| G[fa:fa-highlighter 关键证据高亮]
    D -->|模式 2: 层次化展示| H[fa:fa-sitemap 结构化展示]
    D -->|模式 3: 知识图谱| I[fa:fa-network-wired 相关概念可视化]

    %% 强化学习 Action 选择
    F -->|A1: 关键证据高亮| G
    F -->|A2: 层次化展示| H
    F -->|A3: 知识图谱| I

    %% 交互方式（自动选择 & 固定设置 共用相同交互逻辑）
    G -->|鼠标悬停| J[fa:fa-mouse-pointer 显示高亮句详情]
    G -->|点击跳转| K[fa:fa-arrow-down 快速定位至证据]
    
    H -->|展开/折叠章节| L[fa:fa-expand-arrows 层次化查看文档结构]
    
    I -->|点击概念| M[fa:fa-hand-pointer 展开相关文档]
    I -->|拖动知识图谱| N[fa:fa-project-diagram 探索更多关系]

    %% 用户反馈 & 强化学习调整
    J --> O{fa:fa-thumbs-up 用户是否满意?}
    K --> O
    L --> O
    M --> O
    N --> O

    O -->|是| P[fa:fa-check 结束交互]
    O -->|否| Q[fa:fa-redo RL 进行策略更新]
    Q --> C  %% 重新优化可解释性选择

```