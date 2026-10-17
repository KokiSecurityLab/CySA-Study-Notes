# Koki's Technical Paper #053

## Compliance Mapping — Regulatory Obligation Tracking, PCI DSS and GDPR Alignment, and Breach Notification Timelines

### Summary Digest
This paper defines a compliance-obligation mapping framework, aligned with CISSP Domain 1, tracking regulatory requirements such as PCI DSS and GDPR against the controls that satisfy each one.

Breach notification timelines, including the 72-hour GDPR Article 33 requirement, are tracked so a confirmed incident triggers the correct notification clock.

---
### 1. Untracked Obligation Risk
Structural Vulnerabilities of Informal Compliance Tracking:

* **Regulatory Requirements Known Informally, Not Documented**: Relying on institutional memory of which regulations apply, rather than a documented register, risks a requirement being missed entirely when the person who knew about it leaves.
* **Unmapped Control-to-Requirement Relationships**: Implementing security controls without explicitly mapping which regulatory requirement each control satisfies makes it difficult to demonstrate compliance during an actual audit or investigation.
* **Undefined Breach Notification Timelines**: Without a documented, jurisdiction-specific notification timeline, an organization risks missing a legally mandated notification deadline during the confusion of an actual incident.

### 2. Regulatory Mapping and Notification Foundation
Obligation Register and Timeline Documentation Principles:

* **Compliance Obligation Register**: Applicable regulatory and contractual requirements, such as PCI DSS for payment card handling and GDPR for personal data processing, are documented in a maintained register rather than tracked informally.
* **Control-to-Requirement Mapping**: Each documented obligation is mapped to the specific technical or administrative control that satisfies it, consistent with the control-traceability approach defined in Technical Paper #050.
* **Jurisdiction-Specific Notification Timelines**: Breach notification deadlines, such as the 72-hour requirement under GDPR Article 33, are documented per applicable jurisdiction rather than assumed to be uniform across all regulations.

### 3. Obligation Verification and Notification Sequence
Applicability Review, Control Mapping, and Timeline Activation:

1. **Regulatory Applicability Review**: New or changed business activities are reviewed against the compliance obligation register to determine which regulations newly apply or no longer apply.
2. **Control Coverage Verification**: Each applicable obligation is checked against the control-mapping register to confirm a corresponding control actually exists and is currently active.
3. **Incident-Triggered Notification Clock**: A confirmed incident involving regulated data immediately triggers the documented notification timeline for the applicable jurisdiction, consistent with the incident-response process defined in Technical Paper #033.

### 4. Compliance Governance and Register Auditing
Register Currency and Notification Readiness Review:

* **Scheduled Register Review**: The compliance obligation register is reviewed on a defined cadence to capture new regulatory requirements or changes to existing ones.
* **Separation of Legal Interpretation from Technical Mapping**: Legal counsel determines which regulations apply and their specific requirements; the technical mapping team translates those requirements into control mappings, keeping the two functions distinct but coordinated.
* **Continuous Notification-Readiness Drilling**: Notification procedures are tested through drills on a defined cadence, consistent with the drill approach defined in Technical Paper #045, confirming the organization can actually meet documented deadlines.

### 5. Conclusion
A compliance requirement that exists only in someone's memory is not something an organization can reliably demonstrate meeting during an actual audit.

Mapping each obligation to a specific control and notification timeline, consistent with CISSP Domain 1, turns compliance from an assumption into something verifiable on demand.

---
# テクニカルペーパーシリーズ #053

## コンプライアンスマッピング — 規制上の義務追跡、PCI DSSおよびGDPRとの整合、および侵害通知の期限

### サマリー・ダイジェスト
本論文は、CISSPドメイン1に準拠したコンプライアンス義務マッピングフレームワークを定義し、PCI DSSやGDPRなどの規制要件を、それぞれを満たす統制と照合して追跡します。

GDPR第33条の72時間要件を含む侵害通知の期限を追跡し、確認済みのインシデントが正しい通知の時計を作動させるようにします。

---
### 1. 追跡されていない義務のリスク
非公式なコンプライアンス追跡に伴う構造的脆弱性:

* **文書化されず非公式に把握されている規制要件**: どの規制が適用されるかを文書化された台帳ではなく組織内の記憶に頼ると、それを知っていた担当者が離職した際に要件が完全に見落とされるリスクがあります。
* **マッピングされていない統制と要件の関係**: どの規制要件をどの統制が満たしているかを明示的にマッピングせずにセキュリティ統制を実装すると、実際の監査や調査の際にコンプライアンスを示すことが困難になります。
* **未定義の侵害通知期限**: 法域ごとの通知期限を文書化していない組織は、実際のインシデント発生時の混乱の中で法的に義務付けられた通知期限を逃すリスクを抱えます。

### 2. 規制マッピングと通知の基盤
義務台帳と期限文書化の原則:

* **コンプライアンス義務台帳**: カード情報取り扱いに関するPCI DSSや個人データ処理に関するGDPRなど、適用される規制・契約上の要件は、非公式に追跡されるのではなく維持管理された台帳に文書化されます。
* **統制と要件のマッピング**: 文書化された各義務は、テクニカルペーパーシリーズ #050 で定義した統制トレーサビリティのアプローチと整合する形で、それを満たす特定の技術的または管理的統制に対応付けられます。
* **法域別の通知期限**: GDPR第33条の72時間要件などの侵害通知期限は、すべての規制で一律であると想定するのではなく、適用される法域ごとに文書化されます。

### 3. 義務検証と通知の手順
適用性レビュー・統制マッピング・期限の起動:

1. **規制適用性レビュー**: 新規または変更された事業活動は、コンプライアンス義務台帳に照らしてレビューされ、新たに適用される、または適用されなくなった規制を特定します。
2. **統制カバレッジの検証**: 適用される各義務は統制マッピング台帳と照合され、対応する統制が実際に存在し現在も有効であることを確認します。
3. **インシデントによる通知時計の起動**: 規制対象データに関わる確認済みのインシデントは、テクニカルペーパーシリーズ #033 で定義したインシデント対応プロセスと整合する形で、適用される法域の文書化された通知期限を直ちに起動させます。

### 4. コンプライアンスガバナンスと台帳監査
台帳の鮮度と通知対応能力のレビュー:

* **定期的な台帳レビュー**: コンプライアンス義務台帳は、新たな規制要件や既存要件の変更を捉えるため、定められた周期でレビューされます。
* **法的解釈と技術的マッピングの分離**: 法務担当がどの規制が適用されるかとその具体的要件を判断し、技術マッピングチームがそれらの要件を統制マッピングへ変換します。両機能は明確に分離しつつ連携します。
* **通知対応能力の継続的な訓練**: 通知手続きは、テクニカルペーパーシリーズ #045 で定義した訓練アプローチと整合する形で定められた周期で訓練され、組織が文書化された期限を実際に遵守できることを確認します。

### 5. 結論
誰かの記憶にしか存在しないコンプライアンス要件は、実際の監査時に組織が確実に遵守を示せるものにはなりません。

各義務を特定の統制と特定の通知期限に対応付けることは、CISSPドメイン1に沿いつつ、コンプライアンスを想定から必要に応じて検証可能なものへと変えます。
