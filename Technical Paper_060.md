# Koki's Technical Paper #060

## Security Baseline Tailoring — Control Scoping by Classification and Environment, NIST SP 800-53B Baseline Selection, and Compensating Control Justification

### Summary Digest
This paper defines a control-tailoring methodology, aligned with CISSP Domain 2 and NIST SP 800-53B, adapting a standard baseline to a system's classification tier, data states, and environment.

Controls that cannot be implemented as specified are documented with an approved compensating control rather than silently omitted from the baseline.

---
### 1. Uniform Baseline Misapplication Risk
Structural Vulnerabilities of Untailored Control Baselines:

* **Over-Application to Low-Sensitivity Systems**: Applying the full high-sensitivity control baseline to a low-classification system consumes resources on controls that provide little additional risk reduction for that system's actual exposure.
* **Under-Application to High-Sensitivity Systems**: Applying a generic baseline without considering a system's higher classification tier can leave genuinely sensitive systems under-protected relative to the risk they actually carry.
* **Undocumented Baseline Deviations**: Deviating from a standard control baseline without documenting why creates an untraceable gap that an audit cannot distinguish from an oversight.

### 2. Baseline Selection and Tailoring Foundation
NIST SP 800-53B Baselines and Compensating Control Principles:

* **Classification-Driven Baseline Selection**: The applicable control baseline (low, moderate, or high impact) is selected based on the classification tier defined in Technical Paper #027, rather than applied uniformly across all systems.
* **Scoping Guidance Application**: Controls not applicable to a given system's actual technology or environment, consistent with NIST SP 800-53B scoping guidance, are formally scoped out with documented justification rather than left ambiguous.
* **Compensating Control Documentation**: Where a specified control cannot be implemented as written, an approved compensating control providing equivalent risk reduction is documented and justified.

### 3. Tailoring Application and Approval Sequence
Baseline Assignment, Scoping Decisions, and Sign-Off:

1. **Baseline Assignment by Classification**: Each system is assigned its applicable control baseline based on its documented classification tier and data states.
2. **Scoping and Tailoring Decisions**: Individual controls within the assigned baseline are scoped in, scoped out, or tailored, with each decision documented alongside its rationale.
3. **Compensating Control Approval**: Any proposed compensating control is reviewed and approved by an accountable party before being accepted as equivalent to the original specified control.

### 4. Baseline Governance and Deviation Review
Tailoring Documentation Currency and Deviation Auditing:

* **Centralized Tailoring Decision Record**: All scoping, tailoring, and compensating-control decisions are recorded in a single, retrievable location rather than scattered across individual system documentation.
* **Reassessment on Classification Change**: A system's control baseline is reassessed whenever its classification tier or data states change, rather than remaining fixed at its original assignment indefinitely.
* **Continuous Deviation Auditing**: Documented deviations and compensating controls are reviewed on a defined cadence to confirm they remain justified and that the compensating control still provides equivalent protection.

### 5. Conclusion
A control baseline applied without tailoring wastes effort on low-risk systems or leaves high-risk ones under-protected, invisible without a documented tailoring decision to check.

Scoping baselines to actual classification and environment, consistent with CISSP Domain 2 and NIST SP 800-53B, makes appropriate control something an auditor can verify rather than assume.

---
# テクニカルペーパーシリーズ #060

## セキュリティベースラインのテーラリング — 分類・環境に応じた統制の適用範囲決定、NIST SP 800-53Bベースライン選定、および代替統制の正当化

### サマリー・ダイジェスト
本論文は、CISSPドメイン2およびNIST SP 800-53Bに準拠した統制テーラリング手法を定義し、標準ベースラインをシステムの分類ティア・データ状態・環境に合わせて調整します。

指定通りに実装できない統制は、黙って基準から省くのではなく、承認された代替統制とともに文書化されます。

---
### 1. 画一的ベースライン誤適用のリスク
テーラリングされていない統制ベースラインに伴う構造的脆弱性:

* **低機微性システムへの過剰適用**: 高機微性向けの統制ベースライン全体を低分類のシステムへ適用すると、そのシステムの実際の露出に対してほとんど追加のリスク低減効果を持たない統制にリソースが費やされます。
* **高機微性システムへの過小適用**: システムのより高い分類ティアを考慮せずに汎用のベースラインを適用すると、本当に機微なシステムが実際に抱えるリスクに対して保護不十分な状態のままになり得ます。
* **文書化されていないベースラインからの逸脱**: 理由を文書化せずに標準の統制ベースラインから逸脱すると、監査では見落としと区別のつかない追跡不能な隙間が生まれます。

### 2. ベースライン選定とテーラリングの基盤
NIST SP 800-53Bベースラインと代替統制の原則:

* **分類に基づくベースライン選定**: 適用すべき統制ベースライン（低・中・高影響度）は、すべてのシステムに一律に適用されるのではなく、テクニカルペーパーシリーズ #027 で定義した分類ティアに基づいて選定されます。
* **適用範囲決定（スコーピング）ガイダンスの適用**: あるシステムの実際の技術や環境に該当しない統制は、曖昧なまま放置されるのではなく、NIST SP 800-53Bの適用範囲決定ガイダンスと整合する形で、文書化された正当性とともに正式に対象外とされます。
* **代替統制の文書化**: 指定された統制を記載通りに実装できない場合、同等のリスク低減効果を提供する承認済みの代替統制が文書化・正当化されます。

### 3. テーラリング適用と承認の手順
ベースライン割り当て・適用範囲決定・承認:

1. **分類に基づくベースライン割り当て**: 各システムには、文書化された分類ティアとデータ状態に基づいて適用すべき統制ベースラインが割り当てられます。
2. **適用範囲決定とテーラリングの判断**: 割り当てられたベースライン内の個々の統制は、対象に含める・対象外とする・調整するのいずれかとされ、各判断はその根拠とともに文書化されます。
3. **代替統制の承認**: 提案された代替統制は、元の指定統制と同等であると認められる前に、責任を負う者によってレビュー・承認されます。

### 4. ベースラインガバナンスと逸脱レビュー
テーラリング文書の鮮度と逸脱の監査:

* **一元化されたテーラリング判断記録**: すべての適用範囲決定・テーラリング・代替統制の判断は、個々のシステム文書に散在するのではなく、単一の参照可能な場所に記録されます。
* **分類変化時の再評価**: システムの統制ベースラインは、当初の割り当てのまま無期限に固定されるのではなく、分類ティアやデータ状態が変化するたびに再評価されます。
* **逸脱の継続的監査**: 文書化された逸脱と代替統制は、引き続き正当であり、代替統制が依然として同等の保護を提供しているかを確認するため、定められた周期でレビューされます。

### 5. 結論
テーラリングされずに適用された統制ベースラインは、低リスクシステムに労力を浪費するか、高リスクシステムを保護不足にするかのいずれかであり、文書化されたテーラリング判断と照合しない限りどちらも見えません。

ベースラインを実際の分類と環境に合わせて調整することは、CISSPドメイン2およびNIST SP 800-53Bに沿いつつ、「適切な統制」を想定ではなく監査担当者が検証できるものへと変えます。
