# Koki's Technical Paper #066

## OSI Layered Security — Layer-Specific Control Mapping, 802.1X Port-Based Access Control, and Cross-Layer Defense Coordination

### Summary Digest
This paper defines layer-specific security controls, aligned with CISSP Domain 4 and the OSI model, mapping controls to physical, network, transport, and application layers.

802.1X access control at the data link layer complements the boundary controls in Technical Paper #001, since a control at one layer does not cover another.

---
### 1. Single-Layer Control Gap Risk
Structural Vulnerabilities of Layer-Blind Security Design:

* **Network-Layer Controls Bypassed at the Data Link Layer**: An attacker with physical access to a switch port can bypass network-layer firewall rules entirely by operating below the layer those rules inspect.
* **Application-Layer Assumptions About Lower-Layer Integrity**: Application controls that assume the underlying network delivered data unmodified provide no protection against a data-link-layer attack such as ARP spoofing.
* **Uniform Control Application Across All Layers**: Applying the same generic security control language across all layers without layer-specific technical measures leaves gaps at layers that generic controls do not actually address.

### 2. Layer-Specific Control Foundation
OSI Model Mapping and Port-Based Authentication Principles:

* **Physical and Data Link Layer Controls**: Physical cabling security and 802.1X port-based network access control authenticate a device before it can transmit data-link-layer frames, preventing unauthorized devices from joining the network at the port level.
* **Network and Transport Layer Controls**: IP-layer access control lists and TLS at the transport layer, consistent with the approach defined in Technical Paper #043, address routing-based and connection-based threats respectively.
* **Application Layer Controls**: Application-layer input validation and web application firewall rules address threats that lower-layer controls, by design, cannot inspect or understand.

### 3. Cross-Layer Deployment Sequence
Layer Mapping, Control Deployment, and Gap Verification:

* **Layer-by-Layer Control Mapping**: Existing and planned controls are mapped against each OSI layer to identify which layers currently lack a dedicated technical control.
* **802.1X Deployment at Network Access Points**: Port-based authentication is deployed at switch ports and wireless access points, requiring device authentication before data-link-layer access is granted.
* **Cross-Layer Gap Verification**: A penetration test specifically targets layer-boundary assumptions, confirming that a control effective at one layer is not silently relied upon to cover an adjacent layer's risks.

### 4. Layered Control Governance and Coverage Auditing
Layer Coverage Mapping Currency and Control Effectiveness Review:

* **Maintained Layer Coverage Map**: The mapping of controls to OSI layers is kept current as new controls are added or network architecture changes, rather than documented once and left static.
* **Layer-Specific Incident Correlation**: Incidents are analyzed to identify which OSI layer the initial compromise occurred at, informing whether that layer's controls need strengthening.
* **Continuous Cross-Layer Penetration Testing**: Layer-boundary assumptions are re-tested on a defined cadence, consistent with the testing approach defined in Technical Paper #039, as new controls or architecture changes are introduced.

### 5. Conclusion
A firewall rule at the network layer says nothing about the data link layer below it, which is why layer-specific gaps persist even where other controls are strong.

Mapping controls explicitly to each OSI layer, consistent with CISSP Domain 4, surfaces the layer nobody addressed rather than leaving it undiscovered.

---
# テクニカルペーパーシリーズ #066

## OSI層別セキュリティ — 層固有の統制マッピング、802.1Xポートベースアクセス制御、および層横断的な防御連携

### サマリー・ダイジェスト
本論文は、CISSPドメイン4およびOSIモデルに準拠した層固有のセキュリティ統制を定義し、物理層・ネットワーク層・トランスポート層・アプリケーション層それぞれに統制をマッピングします。

データリンク層における802.1Xアクセス制御は、テクニカルペーパーシリーズ #001 で定義した境界統制を補完します。ある層で有効な統制が別の層をカバーするとは限らないためです。

---
### 1. 単一層統制の隙間リスク
層を意識しないセキュリティ設計に伴う構造的脆弱性:

* **データリンク層で回避されるネットワーク層統制**: スイッチポートへの物理アクセスを持つ攻撃者は、ファイアウォールルールが検査する層より下位で操作することで、ネットワーク層のファイアウォールルールを完全に回避できます。
* **下位層の整合性を前提としたアプリケーション層の想定**: 基盤となるネットワークがデータを未改変のまま配送したと想定するアプリケーション統制は、ARPスプーフィングのようなデータリンク層攻撃に対して保護を提供しません。
* **全層への画一的な統制の適用**: 層固有の技術的対策なしにすべての層へ同じ一般的なセキュリティ統制の文言を適用すると、一般的な統制では実際には対処されない層に隙間が残ります。

### 2. 層固有統制の基盤
OSIモデルのマッピングとポートベース認証の原則:

* **物理層とデータリンク層の統制**: 物理ケーブル配線のセキュリティと802.1Xポートベースのネットワークアクセス制御は、デバイスがデータリンク層のフレームを送信できるようになる前にそれを認証し、未承認のデバイスがポートレベルでネットワークへ参加することを防ぎます。
* **ネットワーク層とトランスポート層の統制**: テクニカルペーパーシリーズ #043 で定義したアプローチと整合するIP層のアクセス制御リストとトランスポート層のTLSは、それぞれルーティングベースの脅威と接続ベースの脅威に対処します。
* **アプリケーション層の統制**: アプリケーション層の入力検証とWebアプリケーションファイアウォールルールは、設計上、下位層の統制では検査・理解できない脅威に対処します。

### 3. 層横断的な展開の手順
層マッピング・統制展開・隙間検証:

* **層ごとの統制マッピング**: 既存および計画中の統制は各OSI層に照らしてマッピングされ、現在専用の技術的統制を欠いている層が特定されます。
* **ネットワークアクセスポイントへの802.1X展開**: ポートベース認証はスイッチポートおよび無線アクセスポイントに展開され、データリンク層のアクセスが許可される前にデバイス認証を要求します。
* **層横断的な隙間の検証**: ペネトレーションテストは層の境界に関する想定を特に対象とし、ある層で有効な統制が隣接する層のリスクをカバーするものとして黙って頼りにされていないことを確認します。

### 4. 層別統制のガバナンスとカバレッジ監査
層カバレッジマッピングの鮮度と統制実効性のレビュー:

* **維持されている層カバレッジマップ**: 統制とOSI層のマッピングは、一度文書化されたまま放置されるのではなく、新しい統制が追加されたりネットワークアーキテクチャが変化したりする中で最新の状態に保たれます。
* **層固有のインシデント相関分析**: インシデントは、最初の侵害がどのOSI層で発生したかを特定するため分析され、その層の統制を強化すべきかどうかの判断に活用されます。
* **層横断的な継続的ペネトレーションテスト**: 層の境界に関する想定は、テクニカルペーパーシリーズ #039 で定義したテストアプローチと整合する形で、新しい統制やアーキテクチャの変化が導入されるたびに定められた周期で再テストされます。

### 5. 結論
ネットワーク層のファイアウォールルールは、その下層にあるデータリンク層で何が起きているかについては何も語りません。だからこそ、他の統制が強固なネットワークであっても層固有の隙間が残り続けます。

統制を各OSI層に明示的にマッピングすることは、CISSPドメイン4に沿いつつ、誰も対応していなかった層を未発見のまま放置するのではなく浮かび上がらせます。
