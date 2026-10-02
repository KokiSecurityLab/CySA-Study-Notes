# Koki's Technical Paper #046

## Orbital Link Hardening — Satellite Telemetry Encryption, CCSDS Space Data Link Security, and Anti-Jamming Frequency Hopping

### Summary Digest
This paper defines a satellite telemetry security architecture, aligned with CISSP Domain 4 and the CCSDS Space Data Link Security Protocol, encrypting and authenticating command traffic between ground stations and orbital assets.

Frequency-hopping spread-spectrum techniques reduce the effectiveness of radio-frequency jamming, complementing cryptographic protection rather than replacing it.

---
### 1. Unencrypted Uplink Exposure
Structural Vulnerabilities of Legacy Satellite Communication Links:

* **Unencrypted Legacy Telemetry Channels**: Satellite systems still operating on older, unencrypted telemetry protocols remain exposed to interception and command spoofing, a documented weakness in aging space communication infrastructure.
* **Command Injection via Ground-Segment Compromise**: An attacker who compromises a ground station rather than the satellite itself can inject unauthorized commands through what appears to be a legitimate uplink.
* **Jamming of Command and Control Frequencies**: A fixed-frequency uplink without anti-jamming measures can be disrupted by radio-frequency interference targeting that specific frequency, denying legitimate command access.

### 2. CCSDS Security Protocol Foundation
Space Data Link Encryption and Anti-Jamming Principles:

* **CCSDS Space Data Link Security Protocol**: Uplink and downlink traffic is encrypted and authenticated consistent with the CCSDS (Consultative Committee for Space Data Systems) Space Data Link Security Protocol, an internationally recognized standard for space communications.
* **Frequency-Hopping Spread Spectrum**: Command and telemetry links use frequency-hopping spread-spectrum transmission, making sustained jamming of a single frequency substantially less effective against the overall link.
* **Alignment with Ground-Segment Access Controls**: Ground-station access to command uplink capability is governed by the continuous authorization approach defined in Technical Paper #030, rather than relying on link encryption alone.

### 3. Command Authentication and Anomaly Sequence
Uplink Verification, Telemetry Monitoring, and Isolation:

1. **Cryptographic Command Authentication**: Every uplink command is authenticated against the CCSDS security protocol keys before execution, rejecting commands that fail authentication regardless of apparent source.
2. **Continuous Downlink Telemetry Monitoring**: Telemetry integrity is monitored in real time, consistent with the integrity-verification approach defined in Technical Paper #001, flagging inconsistencies for review.
3. **Isolation of a Compromised Ground Station**: A ground station exhibiting anomalous command patterns is isolated from uplink capability pending investigation, preventing it from issuing further commands to the satellite.

### 4. Space-Link Governance and Key Management
Key Rotation Scheduling and Link Integrity Review:

* **Scheduled Cryptographic Key Rotation**: Command-authentication keys are rotated on a defined schedule, limiting the exposure window if a key is ever compromised without immediate detection.
* **Separation of Ground-Segment Roles**: Personnel authorized to issue commands are separated from those managing key material, consistent with segregation-of-duties principles in CISSP Domain 4.
* **Continuous Link Integrity Auditing**: Uplink and downlink integrity metrics are reviewed on a defined cadence to identify degrading link quality or authentication failures that may indicate an emerging threat.

### 5. Conclusion
A satellite link is only as secure as its weakest ground-segment control, since an attacker rarely needs to compromise the spacecraft itself to inject unauthorized commands.

Applying CCSDS-standardized encryption and authentication, consistent with CISSP Domain 4, addresses that ground-to-orbit link directly rather than assuming distance alone provides protection.

---
# テクニカルペーパーシリーズ #046

## 軌道リンク強化 — 衛星テレメトリ暗号化、CCSDS宇宙データリンクセキュリティ、および周波数ホッピングによる妨害対策

### サマリー・ダイジェスト
本論文は、CISSPドメイン4およびCCSDS宇宙データリンクセキュリティプロトコルに準拠した衛星テレメトリセキュリティアーキテクチャを定義し、地上局と軌道上資産の間のコマンドトラフィックを暗号化・認証します。

