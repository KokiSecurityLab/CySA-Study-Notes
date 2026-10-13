# Koki's Technical Paper #051

## Security Governance — Policy Frameworks and Risk Metrics, Governance Infrastructure Engineering, and Quantitative Risk Analysis

### Summary Digest
This paper defines a security governance structure, aligned with CISSP Domain 1 and ISO/IEC 27001, that establishes a policy hierarchy of policies, standards, procedures, and guidelines under documented executive and board oversight.

Quantitative risk metrics, including Annualized Loss Expectancy (ALE), inform governance decisions rather than relying on qualitative judgment alone.

---
### 1. Undocumented Governance Structure Risk
Structural Vulnerabilities of Informal Security Oversight:

* **Absence of a Defined Policy Hierarchy**: Organizations without a documented distinction between policy, standard, procedure, and guideline produce inconsistent expectations, since staff cannot tell which documents are mandatory and which are advisory.
* **Unclear Executive Accountability**: Security programs without a documented reporting line to executive leadership or the board lack a clear point of accountability when a governance decision needs to be made or defended.
* **Purely Qualitative Risk Communication**: Risk discussions conducted only in qualitative terms, such as "high" or "low," give executives no consistent basis for comparing the relative cost-benefit of different risk-treatment options.

### 2. Policy Hierarchy and Metrics Foundation
Governance Structure and Quantitative Risk Principles:

* **Policy, Standard, Procedure, and Guideline Hierarchy**: Governance documentation follows the standard CISSP hierarchy, with policies defining mandatory intent, standards defining specific mandatory requirements, procedures defining mandatory steps, and guidelines providing optional recommendations.
* **Three-Lines-of-Defense Structure**: Organizational accountability is structured using the three-lines-of-defense model, separating operational risk ownership, risk and compliance oversight, and independent internal audit.
* **Quantitative Risk Metrics**: Risk is expressed using quantitative metrics such as Annualized Loss Expectancy (ALE), calculated from Single Loss Expectancy (SLE) and Annualized Rate of Occurrence (ARO), consistent with CISSP Domain 1 quantitative risk analysis.

### 3. Policy Development and Approval Sequence
Drafting, Review, and Executive Ratification Stages:

1. **Policy Drafting Against Business Objectives**: Security policy is drafted with explicit reference to documented business objectives, consistent with the principle that security governance exists to support, not obstruct, organizational mission.
2. **Cross-Functional Review**: Draft policy is reviewed by legal, compliance, and affected business units before executive submission, surfacing conflicts with existing obligations before ratification.
3. **Executive or Board Ratification**: Final policy is formally ratified by an accountable executive or board committee, with the ratification decision documented and retained.

### 4. Governance Maintenance and Metrics Review
Policy Currency and Risk-Metric Reporting Cadence:

* **Scheduled Policy Review Cycle**: Ratified policies are reviewed on a defined cycle rather than left static indefinitely, updating them as business objectives, regulatory requirements, or the threat landscape change.
* **Recurring Quantitative Risk Reporting**: ALE and related quantitative metrics are recalculated and reported to governance stakeholders on a defined cadence, rather than produced only during an annual audit.
* **Continuous Governance Effectiveness Auditing**: The internal audit function periodically assesses whether documented governance processes are actually followed in practice, rather than assuming written policy reflects operational reality.

### 5. Conclusion
A policy hierarchy only functions as governance if someone with accountability approved it and someone independent periodically checks that it is being followed.

Pairing that structure with quantitative risk metrics such as ALE, consistent with CISSP Domain 1, gives executives a comparable basis for risk decisions instead of a qualitative impression.

---
# テクニカルペーパーシリーズ #051

## セキュリティガバナンス — ポリシーフレームワークとリスク指標、ガバナンス基盤エンジニアリング、および定量的リスク分析

