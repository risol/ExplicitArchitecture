# Explicit Architecture

**Languages / 语言 / 言語:** [简体中文](#简体中文) · [English](#english) · [日本語](#日本語)

---

# 简体中文

## 显式架构：面向可理解、可演进、可验证的软件工程

### 一、架构定义

**Explicit Architecture（显式架构）是一种以系统可理解性、行为可追踪性和修改可控性为核心的软件架构设计方法。**

它要求软件的核心能力、模块职责、关键控制流、依赖关系、共享规则和测试边界都具有明确、可发现的表达，使开发者和 AI 能够在有限上下文中理解系统、实施局部修改，并通过分层测试可靠地验证修改结果。

显式架构不规定唯一的目录结构、分层模式或技术栈。它通过一组可执行的设计约束，确保软件在满足实际功能、运行、安全和可靠性要求的同时，保持结构清晰、职责合理、复杂度受控，并能够持续演进。

### 二、核心架构原则

**1. Capability & Kernel Boundaries — 核心能力与共享机制边界清晰**

工程应围绕系统的核心能力和概念组织。对于存在共享执行内核或基础运行机制的系统，必须明确各能力与共享机制的职责边界。能力模块拥有自身的领域规则，共享内核负责跨能力必须保持一致的执行机制和共同不变量。共享代码不应仅因复用而集中到内核，也不应因局部自治而重复实现全局规则。

**2. Structural Transparency — 结构与关键路径可见**

工程目录、模块命名、应用入口和架构文档应能清晰表达系统组成、模块职责、依赖方向和主要运行路径。应用入口应明确展示模块的装配关系，各类外部入口应将具体工作交给职责明确的模块。关键架构信息不应依赖开发者记忆、大量文件搜索或不可见的框架约定才能获得。

**3. Responsibility Cohesion — 按职责、变化原因与测试边界组织**

语义相关、紧密协作或因相同原因变化的规则、状态、实现和测试应合理聚拢。只有当职责、变化原因、依赖关系或测试边界确实不同，并且拆分能够降低整体复杂度时，才引入新的模块或抽象。模块粒度应由职责内聚、协作成本和变化特征决定，而不是由文件行数、目录数量或代码复用率单独决定。

**4. Explicit Control Flow — 关键控制流可追踪**

关键决策、调用顺序、状态转换、副作用、错误处理、重试和恢复行为应能够通过代码或明确的执行契约追踪。事件、回调、异步任务和框架机制可以使用，但必须明确其触发条件、执行语义、状态影响和失败处理方式。关键业务或系统行为不得依赖不可发现的隐式控制逻辑。

**5. Explicit Dependencies & Assembly — 依赖与装配显式**

模块依赖应当可见、方向稳定，并通过明确的接口或契约进行协作。应用组合根负责连接各模块及其基础设施依赖，模块不应反向依赖应用入口或不必要地依赖其他模块的内部实现。只有在真实的替换、隔离、独立演进或稳定契约需求存在时，才引入额外接口和抽象。避免循环依赖、隐式全局依赖及无必要的间接调用。

**6. Necessary Complexity — 复杂度由真实需求与风险驱动**

架构中的抽象、层级、模式和基础设施应服务于已确认的功能需求、运行约束及风险要求。必要的持久化、状态恢复、权限控制、预算管理、版本一致性和故障处理不得为了表面简洁而省略；同时，应避免缺乏现实依据的过度设计。每项重要的结构性复杂度都应能够说明其解决的问题、提供的价值及移除后的影响。

**7. Local Change & Shared Invariants — 局部变化与共享不变量兼顾**

独立变化的职责应尽可能在所属模块内演进；跨模块必须保持一致的规则，应由明确的权威定义或实现负责。共享规则的统一依据是语义和不变量的一致性，而不是代码表面相似。各模块通过稳定契约使用共享规则，既避免重复实现和语义分歧，也避免共享模块演变为集中所有业务逻辑的上帝模块。局部化的目标是减少不必要的变化传播，而不是破坏必须保持的一致性。

**8. Composable Testability — 测试细粒度且可组合**

各项规则和能力应能够独立验证，并通过清晰的接口逐层组合测试。单元测试验证局部规则，用例测试验证完整操作，协议和集成测试验证模块协作，端到端测试验证真实运行路径。各层测试应有明确的验证目标，测试失败应尽可能容易定位。对于依赖模型的系统，应区分确定性软件行为测试与模型行为评估，分别根据验证目标、稳定性和运行成本设计测试策略。

**9. Bounded Context — 提供最小充分上下文**

工程结构、模块说明、公开契约、重要约束和测试应帮助开发者或 AI 快速理解局部任务及其必要上下游，使任务能够在不理解整个系统的前提下可靠完成。通过合理的模块内聚、依赖收敛、清晰命名和渐进式信息加载，降低理解成本。上下文效率追求的是完成任务所需的最小充分信息，而不是最少文件、最小模块或大量微型包。

**10. Layered Feedback & Continuous Verification — 分层反馈与持续验证**

每类变更都应有明确、适当且可重复的验证路径，并通过自动化测试、类型检查、静态分析和架构约束检查保护关键不变量。验证应优先提供快速反馈，再根据变更风险、影响范围和发布阶段执行更昂贵的集成、真实模型及端到端测试。持续清理废弃契约、重复规则、无用抽象和架构边界泄漏，确保系统在持续演进中仍符合既定原则。

### 三、架构决策准则

任何重要的架构设计，都应能够回答以下问题：

- **能力归属：** 这项能力或规则由哪个模块负责？哪些规则必须共享并保持统一？
- **结构可见性：** 开发者能否从工程结构和入口快速找到它？
- **行为可追踪性：** 能否明确理解它如何执行、改变状态以及处理失败？
- **依赖合理性：** 它为什么依赖其他模块？依赖是否必要且方向稳定？
- **复杂度合理性：** 新增的抽象、层级或基础设施解决了什么实际问题？
- **变化局部性：** 修改它会影响哪些模块？哪些影响是必要的，哪些可以避免？
- **测试可组合性：** 能否独立验证它，并逐层组合验证更完整的行为？
- **上下文充分性：** 开发者或 AI 能否以有限且相关的信息完成任务？
- **反馈有效性：** 是否存在与变更风险相匹配的验证路径？

如果这些问题无法得到清晰回答，说明相关设计仍需要进一步明确。

### 四、总体设计目标

显式架构不以代码量最少、模块数量最少或抽象层级最少为目标，而是在满足真实运行要求的前提下，尽可能降低系统的理解成本、变化传播成本和验证成本。

其核心是：

- 让必要的复杂度有明确归属和可追踪的表达。
- 让跨模块的一致性由明确的权威规则保障。
- 让独立职责可以局部演进和独立验证。
- 让系统的结构、行为和约束能够被人和 AI 有效发现。
- 让测试和反馈机制持续验证架构设计是否仍然成立。

### 五、核心设计宣言

**Make Structure Visible. Make Behavior Explicit. Keep Dependencies Clear. Preserve Shared Invariants. Keep Changes Local. Make Tests Composable.**

让结构可见，让行为显式，让依赖清晰，让共享不变量保持一致，让变化尽可能局部，让测试可组合。

### 六、一句话定义

**显式架构是一种通过明确的能力边界、可见的工程结构、可追踪的控制流、稳定的依赖关系、统一的共享不变量和可组合的测试体系，在有限上下文中实现可靠理解、局部修改与持续演进的软件架构方法。**

---

# English

## Explicit Architecture: Software Architecture for Understandable, Evolvable, Verifiable Systems

### 1. Definition

**Explicit Architecture is a software architecture design method centered on system understandability, traceable behavior, and controlled change.**

It calls for clear, discoverable expression of a system’s core capabilities, module responsibilities, critical control flows, dependencies, shared rules, and testing boundaries. This lets developers and AI understand the system within a limited context, make focused changes, and verify the results reliably through layered tests.

Explicit Architecture does not prescribe one folder layout, layering style, or technology stack. It uses a set of actionable design constraints to keep software clear in structure, sound in responsibility, and controlled in complexity while meeting real functional, operational, security, and reliability requirements and continuing to evolve.

### 2. Core Principles

**1. Capability & Kernel Boundaries — Keep core capabilities and shared mechanisms distinct**

Organize the project around its core capabilities and concepts. When a system has a shared execution kernel or foundational runtime mechanisms, make the responsibilities of each capability and the shared mechanism explicit. Capability modules own their domain rules; the shared kernel owns execution mechanisms and common invariants that must hold across capabilities. Do not centralize code in the kernel solely for reuse, and do not reimplement global rules in the name of local autonomy.

**2. Structural Transparency — Make structure and critical paths visible**

Project structure, module names, application entry points, and architecture documentation should clearly express the system’s composition, module responsibilities, dependency directions, and main runtime paths. The application entry point should show how modules are assembled, while external entry points should delegate work to modules with clear responsibilities. Critical architecture information should not depend on memory, extensive file searches, or invisible framework conventions.

**3. Responsibility Cohesion — Organize around responsibility, reasons for change, and test boundaries**

Keep related rules, state, implementations, and tests together when they share meaning, collaborate closely, or change for the same reason. Introduce a new module or abstraction when responsibilities, reasons for change, dependencies, or testing boundaries are genuinely different and the split lowers overall complexity. Let cohesion, collaboration cost, and change patterns determine module size; do not use line count, directory count, or code reuse rate as the sole measure.

**4. Explicit Control Flow — Make critical control flow traceable**

Make critical decisions, call order, state transitions, side effects, error handling, retries, and recovery traceable in code or a clear execution contract. Events, callbacks, asynchronous jobs, and framework mechanisms are valid choices when their triggers, execution semantics, state effects, and failure handling are explicit. Critical business or system behavior must not depend on undiscoverable implicit control logic.

**5. Explicit Dependencies & Assembly — Make dependencies and assembly explicit**

Keep module dependencies visible and their direction stable, and have modules collaborate through clear interfaces or contracts. The application composition root connects modules and their infrastructure dependencies. Modules should not depend back on the application entry point or unnecessarily on other modules’ internals. Add interfaces and abstractions when there is a real need for replacement, isolation, independent evolution, or a stable contract. Avoid circular dependencies, implicit global dependencies, and unnecessary indirection.

**6. Necessary Complexity — Let real needs and risks drive complexity**

Abstractions, layers, patterns, and infrastructure should serve confirmed functional needs, operating constraints, and risks. Do not omit necessary persistence, state recovery, access control, budget management, version consistency, or failure handling for the sake of surface simplicity. Also avoid overdesign without a real basis. Be able to explain the problem each important structural choice solves, the value it provides, and the effect of removing it.

**7. Local Change & Shared Invariants — Balance local change with shared invariants**

Let independently changing responsibilities evolve within their owning modules. Give rules that must remain consistent across modules one clear authority. Shared rules should be unified because their meaning and invariants match, not because their code looks similar. Stable contracts let modules use shared rules without duplication or semantic drift, while keeping a shared module from becoming a god module that owns all business logic. Locality should reduce unnecessary change propagation while preserving required consistency.

**8. Composable Testability — Make tests focused and composable**

Rules and capabilities should be independently verifiable and composable through clear interfaces. Unit tests verify local rules; use-case tests verify complete operations; protocol and integration tests verify module collaboration; end-to-end tests verify real runtime paths. Give every test layer a clear purpose and make failures easy to locate. For systems that depend on models, distinguish deterministic software behavior tests from model behavior evaluations, and design each strategy for its validation goal, stability, and cost.

**9. Bounded Context — Provide the smallest sufficient context**

Project structure, module documentation, public contracts, important constraints, and tests should help developers and AI quickly understand a local task and its necessary upstream and downstream context. This allows reliable work without requiring an understanding of the whole system. Use cohesive modules, focused dependencies, clear names, and progressive information loading to lower the cost of understanding. Context efficiency means the smallest sufficient information for the task, not the fewest files, the smallest modules, or a large collection of tiny packages.

**10. Layered Feedback & Continuous Verification — Use layered feedback and continuous verification**

Every kind of change should have a clear, appropriate, repeatable verification path. Protect key invariants with automated tests, type checks, static analysis, and architecture checks. Provide fast feedback first, then run more costly integration, real-model, and end-to-end tests according to change risk, impact, and release stage. Continuously remove obsolete contracts, duplicate rules, unused abstractions, and leaking boundaries so the system remains aligned with its principles as it evolves.

### 3. Architecture Decision Criteria

Every important architecture decision should have clear answers to these questions:

- **Capability ownership:** Which module owns this capability or rule? Which rules must be shared and kept consistent?
- **Structural visibility:** Can a developer find it quickly from the project structure and entry point?
- **Behavioral traceability:** Can someone understand how it runs, changes state, and handles failure?
- **Dependency rationale:** Why does it depend on another module? Is the dependency necessary and its direction stable?
- **Complexity rationale:** What real problem does a new abstraction, layer, or infrastructure component solve?
- **Change locality:** Which modules will a change affect? Which effects are necessary, and which can be avoided?
- **Composable testing:** Can it be verified independently and then as part of a larger behavior?
- **Sufficient context:** Can developers or AI complete the task with limited, relevant information?
- **Effective feedback:** Is there a verification path suited to the change’s risk?

If these questions do not have clear answers, the design needs further clarification.

### 4. Overall Design Goal

Explicit Architecture aims to lower the cost of understanding, change propagation, and verification as much as practical while meeting real operating requirements. Code volume, module count, and abstraction depth are design choices rather than measures of success.

Its purpose is to:

- Give necessary complexity a clear owner and a traceable expression.
- Protect cross-module consistency through an explicit source of authority.
- Let independent responsibilities evolve locally and be verified independently.
- Make system structure, behavior, and constraints discoverable to people and AI.
- Keep tests and feedback continuously checking that the architecture still holds.

### 5. Core Declaration

**Make Structure Visible. Make Behavior Explicit. Keep Dependencies Clear. Preserve Shared Invariants. Keep Changes Local. Make Tests Composable.**

### 6. In One Sentence

**Explicit Architecture is a software architecture method that uses clear capability boundaries, visible project structure, traceable control flow, stable dependencies, consistent shared invariants, and composable tests to enable reliable understanding, focused change, and continuous evolution within a limited context.**

---

# 日本語

## Explicit Architecture：理解しやすく、進化し続け、検証できるソフトウェアアーキテクチャ

### 1. 定義

**Explicit Architecture は、システムの理解しやすさ、追跡可能な振る舞い、制御可能な変更を中心に据えたソフトウェアアーキテクチャ設計手法です。**

システムの中核機能、モジュールの責務、重要な制御フロー、依存関係、共有ルール、テスト境界を明確かつ見つけやすく表現します。開発者や AI は限られたコンテキストでシステムを理解し、変更範囲を絞って実装し、段階的なテストで結果を確実に検証できます。

Explicit Architecture は、特定のフォルダー構成、レイヤー構成、技術スタックを指定しません。実際の機能、運用、セキュリティ、信頼性の要件を満たしながら、構造を明快にし、責務を適切に保ち、複雑さを管理し、継続的に進化できるようにする実践的な設計制約を示します。

### 2. 中核となる原則

**1. Capability & Kernel Boundaries — 中核機能と共有カーネルの境界**

システムの中核機能と概念を軸にプロジェクトを構成します。共有の実行カーネルや基盤となるランタイム機構がある場合、各機能と共有機構の責務を明確にします。機能モジュールは固有のドメインルールを持ち、共有カーネルは機能をまたいで一貫性が必要な実行機構と共通の不変条件を担います。再利用だけを理由にコードをカーネルへ集約せず、局所的な自律性を理由に全体ルールを重複実装しないようにします。

**2. Structural Transparency — 構造と主要経路の可視性**

プロジェクト構成、モジュール名、アプリケーションのエントリーポイント、アーキテクチャ文書から、システムの構成、モジュールの責務、依存方向、主要な実行経路が分かるようにします。アプリケーションの入口はモジュールの組み立て方を示し、外部からの入口は責務の明確なモジュールへ処理を委ねます。重要な設計情報を、開発者の記憶、大量のファイル検索、見えないフレームワーク規約に頼って見つける状態にしません。

**3. Responsibility Cohesion — 責務、変更理由、テスト境界に基づく凝集**

意味的に関連し、密接に協力し、または同じ理由で変わるルール、状態、実装、テストをまとめます。責務、変更理由、依存関係、テスト境界に実質的な違いがあり、分割によって全体の複雑さが下がる場合に新しいモジュールや抽象化を導入します。モジュールの粒度は責務の凝集度、協力コスト、変更の特性から決めます。行数、ディレクトリ数、コード再利用率だけで決めません。

**4. Explicit Control Flow — 重要な制御フローの追跡可能性**

重要な判断、呼び出し順序、状態遷移、副作用、エラー処理、再試行、復旧をコードまたは明確な実行契約から追跡できるようにします。イベント、コールバック、非同期タスク、フレームワーク機構を使う場合は、起動条件、実行上の意味、状態への影響、失敗時の処理を明示します。重要な業務やシステムの振る舞いを、見つけられない暗黙の制御ロジックに依存させません。

**5. Explicit Dependencies & Assembly — 依存関係と組み立ての明示**

モジュール間の依存関係を見えるようにし、依存方向を安定させ、明確なインターフェースや契約で協調させます。アプリケーションのコンポジションルートが、各モジュールとその基盤依存を接続します。モジュールがアプリケーションの入口に逆依存したり、他モジュールの内部実装へ不必要に依存したりしないようにします。置き換え、分離、独立した進化、安定した契約が実際に必要な場合にインターフェースや抽象化を追加します。循環依存、暗黙のグローバル依存、不要な間接呼び出しを避けます。

**6. Necessary Complexity — 実際の要件とリスクに基づく複雑さ**

抽象化、レイヤー、パターン、基盤は、確認済みの機能要件、運用上の制約、リスクに役立つ形で導入します。表面的な単純さを優先して、必要な永続化、状態復旧、アクセス制御、予算管理、バージョン整合性、障害対応を省略しません。同時に、現実的な根拠のない過剰設計も避けます。重要な構造上の複雑さごとに、解決する問題、もたらす価値、取り除いた場合の影響を説明できるようにします。

**7. Local Change & Shared Invariants — 局所的な変更と共有不変条件の両立**

独立して変わる責務は、それぞれのモジュール内で進化させます。モジュールをまたいで一貫性が必要なルールには、明確な定義元または実装の権威を設けます。共有ルールを統一する根拠は意味と不変条件の一致であり、コードの見た目の類似ではありません。安定した契約によって重複実装や意味のずれを防ぎながら、共有モジュールがすべての業務ロジックを抱える巨大なモジュールになることも防ぎます。局所化によって不要な変更の波及を抑えつつ、必要な一貫性を保ちます。

**8. Composable Testability — 細かく組み合わせ可能なテスト**

各ルールや機能を独立して検証でき、明確なインターフェースを通じて段階的に組み合わせてテストできるようにします。ユニットテストは局所ルールを、ユースケーステストは一連の操作を、プロトコルテストや統合テストはモジュール間の協調を、エンドツーエンドテストは実際の実行経路を検証します。各層の目的を明確にし、失敗箇所を特定しやすくします。モデルに依存するシステムでは、決定的なソフトウェア動作テストとモデル動作の評価を分け、それぞれの検証目的、安定性、実行コストに合わせて設計します。

**9. Bounded Context — 必要十分に絞ったコンテキスト**

プロジェクト構成、モジュールの説明、公開契約、重要な制約、テストによって、開発者や AI が局所的なタスクと必要な前後関係をすばやく理解できるようにします。システム全体を把握しなくても、信頼できる作業ができる状態を目指します。適切なモジュール凝集、絞り込んだ依存関係、明確な命名、段階的な情報提示によって理解コストを下げます。コンテキスト効率とは、タスクに必要十分な情報を提供することです。ファイル数やモジュールを最少にすること、小さなパッケージを大量に作ることではありません。

**10. Layered Feedback & Continuous Verification — 段階的なフィードバックと継続検証**

変更の種類ごとに、明確で適切かつ再現可能な検証経路を用意します。自動テスト、型チェック、静的解析、アーキテクチャ制約のチェックで重要な不変条件を守ります。まず速いフィードバックを提供し、その後は変更のリスク、影響範囲、リリース段階に応じて、統合テスト、実モデルでの検証、エンドツーエンドテストを行います。古い契約、重複ルール、使われない抽象化、漏れた境界を継続的に整理し、進化の中でも原則との整合性を保ちます。

### 3. アーキテクチャ判断の基準

重要なアーキテクチャ判断では、次の問いに明確に答えられるようにします。

- **機能の所有者：** この機能やルールを担当するモジュールはどれか。共有して一貫性を保つルールは何か。
- **構造の見つけやすさ：** プロジェクト構成や入口からすぐに見つけられるか。
- **振る舞いの追跡可能性：** 実行方法、状態変更、失敗処理を明確に理解できるか。
- **依存関係の妥当性：** 他モジュールに依存する理由は何か。依存は必要で、方向は安定しているか。
- **複雑さの妥当性：** 新しい抽象化、レイヤー、基盤はどの実際の問題を解決するか。
- **変更の局所性：** 変更によってどのモジュールが影響を受けるか。必要な影響と避けられる影響は何か。
- **テストの組み合わせやすさ：** 独立して検証し、より大きな振る舞いの一部としても検証できるか。
- **コンテキストの十分さ：** 開発者や AI は限られた関連情報でタスクを完了できるか。
- **フィードバックの有効性：** 変更のリスクに合った検証経路があるか。

これらに明確な答えがない場合、設計をさらに明確にする必要があります。

### 4. 全体設計の目標

Explicit Architecture は、実際の運用要件を満たしながら、システムの理解、変更の波及、検証にかかるコストをできるだけ抑えることを目指します。コード量、モジュール数、抽象化の深さは設計上の選択肢であり、成功を測る指標ではありません。

目指すことは次のとおりです。

- 必要な複雑さに明確な担当を設け、追跡できる形で表現する。
- モジュールをまたぐ一貫性を、明確な権威を持つルールで守る。
- 独立した責務を局所で進化させ、独立して検証できるようにする。
- 人と AI がシステムの構造、振る舞い、制約を見つけられるようにする。
- テストとフィードバックで、設計が今も成り立つかを継続的に確かめる。

### 5. 中核となる宣言

**Make Structure Visible. Make Behavior Explicit. Keep Dependencies Clear. Preserve Shared Invariants. Keep Changes Local. Make Tests Composable.**

構造を見えるようにし、振る舞いを明示し、依存関係を明確にし、共有不変条件を守り、変更を局所に保ち、テストを組み合わせ可能にする。

### 6. 一文で表すと

**Explicit Architecture は、明確な機能境界、見えるプロジェクト構造、追跡可能な制御フロー、安定した依存関係、一貫した共有不変条件、組み合わせ可能なテストを通じて、限られたコンテキストでの確かな理解、局所的な変更、継続的な進化を実現するソフトウェアアーキテクチャ手法です。**
