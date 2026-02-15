# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [2.0.0] - 2026-02-15

### Added
- **三层文档结构 (P -> M -> F)**: 引入项目(Project)、模块(Module)、功能(Feature)三层结构
  - `Pxxx-{项目名}/` - 项目目录
  - `Pxxx/Mxxx-{模块名}.md` - 模块文档
  - `Pxxx/Mxxx/Fxxx-{功能名}.md` - 功能文档
- **新增 Phase 3 (项目构建)**: 专门用于创建项目目录和项目级 README
- **beautiful-mermaid 集成**: 使用 beautiful-mermaid 渲染高质量 SVG 图表
  - 支持 15+ 内置主题 (tokyo-night, catppuccin-mocha, nord, etc.)
  - 支持 SVG 和 ASCII 两种输出模式
  - 零 DOM 依赖，渲染速度快

### Changed
- **工作流更新**: 从 5 阶段更新为 6 阶段
  - Phase 1: 需求孵化
  - Phase 2: 方案预研
  - Phase 3: 项目构建 (新增)
  - Phase 4: 模块构建
  - Phase 5: 功能细化
  - Phase 6: 多角色评审
- **命名规范更新**: 
  - 旧: `M001-模块.md`, `M001/F001-功能.md`
  - 新: `P001/M001-模块.md`, `P001/M001/F001-功能.md`
- **文档模板更新**: 模块模板和功能模板添加 beautiful-mermaid 渲染说明

### Improved
- **多项目支持**: 更好的支持大型项目拆分为多个子项目
- **图表渲染**: 使用 beautiful-mermaid 确保跨平台一致的视觉效果
- **文档结构**: 更清晰的三层结构，便于管理和维护

## [1.0.0] - 2024-XX-XX

### Added
- 初始版本发布
- 5 阶段 PRD 创建工作流
  - Phase 1: 需求孵化
  - Phase 2: 方案预研
  - Phase 3: 模块构建
  - Phase 4: 功能细化
  - Phase 5: 多角色评审
- 模块和功能两层文档结构
- Mermaid 图表支持
- 多角色评审机制
