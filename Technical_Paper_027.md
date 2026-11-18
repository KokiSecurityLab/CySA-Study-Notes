# Koki's Technical Paper #027

## Asset Classification — Confidentiality Tiers for System Records, Secure Sanitization, and Air-Gapped Controls

### Summary Digest
This paper defines a data-classification framework for system records, aligned with CISSP Domain 2, assigning each record to a confidentiality tier by sensitivity and operational value.

Top-tier records are held in air-gapped storage, lower tiers use cryptographic access controls, and obsolete records are destroyed per NIST SP 800-88 Rev. 2 sanitization guidance.

---
### 1. Undifferentiated Storage Risk
Structural Vulnerabilities of Unclassified Data Repositories:

* **Mixed-Sensitivity Storage**: Repositories that store highly sensitive records alongside routine or public logs without a classification scheme make it easier for an attacker who gains any access to locate and exfiltrate the most valuable data.
* **Undefined Retention and Destruction Criteria**: Without documented criteria for when a record should be classified, retained, or destroyed, obsolete or unnecessary sensitive data can persist indefinitely, increasing the impact of any future breach.
* **Inconsistent Access Control Across Record Types**: Applying the same access policy to records of differing sensitivity either over-restricts routine data or under-protects the most sensitive records. The gap widens when AI assistants or agents are granted broad read access to a repository, since an agent can surface any record its permissions reach, regardless of how sensitive that record is.

### 2. Tiered Classification Foundation
Confidentiality Tiers and Physical Isolation Principles:

* **Top-Tier Isolation via Air-Gapping**: The most sensitive records, such as core configuration baselines and historical security telemetry, are stored on physically air-gapped systems disconnected from external networks, consistent with CISSP Domain 2 asset-handling guidance and with the baseline-protection requirement in Technical Paper #001.
* **Mid-Tier Cryptographic Access Control**: Records of moderate sensitivity, such as internal operational logs, are encrypted and restricted to authenticated personnel rather than isolated physically.
* **Public-Tier Designation for Non-Sensitive Records**: Records intended for external use, such as published documentation, are explicitly designated as public and excluded from the higher classification tiers.

### 3. Classification and Sanitization Sequence
Ingestion, Verification, and Disposal Stages:

* **Classification at Ingestion**: Each new record is assigned a confidentiality tier at the point of creation, based on defined criteria rather than left unclassified by default.
* **Periodic Integrity Verification**: Stored records in each tier are periodically checked against their original hash values, consistent with the file-integrity approach defined in Technical Paper #001, to detect unauthorized alteration.
* **NIST SP 800-88 Rev. 2-Aligned Sanitization**: Records identified as obsolete or no longer needed are destroyed using the Clear, Purge, or Destroy method appropriate to the media and tier, consistent with NIST SP 800-88 Rev. 2, rather than simply deleted at the file-system level.

### 4. Classification Governance and Boundary Review
Access Criteria and Retention Policy Oversight:

* **Documented Classification Criteria**: The criteria used to assign a record to a given confidentiality tier are documented and applied consistently, rather than left to individual judgment at the time of storage.
* **Boundary Alignment with Perimeter Controls**: Classification tiers are reconciled with the baseline boundary controls defined in Technical Paper #001, so that access-tier decisions and network-boundary decisions remain consistent.
* **Continuous Classification and Retention Auditing**: Stored records are periodically reviewed against their assigned classification and retention schedule, identifying records that should be reclassified or destroyed.

### 5. Conclusion
A classification scheme only reduces risk if every record is actually assigned a tier, not just the ones someone remembers are sensitive, especially once AI agents can read entire repositories.

Pairing air-gapped storage for the top tier with NIST SP 800-88 Rev. 2 sanitization for retired records, consistent with CISSP Domain 2, closes the gap indefinite, unclassified retention leaves open.

---
# テクニカルペーパーシリーズ #027

## 資産分類 — システム記録の機密性ティア、安全なサニタイジング、およびエアギャップ制御

### サマリー・ダイジェスト
本論文は、CISSPドメイン2に準拠し、システム記録を機密度と運用上の価値に基づいて機密性ティアへ割り当てるデータ分類フレームワークを定義します。