### サマリー・ダイジェスト
本論文は、CISSPドメイン1およびISO/IEC 27001に準拠したセキュリティガバナンス構造を定義し、文書化された経営層・取締役会の監督のもと、ポリシー・スタンダード・手順書・ガイドラインという文書階層を確立します。

年間予想損失額（ALE）を含む定量的リスク指標が、定性的な判断のみに頼るのではなくガバナンス上の意思決定に反映されます。

---
### 1. 未文書化のガバナンス構造リスク
非公式なセキュリティ監督に伴う構造的脆弱性:

* **明確なポリシー階層の欠如**: ポリシー・スタンダード・手順書・ガイドラインの区別を文書化していない組織は、どの文書が必須でどれが推奨事項なのかを職員が判断できず、期待水準に一貫性がなくなります。
* **不明確な経営層の説明責任**: 経営層や取締役会への報告経路を文書化していないセキュリティプログラムは、ガバナンス上の判断が必要または擁護されるべき場面での明確な説明責任の所在を欠きます。
* **純粋に定性的なリスクコミュニケーション**: 「高い」「低い」といった定性的な表現のみで行われるリスクの議論は、異なるリスク対応策間の相対的なコストと効果を比較する一貫した根拠を経営層に与えません。

### 2. ポリシー階層と指標の基盤
ガバナンス構造と定量的リスクの原則:

* **ポリシー・スタンダード・手順書・ガイドラインの階層**: ガバナンス文書は標準的なCISSPの階層に従い、ポリシーが必須の意図を定め、スタンダードが具体的な必須要件を定め、手順書が必須の手順を定め、ガイドラインが任意の推奨事項を示します。
* **3線ディフェンスモデル**: 組織的な説明責任は3線ディフェンスモデルを用いて構成され、業務上のリスク保有、リスク・コンプライアンス監督、独立した内部監査を分離します。
* **定量的リスク指標**: リスクは、単一予想損失額（SLE）と年間発生率（ARO）から算出される年間予想損失額（ALE）などの定量的指標を用いて表現され、CISSPドメイン1の定量的リスク分析と整合します。

### 3. ポリシー策定と承認の手順
起草・レビュー・経営層による承認の各段階:

1. **事業目標に基づくポリシー起草**: セキュリティポリシーは文書化された事業目標を明示的に参照して起草され、セキュリティガバナンスが組織の使命を阻害するのではなく支えるために存在するという原則と整合します。
2. **部門横断レビュー**: 起草されたポリシーは、経営層への提出前に法務・コンプライアンス部門および影響を受ける事業部門によってレビューされ、承認前に既存の義務との矛盾を明らかにします。
3. **経営層または取締役会による承認**: 最終的なポリシーは、責任を負う経営層または取締役会委員会によって正式に承認され、その承認判断は文書化・保管されます。

### 4. ガバナンス維持と指標レビュー
ポリシーの鮮度とリスク指標報告の頻度:

* **定められたポリシーレビューサイクル**: 承認済みのポリシーは無期限に固定されるのではなく定められた周期でレビューされ、事業目標・規制要件・脅威状況の変化に応じて更新されます。
* **定量的リスクの反復的な報告**: ALEおよび関連する定量的指標は、年次監査時のみに作成されるのではなく、定められた周期で再計算されガバナンス関係者へ報告されます。
* **ガバナンス実効性の継続的監査**: 内部監査機能は、文書化されたポリシーが実際の運用状況を反映していると想定するのではなく、文書化されたガバナンスプロセスが実務で本当に遵守されているかを定期的に評価します。

### 5. 結論
ポリシー階層がガバナンスとして機能するのは、実際に説明責任を負う者がそれを承認し、独立した立場の者がそれが遵守されているかを定期的に確認する場合に限られます。

その構造をALEなどの定量的リスク指標と組み合わせることは、CISSPドメイン1に沿いつつ、単なる定性的な印象ではなく、経営層にリスク判断のための比較可能な根拠を与えます。
