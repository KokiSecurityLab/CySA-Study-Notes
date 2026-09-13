# Koki's Technical Paper #032

## Quantum Defense — Protecting Memories from Future Threats, Post-Quantum Cryptography Migration, and Forward Secrecy Assurance

### Summary Digest
This paper defines a post-quantum cryptography migration framework, aligned with CISSP Domain 3 and NIST FIPS 203/204/205, replacing vulnerable asymmetric algorithms with lattice-based alternatives before quantum decryption matures.

Store-now-decrypt-later interception is addressed by migrating encrypted archives ahead of the threat, rather than waiting until a cryptographically relevant quantum computer exists.

---
### 1. Cryptographic Longevity Exposure
Structural Vulnerabilities of Legacy Asymmetric Encryption:

* **Shor's Algorithm Threat to Asymmetric Cryptography**: RSA and elliptic-curve algorithms currently in use are theoretically vulnerable to Shor's algorithm on a sufficiently capable quantum computer, a risk documented in NIST's post-quantum cryptography standardization effort.
* **Store-Now-Decrypt-Later (SNDL) Interception**: Adversaries can intercept and store currently encrypted traffic today with the intent of decrypting it once quantum computing capability becomes available, exposing historically sensitive data retroactively.
* **Undocumented Long-Lived Key Exposure**: Archives encrypted years ago with long-since-rotated keys may still be discoverable and stored by an adversary, meaning historical data retains exposure even after current key material is retired.

### 2. Lattice Cryptography and Standards Foundation
NIST-Standardized Algorithms and Forward Secrecy Principles:

* **NIST FIPS 203/204/205 Algorithm Selection**: Migration prioritizes the algorithms formally standardized by NIST in FIPS 203 (ML-KEM), FIPS 204 (ML-DSA), and FIPS 205 (SLH-DSA), rather than unstandardized or vendor-proprietary lattice constructions.
* **Forward Secrecy for Session Keys**: Session keys are derived independently for each session, consistent with forward-secrecy design principles, so that compromise of a later key does not expose previously recorded traffic.
* **Alignment with Baseline Boundary Controls**: Cryptographic migration is reconciled with the baseline boundary controls defined in Technical Paper #001, keeping algorithm changes consistent with the wider security architecture.

### 3. Hybrid Migration Sequence
Algorithm Inventory, Hybrid Deployment, and Legacy Retirement:

1. **Cryptographic Algorithm Inventory**: Systems and protocols using vulnerable asymmetric algorithms are inventoried to establish which components require migration and in what priority order.
2. **Hybrid Classical-PQC Deployment**: New connections use a hybrid scheme combining a classical algorithm with a NIST-standardized post-quantum algorithm, maintaining compatibility during the transition period.
3. **Scheduled Legacy Algorithm Retirement**: Once hybrid deployment is validated and interoperability is confirmed, purely classical asymmetric algorithms are retired from active use on a defined schedule.

### 4. Migration Governance and Archive Review
Historical Data Re-Encryption and Transition Tracking:

* **Re-Encryption of Sensitive Historical Archives**: Archived data still within its sensitivity or retention period is identified and re-encrypted using post-quantum algorithms, rather than left protected only by its original, now-vulnerable encryption.
* **Isolation of Legacy-Encrypted Cold Storage**: Data that cannot yet be re-encrypted is isolated in access-restricted cold storage, consistent with the classification approach defined in Technical Paper #027, reducing its exposure while migration is completed.
* **Continuous Migration Progress Auditing**: The proportion of systems and archives migrated to post-quantum algorithms is tracked and reviewed on a defined cadence against the overall migration plan.

### 5. Conclusion
Data encrypted today with a vulnerable algorithm can be exposed years from now, which is why migration must start before a capable quantum computer exists.

Adopting the NIST FIPS 203/204/205 algorithms in hybrid configuration, consistent with CISSP Domain 3, moves that timeline ahead of the threat rather than behind it.

---
# テクニカルペーパーシリーズ #032

## 量子防衛 — 未来の脅威から記憶を守る、ポスト量子暗号への移行、および前方秘匿性の保証

