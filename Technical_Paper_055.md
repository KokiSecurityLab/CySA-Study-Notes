# Koki's Technical Paper #055

## Threat Modeling — STRIDE Methodology Application, Data Flow Diagramming, and Design-Phase Risk Identification

### Summary Digest
This paper defines a design-phase threat-modeling process, aligned with CISSP Domain 1 and STRIDE methodology, identifying spoofing, tampering, repudiation, disclosure, denial-of-service, and privilege-escalation risks before implementation begins.

Each identified threat is fed into the quantitative risk-assessment process defined in Technical Paper #052, connecting early design analysis to measurable risk prioritization.

---
### 1. Post-Implementation Discovery Risk
Structural Vulnerabilities of Threat Modeling Skipped at Design Time:

* **Threats Discovered Only After Implementation**: Systems designed without structured threat analysis often have their most significant design-level flaws discovered only during testing or, worse, after deployment, when remediation is substantially more costly.
* **Unsystematic, Ad Hoc Threat Brainstorming**: Identifying threats through unstructured discussion rather than a defined methodology tends to produce inconsistent coverage, with some threat categories consistently overlooked across different projects.
* **Undocumented Trust Boundaries**: Without an explicit data flow diagram identifying where trust boundaries exist, it is difficult to systematically evaluate which specific interactions require security controls.

### 2. STRIDE and Data Flow Foundation
Threat Category Definitions and Diagramming Principles:

* **STRIDE Threat Categories**: Threats are systematically evaluated against each of the six STRIDE categories, Spoofing, Tampering, Repudiation, Information disclosure, Denial of service, and Elevation of privilege, for every relevant system component.
* **Data Flow Diagramming**: A data flow diagram documents processes, data stores, external entities, and trust boundaries, providing the structural basis against which STRIDE categories are systematically applied.
* **Alignment with Quantitative Risk Assessment**: Each identified threat is handed off to the SLE and ALE calculation process defined in Technical Paper #052, converting a qualitative threat-modeling finding into a quantified, prioritized risk.

### 3. Diagramming and Threat Enumeration Sequence
Diagram Construction, Boundary Identification, and Category Review:

1. **Data Flow Diagram Construction**: The system under review is diagrammed to show processes, data stores, external entities, and the trust boundaries between them.
2. **Systematic STRIDE Application**: Each element crossing a trust boundary is evaluated against all six STRIDE categories in turn, rather than only the categories that come to mind first.
3. **Threat Documentation and Handoff**: Each identified threat is documented with its STRIDE category and affected component, then handed off for quantitative scoring consistent with Technical Paper #052.

### 4. Threat Model Governance and Currency Review
Model Maintenance and Design-Change Review:

* **Threat Model Updates Tied to Design Changes**: The threat model is revisited whenever the system architecture changes materially, rather than being treated as a one-time exercise completed only at initial design.
* **Peer Review of Threat Model Completeness**: A second reviewer independently checks that all STRIDE categories were applied to all relevant components, reducing the chance that a category was skipped unnoticed.
* **Continuous Threat-to-Incident Correlation**: Actual incidents are reviewed against the existing threat model to confirm whether the responsible threat was previously identified, informing whether the modeling process itself needs adjustment.

### 5. Conclusion
A threat found during design costs a fraction of what the same threat costs to fix after the system is already in production.

Applying STRIDE systematically to a data flow diagram, per CISSP Domain 1 and the process in Technical Paper #052, catches design-level risk before implementation makes it expensive.

---
# テクニカルペーパーシリーズ #055

## 脅威モデリング — STRIDE方法論の適用、データフロー図作成、および設計段階でのリスク特定

### サマリー・ダイジェスト
本論文は、CISSPドメイン1およびSTRIDE方法論に準拠した設計段階の脅威モデリングプロセスを定義し、実装開始前になりすまし・改ざん・否認・情報漏えい・サービス拒否・権限昇格のリスクを特定します。

