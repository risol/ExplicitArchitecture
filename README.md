# Explicit Architecture

**版本 / Version / バージョン：V1**

> **Make Structure Visible. Make Behavior Explicit. Keep Dependencies Clear. Preserve Shared Invariants. Keep Changes Local. Make Tests Composable.**

[简体中文](#简体中文) · [English](#english) · [日本語](#日本語)

## 简体中文

### 什么是显式架构？

**显式架构是一种让软件系统更容易理解、修改和验证的设计方法。**

它通过清晰表达系统能力、模块职责、关键控制流、依赖关系、共享规则和测试边界，帮助开发者和 AI 在有限上下文中完成可靠的局部修改。显式架构不限定技术栈、目录结构或分层模式；设计应由真实需求、运行约束和风险驱动。

### 十项核心原则

1. **核心能力与共享内核边界清晰**：能力模块负责领域规则；共享内核只负责必须一致的执行机制与不变量。
2. **结构与关键路径可见**：从项目结构和入口能找到模块职责、依赖方向和主要运行路径。
3. **按职责、变化原因与测试边界组织**：将共同演进的规则、状态、实现和测试合理聚拢。
4. **关键控制流可追踪**：明确决策、执行顺序、状态变化、副作用与失败处理。
5. **依赖与装配显式**：保持依赖方向稳定，通过清晰契约协作，并在组合根装配模块。
6. **复杂度由真实需求与风险驱动**：每项重要抽象和基础设施都应有明确的问题与价值。
7. **兼顾局部变化与共享不变量**：让独立职责局部演进，让必须一致的规则有明确权威。
8. **测试细粒度且可组合**：逐层验证局部规则、完整用例、模块协作和真实运行路径。
9. **提供最小充分上下文**：为开发者和 AI 提供完成局部任务所需的相关信息。
10. **分层反馈与持续验证**：让验证成本匹配变更风险，并持续检查架构约束。

### 设计时可以先问

- 这项能力或规则由哪个模块负责？
- 从工程结构和入口能否快速找到它？
- 能否追踪它如何执行、改变状态并处理失败？
- 新增的抽象解决了什么实际问题？
- 能否独立验证，并逐层组合验证更完整的行为？

**设计目标：** 满足真实运行要求，同时降低理解成本、变化传播成本和验证成本。

## English

### What is Explicit Architecture?

**Explicit Architecture is a software design method that makes systems easier to understand, change, and verify.**

It makes capabilities, responsibilities, control flow, dependencies, shared rules, and testing boundaries discoverable. Developers and AI can then work within a focused context and verify changes reliably. It leaves room for different stacks and architectural styles; structure follows real requirements, operating constraints, and risks.

The ten principles cover capability and kernel boundaries, structural transparency, responsibility cohesion, explicit control flow, explicit dependencies and assembly, necessary complexity, local change and shared invariants, composable testability, bounded context, and layered feedback with continuous verification.

**Design goal:** Meet real operating requirements while lowering the cost of understanding, change propagation, and verification.

## 日本語

### Explicit Architecture とは

**Explicit Architecture は、システムを理解し、変更し、検証しやすくするソフトウェア設計手法です。**

機能、責務、制御フロー、依存関係、共有ルール、テスト境界を見つけやすく表現し、開発者や AI が限られたコンテキストで安全に変更できるようにします。技術スタックや構成を指定せず、実際の要件、運用条件、リスクに沿って設計します。

十の原則は、機能と共有カーネルの境界、構造の透明性、責務の凝集、制御フローの明示、依存関係と組み立て、必要な複雑さ、局所的な変更と共有不変条件、組み合わせ可能なテスト、必要十分なコンテキスト、段階的なフィードバックと継続検証を扱います。

**設計目標：** 実際の運用要件を満たしながら、理解、変更の波及、検証にかかるコストを抑えること。

## 完整说明 / Full document / 詳細な説明

- [简体中文完整说明](Explicit%20Architecture.md#简体中文)
- [Full English text](Explicit%20Architecture.md#english)
- [日本語の全文](Explicit%20Architecture.md#日本語)
