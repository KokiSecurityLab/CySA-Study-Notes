# Koki's Technical Paper #026

## The AI Sanctuary — Data Provenance Integrity, Supply Chain Risk Management, and Data Poisoning Mitigation Frameworks

### Summary Digest
This paper defines an ML supply-chain integrity framework, aligned with CISSP Domain 8, NIST SP 800-218, and the SLSA provenance framework, verifying training-data origin before ingestion.

Cryptographic hashing and source authentication, consistent with the baseline approach in Technical Paper #001, reject unverified or altered data before it reaches the pipeline.

---
### 1. Training-Data Ingestion Risk
Structural Vulnerabilities of Unverified Pipeline Inputs:

* **Untrusted External Data Sources**: Machine-learning pipelines that ingest external datasets without verifying their origin are exposed to manipulated or fabricated training data introduced anywhere upstream in the supply chain.
* **Covert Data Poisoning**: Adversaries can inject a small number of manipulated training examples designed to create a hidden backdoor in the resulting model, a technique documented in MITRE ATLAS.
* **Undocumented Dependency Provenance**: Training pipelines that rely on third-party libraries, pretrained weights, or datasets without a recorded bill of materials have no reliable way to trace which components a given model build actually depends on.

### 2. Provenance and Attestation Foundation
Source Authentication and Build Provenance Standards:

* **Cryptographic Source Verification**: Data ingestion is restricted to authenticated repositories, and each accepted dataset is mapped to a recorded, verifiable point of origin.
* **File-Integrity Hashing at Ingestion**: Incoming data blocks are hashed and compared against expected values before integration, consistent with the file-integrity approach defined in Technical Paper
#001.
* **SLSA-Aligned Build Provenance**: Model-build artifacts are accompanied by provenance attestations consistent with the Supply-chain Levels for Software Artifacts (SLSA) framework, documenting how and from what inputs each build was produced.

### 3. Ingestion Filtering and Attestation Sequence
Verified-Source Selection, Scanning, and Registry Sync:

1. **Verified-Source Data Selection**: Training inputs are drawn only from datasets that pass source-verification checks defined in Technical Paper #011, rather than from unauthenticated external feeds.
2. **Backdoor Pattern Scanning**: Trained models are evaluated against known backdoor-trigger patterns before deployment, flagging behavior consistent with documented data-poisoning outcomes for further review.
3. **Software Bill of Materials (SBOM) Synchronization**: Dependency and dataset provenance records are synchronized into a maintained SBOM, giving downstream teams a current record of what each model build actually contains.

### 4. Supply-Chain Auditing and Attestation Review
Dependency Transparency and Ongoing Verification:

* **Provenance as a Standing Requirement**: Data-integrity verification is treated as a mandatory gate in the build pipeline rather than an optional check, consistent with NIST SP 800-218 secure-development practices.
* **Isolation of Unverified Dependencies**: External libraries and datasets that have not yet passed verification are kept isolated from the production training pipeline until review is complete.
* **Continuous SBOM and Attestation Auditing**: The software bill of materials and build attestations are reviewed on a defined cadence to confirm they still accurately reflect the dependencies in active use.

### 5. Conclusion
A model is only as trustworthy as the data and dependencies used to build it, most of which are invisible without a maintained provenance record.

Aligning that record with SLSA and NIST SP 800-218, consistent with CISSP Domain 8, turns supply-chain risk into something that can actually be checked.

---
# テクニカルペーパーシリーズ #026

## AIサンクチュアリ — データプロベナンスの完全性､サプライチェーンリスク管理､およびデータポイズニング緩和フレームワーク

### サマリー・ダイジェスト
本論文は､CISSPドメイン8､NIST SP 800-218､およびSLSA出自証明の枠組みに準拠した機械学習サプライチェーンの完全性フレームワークを定義し､学習データの発生元を取り込み前に検証します｡

暗号学的ハッシュとソース認証は､　テクニカルペーパーシリーズ #001のベースラインの考え方と整合しつつ､未検証または改ざんされたデータがパイプラインに到達する前に拒否します｡

---
### 1. 学習データ取り込みリスク
未検証のパイプライン入力に伴う構造的脆弱性:

* **未信頼な外部データソース**: 発生元を検証せずに外部データセットを取り込む機械学習パイプラインは､サプライチェーンの上流のどこかで混入した改ざん・捏造された学習データにさらされます｡
* **隠密なデータポイズニング**: 攻撃者は､結果として得られるモデルに隠れたバックドアを作り出すよう設計された少数の改ざん済み学習事例を注入することがあります｡これはMITRE ATLASに文書化されている手法です｡
* **未文書化された依存関係の出自**: 記録された部品構成表を持たずにサードパーティ製ライブラリ､事前学習済みの重み､データセットに依存する学習パイプラインには､あるモデルビルドが実際に何に依存しているかを追跡する信頼できる手段がありません｡

### 2. 出自証明の基盤
ソース認証とビルド出自証明の標準:

* **暗号学的なソース検証**: データの取り込みは認証済みのリポジトリに限定され､受け入れられた各データセットは記録された検証可能な発生元に対応付けられます｡
* **取り込み時のファイル整合性ハッシュ**: 着信データブロックはハッシュ化され､統合される前に想定値と照合されます｡これは　テクニカルペーパーシリーズ　#001で定義したファイル整合性のアプローチと整合します｡
* **SLSAに準拠したビルド出自証明**: モデルビルドの成果物には､Supply-chain Levels for Software Artifacts SLSAフレームワークに準拠した出自証明が付随し､各ビルドがどの入力からどのように生成されたかを文書化します｡

### 3. 取り込みフィルタリングと出自証明の手順
検証済みソースの選定・スキャン・レジストリ同期:

1. **検証済みソースからのデータ選定**: 学習入力は､未認証の外部フィードからではなく､テクニカルペーパーシリーズ #011で定義したソース検証チェックを通過したデータセットのみから選定されます｡
2. **バックドアパターンのスキャン**: 学習済みモデルは､デプロイ前に既知のバックドアトリガーパターンと照合され､文書化されたデータポイズニングの結果と整合する挙動を追加レビュー対象としてフラグ付けします｡
3. **ソフトウェア部品構成表SBOMの同期**: 依存関係とデータセットの出自記録は維持管理されたSBOMへ同期され､下流のチームに各モデルビルドが実際に含む内容の最新の記録を提供します｡

### 4. サプライチェーン監査と出自証明のレビュー
依存関係の透明性と継続的検証:

* **標準要件としての出自証明**: データ完全性検証は､任意のチェックではなくビルドパイプライン上の必須ゲートとして扱われ､NIST SP 800-218のセキュア開発実務と整合します｡
* **未検証の依存関係の隔離**: まだ検証を通過していない外部ライブラリやデータセットは､レビューが完了するまで本番の学習パイプラインから隔離された状態に保たれます｡
* **SBOMと出自証明の継続的監査**: ソフトウェア部品構成表とビルド出自証明は定められた周期でレビューされ､現在使用中の依存関係を引き続き正確に反映しているかを確認します｡

### 5. 結論
モデルの信頼性は､その構築に使われたデータや依存関係の信頼性を超えるものにはなり得ませんが､その多くは維持管理された出自記録なしには見えないままです｡

その記録をSLSAおよびNIST SP 800-218と整合させることは､CISSPドメイン8に沿いつつ､サプライチェーンリスクを実際に確認可能なものへと変えます｡