周波数ホッピング・スペクトラム拡散技術は、暗号による保護を置き換えるのではなく補完する形で、無線周波数妨害の効果を低減します。

---
### 1. 未暗号化アップリンクへの露出
レガシーな衛星通信リンクに伴う構造的脆弱性:

* **未暗号化のレガシーテレメトリチャネル**: 古い未暗号化のテレメトリプロトコルを依然として使用している衛星システムは、傍受やコマンドのなりすましにさらされたままです。これは老朽化した宇宙通信インフラのよく文書化された弱点です。
* **地上セグメントの侵害を通じたコマンド注入**: 衛星本体ではなく地上局を侵害した攻撃者は、正規のアップリンクに見せかけて未認可のコマンドを注入できます。
* **指令・制御周波数への妨害**: 対妨害策を伴わない固定周波数のアップリンクは、その特定周波数を狙った無線周波数妨害によって混乱させられ、正規のコマンドアクセスを妨げられる可能性があります。

### 2. CCSDSセキュリティプロトコルの基盤
宇宙データリンクの暗号化と対妨害の原則:

* **CCSDS宇宙データリンクセキュリティプロトコル**: アップリンクおよびダウンリンクのトラフィックは、宇宙通信に関する国際的に認知された標準である**CCSDS（宇宙データシステム諮問委員会）宇宙データリンクセキュリティプロトコル**と整合する形で暗号化・認証されます。
* **周波数ホッピング・スペクトラム拡散**: コマンドおよびテレメトリリンクは周波数ホッピング・スペクトラム拡散伝送を用いており、単一周波数への持続的な妨害をリンク全体に対して大幅に効果の低いものにします。
* **地上セグメントアクセス制御との整合**: 地上局によるコマンドアップリンク能力へのアクセスは、リンク暗号化のみに依存するのではなく、テクニカルペーパーシリーズ #030 で定義した継続的認可アプローチによって統治されます。

### 3. コマンド認証と異常検知の手順
アップリンク検証・テレメトリ監視・隔離:

1. **暗号によるコマンド認証**: すべてのアップリンクコマンドは、実行前にCCSDSセキュリティプロトコルの鍵と照合して認証され、見かけ上の発信元にかかわらず認証に失敗したコマンドは拒否されます。
2. **継続的なダウンリンクテレメトリ監視**: テレメトリの整合性は、テクニカルペーパーシリーズ #001 で定義した整合性検証アプローチと整合する形でリアルタイムに監視され、不整合はレビュー対象としてフラグ付けされます。
3. **侵害された地上局の隔離**: 異常なコマンドパターンを示す地上局は、調査を待つ間アップリンク能力から隔離され、衛星へのさらなるコマンド発行を防ぎます。

### 4. 宇宙リンクガバナンスと鍵管理
鍵ローテーションの計画とリンク整合性のレビュー:

* **計画的な暗号鍵のローテーション**: コマンド認証鍵は定められたスケジュールでローテーションされ、鍵が侵害されても即座に検知されなかった場合の露出期間を制限します。
* **地上セグメントの役割分離**: コマンドを発行できる権限を持つ担当者は、鍵素材を管理する担当者とは分離されます。これはCISSPドメイン4の職務分離原則と整合します。
* **リンク整合性の継続的監査**: アップリンクおよびダウンリンクの整合性指標は定められた周期でレビューされ、劣化しつつあるリンク品質や認証失敗を特定し、新たな脅威の兆候を検知します。

### 5. 結論
衛星リンクの安全性は、最も脆弱な地上セグメントの統制と同程度でしかありません。攻撃者は未認可のコマンドを注入するために宇宙機自体を侵害する必要がほとんどないためです。

CCSDSに準拠した暗号化・認証を適用することは、CISSPドメイン4に沿いつつ、距離があること自体が保護になると想定するのではなく、その地上-軌道間リンクへ直接対処します。
