# Koki's Technical Paper #064

## Physical Security Design — CPTED Principles and Layered Facility Controls, Environmental Protection Systems, and Access Control Vestibules

### Summary Digest
This paper defines a physical security design framework, aligned with CISSP Domain 3 and CPTED principles, layering natural surveillance and access control across concentric facility zones.

Data center environments add clean-agent fire suppression, since a physical failure can destroy the same assets the technical controls in this series protect.

---
### 1. Single-Layer Physical Exposure Risk
Structural Vulnerabilities of Undifferentiated Facility Access:

* **Uniform Access Across Sensitivity Zones**: Facilities that grant the same physical access level throughout, rather than layering stricter controls around more sensitive areas, allow anyone who reaches the building to reach the most critical assets.
* **Unmonitored Natural Surveillance Gaps**: Building layouts with poor sightlines and inadequate lighting create areas where unauthorized activity can occur without being naturally observed by occupants or passersby.
* **Water-Based Fire Suppression in Server Areas**: Server rooms protected only by standard water-based sprinkler systems risk destroying electronic equipment during a fire event that a clean-agent system would have suppressed without water damage.

### 2. CPTED and Environmental Protection Foundation
Layered Zone Design and Facility Control Principles:

* **CPTED Natural Surveillance and Access Control**: Facility layout uses sightlines, lighting, and landscaping to maximize natural observation, and physical pathways are designed to funnel visitors through monitored access points rather than multiple unmonitored entries.
* **Concentric Zone Layering**: Physical security is layered in concentric zones, from perimeter fencing through building entry, floor access, and individual room or rack access, consistent with the defense-in-depth principle defined in Technical Paper #061.
* **Clean-Agent Fire Suppression**: Server and equipment rooms use clean-agent fire suppression systems rather than water-based sprinklers, protecting electronic equipment from suppression-related damage.

### 3. Access Control and Environmental Monitoring Sequence
Vestibule Verification, Zone Transition, and Sensor Monitoring:

1. **Access Control Vestibule Verification**: Entry to higher-security zones requires passing through a mantrap-style access control vestibule that verifies a single authorized individual before permitting entry, preventing tailgating.
2. **Zone Transition Logging**: Movement between concentric security zones is logged with individual identity and timestamp, consistent with the accountability-logging approach defined in Technical Paper #018.
3. **Environmental Sensor Monitoring**: Temperature, humidity, and smoke sensors in server areas are continuously monitored, triggering alerts before conditions reach a threshold that risks equipment damage.

### 4. Physical Security Governance and Zone Auditing
Access Log Review and Environmental Control Testing:

* **Periodic Access Log Review**: Physical access logs are reviewed on a defined cadence to identify unusual access patterns, such as entry at atypical hours or by personnel without a documented business need.
* **Scheduled Environmental System Testing**: Fire suppression and environmental monitoring systems are tested on a defined schedule rather than assumed functional until an actual incident reveals otherwise.
* **Continuous CPTED Effectiveness Review**: Facility layout and lighting are periodically reassessed against CPTED principles as the physical environment changes, such as new construction or landscaping that affects sightlines.

### 5. Conclusion
A server rack protected by strong encryption and access control software is still vulnerable if anyone can walk into the room and remove the hardware.

Layering CPTED principles across concentric physical zones, consistent with CISSP Domain 3, extends the same defense-in-depth logic applied to networks into the facility itself.

---
# テクニカルペーパーシリーズ #064

## 物理セキュリティ設計 — CPTED原則と階層化された施設統制、環境保護システム、およびアクセス制御ベスティビュール

### サマリー・ダイジェスト
本論文は、CISSPドメイン3およびCPTED（環境設計による犯罪予防）原則に準拠した物理セキュリティ設計フレームワークを定義し、自然監視とアクセス制御を同心円状の施設ゾーンにわたって階層化します。

データセンター環境にはクリーンエージェント消火設備も加わります。物理的な障害は、この一連の論文で扱う技術的統制が保護しようとしているのと同じ資産を破壊し得るためです。

---
### 1. 単層物理露出のリスク
無差別な施設アクセスに伴う構造的脆弱性:

* **機微度ゾーン間での均一なアクセス**: より機微なエリアに厳格な統制を階層化するのではなく、施設全体で同一の物理アクセスレベルを許可すると、建物に到達できる誰もが最も重要な資産に到達できてしまいます。
* **監視されていない自然監視の死角**: 見通しが悪く照明が不十分な建物レイアウトは、居住者や通行人による自然な観察を経ずに不正な活動が発生し得るエリアを生み出します。
* **サーバーエリアにおける水系消火設備**: 標準的な水系スプリンクラーのみで保護されたサーバールームは、クリーンエージェント方式であれば水損なしに消火できたはずの火災事象の際に、電子機器を破壊するリスクを抱えます。

### 2. CPTEDと環境保護の基盤
階層化されたゾーン設計と施設統制の原則:

* **CPTEDによる自然監視とアクセス制御**: 施設レイアウトは、見通し・照明・植栽を用いて自然な観察を最大化し、複数の未監視の入口ではなく監視された入場ポイントへ来訪者を誘導するよう物理的な経路が設計されます。
* **同心円状のゾーン階層化**: 物理セキュリティは、テクニカルペーパーシリーズ #061 で定義した多層防御の原則と整合する形で、境界フェンスから建物入口、フロアアクセス、個別の部屋やラックアクセスに至るまで同心円状に階層化されます。
* **クリーンエージェント消火**: サーバー・機器室では、水系スプリンクラーではなくクリーンエージェント消火システムを用い、消火に伴う電子機器の損傷から保護します。

### 3. アクセス制御と環境監視の手順
ベスティビュール検証・ゾーン移動・センサー監視:

1. **アクセス制御ベスティビュールでの検証**: より高セキュリティのゾーンへの入場には、共連れを防ぐため、入場前に単一の許可された個人を検証するマントラップ方式のアクセス制御ベスティビュールを通過することが求められます。
2. **ゾーン移動のログ記録**: 同心円状のセキュリティゾーン間の移動は、テクニカルペーパーシリーズ #018 で定義した説明責任のログ記録アプローチと整合する形で、個人の身元とタイムスタンプとともに記録されます。
3. **環境センサーの監視**: サーバーエリアの温度・湿度・煙センサーは継続的に監視され、機器損傷のリスクがあるしきい値に達する前に警告を発生させます。

### 4. 物理セキュリティガバナンスとゾーン監査
アクセスログレビューと環境統制のテスト:

* **定期的なアクセスログレビュー**: 物理アクセスログは、通常とは異なる時間帯の入場や、文書化された業務上の必要性を持たない職員による入場など、異常なアクセスパターンを特定するため、定められた周期でレビューされます。
* **計画的な環境システムテスト**: 消火・環境監視システムは、実際のインシデントが機能不全を明らかにするまで機能していると前提するのではなく、定められたスケジュールでテストされます。
* **CPTED実効性の継続的レビュー**: 施設レイアウトと照明は、新築や見通しに影響する造園など物理環境が変化する中で、CPTED原則に照らして定期的に再評価されます。

### 5. 結論
強力な暗号化とアクセス制御ソフトウェアで保護されたサーバーラックも、誰かが部屋に入り込んでハードウェアを取り除くことができるのであれば、依然として脆弱なままです。

同心円状の物理ゾーン全体にCPTED原則を階層化することは、CISSPドメイン3に沿いつつ、ネットワークに適用されるのと同じ多層防御の論理を物理的な施設そのものへ拡張します。
