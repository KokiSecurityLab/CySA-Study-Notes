# Koki's Technical Paper #067

## Network Segmentation — VLAN Architecture and DMZ Design, IEEE 802.1Q Tagging, and VLAN Hopping Mitigation

### Summary Digest
This paper defines a network segmentation architecture using IEEE 802.1Q VLANs, aligned with CISSP Domain 4, separating traffic by trust level rather than treating the network as flat, and anticipates AI agents as a new class of workload whose machine-speed lateral movement makes segment boundaries more important, not less.

A demilitarized zone (DMZ) isolates externally-facing services, extending the default-deny perimeter posture of Technical Paper #001, while VLAN hopping mitigations prevent traffic crossing segments without inspection.

---
### 1. Flat Network Lateral Movement Risk
Structural Vulnerabilities of Undifferentiated Network Segments:

* **Unrestricted Lateral Movement in Flat Networks**: A network without segmentation allows a compromised device to reach any other device on the same broadcast domain without crossing an inspection point. In a 2026 intrusion investigated by Palo Alto Networks Unit 42, an attacker entered through a public-facing API endpoint and deployed an automated reconnaissance agent to map internal microservices, completing work estimated at roughly two weeks of human effort in under 10 hours; a flat network offers no inspection point to slow that kind of automated movement.
* **Externally-Facing Services Sharing the Internal Network**: Publicly reachable services hosted on the same network segment as internal systems give an attacker who compromises that service a direct path into internal infrastructure.
* **VLAN Hopping via Switch Spoofing and Double Tagging**: An attacker can reach a VLAN they are not authorized to access either by negotiating an unauthorized trunk through the Dynamic Trunking Protocol (DTP), known as switch spoofing, or by sending double-tagged 802.1Q frames from a trunk's native VLAN, an attack that depends on switches left at default native VLAN settings.

### 2. VLAN and DMZ Architecture Foundation
802.1Q Tagging and Trust-Zone Separation Principles:

* **IEEE 802.1Q VLAN Tagging**: Traffic is logically separated into VLANs using the IEEE 802.1Q tagging standard, grouping devices by trust level and function rather than physical location alone.
* **Demilitarized Zone Placement**: Externally-facing services are placed in a dedicated DMZ segment, isolated from the internal network by separate firewall rules on each side, extending the default-deny perimeter posture defined in Technical Paper #001.
* **Inter-VLAN Routing Control**: Traffic routed between VLANs passes through a firewall or Layer 3 device applying access control rules, rather than routing freely between segments by default.

### 3. Segmentation Deployment and Hardening Sequence
VLAN Assignment, DMZ Isolation, and Hopping Mitigation:

* **VLAN Assignment by Trust Level**: Devices and services are assigned to VLANs based on their trust level and function. Systems handling mid-tier records under the classification scheme defined in Technical Paper #027 are placed in restricted internal segments, while top-tier records remain on the air-gapped systems defined there, outside the switched network entirely. Non-human workloads such as AI agents receive their own segment rather than sharing a user VLAN, so their access can be restricted and observed separately.
* **DMZ Firewall Rule Configuration**: Separate firewall rule sets govern traffic between the internet and the DMZ, and between the DMZ and the internal network, preventing direct internet-to-internal paths.
* **VLAN Hopping Mitigation**: User-facing switch ports are fixed in access mode with DTP negotiation disabled, closing the switch spoofing path. On each trunk, the native VLAN is moved from VLAN 1 to a dedicated VLAN that carries no user traffic and is explicitly tagged where the switch platform supports it, removing the conditions double tagging relies on.

### 4. Segmentation Governance and Configuration Auditing
VLAN Assignment Currency and Trunk Configuration Review:

* **Documented VLAN Assignment Rationale**: Each VLAN assignment is documented with the trust-level rationale behind it, rather than assigned informally without a traceable basis.
* **Trunk Port Configuration Hardening**: Trunk ports are explicitly configured rather than left at default settings, consistent with the fail-safe-default principle defined in Technical Paper #061.
* **Continuous Inter-VLAN Traffic Auditing**: Traffic crossing VLAN boundaries is logged and compared against a per-segment baseline, so unexpected inter-segment communication surfaces as it occurs rather than at the next scheduled review. This becomes more important as AI agents are deployed: Cisco's 2026 report on AI and wide area networks measured an agentic task generating 450% more network traffic than the equivalent human task, and agent traffic is not tied to human working hours.

### 5. Conclusion
A flat network turns a single compromised device into access to everything else on that network, which is exactly what segmentation is designed to prevent.

Combining VLAN-based segmentation with an isolated DMZ, per CISSP Domain 4, keeps a breach of one segment from becoming a breach of all of them, and as agent-driven intrusions shorten the time an attacker needs to move between systems, each boundary becomes one of the few points where that movement can still be inspected and stopped.

---
# テクニカルペーパーシリーズ #067

## ネットワークセグメンテーション — VLANアーキテクチャとDMZ設計、IEEE 802.1Qタギング、およびVLANホッピング対策

### サマリー・ダイジェスト
本論文は、IEEE 802.1Q VLANを用いたネットワークセグメンテーションアーキテクチャを定義し、CISSPドメイン4に準拠して、ネットワークを平坦に扱うのではなく信頼レベルに応じてトラフィックを分離するとともに、機械の速度で横方向移動を行うAIエージェントを新たな種類のワークロードとして想定し、セグメント境界の重要性がむしろ高まることを示します。

非武装地帯（DMZ）は、テクニカルペーパーシリーズ #001 のデフォルト拒否の境界方針を発展させる形で外部向けサービスを隔離し、VLANホッピング対策は検査を経ずセグメントを越えるトラフィックを防ぎます。