### サマリー・ダイジェスト
本論文は、CISSPドメイン3およびNIST FIPS 203/204/205に準拠したPQC移行フレームワークを定義し、量子解読能力が成熟する前に脆弱な非対称アルゴリズムを格子暗号ベースへ置き換えます。

ストア・ナウ、デクリプト・レイター（SNDL）による傍受には、暗号的に有意な量子コンピュータの登場を待つのではなく、暗号化アーカイブを脅威に先立って移行することで対処します。

---
### 1. 暗号寿命の露出リスク
レガシーな非対称暗号に伴う構造的脆弱性:

* **非対称暗号に対するショアのアルゴリズムの脅威**: 現在使用されているRSAや楕円曲線アルゴリズムは、十分な性能を持つ量子コンピュータ上でショアのアルゴリズムに対して理論上脆弱です。これはNISTのポスト量子暗号標準化の取り組みで文書化されているリスクです。
* **ストア・ナウ、デクリプト・レイター（SNDL）による傍受**: 攻撃者は、量子コンピューティング能力が利用可能になった時点で解読する意図を持って、現在暗号化されている通信を今のうちに傍受・蓄積し、過去の機微なデータを事後的に暴露する可能性があります。
* **未文書化された長期利用鍵の露出**: 何年も前にすでにローテーション済みの鍵で暗号化されたアーカイブでも、攻撃者によって発見・保存され得るため、現行の鍵素材が失効した後も過去のデータは露出リスクを保持し続けます。

### 2. 格子暗号と標準規格の基盤
NIST標準化アルゴリズムと前方秘匿性の原則:

* **NIST FIPS 203/204/205アルゴリズムの選定**: 移行では、標準化されていない、またはベンダー独自の格子構成ではなく、NISTがFIPS 203（ML-KEM）、FIPS 204（ML-DSA）、FIPS 205（SLH-DSA）として正式に標準化したアルゴリズムを優先します。
* **セッション鍵の前方秘匿性**: セッション鍵はセッションごとに独立して導出され、前方秘匿性の設計原則と整合するため、後の鍵が侵害されても以前に記録された通信が露出することはありません。
* **ベースライン境界統制との整合**: 暗号移行をテクニカルペーパーシリーズ #001で定義したベースライン境界統制と突き合わせ、アルゴリズムの変更をより広いセキュリティアーキテクチャと一貫させます。

### 3. ハイブリッド移行の手順
アルゴリズム棚卸し・ハイブリッド展開・レガシーの廃止:

1. **暗号アルゴリズムの棚卸し**: 脆弱な非対称アルゴリズムを使用しているシステムとプロトコルを棚卸しし、どのコンポーネントをどの優先順位で移行すべきかを明らかにします。
2. **クラシック・PQCハイブリッド展開**: 新規接続では、従来のアルゴリズムとNIST標準化済みのポスト量子アルゴリズムを組み合わせたハイブリッド方式を用い、移行期間中の互換性を維持します。
3. **レガシーアルゴリズムの計画的廃止**: ハイブリッド展開が検証され相互運用性が確認された後、純粋な従来型非対称アルゴリズムは定められたスケジュールで運用から廃止されます。

### 4. 移行ガバナンスとアーカイブレビュー
過去データの再暗号化と移行状況の追跡:

* **機微な過去アーカイブの再暗号化**: 機密性・保持期間内にあるアーカイブデータは特定され、脆弱になった元の暗号化のみに保護を委ねるのではなく、ポスト量子アルゴリズムで再暗号化されます。
* **レガシー暗号化されたコールドストレージの隔離**: まだ再暗号化できていないデータは、テクニカルペーパーシリーズ #027で定義した分類アプローチと整合する形でアクセス制限されたコールドストレージに隔離され、移行完了までの露出を低減します。
* **移行進捗の継続的監査**: ポスト量子アルゴリズムへ移行済みのシステムおよびアーカイブの割合は、全体の移行計画に照らして定められた周期で追跡・レビューされます。

### 5. 結論
今日弱いアルゴリズムで暗号化されたデータは、何年も先になっても露出し得るため、実用的な量子コンピュータが実在するようになる前に移行を開始する必要があります。

NIST FIPS 203/204/205のアルゴリズムをハイブリッド構成で採用することは、CISSPドメイン3に沿いつつ、この移行時期を脅威の後ではなく前へ動かします。
