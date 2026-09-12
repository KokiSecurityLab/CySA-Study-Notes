# Koki's Technical Paper #018

## Human-in-the-Loop — Ethical Leadership in the AI Era, Continuous Ingestion Audit Protocols, and Manual Intervention Governance

### Summary Digest
This paper defines a human-oversight model for automated systems, aligned with CISSP Domain 1, NIST AI RMF practices, and EU AI Act Article 14 human-oversight requirements.

Automated outputs below a defined confidence threshold, or affecting a defined category of high-impact decisions, are held for human review before being executed.

---
### 1. Algorithmic Processing Limitations
Structural Risks of Unreviewed Automated Decision-Making:

* **Absence of Contextual Judgment in Automated Systems**: Automated decision systems evaluate inputs against trained patterns and defined rules, and can produce technically valid but contextually inappropriate outputs when a situation falls outside the conditions represented in their training or configuration.
* **Unverified Acceptance of Model Output**: Treating automated output as authoritative without a review step allows an incorrect or low-confidence prediction to directly drive a consequential action.
* **Volume-Based Evasion of Manual Review**: A high volume of automated requests or outputs can make comprehensive manual review impractical unless review is targeted specifically at higher-risk or lower-confidence cases.

### 2. Methodological Foundation
Confidence-Based Escalation and Oversight Principles:

* **Confidence-Threshold Escalation**: Automated outputs that fall below a defined confidence threshold are routed to a human reviewer rather than being executed automatically, consistent with human-oversight requirements described in EU AI Act Article 14.
* **Category-Based Mandatory Review**: Certain categories of decisions, defined in advance as high-impact, require human review regardless of model confidence, reducing reliance on confidence scores alone for high-stakes cases.
* **Alignment with Awareness Program Findings**: Escalation criteria are informed by the incident patterns and human-factor findings described in Technical Paper #010, keeping oversight triggers grounded in observed conditions rather than assumptions.

### 3. Pipeline Implementation
Review Routing and Accountability Logging:

1. **Confidence and Category Tagging**: Each automated output is tagged with its confidence score and decision category at the point of generation, before any escalation logic is applied.
2. **Routing to a Designated Reviewer**: Outputs requiring review are routed to a designated human reviewer with the relevant context, rather than a general queue lacking supporting information.
3. **Signed Decision Logging**: The reviewer's decision, along with their identity and the rationale provided, is logged for accountability and later audit, consistent with the logging approach in Technical Paper #002.

### 4. Boundary Governance
Override Authority and Escalation Review:

* **Defined Override Authority**: Specific roles are authorized to override or halt an automated process, and that authority is documented rather than left informal or assumed.
* **Separation of Model Operation from Override Capability**: The mechanism used to pause or override an automated system operates independently of the model itself, so a malfunctioning model cannot also disable the ability to intervene.
* **Continuous Review of Escalation Thresholds**: Confidence thresholds and mandatory-review categories are periodically reassessed against actual review outcomes, adjusting thresholds that generate too many or too few escalations.

### 5. Conclusion
Human-in-the-loop oversight only functions if the escalation criteria route the cases that actually need review, not simply the ones that are easiest to flag.

Aligning those criteria with CISSP Domain 1 and EU AI Act human-oversight expectations gives this review process a documented basis, not an ad hoc one.

---
# テクニカルペーパーシリーズ #018

## ヒューマン・イン・ザ・ループ — AI時代における倫理的リーダーシップ、継続的入力監査プロトコル、および手動介入ガバナンス

### サマリー・ダイジェスト
本論文は、CISSPドメイン1、NIST AI RMFの実務、およびEU AI法第14条の人的監視要件に準拠した、自動化システムに対する人的監視のガバナンスモデルを定義します。

定義済みの信頼度しきい値を下回る自動出力、または定義済みの高影響カテゴリに該当する判断は、実行される前に人間によるレビューへ回されます。

---
### 1. アルゴリズム処理の限界
未レビューの自動判断に伴う構造的リスク:

* **自動化システムにおける文脈判断の欠如**: 自動判断システムは学習済みのパターンと定義済みのルールに照らして入力を評価するため、学習・設定時に想定されていた条件から外れた状況では、技術的には妥当でも文脈的には不適切な出力を生成する可能性があります。
* **モデル出力の未検証な受容**: レビュー工程を経ずに自動出力を権威あるものとして扱うと、誤った予測や信頼度の低い予測が、そのまま重大な結果を伴う行動を直接引き起こしてしまいます。
* **大量処理による手動レビューの形骸化**: 大量の自動リクエストや出力は、より高リスクまたは低信頼度の事案に絞ってレビューを行わない限り、網羅的な手動レビューを非現実的にしてしまいます。

### 2. 方法論的基盤
信頼度に基づくエスカレーションと監視の原則:

* **信頼度しきい値によるエスカレーション**: 定義済みの信頼度しきい値を下回る自動出力は、自動的に実行されるのではなく人間のレビュー担当者へ回されます。これはEU AI法第14条に定められる人的監視要件と整合します。
* **カテゴリに基づく必須レビュー**: あらかじめ高影響と定義された特定のカテゴリの判断は、モデルの信頼度にかかわらず人間によるレビューを必要とし、重大な事案において信頼度スコアのみに依存することを避けます。
* **意識向上プログラムの知見との整合**: エスカレーション基準は、Technical Paper #010で述べたインシデントパターンや人的要因の知見を踏まえて策定され、監視のトリガーを想定ではなく観測された状況に根ざしたものにします。

### 3. パイプラインの実装
レビューへの振り分けと説明責任のログ記録:

1. **信頼度およびカテゴリのタグ付け**: 各自動出力は、エスカレーションロジックが適用される前の生成時点で、信頼度スコアと判断カテゴリのタグを付与されます。
2. **指定レビュー担当者への振り分け**: レビューが必要な出力は、補足情報のない一般的なキューではなく、関連する文脈情報とともに指定されたレビュー担当者へ振り分けられます。
3. **署名付きの判断ログ記録**: レビュー担当者の判断は、その担当者の識別情報および判断理由とともに、説明責任と後の監査のために記録されます。これはTechnical Paper #002で述べたログ記録の考え方と整合します。

### 4. 境界統治
上書き権限とエスカレーションレビュー:

* **明確化された上書き権限**: 自動化プロセスを上書きまたは停止できる権限は特定の役割に限定して付与され、その権限は非公式なものや暗黙の了解に留めず文書化されます。
* **モデルの動作と上書き機能の分離**: 自動化システムを一時停止または上書きする仕組みは、モデル自体から独立して動作するため、モデルの誤動作が介入能力そのものを無効化することはありません。
* **エスカレーションしきい値の継続的レビュー**: 信頼度しきい値と必須レビュー対象カテゴリは、実際のレビュー結果に照らして定期的に見直され、エスカレーションが過多または過少となっているしきい値が調整されます。

### 5. 結論
ヒューマン・イン・ザ・ループによる監視が機能するのは、単にフラグを立てやすいケースではなく、実際にレビューを要するケースをエスカレーション基準が正しく拾い上げる場合に限られます。

その基準をCISSPドメイン1およびEU AI法の人的監視に関する期待事項と整合させることで、このレビュープロセスは場当たり的なものではなく文書化された根拠を持つものになります。
