# Jason Zhou Twitter推文完整线程内容

**来源**: https://x.com/jasonzhou1993/status/1955970025984287004  
**ThreadReader**: https://threadreaderapp.com/thread/1955970025984287004.html  
**发布时间**: 2025年8月14日  
**用户**: @jasonzhou1993 (Jason Zhou)  
**线程长度**: 7条推文，约3分钟阅读时间

## 完整推文线程内容

### 🧵 Thread 1/7
> I was using Claude Code Sub-agent wrong...
> 
> Here's what I learnt after 20+ hrs trial & errors
> 
> Made my agents way more effective
> 
> 👇 Thread below

### 🧵 Thread 2/7 - 设计初衷
> First -
> 
> Why did Anthropic build sub-agents initially?
> 
> It's all about **context engineer & context optimisations**
> 
> It works best when focusing on **planning & researching** and send back with a **summary plan** to conversation thread

### 🧵 Thread 3/7 - 核心问题
> However,
> 
> **Context sharing between sub-agents is non-exist**
> 
> That's why if you have sub-agent do actual work, then this context is not visible to all other agents
> 
> This cause problems...

### 🧵 Thread 4/7 - 解决方案灵感
> Meanwhile,
> 
> @ManusAI_HQ has this blog on how they use **file storage as the ultimate context system**
> 
> It inspired me to design a **context sharing setup** to get main agent & sub agents to share context between each other

### 🧵 Thread 5/7 - 文件系统架构
> .claude/
> └ tasks/ (Updated by all agents)
>   └ session_context_01.md
>   └ session_context_02.md
>   └ ...
> └ docs/ (Store result of each sub agent)
>   └ shadcn-frontend-implementation.md
>   └ vercel-ai-sdk-5-plan.md
>   └ usage-pricing-plan.md
>   └ ...
> 
> This allow **effective handover & ability to maintain context**

### 🧵 Thread 6/7 - 具体实现
> This is how I built:
> - @shadcn -ui-expert agent
> - vercel-@aisdk -5-expert agent
> 
> Using principles above
> 
> **Result?**
> 
> It can **one-shot building** a fully functional chatGPT replica using latest @aisdk v5 (introduced a few weeks ago)

### 🧵 Thread 7/7 - 资源获取
> If you interested in learning more
> 
> We have a claude code template in @aibuilderclub_ with best hooks/agents/commands that actually useful
> 
> We do **weekly build together sessions**

## 关键概念提取

### 核心问题诊断
1. **上下文隔离**: Sub-agent之间无法共享上下文
2. **信息孤岛**: 各代理只能看到自己的操作历史
3. **协作困难**: 缺乏有效的信息传递机制

### 解决方案设计
1. **文件系统作为上下文桥梁**: 受ManusAI团队启发
2. **双层目录结构**: 
   - `tasks/` - 所有agent更新的会话上下文
   - `docs/` - 各sub-agent的研究结果存储
3. **有效移交**: 实现上下文的持续传递

### 实际应用成果
- **一次性构建**: 能够一次性生成完整的ChatGPT复制品
- **最新技术**: 使用Vercel AI SDK v5（几周前刚发布）
- **专家代理**: ShadCN UI专家和Vercel AI SDK专家

## 影响力分析

**社区反响**:
- 浏览量: 363.5K+（极高的关注度）
- 互动率: 高转发和收藏比例
- 技术深度: 提供了具体的实现架构

**知识价值**:
- 解决了Sub-agent的实际使用痛点
- 提供了可操作的解决方案架构
- 与ManusAI团队的最佳实践形成呼应

## 相关资源引用

- **ManusAI团队博客**: 关于文件存储作为终极上下文系统
- **AI Builder Club**: @aibuilderclub_ - 提供完整的Claude Code模板
- **技术栈**: @shadcn UI框架 + @aisdk Vercel AI SDK v5