最上位ティアの記録はエアギャップ環境で保管され、下位ティアは暗号学的アクセス制御を用い、不要となった記録はNIST SP 800-88 Rev. 2のサニタイジング指針に沿って破棄されます。

---
### 1. 未分類ストレージのリスク
未分類データリポジトリに伴う構造的脆弱性:

* **機密度混在型のストレージ**: 分類スキームを持たず、機密度の高い記録を日常的・公開的なログと同じ場所に保管するリポジトリは、いずれかの経路でアクセスを得た攻撃者が最も価値のあるデータを見つけ出し持ち出すことを容易にします。
* **未定義の保持・破棄基準**: ある記録をいつ分類・保持・破棄すべきかという基準が文書化されていない場合、不要または陳腐化した機密データが無期限に残存し、将来の侵害の影響を拡大させます。
* **記録種別間で一貫しないアクセス制御**: 機密度の異なる記録に同一のアクセスポリシーを適用すると、日常的なデータを過度に制限するか、最も機密性の高い記録の保護が不十分になるかのいずれかに陥ります。AIアシスタントやエージェントにリポジトリへの広範な読み取り権限が与えられると、この隙間はさらに広がります。エージェントは、記録の機密度にかかわらず、自らの権限が届くあらゆる記録を表に出し得るためです。

### 2. 階層的分類の基盤
機密性ティアと物理隔離の原則:

* **エアギャップによる最上位ティアの隔離**: コアとなる構成ベースラインや過去のセキュリティテレメトリなど最も機密性の高い記録は、外部ネットワークから物理的に切り離されたエアギャップシステムに保管されます。これは、CISSPドメイン2の資産取り扱い指針、およびテクニカルペーパーシリーズ #001 のベースライン保護の要件と整合します。
* **中間ティアの暗号学的アクセス制御**: 内部の運用ログなど中程度の機密性を持つ記録は、物理的に隔離するのではなく暗号化され、認証済みの担当者のみに限定されます。
* **非機密記録の公開ティア指定**: 公開済みの文書など外部利用を意図した記録は、明示的に公開扱いとして指定され、上位の機密性ティアから除外されます。

### 3. 分類とサニタイジングの手順
取り込み・検証・廃棄の各段階:

* **取り込み時の分類**: 新しい記録はそれぞれ、既定で未分類のまま放置されるのではなく、定義済みの基準に基づいて生成時点で機密性ティアを割り当てられます。
* **定期的な整合性検証**: 各ティアに保管された記録は、テクニカルペーパーシリーズ #001 で定義したファイル整合性のアプローチと整合する形で元のハッシュ値と定期的に照合され、不正な改ざんを検出します。
* **NIST SP 800-88 Rev. 2に準拠したサニタイジング**: 陳腐化または不要と判定された記録は、ファイルシステム上の単純な削除ではなく、NIST SP 800-88 Rev. 2に沿って、媒体とティアに応じたClear（消去）、Purge（除去）、Destroy（破壊）のいずれかの方法で破棄されます。

### 4. 分類ガバナンスと境界レビュー
アクセス基準と保持ポリシーの監督:

* **文書化された分類基準**: ある記録を特定の機密性ティアに割り当てる際の基準は文書化され、保管時点の個人の判断に委ねるのではなく一貫して適用されます。
* **境界統制との整合**: 分類ティアはテクニカルペーパーシリーズ #001 で定義したベースライン境界統制と突き合わされ、アクセスティアの判断とネットワーク境界の判断が一貫した状態に保たれます。
* **分類・保持状況の継続的監査**: 保管された記録は、割り当てられた分類および保持スケジュールに照らして定期的にレビューされ、再分類または破棄が必要な記録を特定します。

### 5. 結論
分類スキームがリスクを低減するのは、管理者がたまたま機密だと覚えている記録だけでなく、すべての記録に実際にティアが割り当てられている場合に限られ、AIエージェントがリポジトリ全体を読めるようになった今、その重要性はさらに高まっています。

最上位ティアのエアギャップ保管と、廃棄記録に対するNIST SP 800-88 Rev. 2のサニタイジングを組み合わせることは、CISSPドメイン2に沿いつつ、無期限で未分類のまま保持される隙間を塞ぎます。