---
### 1. 平坦ネットワークにおける横方向移動のリスク
無差別なネットワークセグメントに伴う構造的脆弱性:

* **平坦なネットワークにおける無制限の横方向移動**: セグメンテーションを持たないネットワークでは、侵害されたデバイスが検査ポイントを経由することなく同一ブロードキャストドメイン上の他のあらゆるデバイスに到達できてしまいます。Palo Alto NetworksのUnit 42が2026年に調査した侵入事案では、攻撃者が外部公開されたAPIエンドポイントから侵入し、自動化された偵察エージェントを展開して内部のマイクロサービスを把握しました。人間であれば約2週間かかると推定される作業が、10時間未満で完了しています。平坦なネットワークには、こうした自動化された移動を遅らせる検査ポイントが存在しません。
* **内部ネットワークと同居する外部向けサービス**: 内部システムと同じネットワークセグメントでホストされる公開到達可能なサービスは、そのサービスを侵害した攻撃者に内部インフラへの直接経路を与えてしまいます。
* **スイッチスプーフィングとダブルタギングによるVLANホッピング**: 攻撃者は、Dynamic Trunking Protocol（DTP）を通じて不正なトランクを確立するスイッチスプーフィング、またはトランクのネイティブVLANからダブルタグ付きの802.1Qフレームを送信するダブルタギングによって、アクセスを許可されていないVLANに到達できます。後者は、既定のネイティブVLAN設定のまま運用されているスイッチを前提とする攻撃です。

### 2. VLANとDMZアーキテクチャの基盤
802.1Qタギングと信頼ゾーン分離の原則:

* **IEEE 802.1Q VLANタギング**: トラフィックは、単に物理的な場所だけでなく信頼レベルと機能に基づいてデバイスをグループ化する、IEEE 802.1Qタギング標準を用いて論理的にVLANへ分離されます。
* **非武装地帯（DMZ）の配置**: 外部向けサービスは、両側に個別のファイアウォールルールを持つ専用のDMZセグメントに配置され、内部ネットワークから隔離されます。これは、テクニカルペーパーシリーズ #001 で定義したデフォルト拒否の境界方針を発展させたものです。
* **VLAN間ルーティング制御**: VLAN間でルーティングされるトラフィックは、既定でセグメント間を自由にルーティングされるのではなく、アクセス制御ルールを適用するファイアウォールまたはレイヤー3デバイスを経由します。

### 3. セグメンテーション展開と強化の手順
VLAN割り当て・DMZ隔離・ホッピング対策:

* **信頼レベルに基づくVLAN割り当て**: デバイスとサービスは、その信頼レベルと機能に基づいてVLANへ割り当てられます。テクニカルペーパーシリーズ #027 で定義した分類スキームにおける中位ティアの記録を扱うシステムは制限された内部セグメントに配置し、最上位ティアの記録は同論文で定義したとおり、スイッチネットワークの外にあるエアギャップされたシステムにとどめます。AIエージェントのような人間以外のワークロードはユーザーVLANに同居させず専用のセグメントに配置し、そのアクセスを個別に制限・観測できるようにします。
* **DMZファイアウォールルールの設定**: インターネットとDMZの間、およびDMZと内部ネットワークの間には個別のファイアウォールルールセットが適用され、インターネットから内部への直接経路を防ぎます。
* **VLANホッピング対策**: ユーザー向けのスイッチポートはアクセスモードに固定してDTPネゴシエーションを無効化し、スイッチスプーフィングの経路を断ちます。各トランクではネイティブVLANをVLAN 1から、ユーザートラフィックを流さない専用VLANへ移し、スイッチ機種が対応する場合はネイティブVLANにも明示的にタグを付けることで、ダブルタギングが成立する条件を取り除きます。

### 4. セグメンテーションガバナンスと構成監査
VLAN割り当ての鮮度とトランク構成のレビュー:

* **文書化されたVLAN割り当ての根拠**: 各VLAN割り当ては、追跡可能な根拠なく非公式に割り当てられるのではなく、その背後にある信頼レベルの根拠とともに文書化されます。
* **トランクポート構成の強化**: トランクポートは、テクニカルペーパーシリーズ #061 で定義したフェイルセーフなデフォルトの原則と整合する形で、既定設定のまま放置されるのではなく明示的に設定されます。
* **VLAN間トラフィックの継続的監査**: VLAN境界を越えるトラフィックは記録され、セグメントごとのベースラインと比較されます。これにより、予期しないセグメント間通信は次の定期レビューを待たず、発生した時点で検出されます。AIエージェントの導入が進むほど、この仕組みの重要性は増します。Ciscoが2026年に発表した、AIが広域ネットワーク（WAN）に与える影響に関する報告書は、エージェントによるタスクが同等の人間のタスクより450%多いネットワークトラフィックを生むと測定しています。また、エージェントの通信は人間の勤務時間に縛られません。

### 5. 結論
平坦なネットワークでは、単一の侵害されたデバイスがそのネットワーク上の他のすべてへのアクセスとなってしまいますが、これはまさにセグメンテーションが防ぐよう設計されている事態です。

VLANベースのセグメンテーションと適切に隔離されたDMZを組み合わせることは、CISSPドメイン4に沿いつつ、あるセグメントの侵害が自動的にすべてのセグメントの侵害となることを防ぎ、エージェント主導の侵入によって攻撃者がシステム間を移動する時間が短くなる中で、各境界はその移動を検査し食い止められる数少ない地点の一つとなります。
