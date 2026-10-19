# Koki's Technical Paper #054

## Personnel Security — Background Screening and Offboarding, Employment Lifecycle Access Controls, and Mandatory Vacation Policy

### Summary Digest
This paper defines a personnel security framework, aligned with CISSP Domain 1, that ties access provisioning and revocation to specific employment-lifecycle events rather than to informal manager requests.

Background screening before hire, immediate access revocation at termination, and mandatory vacation for fraud detection form the core of this control set.

---
### 1. Lifecycle-Detached Access Risk
Structural Vulnerabilities of Informal Personnel Access Management:

* **Access Provisioning Without Screening Verification**: Granting system access before background screening is confirmed complete allows an unvetted individual to hold sensitive access during the screening window.
* **Delayed Termination Deprovisioning**: Access that is not revoked immediately upon termination remains available to a departed employee for as long as the deprovisioning process takes, creating an unnecessary window of exposure.
* **Absence of Mandatory Vacation or Job Rotation**: Roles where one person exclusively performs a sensitive function without ever being required to step away allow ongoing fraud or error to remain undetected indefinitely, since no one else reviews that person's work.

### 2. Screening and Lifecycle-Control Foundation
Background Verification and Access-Timing Principles:

* **Role-Appropriate Background Screening**: Screening depth is scaled to the sensitivity of the role, with higher-sensitivity roles, such as those with financial or privileged system access, requiring more thorough verification before hire.
* **Access Tied to Employment Status Change**: Provisioning and deprovisioning are triggered automatically by documented employment-lifecycle events, such as hire, role change, and termination, rather than requiring a separate manual request each time.
* **Mandatory Vacation and Job Rotation**: Roles with elevated financial or system privilege require periodic mandatory time away or rotation, consistent with fraud-detection practices in CISSP Domain 1, so another person's review can surface irregularities.

### 3. Onboarding and Offboarding Sequence
Screening Confirmation, Provisioning, and Immediate Revocation:

1. **Screening Confirmation Before Access Grant**: Access provisioning does not proceed until background screening for the role is confirmed complete, rather than running in parallel with onboarding.
2. **Least-Privilege Initial Provisioning**: Initial access is scoped to the minimum required for the role's function, consistent with the least-privilege approach defined in Technical Paper #030, with additional access requested separately as needed.
3. **Immediate Termination Revocation**: Access across all systems is revoked at the effective moment of termination, consistent with the automated session-revocation approach defined in Technical Paper #030, rather than at the end of a manual offboarding checklist.

### 4. Personnel Control Governance and Access Auditing
Deprovisioning Timeliness and Rotation Compliance Review:

* **Deprovisioning Timeliness Metrics**: The time between a termination event and actual access revocation is measured and tracked, identifying delays that need process correction.
* **Documented Mandatory Vacation Compliance**: Compliance with mandatory vacation or rotation policy for applicable roles is tracked and reported, rather than left to informal manager discretion.
* **Continuous Orphaned Account Auditing**: Active accounts are periodically reconciled against current employment records to identify orphaned accounts belonging to individuals no longer employed.

### 5. Conclusion
Access not explicitly tied to an employment-lifecycle event tends to outlive its reason, whether a screening gap at hire or a forgotten account at termination.

Automating provisioning and revocation around documented lifecycle events, consistent with CISSP Domain 1, closes both windows without depending on someone remembering to act.

---
# テクニカルペーパーシリーズ #054

## 人事セキュリティ — 採用時審査と離職時のアクセス管理、雇用ライフサイクルアクセス制御、および強制休暇ポリシー

### サマリー・ダイジェスト
本論文は、CISSPドメイン1に準拠した人事セキュリティフレームワークを定義し、アクセスの付与・剥奪を、非公式な上長からの依頼ではなく特定の雇用ライフサイクルイベントに結びつけます。

採用前の身元調査、離職時の即時アクセス剥奪、そして不正検知のための強制休暇の義務化が、この統制群の中核を成します。

---
### 1. ライフサイクルから切り離されたアクセスのリスク
非公式な人事アクセス管理に伴う構造的脆弱性:

* **審査確認前のアクセス付与**: 身元審査の完了が確認される前にシステムアクセスを付与すると、審査期間中に未審査の人物が機微なアクセス権を保持することになります。
* **離職時のアクセス剥奪の遅延**: 離職と同時に剥奪されないアクセスは、剥奪処理にかかる期間だけ離職者に利用可能なままとなり、不必要な露出期間を生み出します。
* **強制休暇・職務ローテーションの不在**: 一人が機微な職務を独占し、一度も職務を離れることを求められない役職は、他者によるレビューが働かないため、不正やミスが検知されないまま無期限に継続する余地を生みます。

### 2. 審査とライフサイクル統制の基盤
身元検証とアクセスタイミングの原則:

* **役職に応じた身元審査**: 審査の深度は役職の機微性に応じて調整され、金融アクセスや特権的なシステムアクセスを伴うより機微な役職ほど、採用前により入念な検証が求められます。
* **雇用状況の変化に紐づいたアクセス**: 付与・剥奪は、その都度個別の手動リクエストを必要とするのではなく、採用・役職変更・離職といった文書化された雇用ライフサイクルイベントによって自動的に発動します。
* **強制休暇と職務ローテーション**: 金融面またはシステム上の特権が高い役職には、CISSPドメイン1の不正検知実務と整合する形で、定期的な強制的な休暇取得またはローテーションが求められ、他者によるレビューで不正を表面化させます。

### 3. オンボーディングとオフボーディングの手順
審査確認・付与・即時剥奪:

1. **アクセス付与前の審査確認**: アクセス付与は、オンボーディングと並行して進めるのではなく、その役職の身元審査が完了したと確認されるまで進みません。
2. **最小権限による初期付与**: 初期アクセスは、テクニカルペーパーシリーズ #030 で定義した最小権限アプローチと整合する形でその役職の職務に必要な最小限に限定され、追加のアクセスは必要に応じて別途申請されます。
3. **離職時の即時剥奪**: すべてのシステムにわたるアクセスは、手動のオフボーディングチェックリストの完了時点ではなく、テクニカルペーパーシリーズ #030 で定義した自動セッション失効アプローチと整合する形で、離職の発効時点で剥奪されます。

### 4. 人事統制ガバナンスとアクセス監査
剥奪の迅速性とローテーション遵守のレビュー:

* **剥奪迅速性の指標**: 離職イベントと実際のアクセス剥奪との間の時間が測定・追跡され、プロセス上の是正が必要な遅延を特定します。
* **文書化された強制休暇の遵守状況**: 該当する役職における強制休暇・ローテーションポリシーの遵守状況は、非公式な上長の裁量に委ねるのではなく、追跡・報告されます。
* **孤立アカウントの継続的監査**: 有効なアカウントは、現在の雇用記録と定期的に突き合わされ、すでに在籍していない人物に属する孤立アカウントを特定します。

### 5. 結論
雇用ライフサイクルイベントに明示的に紐づけられていないアクセスは、それが採用時の審査漏れであれ離職時の失念されたアカウントであれ、付与された理由が消えた後も存続しがちです。

文書化されたライフサイクルイベントを軸に付与・剥奪を自動化することは、CISSPドメイン1に沿いつつ、誰かが対応を覚えていることに頼らずにその両方の隙間を塞ぎます。
