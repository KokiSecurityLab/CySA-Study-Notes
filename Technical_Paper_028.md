# Koki's Technical Paper #028

## Personal BCP — Ensuring Continuity Through Independence,Operations Continuity Planning, and Business Impact Analysis

### Summary Digest
This paper defines a business-continuity framework for single-administrator environments, aligned with CISSP Domain 1 BCP practices and Business Impact Analysis (BIA), that reduces key-person dependency through documentation and automation.

A designated backup administrator, pre-provisioned with break-glass access and current runbooks, maintains defined RTO targets if the primary administrator becomes unavailable.

---
### 1. Key-Person Dependency Risk
Structural Vulnerabilities of Single-Administrator Environments:

* **Undocumented Tribal Knowledge**: Operational procedures that exist only in one administrator's memory, without written documentation, cannot be executed by anyone else if that administrator is unavailable.
* **Single Point of Failure in Access Credentials**: Environments where only one person holds the credentials needed for critical recovery actions create a bus-factor-of-one condition that blocks all response until that person is reachable.
* **Undefined Recovery Priorities**: Without a documented Business Impact Analysis, there is no basis for deciding which systems to restore first during an extended absence, risking wasted effort on lower-priority recovery tasks.

### 2. Business Impact Analysis Foundation
Impact Tiers and Recovery Prioritization Criteria:

* **Tiered Recovery Prioritization**: Systems and tasks are ranked by business impact using a standard Business Impact Analysis (BIA) methodology, consistent with CISSP Domain 1, rather than being addressed in an arbitrary order during a disruption.
* **Defined RTO per Priority Tier**: Each priority tier is assigned a Recovery Time Objective (RTO), consistent with the recovery-objective approach defined in Technical Paper #012, setting explicit expectations for how quickly each tier must be restored.
* **Break-Glass Access Provisioning**: A designated backup administrator holds pre-provisioned, audited emergency access credentials, commonly referred to as break-glass access, usable only when the primary administrator is unavailable.

### 3. Documentation and Backup Readiness Sequence
SOP Compilation, Cross-Training, and Access Testing:

1. **Standard Operating Procedure Documentation**: Recovery and routine maintenance procedures are documented as step-by-step SOPs, consistent with the integrity-verification approach defined in Technical Paper #001, so they can be followed by someone other than the primary administrator.
2. **Backup Administrator Cross-Training**: The designated backup administrator is trained to execute documented SOPs independently, and this capability is periodically tested rather than assumed.
3. **Break-Glass Access Verification**: Emergency access credentials are tested on a defined schedule to confirm they remain valid and functional, rather than being verified for the first time during an actual incident.
4. 
### 4. Continuity Governance and Access Auditing
RTO Compliance and Emergency Access Review:

* **Logged Break-Glass Usage**: Any use of break-glass access is logged and reviewed after the fact, consistent with the accountability logging approach defined in Technical Paper #018, so emergency access remains auditable rather than untracked.
* **Automation to Reduce Manual Dependency**: Routine tasks are automated where feasible, reducing the number of actions that depend on manual execution by a specific individual.
* **Continuous SOP and BIA Currency Review**: Documented SOPs and the underlying Business Impact Analysis are reviewed on a defined cadence to confirm they still reflect the current infrastructure and priorities.

### 5. Conclusion
A continuity plan that lives only in one administrator's head provides
no actual continuity once that administrator is unreachable.

Pairing documented SOPs with tested break-glass access and
defined RTOs, consistent with CISSP Domain 1, is what makes a
single-administrator environment survivable rather than merely
convenient.

---
# テクニカルペーパーシリーズ #028

## パーソナルBCP — 独立性による業務継続の確保､業務継続計画､および
ビジネス影響分析

### サマリー・ダイジェスト
本論文は､CISSPドメイン1のBCP実務およびビジネス影響分析BIAに準
拠した､単一管理者環境向けの事業継続フレームワークを定義し､文書化と
自動化によりキーパーソンへの依存を低減します｡

