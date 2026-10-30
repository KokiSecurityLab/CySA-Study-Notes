# Koki's Technical Paper #058

## Asset Inventory Management — Automated Discovery and CMDB Reconciliation, CIS Controls Alignment, and Shadow IT Detection

### Summary Digest
This paper defines an automated asset-inventory framework, aligned with CISSP Domain 2 and CIS Controls 1-2, continuously discovering hardware and software assets rather than relying on a manual list.

Discovered assets are reconciled against the configuration management database (CMDB) to surface shadow IT before it becomes an unmanaged security gap.

---
### 1. Undiscovered Asset Risk
Structural Vulnerabilities of Manually Maintained Inventories:

* **Stale Manual Inventory Records**: An inventory updated only through manual entry falls out of date as soon as hardware is added or removed without someone remembering to record the change.
* **Undetected Shadow IT**: Devices, cloud accounts, or software installed without going through a formal procurement or approval process remain invisible to security controls that rely on the official inventory alone.
* **Unpatched Assets Absent From Scanning Scope**: Vulnerability scanning and patch management defined in Technical Paper #004 can only cover assets the scanning system knows exist, leaving undiscovered assets permanently outside that coverage.

### 2. Automated Discovery and CMDB Foundation
Continuous Discovery and Reconciliation Principles:

* **Continuous Automated Discovery**: Network scanning, endpoint agents, and cloud API queries continuously identify active hardware and software assets, consistent with CIS Control 1 (hardware) and CIS Control 2 (software) practices.
* **CMDB as the System of Record**: Discovered assets are reconciled against a configuration management database (CMDB) that serves as the authoritative record, rather than treating spreadsheets or informal lists as authoritative.
* **Alignment with Vulnerability Scanning Scope**: The asset inventory feeds the scanning scope defined in Technical Paper #004, ensuring newly discovered assets are automatically included in vulnerability scanning rather than added manually after the fact.

### 3. Discovery and Reconciliation Sequence
Scanning, Matching, and Discrepancy Flagging:

1. **Automated Asset Discovery Scan**: Scheduled and continuous scans identify active devices and installed software across the environment.
2. **CMDB Matching**: Discovered assets are matched against existing CMDB entries, confirming known assets remain accurately recorded.
3. **Discrepancy Flagging and Investigation**: Assets discovered but not present in the CMDB are flagged as potential shadow IT and routed for investigation and formal onboarding or removal.

### 4. Inventory Governance and Discrepancy Review
CMDB Accuracy and Shadow IT Resolution Review:

* **Documented Asset Onboarding Process**: New assets discovered through scanning follow a documented onboarding process before being marked as approved in the CMDB, rather than being added without review.
* **Shadow IT Resolution Tracking**: Identified shadow IT instances are tracked to resolution, either formal approval and onboarding or removal, rather than being flagged and left unresolved.
* **Continuous CMDB Accuracy Auditing**: CMDB accuracy is periodically verified against live discovery scan results to identify drift between the recorded inventory and actual environment state.

### 5. Conclusion
An asset that security tooling does not know exists cannot be scanned, patched, or classified, no matter how good downstream controls otherwise are.

Continuous automated discovery reconciled against a CMDB, consistent with CIS Controls 1-2 and CISSP Domain 2, closes that gap before it undermines everything built on it.

---
# テクニカルペーパーシリーズ #058

## 資産棚卸し管理 — 自動検出とCMDB照合、CISコントロールとの整合、およびシャドーIT検知

### サマリー・ダイジェスト
本論文は、CISSPドメイン2およびCISコントロール1・2に準拠した自動化資産棚卸しフレームワークを定義し、手動維持の一覧に頼るのではなく、ハードウェアとソフトウェアの資産を継続的に検出します。

検出された資産は構成管理データベース（CMDB）と突き合わされ、シャドーITが未管理のセキュリティ上の隙間となる前にそれを浮かび上がらせます。

---
### 1. 未発見資産のリスク
手動維持型棚卸しに伴う構造的脆弱性:

* **陳腐化した手動棚卸し記録**: 手動入力でのみ更新される棚卸しは、ハードウェアが追加・撤去された際に誰かが変更の記録を覚えていない限り、すぐに古くなってしまいます。
* **検知されないシャドーIT**: 正式な調達・承認プロセスを経ずに導入されたデバイス、クラウドアカウント、ソフトウェアは、公式な棚卸しのみに依存するセキュリティ統制からは見えないままとなります。
* **スキャン対象範囲から漏れる未パッチ資産**: テクニカルペーパーシリーズ #004 で定義した脆弱性スキャンとパッチ管理は、スキャンシステムが存在を認識している資産しかカバーできず、未発見の資産は恒久的にその対象範囲外に置かれます。

### 2. 自動検出とCMDBの基盤
継続的検出と照合の原則:

* **継続的な自動検出**: ネットワークスキャン、エンドポイントエージェント、クラウドAPIへの問い合わせにより、CISコントロール1（ハードウェア）およびCISコントロール2（ソフトウェア）の実務と整合する形で、稼働中のハードウェア・ソフトウェア資産を継続的に特定します。
* **記録の正本としてのCMDB**: 検出された資産は、スプレッドシートや非公式な一覧を正本として扱うのではなく、正本として機能する構成管理データベース（CMDB）と照合されます。
* **脆弱性スキャン対象範囲との整合**: 資産棚卸しは テクニカルペーパーシリーズ #004 で定義したスキャン対象範囲へ供給され、新たに発見された資産が事後に手動で追加されるのではなく、脆弱性スキャンへ自動的に含まれるようにします。

### 3. 検出と照合の手順
スキャン・照合・不一致のフラグ付け:

1. **自動資産検出スキャン**: 定期的かつ継続的なスキャンにより、環境全体で稼働中のデバイスとインストール済みソフトウェアが特定されます。
2. **CMDB照合**: 検出された資産は既存のCMDBエントリと照合され、既知の資産が正確に記録され続けていることを確認します。
3. **不一致のフラグ付けと調査**: 検出されたがCMDBに存在しない資産は、潜在的なシャドーITとしてフラグ付けされ、調査および正式なオンボーディングまたは撤去へ回されます。

### 4. 棚卸しガバナンスと不一致レビュー
CMDBの正確性とシャドーIT解消のレビュー:

* **文書化された資産オンボーディングプロセス**: スキャンで発見された新規資産は、レビューなしに追加されるのではなく、CMDB上で承認済みとマークされる前に文書化されたオンボーディングプロセスを経ます。
* **シャドーIT解消の追跡**: 特定されたシャドーITの事例は、フラグ付けされたまま未解決となるのではなく、正式な承認・オンボーディングまたは撤去のいずれかの解消まで追跡されます。
* **CMDB正確性の継続的監査**: CMDBの正確性は、記録された棚卸しと実際の環境状態との間のドリフトを特定するため、実際の検出スキャン結果と定期的に照合されます。

### 5. 結論
セキュリティツールが存在を認識していない資産は、下流の統制がどれほど優れていても、スキャン・パッチ適用・分類のいずれもできません。

CMDBと突き合わせた継続的な自動検出は、CISコントロール1・2およびCISSPドメイン2に沿いつつ、その出発点の隙間が上に積み上げたすべてを損なう前に塞ぎます。
