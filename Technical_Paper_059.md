# Koki's Technical Paper #059

## Data State Encryption — At-Rest, In-Transit, and In-Use Protection, Confidential Computing, and Key Management Alignment

### Summary Digest
This paper defines an encryption framework for all three data states, aligned with CISSP Domain 2, applying distinct mechanisms for data at rest, in transit, and in use.

Confidential computing using hardware-based trusted execution environments protects data in use, a state that at-rest and in-transit encryption alone do not cover.

---
### 1. Single-State Encryption Gap Risk
Structural Vulnerabilities of Incomplete State Coverage:

* **Data Exposed During Processing**: Data encrypted at rest and in transit is typically decrypted in plaintext memory during active processing, leaving it exposed to anyone with sufficient access to that memory space.
* **Assumed Coverage From Partial Encryption**: Treating at-rest and in-transit encryption as complete protection creates a false sense of coverage that overlooks the in-use state entirely.
* **Inconsistent Encryption Across Storage Locations**: Full-disk encryption on primary storage does not automatically extend to backups, temporary files, or cache locations, leaving inconsistent protection across copies of the same data.

### 2. Three-State Protection Foundation
State-Specific Mechanisms and Confidential Computing Principles:

* **At-Rest Protection**: Data stored on disk is protected using full-disk or database-level transparent data encryption (TDE), with keys managed consistent with the key-management approach defined in Technical Paper #049.
* **In-Transit Protection**: Data moving across a network is protected using TLS, consistent with the hybrid post-quantum approach defined in Technical Paper #043.
* **In-Use Protection via Confidential Computing**: Data actively being processed is protected within a hardware-based trusted execution environment (TEE), keeping it encrypted in memory even from a compromised operating system or hypervisor.

### 3. State Transition Protection Sequence
Storage, Transmission, and Processing Coverage Verification:

1. **At-Rest Coverage Verification**: All storage locations, including backups and temporary files, are verified to have encryption applied consistently, not only primary storage.
2. **In-Transit Coverage Verification**: Network paths are verified to use current TLS configuration for all data transmission, including internal service-to-service traffic.
3. **In-Use Coverage for Sensitive Processing**: Processing of the most sensitive data categories, as classified under Technical Paper #027, is routed through a trusted execution environment rather than standard unprotected memory.

### 4. Encryption Coverage Governance and Gap Auditing
State Coverage Mapping and Residual Gap Review:

* **Documented State Coverage Map**: Each data classification tier has a documented statement of which protection applies at each of the three states, rather than an assumption that encryption is uniformly applied.
* **Residual Gap Acceptance or Remediation**: Where full three-state coverage is not yet feasible for a given system, the residual gap is documented and either accepted with justification or scheduled for remediation.
* **Continuous Encryption Coverage Auditing**: Coverage across all three states is reviewed on a defined cadence to identify newly introduced storage locations or processing paths that lack appropriate protection.

### 5. Conclusion
Encrypting data at rest and in transit protects it everywhere except the moment it is actively being used, exactly when most processing exposure occurs.

Extending protection into that state with confidential computing, consistent with CISSP Domain 2, closes the gap at-rest and in-transit encryption were never designed to cover.

---
# テクニカルペーパーシリーズ #059

## データ状態別暗号化 — 保管時・転送時・使用時の保護、機密計算、および鍵管理との整合

### サマリー・ダイジェスト
本論文は、CISSPドメイン2に準拠したデータの3つの状態すべてを対象とする暗号化フレームワークを定義し、保管時・転送時・使用時それぞれに異なる機構を適用します。

ハードウェアに基づく信頼実行環境（TEE）を用いた機密計算は使用時のデータを保護します。これは保管時・転送時の暗号化だけではカバーできない状態です。

---
### 1. 単一状態暗号化の隙間リスク
不完全な状態カバレッジに伴う構造的脆弱性:

* **処理中に露出するデータ**: 保管時・転送時に暗号化されたデータも、能動的な処理中には通常プレーンテキストのメモリへ復号され、そのメモリ空間に十分なアクセス権を持つ誰にでも露出したままとなります。
* **部分的な暗号化から生じる想定上のカバレッジ**: 保管時・転送時の暗号化を完全な保護として扱うと、使用時の状態を完全に見落とした誤った安心感が生まれます。
* **保管場所間で一貫しない暗号化**: 主要ストレージ上のフルディスク暗号化は、バックアップや一時ファイル、キャッシュ領域へ自動的に拡張されるわけではなく、同一データのコピー間で保護に一貫性がなくなります。

### 2. 3状態保護の基盤
状態別の機構と機密計算の原則:

* **保管時の保護**: ディスクに保存されたデータは、フルディスクまたはデータベースレベルの透過的データ暗号化（TDE）で保護され、鍵はTechnical Paper #049で定義した鍵管理アプローチと整合する形で管理されます。
* **転送時の保護**: ネットワークを移動するデータは、テクニカルペーパーシリーズ #043で定義したハイブリッド耐量子アプローチと整合するTLSで保護されます。
* **機密計算による使用時の保護**: 能動的に処理されているデータは、ハードウェアに基づく信頼実行環境（TEE）内で保護され、侵害されたオペレーティングシステムやハイパーバイザーからも、メモリ内で暗号化された状態が保たれます。

### 3. 状態遷移保護の手順
保管・伝送・処理カバレッジの検証:

1. **保管時カバレッジの検証**: バックアップや一時ファイルを含むすべての保管場所について、主要ストレージのみでなく暗号化が一貫して適用されていることが検証されます。
2. **転送時カバレッジの検証**: 内部のサービス間トラフィックを含むすべてのデータ伝送について、ネットワーク経路が最新のTLS構成を使用していることが検証されます。
3. **機微な処理に対する使用時カバレッジ**: テクニカルペーパーシリーズ #027 で分類された最も機微なデータカテゴリの処理は、標準的な無防備なメモリではなく信頼実行環境を経由させられます。

### 4. 暗号化カバレッジガバナンスと隙間監査
状態カバレッジマッピングと残存する隙間のレビュー:

* **文書化された状態カバレッジマップ**: 各データ分類ティアには、暗号化が一律に適用されているという想定ではなく、3つの状態それぞれにどの保護が適用されるかを示す文書化された記述があります。
* **残存する隙間の許容または是正**: 特定のシステムで3状態すべての完全なカバレッジがまだ実現できない場合、残存する隙間は文書化され、正当な理由とともに許容されるか、是正計画が立てられます。
* **暗号化カバレッジの継続的監査**: 3状態すべてのカバレッジは、適切な保護を欠く新たに導入された保管場所や処理経路を特定するため、定められた周期でレビューされます。

### 5. 結論
保管時と転送時のデータを暗号化しても、それが最も能動的に使用されている瞬間だけは保護されず、まさにその瞬間こそ処理に関連する露出のほとんどが実際に発生する場面です。

機密計算によってその状態にまで保護を拡張することは、CISSPドメイン2に沿いつつ、保管時・転送時の暗号化がそもそもカバーするよう設計されていなかった隙間を塞ぎます。
