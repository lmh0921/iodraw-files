```mermaid
graph TD
    %% 用户输入查询
    A[fa:fa-user 用户输入查询] --> B[解析查询 & 交互历史]
    
    %% 强化学习环境
    B -->|特征提取| C[fa:fa-cogs 强化学习 Environment]
    
    %% RL Agent 选择最优 Action
    C -->|环境状态输入| D{fa:fa-robot RL Agent 决策交互方式}

    %% 强化学习 Action 选择
    D -->|A1: 直接检索| E[fa:fa-search 直接返回 SERP]
    D -->|A2: 生成搜索澄清| F[fa:fa-comments 生成搜索澄清问题]
    D -->|A3: 直接优化查询| G[fa:fa-edit 自动扩展或重构查询]
    D -->|A4: 推荐相关查询| H[fa:fa-lightbulb 推荐更精准的查询]

    %% A2: 搜索澄清的子流程
    F -->|用户选择选项| I[fa:fa-filter 选择最优搜索路径]
    I -->|强化学习继续判断| D  %% 回到 RL 继续决策，形成多轮交互
    I --> J[fa:fa-search 执行搜索]  %% 直到 RL 认为可以直接执行搜索
    
    %% A3: 直接优化查询的子流程
    G --> K[fa:fa-search 用优化后的查询执行搜索]
    
    %% 反馈机制
    E --> L{fa:fa-thumbs-up 用户是否满意?}
    J --> L
    K --> L
    H --> L

    L -->|是| M[fa:fa-check 结束交互]
    L -->|否| N[fa:fa-redo RL 进行策略更新]
    
    N -->|更新策略| C

```