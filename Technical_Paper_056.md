# Koki's Technical Paper #056

## Data Ownership Roles — Data Lifecycle Stage Controls, Data Owner and Custodian Responsibilities, and Privacy Role Alignment

### Summary Digest
This paper defines a data-ownership and lifecycle framework, aligned with CISSP Domain 2, assigning each asset an owner, custodian, and steward across create, store, use, and destroy stages.

Data-owner classification decisions determine the controls a custodian implements at each stage, consistent with the classification tiers defined in Technical Paper #027.

---
### 1. Undefined Ownership Risk
Structural Vulnerabilities of Unassigned Data Accountability:

* **No Accountable Owner for Classification Decisions**: Data without a documented, accountable owner has no one positioned to make or defend a classification decision, leaving handling requirements ambiguous.
* **Confused Owner and Custodian Responsibilities**: Conflating the business decision-maker (owner) with the technical implementer (custodian) obscures who is actually accountable when a classification is wrong or a control is missing.
* **Lifecycle Stages Without Assigned Controls**: Data protected only at creation, without corresponding controls for its later use, sharing, archival, and destruction stages, remains under-protected for most of its actual lifetime.

### 2. Ownership Role and Lifecycle Foundation
Owner, Custodian, and Steward Role Definitions:

* **Data Owner Accountability**: A designated business-side data owner makes and is accountable for classification decisions and handling requirements, consistent with CISSP Domain 2 role definitions.
* **Data Custodian Implementation**: A technical custodian implements the controls the data owner's classification requires, without independently making classification decisions.
* **Data Steward Quality Oversight**: A data steward maintains data quality and metadata accuracy, a distinct function from both ownership and custodianship, consistent with CISSP Domain 2 role separation.

### 3. Lifecycle Control Mapping Sequence
Stage Identification, Control Assignment, and Verification:

1. **Lifecycle Stage Identification**: Each data asset is mapped to its current lifecycle stage, create, store, use, share, archive, or destroy, as the basis for determining applicable controls.
2. **Stage-Specific Control Assignment**: Controls appropriate to each stage, such as encryption at rest for storage or the sanitization approach defined in Technical Paper #027 for destruction, are assigned and documented.
3. **Owner Sign-Off on Control Adequacy**: The data owner confirms that the assigned controls satisfy the classification requirement before the asset is considered adequately protected at that stage.

### 4. Ownership Governance and Lifecycle Auditing
Role Currency and Cross-Stage Control Review:

* **Documented Owner Assignment per Asset**: Every data asset has a documented, current owner assignment, reviewed when organizational roles change rather than left pointing to a departed employee.
* **Alignment with Privacy Controller and Processor Roles**: Where applicable privacy regulation distinguishes a controller from a processor, those legal roles are mapped to the corresponding data owner and custodian, keeping legal and technical accountability consistent.
* **Continuous Lifecycle Control Auditing**: Controls at each lifecycle stage are reviewed on a defined cadence to confirm they remain in place and appropriate as the asset moves between stages.

### 5. Conclusion
Data that is protected at creation but unaccounted for during sharing or archival is not actually protected across its lifecycle, only at one moment of it.

Assigning a documented owner and custodian to each lifecycle stage, per CISSP Domain 2, closes the gaps a single point-in-time classification decision leaves open.

---
# テクニカルペーパーシリーズ #056

## データ所有権の役割 — データライフサイクル段階別統制、データオーナーとカストディアンの責務、およびプライバシー上の役割との整合

### サマリー・ダイジェスト
本論文は、CISSPドメイン2に準拠したデータ所有権・ライフサイクルフレームワークを定義し、生成・保管・利用・破棄の各段階にわたって各資産にオーナー・カストディアン・スチュワードを割り当てます。

データオーナーによる分類判断が各段階でカストディアンが実装する統制を決定し、テクニカルペーパーシリーズ #027で定義した分類ティアと整合します。

---
### 1. 未定義の所有権リスク
未割り当てのデータ説明責任に伴う構造的脆弱性:

* **分類判断に対する説明責任者の不在**: 文書化された説明責任を負うオーナーを持たないデータには、分類判断を行い擁護する立場の者がおらず、取り扱い要件が曖昧なままになります。
* **オーナーとカストディアンの責務の混同**: 事業側の意思決定者（オーナー）と技術的な実装担当者（カストディアン）を混同すると、分類が誤っていたり統制が欠けていたりした場合に実際に誰が説明責任を負うのかが不明瞭になります。
* **統制が割り当てられていないライフサイクル段階**: 生成時にのみ保護され、その後の利用・共有・保管・破棄の各段階に対応する統制を持たないデータは、実際の存続期間の大半において保護が不十分なままとなります。

### 2. 所有権の役割とライフサイクルの基盤
オーナー・カストディアン・スチュワードの役割定義:

* **データオーナーの説明責任**: 指定された事業側のデータオーナーが、CISSPドメイン2の役割定義と整合する形で、分類判断と取り扱い要件について決定し説明責任を負います。
* **データカストディアンによる実装**: 技術的なカストディアンは、独立して分類判断を行うのではなく、データオーナーの分類が要求する統制を実装します。
* **データスチュワードによる品質監督**: データスチュワードはデータ品質とメタデータの正確性を維持する役割を担い、これはCISSPドメイン2の役割分離と整合する、所有権・カストディアンシップのいずれとも異なる機能です。

### 3. ライフサイクル統制マッピングの手順
段階特定・統制割り当て・検証:

1. **ライフサイクル段階の特定**: 各データ資産は、適用すべき統制を判断する基礎として、生成・保管・利用・共有・保管（アーカイブ）・破棄のうち現在の段階にマッピングされます。
2. **段階ごとの統制割り当て**: 保管時の保管時暗号化や、破棄時の テクニカルペーパーシリーズ #027で定義したサニタイジングアプローチなど、各段階に適した統制が割り当てられ文書化されます。
3. **統制の妥当性に対するオーナーの承認**: データオーナーは、その段階で資産が十分に保護されているとみなされる前に、割り当てられた統制が分類要件を満たしていることを確認します。

### 4. 所有権ガバナンスとライフサイクル監査
役割の鮮度と段階横断的な統制レビュー:

* **資産ごとの文書化されたオーナー割り当て**: すべてのデータ資産には文書化された現行のオーナー割り当てがあり、離職した従業員を指したまま放置されるのではなく、組織上の役割が変化した際にレビューされます。
* **プライバシー上のコントローラー・プロセッサ役割との整合**: 適用されるプライバシー規制がコントローラーとプロセッサを区別する場合、それらの法的役割は対応するデータオーナー・カストディアンにマッピングされ、法的な説明責任と技術的な説明責任を一貫させます。
* **ライフサイクル統制の継続的監査**: 各ライフサイクル段階の統制は、資産が段階間を移動する際にも引き続き適切に存在しているかを確認するため、定められた周期でレビューされます。

### 5. 結論
生成時には保護されていても共有時や保管時に管理が行き届いていないデータは、ライフサイクル全体を通じて保護されているのではなく、その一瞬だけ保護されているに過ぎません。

各ライフサイクル段階に文書化されたオーナーとカストディアンを割り当てることは、CISSPドメイン2に沿いつつ、一時点だけの分類判断が残してしまう隙間を塞ぎます。
