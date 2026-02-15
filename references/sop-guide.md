# AI驱动型PRD标准化作业程序 (SOP) 指南

## SOP 核心理念

这套SOP将PRD创建分为**六个递进阶段**，利用AI能力实现：
- **需求结构化**: 自然语言 → 标准化文档
- **方案智能化**: AI搜索行业最佳实践
- **文档分层化**: P(项目) -> M(模块) -> F(功能) 三层结构
- **逻辑可视化**: Mermaid图表替代大段文字，使用 [beautiful-mermaid](https://github.com/lukilabs/beautiful-mermaid) 渲染高质量 SVG

---

## 五阶段深度解读

### Phase 1: 需求孵化 (Human-AI Collaboration)

#### 核心原则
- **从模糊到清晰**: AI通过提问帮助用户梳理思路
- **双向确认**: 不是单向输出，而是多轮对话达成共识
- **文档沉淀**: 最终产出结构化的需求描述文档

#### 提问框架 (5W2H)
| 维度 | 问题 | 目的 |
|------|------|------|
| Who | 谁是目标用户？ | 明确用户画像 |
| What | 核心功能是什么？ | 定义功能边界 |
| Why | 解决什么痛点？ | 验证价值假设 |
| When | 什么时间上线？ | 确定时间约束 |
| Where | 使用场景在哪？ | 理解上下文 |
| How | 用户如何使用？ | 梳理交互流程 |
| How Much | 预期规模多大？ | 评估技术方案 |

#### 产出标准
需求描述文档必须包含：
- 清晰的用户画像（至少1个Primary）
- 功能优先级划分（Must/Should/Could）
- 明确的范围边界（In/Out Scope）

---

### Phase 2: 方案预研 (AI Research)

#### 核心动作
1. **联网搜索**: 使用SearchWeb搜索相关技术方案
2. **竞品分析**: 研究同类产品的实现方式
3. **技术选型**: 对比不同技术栈的优缺点
4. **模块拆分**: 基于调研结果划分业务模块

#### 搜索策略
```
搜索关键词建议:
- "{领域} 系统架构设计"
- "{功能} 最佳实践"
- "{领域} 开源解决方案"
- "{竞品名} 产品分析"
```

#### 三层结构拆分原则

| 层级 | 拆分依据 | 粒度建议 | 示例 |
|------|----------|----------|------|
| **项目 (P)** | 独立部署、独立团队、独立业务域 | 一个项目包含 3-8 个模块 | P001-用户中心平台 |
| **模块 (M)** | 单一职责、高内聚低耦合 | 一个模块包含 3-8 个功能 | M001-用户认证 |
| **功能 (F)** | 独立交付、用户可见、可测试 | 一个功能对应一个用户场景 | F001-注册登录 |

#### 命名规范检查
```
✅ P001-用户中心平台/           (项目目录)
✅ P001/M001-用户认证.md        (模块文档)
✅ P001/M001/F001-注册登录.md   (功能文档)

❌ 用户中心.md                  (缺少层级编号)
❌ P1/用户.md                   (编号不足3位)
❌ P001/M1/F1-登录.md           (编号不足3位)
❌ P001/M001-用户.md/F1-登录.md (层级结构错误)
```

---

### Phase 3: 项目构建 (Project-Level PRD)

#### 项目文档核心要素
1. **项目 README**: 项目背景、目标、范围边界
2. **System Context Diagram**: 展示项目与外部系统的关系
3. **模块拆分规划**: 确定该项目包含的模块清单

---

### Phase 4: 模块构建 (Module-Level PRD)

#### 模块文档核心要素
1. **Context Diagram**: 展示模块与外部的关系
2. **Container Diagram**: 展示模块内部结构
3. **依赖矩阵**: 明确模块间的调用关系

#### Mermaid 图表指南

> **图表渲染工具**: 推荐使用 [beautiful-mermaid](https://github.com/lukilabs/beautiful-mermaid) 将 Mermaid 语法渲染为高质量 SVG，支持 15+ 内置主题，确保在不同系统中的一致性体验。

#### beautiful-mermaid 快速开始

```bash
npm install beautiful-mermaid
# 或
bun add beautiful-mermaid
```

```javascript
import { renderMermaid, THEMES } from 'beautiful-mermaid'

// 使用内置主题渲染
const svg = await renderMermaid(`
  flowchart TD
    A[开始] --> B{判断}
    B -->|是| C[处理]
    B -->|否| D[结束]
`, THEMES['tokyo-night'])

// 或使用自定义主题
const svg = await renderMermaid(diagram, {
  bg: '#1a1b26',
  fg: '#a9b1d6',
  accent: '#7aa2f7'
})
```

#### 推荐主题

| 主题 | 类型 | 适用场景 |
|------|------|----------|
| `tokyo-night` | 暗色 | 技术文档，深色背景 |
| `catppuccin-mocha` | 暗色 | 柔和的暗色主题 |
| `zinc-light` | 亮色 | 打印或浅色背景 |
| `github-light` / `github-dark` | 亮色/暗色 | 与 GitHub 风格一致 |
| `nord` | 暗色 | Polar 风格的北欧主题 |

##### Context Diagram 模板
```mermaid
flowchart TB
    User([用户]) --> Module[本模块]
    Module --> Dep1[依赖模块A]
    Module --> Dep2[依赖模块B]
    External[外部服务] --> Module
```

##### Container Diagram 模板
```mermaid
flowchart LR
    API[API Gateway] --> Controller[Controller]
    Controller --> Service[Service]
    Service --> Repo[Repository]
    Repo --> DB[(Database)]
```

#### 模块文档 checklist
- [ ] 有明确的业务背景说明
- [ ] 包含Context Diagram
- [ ] 列出了所有外部依赖
- [ ] 列出了所有被依赖关系
- [ ] 功能清单与后续F文档对应

---

### Phase 5: 功能细化 (Feature-Level PRD)

#### 功能拆分原则
一个功能应该是：
- **独立交付**: 可以独立开发、测试、上线
- **用户可见**: 从用户视角定义，而非技术视角
- **可测试**: 有明确的验收标准

#### Mermaid 图表选择指南

| 图表类型 | 适用场景 | 示例 |
|----------|----------|------|
| Flowchart | 业务流程、判断分支 | 审批流程、订单状态流转 |
| Sequence | 系统间交互、时序关系 | API调用流程、支付流程 |
| State | 状态机、生命周期 | 订单状态、任务状态 |
| ER | 数据关系 | 实体关系图 |

##### Sequence Diagram 最佳实践
```mermaid
sequenceDiagram
    autonumber  % 自动编号
    actor U as 用户
    participant C as Client
    participant S as Server
    participant D as DB
    
    U->>C: 操作
    Note over C: 关键注释
    C->>S: 请求
    
    alt 成功场景
        S->>D: 查询
        D-->>S: 返回数据
        S-->>C: 成功响应
    else 失败场景
        S-->>C: 错误响应
    end
```

#### 功能文档 checklist
- [ ] 有用户价值说明
- [ ] 包含Sequence Diagram
- [ ] 输入字段有完整校验规则
- [ ] 业务规则有伪代码或逻辑说明
- [ ] 异常场景有处理策略
- [ ] 边界情况有考虑

---

## 从 PRD 到代码的闭环

### 代码生成 Prompt 模板

当PRD文档准备好后，可以使用以下Prompt让AI生成代码：

```
请根据以下PRD文档生成代码：

**参考文档**:
- 项目概述: prd/P001-用户中心平台/README.md
- 模块架构: prd/P001/M001-用户认证.md
- 功能详情: prd/P001/M001/F001-注册登录.md

**要求**:
1. 使用 {技术栈} 实现
2. 遵循模块架构图中的分层设计
3. 严格按照功能文档的校验规则
4. 包含异常处理逻辑
5. 添加必要的注释说明对应PRD的哪个部分

**输出**:
请生成完整的可运行代码，包括：
- Controller/API 层
- Service 层
- Repository/Model 层
- 单元测试
```

### 数据闭环优势
1. **上下文完整**: AI可以读取完整的模块架构和功能细节
2. **一致性保证**: 代码与文档保持一致，有据可查
3. **可追溯性**: 代码注释可以关联到PRD具体章节
4. **维护便利**: 需求变更时，同步更新文档和代码

---

## 常见问题 FAQ

### Q1: 项目/模块/功能的粒度如何把控？
**A**:

**项目 (P)**: 遵循"可独立交付"原则
- 有独立的业务目标
- 可独立部署上线
- 有明确的边界和范围

**模块 (M)**: 遵循"单一职责"原则
- 独立的数据表/实体
- 独立的用户群体或业务场景
- 高内聚低耦合

**功能 (F)**: 遵循"用户可见"原则
- 用户可感知的完整操作
- 有明确的输入和输出
- 可独立测试验收

### Q2: 什么情况下需要画状态图？
**A**: 当功能涉及复杂的状态流转，且有：
- 多个状态节点（>3个）
- 状态间的转换规则复杂
- 有并发/异步的状态变更

### Q3: 如何管理跨模块的功能？
**A**: 
1. 确定主责模块（功能主要归属于谁）
2. 在主责模块中创建功能文档
3. 在相关模块的文档中添加引用链接
4. 在Context Diagram中体现跨模块调用

### Q4: 需求变更如何同步到PRD？
**A**:
1. 更新对应的功能文档 (Fxxx.md)
2. 在变更历史中记录修改内容
3. 如有架构变化，同步更新模块文档 (Mxxx.md)
4. 如有大范围变更，回到Phase 1重新梳理

### Q5: Mermaid图表渲染失败怎么办？
**A**: 

**方案1: 使用 beautiful-mermaid（推荐）**
```javascript
import { renderMermaid, THEMES } from 'beautiful-mermaid'

// beautiful-mermaid 渲染更稳定，支持离线使用
const svg = await renderMermaid(diagram, THEMES['tokyo-night'])

// 若仍有问题，可尝试 ASCII 输出
import { renderMermaidAscii } from 'beautiful-mermaid'
const ascii = renderMermaidAscii(diagram)
```

**方案2: 传统 Mermaid 渲染**
1. 检查语法是否正确（注意缩进和符号）
2. 避免使用中文特殊符号
3. 复杂图表可以拆分为多个小图
4. 使用 Mermaid Live Editor 验证: https://mermaid.live

### Q6: 三层结构 (P->M->F) 如何组织？
**A**:
1. **目录结构**:
   ```
   prd/
   ├── P001-项目A/
   │   ├── README.md
   │   ├── M001-模块A.md
   │   └── M001/
   │       └── F001-功能A.md
   └── P002-项目B/
       ├── README.md
       └── M001-模块B.md
   ```
2. **编号策略**: 各层编号独立，都从 001 开始
   - 项目层: P001, P002...
   - 模块层: 每个项目内 M001, M002...
   - 功能层: 每个模块内 F001, F002...
3. **跨项目引用**: 使用相对路径 `../../P002/M001-模块B.md`

### Q7: 什么时候应该拆分为多个项目(P)？
**A**:
1. **独立部署**: 项目间可以独立部署上线
2. **独立团队**: 不同团队负责不同项目
3. **业务域隔离**: 不同业务域，如用户中心 vs 订单系统
4. **技术栈差异**: 使用完全不同的技术栈

### Q8: 什么情况下模块(M)和功能(F)需要调整？
**A**:
**模块拆分**:
- 一个模块包含超过 8 个功能 → 考虑拆分为多个模块
- 模块内功能耦合度过高 → 重新梳理边界

**功能拆分**:
- 功能描述超过 2 页 → 考虑拆分为多个子功能
- 功能涉及多个用户角色 → 按角色拆分

---

## 检查清单 (Master Checklist)

### 项目启动前
- [ ] 已完成Phase 1需求文档
- [ ] 已完成Phase 2方案预研
- [ ] 项目/模块拆分已获得团队确认

### 项目文档完成时 (Phase 3)
- [ ] 所有项目都有Pxxx-{项目名}/目录
- [ ] 每个项目都有README.md
- [ ] 项目范围边界清晰定义

### 模块文档完成时 (Phase 4)
- [ ] 所有模块都有Pxxx/Mxxx.md文档
- [ ] 每个模块都有Context Diagram
- [ ] 依赖关系已梳理清楚

### 功能文档完成时 (Phase 5)
- [ ] 所有功能都有Pxxx/Mxxx/Fxxx.md文档
- [ ] 关键流程有Sequence Diagram
- [ ] 输入校验规则完整
- [ ] 异常场景已覆盖

### 交付前 (Phase 6)
- [ ] 文档已通过团队评审
- [ ] 开发团队已确认无歧义
- [ ] 测试团队已确认可测试