特定された各脅威は テクニカルペーパーシリーズ #052 で定義した定量的リスク評価プロセスへ引き渡され、初期設計段階の分析を測定可能なリスク優先順位付けへと結びつけます。

---
### 1. 実装後発見のリスク
設計段階で脅威モデリングを省略することに伴う構造的脆弱性:

* **実装後にのみ発見される脅威**: 構造化された脅威分析なしに設計されたシステムは、最も重大な設計レベルの欠陥が、テスト段階、あるいはさらに悪い場合はデプロイ後になって初めて発見され、修復コストが大幅に高くなることがよくあります。
* **体系立っていない場当たり的な脅威の洗い出し**: 定義された方法論ではなく非構造的な議論を通じて脅威を特定すると、カバレッジに一貫性がなくなりがちで、特定の脅威カテゴリが複数のプロジェクトにわたって一貫して見落とされることがあります。
* **文書化されていない信頼境界**: 信頼境界がどこに存在するかを特定する明示的なデータフロー図がなければ、どの具体的なやり取りにセキュリティ統制が必要かを体系的に評価することが困難になります。

### 2. STRIDEとデータフローの基盤
脅威カテゴリの定義と図式化の原則:

* **STRIDE脅威カテゴリ**: 脅威は、関連するすべてのシステムコンポーネントについて、なりすまし（Spoofing）・改ざん（Tampering）・否認（Repudiation）・情報漏えい（Information disclosure）・サービス拒否（Denial of service）・権限昇格（Elevation of privilege）というSTRIDEの6カテゴリそれぞれに照らして体系的に評価されます。
* **データフロー図作成**: データフロー図はプロセス、データストア、外部エンティティ、信頼境界を文書化し、STRIDEカテゴリを体系的に適用するための構造的基盤を提供します。
* **定量的リスク評価との整合**: 特定された各脅威は、定性的な脅威モデリングの所見を定量化され優先順位付けされたリスクへ変換するため、テクニカルペーパーシリーズ #052 で定義したSLE・ALE算出プロセスへ引き渡されます。

### 3. 図式化と脅威列挙の手順
図の構築・境界特定・カテゴリレビュー:

1. **データフロー図の構築**: レビュー対象のシステムは、プロセス、データストア、外部エンティティ、およびそれらの間の信頼境界を示す形で図式化されます。
2. **STRIDEの体系的な適用**: 信頼境界を越える各要素は、最初に思いついたカテゴリのみではなく、6つのSTRIDEカテゴリすべてに順に照らして評価されます。
3. **脅威の文書化と引き渡し**: 特定された各脅威は、そのSTRIDEカテゴリと影響を受けるコンポーネントとともに文書化され、テクニカルペーパーシリーズ #052と整合する定量的スコアリングへ引き渡されます。

### 4. 脅威モデルガバナンスと鮮度レビュー
モデルの維持と設計変更時のレビュー:

* **設計変更に連動した脅威モデルの更新**: 脅威モデルは、初期設計時にのみ完了する一度きりの作業として扱われるのではなく、システムアーキテクチャが大きく変化するたびに見直されます。
* **脅威モデルの完全性に対するピアレビュー**: 第二のレビュー担当者が、すべてのSTRIDEカテゴリがすべての関連コンポーネントに適用されたかを独立して確認し、カテゴリが気づかれないまま省略されるリスクを減らします。
* **脅威とインシデントの継続的な相関分析**: 実際に発生したインシデントは既存の脅威モデルと照合してレビューされ、原因となった脅威が事前に特定されていたかを確認し、モデリングプロセス自体の調整要否を判断します。

### 5. 結論
設計段階で発見された脅威を修正するコストは、システムが既に本番稼働した後に同じ脅威を修正するコストのほんの一部で済みます。

データフロー図に対してSTRIDEを体系的に適用することは、CISSPドメイン1および テクニカルペーパーシリーズ #052 で定義したプロセスに沿いつつ、実装によって高コスト化する前に設計レベルのリスクを捉えます。
