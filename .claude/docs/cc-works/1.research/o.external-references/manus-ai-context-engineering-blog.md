# ManusAI上下文工程博客文章

**来源**: https://manus.im/blog/Context-Engineering-for-AI-Agents-Lessons-from-Building-Manus  
**作者**: Yichao 'Peak' Ji  
**发布时间**: 2025年7月19日  
**标题**: Context Engineering for AI Agents: Lessons from Building Manus

## 核心观点总结

### 文件系统作为终极上下文系统

ManusAI团队提出了一个革命性的概念：**使用文件系统作为AI代理的终极上下文存储**。

#### 问题背景
- 现代LLM虽然支持128K+token的上下文窗口，但在实际代理场景中仍不够用
- 观察结果可能非常庞大（web页面、PDF等）
- 超过一定长度后模型性能下降
- 长输入成本高昂

#### 解决方案
```ascii
传统方式: [上下文窗口] - 有限、昂贵、性能下降
         ↓
文件系统方式: [无限存储] + [按需读写] + [结构化记忆]
```

**核心原理**:
- 文件系统：无限大小、天然持久化、代理可直接操作
- 模型学习按需读写文件
- 文件系统不仅是存储，更是结构化的外置记忆

#### 压缩策略
- **可恢复压缩**: 保留URL而丢弃网页内容，保留文件路径而省略内容
- **信息不丢失**: 代理可随时重新获取需要的信息
- **上下文优化**: 减少token使用而不永久丢失信息

### 其他关键上下文工程原则

#### 1. KV-Cache优化设计
- **KV-cache命中率是生产环境AI代理的最重要指标**
- 直接影响延迟和成本（缓存token成本降低10倍）
- 设计原则：
  - 保持prompt前缀稳定
  - 确保上下文只追加
  - 明确标记缓存断点

#### 2. 掩码而非移除工具
- 避免动态添加/移除工具（破坏KV-cache）
- 使用状态机管理工具可用性
- 通过token logits掩码约束动作选择

#### 3. 通过复述操纵注意力
- 创建todo.md文件并逐步更新
- 将全局计划推入模型的最近注意力范围
- 避免"迷失在中间"问题

#### 4. 保留错误信息
- 不要隐藏错误和失败
- 让模型从错误中学习和适应
- 错误恢复是真正代理行为的指标

#### 5. 避免Few-shot陷阱
- 增加上下文多样性
- 引入结构化变化打破模式
- 防止代理陷入重复行为

## Jason Zhou的引用分析

Jason在推文中明确提到：
> "@ManusAI_HQ has this blog on how they use **file storage as the ultimate context system**"
> 
> "It inspired me to design a **context sharing setup** to get main agent & sub agents to share context between each other"

### 启发应用
Jason受ManusAI启发，设计了类似的文件系统上下文管理：
```
.claude/
└ tasks/ (Updated by all agents)
  └ session_context_01.md
  └ session_context_02.md
  └ ...
└ docs/ (Store result of each sub agent)
  └ shadcn-frontend-implementation.md
  └ vercel-ai-sdk-5-plan.md
  └ usage-pricing-plan.md
  └ ...
```

## 技术深度评估

这篇博客提供了深度的技术洞察，揭示了构建生产级AI代理的核心挑战和解决方案。特别是文件系统作为上下文的概念，为Jason Zhou的sub-agent架构提供了理论基础。

## 关键启示

1. **上下文工程是新兴科学**：需要实验和迭代
2. **文件系统外置记忆**：突破上下文窗口限制的关键
3. **错误也是价值**：不要过度清理失败信息
4. **缓存优化关键**：影响延迟和成本的核心指标
5. **多样性防退化**：避免模式固化和行为漂移

这些原则为理解Jason Zhou的sub-agent最佳实践提供了深层的理论支撑。