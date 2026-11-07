# Koki's Technical Paper #061

## Secure Design Principles — Saltzer and Schroeder Framework Application, Defense in Depth Architecture, and Fail-Safe Default Configuration

### Summary Digest
This paper defines a secure-architecture design methodology, aligned with CISSP Domain 3 and Saltzer-Schroeder principles, evaluating architecture against economy of mechanism, fail-safe defaults, and least privilege.

Each architectural decision is checked against these principles during design review rather than relying on ad hoc judgment about what counts as secure design.

---
### 1. Unprincipled Design Review Risk
Structural Vulnerabilities of Ad Hoc Architecture Review:

* **Complexity Without a Simplicity Check**: Architecture that grows in complexity without a documented economy-of-mechanism review accumulates unnecessary attack surface that no single reviewer can fully reason about.
* **Default-Permit Configuration**: Systems configured to allow access by default and deny only explicitly listed exceptions fail open when a configuration step is missed, unlike a default-deny design.
* **Partial Mediation of Access Requests**: Access-control checks applied only at initial connection, rather than to every subsequent request, allow a request that bypasses the initial check to proceed unmediated afterward.

### 2. Design Principle Application Foundation
Saltzer and Schroeder Principle Definitions:

* **Fail-Safe Defaults and Complete Mediation**: Access decisions default to denial absent explicit permission, and every access request is checked against current authorization rather than relying on a cached prior decision.
* **Least Privilege and Least Common Mechanism**: Each component operates with only the access it requires, consistent with the least-privilege approach defined in Technical Paper #030, and shared mechanisms between components are minimized to reduce cross-component compromise paths.
* **Open Design and Psychological Acceptability**: Security depends on protecting keys and credentials rather than on the secrecy of the design itself, and controls are designed to be usable enough that legitimate users do not routinely circumvent them.

### 3. Principle-Based Review Sequence
Architecture Mapping, Principle Checking, and Finding Documentation:

1. **Architecture Diagramming**: The system architecture is diagrammed showing components, trust boundaries, and access paths, consistent with the data flow diagramming approach defined in Technical Paper #055.
2. **Principle-by-Principle Evaluation**: Each Saltzer and Schroeder principle is evaluated against the diagrammed architecture in turn, documenting where the design satisfies or violates each one.
3. **Finding Remediation Planning**: Identified violations are documented as findings with a proposed remediation, prioritized consistent with the risk-scoring approach defined in Technical Paper #052.

### 4. Design Review Governance and Recurrence Auditing
Review Cadence and Principle-Violation Recurrence Tracking:

* **Design Review Required Before Major Changes**: Significant architectural changes undergo a principle-based review before implementation, rather than being reviewed only after deployment.
* **Recurring Violation Pattern Tracking**: Violations of the same principle recurring across multiple projects are tracked, indicating a need for organization-wide design guidance rather than a one-off fix.
* **Continuous Principle Currency Review**: The set of applied design principles is periodically reviewed to confirm it still reflects current architectural practice as systems evolve.

### 5. Conclusion
Secure architecture is not a single property a system either has or lacks; it is the cumulative result of checking a design against specific, nameable principles.

Applying the Saltzer and Schroeder framework systematically, consistent with CISSP Domain 3, turns "is this design secure" into a checklist someone can actually complete.

---
# テクニカルペーパーシリーズ #061

## セキュア設計原則 — サルツァー＝シュローダーの枠組みの適用、多層防御アーキテクチャ、およびフェイルセーフなデフォルト構成

### サマリー・ダイジェスト
本論文は、CISSPドメイン3およびサルツァー＝シュローダーの設計原則に準拠したセキュアアーキテクチャ設計手法を定義し、機構の経済性、フェイルセーフなデフォルト、最小権限に照らしてアーキテクチャを評価します。

各アーキテクチャ上の判断は、何が安全な設計とみなされるかについての場当たり的な判断に頼るのではなく、設計レビュー時にこれらの原則に照らして確認されます。

---
### 1. 無原則な設計レビューのリスク
場当たり的なアーキテクチャレビューに伴う構造的脆弱性:

* **簡潔性の検証を欠いた複雑化**: 機構の経済性についての文書化されたレビューを経ずに複雑化していくアーキテクチャは、単独のレビュー担当者が全体を把握しきれない不要な攻撃対象領域を蓄積してしまいます。
* **既定で許可する構成**: 既定でアクセスを許可し、明示的に列挙された例外のみを拒否するよう構成されたシステムは、既定で拒否する設計とは異なり、構成手順が漏れた際にフェイルオープン（開いた状態で失敗）します。
* **アクセス要求の部分的な仲介**: アクセス制御チェックが最初の接続時にのみ適用され、以降のすべてのリクエストには適用されない場合、最初のチェックを回避したリクエストはその後仲介されないまま進んでしまいます。

### 2. 設計原則適用の基盤
サルツァー＝シュローダーの原則定義:

* **フェイルセーフなデフォルトと完全な仲介**: アクセス判断は明示的な許可がない限り既定で拒否となり、キャッシュされた過去の判断に頼るのではなく、すべてのアクセス要求が現在の認可状態と照合されます。
* **最小権限と最小共通機構**: 各コンポーネントは、テクニカルペーパーシリーズ #030 で定義した最小権限アプローチと整合する形で必要な範囲のアクセスのみで動作し、コンポーネント間で共有される機構は、コンポーネントをまたぐ侵害経路を減らすため最小限に抑えられます。
* **オープンな設計と心理的受容性**: セキュリティは設計自体の秘匿性ではなく鍵と資格情報の保護に依存し、統制は正規のユーザーが日常的にそれを回避しようとしない程度に使いやすく設計されます。

### 3. 原則に基づくレビューの手順
アーキテクチャマッピング・原則の確認・所見の文書化:

1. **アーキテクチャの図式化**: テクニカルペーパーシリーズ #055 で定義したデータフロー図作成アプローチと整合する形で、システムアーキテクチャはコンポーネント、信頼境界、アクセス経路を示す形で図式化されます。
2. **原則ごとの評価**: サルツァー＝シュローダーの各原則が図式化されたアーキテクチャに対して順に評価され、設計がどの原則を満たし、どの原則に違反しているかが文書化されます。
3. **所見の是正計画**: 特定された違反は、提案された是正策とともに所見として文書化され、テクニカルペーパーシリーズ #052で定義したリスクスコアリングアプローチと整合する形で優先順位付けされます。

### 4. 設計レビューガバナンスと再発監査
レビュー頻度と原則違反の再発追跡:

* **大規模変更前の設計レビューの義務化**: 重大なアーキテクチャ変更は、デプロイ後にのみレビューされるのではなく、実装前に原則に基づくレビューを受けます。
* **繰り返される違反パターンの追跡**: 複数のプロジェクトにわたって同じ原則の違反が繰り返される場合、それは単発の修正ではなく組織全体の設計指針の必要性を示すものとして追跡されます。
* **原則の鮮度の継続的レビュー**: 適用される設計原則のセットは、システムが進化する中で現行のアーキテクチャ実務を引き続き反映しているかを確認するため、定期的にレビューされます。

### 5. 結論
セキュアなアーキテクチャは、システムが持つか持たないかの単一の性質ではなく、具体的で名前の付いた原則に照らして設計を確認した結果の積み重ねです。

サルツァー＝シュローダーの枠組みを体系的に適用することは、CISSPドメイン3に沿いつつ、「この設計は安全か」という問いを実際に完了できるチェックリストへと変えます。