事前に権限付与されたブレークグラス・アクセスと最新のランブックを備え
た指定バックアップ管理者が､主管理者が対応不能になった際に定義済みの
RTO目標を維持します｡

---
### 1. キーパーソン依存リスク
単一管理者環境に伴う構造的脆弱性:

* **文書化されていない属人的知識**: 一人の管理者の記憶にのみ存在し､文書化されていない運用手順は､その管理者が対応できない場合､他の誰も実行できません｡
* **アクセス資格情報における単一障害点**: 重要な復旧対応に必要な資格情報を一人しか保有していない環境は､その人物に連絡が取れるまですべての対応が滞る｢バスファクター1｣の状態を生み出します｡
* **未定義の復旧優先順位**: 文書化されたビジネス影響分析がなければ､長期不在の際にどのシステムを優先的に復旧すべきかを判断する根拠がなく､優先度の低い復旧作業に労力を浪費するリスクがあります｡

### 2. ビジネス影響分析の基盤
影響ティアと復旧優先順位付けの基準:

* **段階的な復旧優先順位付け**: システムやタスクは､混乱発生時に恣意的な順序で対応するのではなく､CISSPドメイン1に準拠した標準的なビジネス影響分析BIA手法を用いて事業影響度に基づきランク付けされます｡
* **優先度ティアごとのRTO設定**: 各優先度ティアには目標復旧時間RTOが設定されます｡これは テクニカルペーパーシリーズ #012で定義した復旧目標のアプローチと整合し､各ティアをどれだけ迅速に復旧すべきかという明確な期待値を定めます｡
* **ブレークグラス・アクセスの事前準備**: 指定バックアップ管理者は､一般に｢ブレークグラス・アクセス｣と呼ばれる､事前に権限付与され監査対象となる緊急アクセス資格情報を保有し､主管理者が対応不能な場合にのみ使用します｡

### 3. 文書化とバックアップ体制準備の手順
SOP作成・クロストレーニング・アクセステスト:

1. **標準作業手順書SOPの文書化**: 復旧および日常保守の手順は､テクニカルペーパーシリーズ #001で定義した整合性検証のアプローチと整合する形で､主管理者以外の人物でも従うことができるよう､段階的なSOPとして文書化されます｡
2. **バックアップ管理者のクロストレーニング**: 指定バックアップ管理者は文書化されたSOPを単独で実行できるよう訓練され､この能力は前提とするのではなく定期的にテストされます｡
3. **ブレークグラス・アクセスの検証**: 緊急アクセス資格情報は､実際のインシデント発生時に初めて確認するのではなく､定められたスケジュールでテストされ､有効かつ機能することを確認します｡

### 4. 継続性ガバナンスとアクセス監査
RTO遵守と緊急アクセスのレビュー:

* **ブレークグラス・アクセス利用のログ記録**: ブレークグラス・アクセスの利用は､テクニカルペーパーシリーズ #018で定義した説明責任のログ記録アプローチと整合する形で記録され､事後にレビューされます｡これにより緊急アクセスが追跡不能な状態にならないようにします｡
* **手動依存を減らすための自動化**: 実現可能な範囲で日常的なタスクを自動化し､特定の個人による手動実行に依存する行動の数を減らします｡
* **SOPおよびBIAの鮮度に関する継続的レビュー**: 文書化されたSOPおよびその基盤となるビジネス影響分析は､現在のインフラと優先順位を引き続き反映しているかを確認するため､定められた周期でレビューされます｡

### 5. 結論
継続計画が一人の管理者の頭の中にしか存在しないのであれば､その管理者
に連絡が取れなくなった時点で実質的な継続性は失われます｡

文書化されたSOPと検証済みのブレークグラス・アクセス､そして定義済み
のRTOを組み合わせることが､CISSPドメイン1に沿いつつ､単一管理者環
境を単なる便宜ではなく存続可能なものにします｡
