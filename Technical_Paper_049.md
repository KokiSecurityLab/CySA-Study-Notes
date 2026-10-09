# Koki's Technical Paper #049

## Cognitive Root Key — Ultimate Human-Anchored Trust Origin, Multi-Party Key Ceremony, and Threshold Cryptography

### Summary Digest
This paper defines a multi-party root-key protection framework, aligned with CISSP Domain 3 and NIST SP 800-57, distributing control of the root key across several trusted individuals.

Threshold cryptography, consistent with Shamir's Secret Sharing, requires a minimum number of custodians to act together before the root key can be reconstructed.

---
### 1. Single-Custodian Root Key Risk
Structural Vulnerabilities of Individually-Held Root Keys:

* **Single Point of Compromise or Loss**: A root key held or controlled entirely by one individual creates both a compromise risk if that person is coerced and an availability risk if that person becomes unreachable.
* **Undetectable Unilateral Key Use**: Without a requirement for multiple parties to act together, a single compromised custodian could use the root key without any independent check on that action.
* **Biometric-Only Protection Limitations**: Protecting a root key with a single individual's biometric trait alone inherits the entropy and irrevocability limitations described in Technical Paper #042, without the additional safeguard multi-party control provides.

### 2. Threshold Cryptography and Key Ceremony Foundation
M-of-N Secret Sharing and Custodian Governance Principles:

* **Shamir's Secret Sharing**: The root key is split into multiple shares using Shamir's Secret Sharing scheme, requiring a defined minimum number of shares (M of N) to reconstruct the original key, so no single share holder can act alone.
* **Documented Key Ceremony Procedure**: Root-key generation and any reconstruction event follow a documented, witnessed key-ceremony procedure, consistent with industry practice for protecting root certificate authority keys.
* **Alignment with Baseline Boundary Controls**: Key-ceremony facilities and procedures are reconciled with the physical and access controls defined in Technical Paper #027, keeping root-key protection consistent with the wider classification framework.

### 3. Share Distribution and Reconstruction Sequence
Share Generation, Custodian Distribution, and Verified Reconstruction:

1. **Secret Share Generation**: The root key is generated within a controlled environment and immediately split into shares using the threshold scheme, with the original unsplit key never persisted to storage.
2. **Independent Custodian Distribution**: Each share is distributed to a separate, independently vetted custodian, with no single custodian receiving enough shares to reconstruct the key alone.
3. **Witnessed Reconstruction Events**: Reconstructing the key for an authorized operation requires the defined minimum number of custodians to be physically present and participate, with the event logged and witnessed.

### 4. Custodian Governance and Ceremony Auditing
Custodian Vetting and Ceremony Record Review:

* **Documented Custodian Vetting Criteria**: Individuals selected as key custodians are vetted against documented criteria, and custodian lists are reviewed rather than left static indefinitely.
* **Separation of Custodianship from Daily Operations**: Key custodians are separated from personnel who manage day-to-day systems that the root key ultimately protects, reducing the chance that a single compromised role controls both.
* **Continuous Ceremony Record Auditing**: Records of past key ceremonies, including custodian attendance and reconstruction justification, are reviewed on a defined cadence to confirm the process was followed as documented.

### 5. Conclusion
A root key protected by one person's presence, biometric or otherwise, is only as available and as trustworthy as that one person.

Splitting control across custodians through threshold cryptography, consistent with CISSP Domain 3 and NIST SP 800-57, makes a root key resistant to coercion or loss of any one individual.

---
# テクニカルペーパーシリーズ #049
## コグニティブ・ルートキー — 究極の人間アンカー型信頼の起点、複数当事者による鍵儀式、およびしきい値暗号方式

### サマリー・ダイジェスト
本論文は、CISSPドメイン3およびNIST SP 800-57に準拠した複数当事者によるルート鍵保護フレームワークを定義し、ルート鍵の管理権限を複数の信頼された個人に分散します。

シャミアの秘密分散法と整合するしきい値暗号方式により、ルート鍵を再構成するには最低限必要な人数のカストディアンが協働する必要があります。

---
### 1. 単独カストディアン型ルート鍵のリスク
個人単独保有型ルート鍵に伴う構造的脆弱性:

* **侵害または喪失の単一障害点**: 一人の個人が完全に保有・管理するルート鍵は、その人物が強要された場合の侵害リスクと、その人物に連絡が取れなくなった場合の可用性リスクの両方を生み出します。
* **検知できない単独での鍵使用**: 複数当事者が協働することを要求する仕組みがなければ、侵害された単独のカストディアンが独立したチェックなしにルート鍵を使用できてしまいます。
* **生体情報のみによる保護の限界**: 単一個人の生体特徴のみでルート鍵を保護すると、複数当事者による統制が提供する追加の安全策を欠いたまま、テクニカルペーパーシリーズ #042 で述べたエントロピーと取り消し不可能性の限界を引き継いでしまいます。

### 2. しきい値暗号方式と鍵儀式の基盤
M-of-N秘密分散とカストディアンガバナンスの原則:

* **シャミアの秘密分散法**: ルート鍵はシャミアの秘密分散法を用いて複数のシェアに分割され、元の鍵を再構成するには定義済みの最低限のシェア数（M of N）が必要となるため、単独のシェア保有者が単独で行動することはできません。
* **文書化された鍵儀式の手順**: ルート鍵の生成および再構成イベントは、ルート認証局の鍵保護に関する業界実務と整合する、文書化され立会人のもとで行われる鍵儀式の手順に従います。
* **ベースライン境界統制との整合**: 鍵儀式の施設と手順は、テクニカルペーパーシリーズ #027 で定義した物理・アクセス統制と突き合わされ、ルート鍵保護をより広い分類フレームワークと一貫させます。

### 3. シェア配布と再構成の手順
シェア生成・カストディアン配布・立会いのもとでの再構成:

1. **秘密シェアの生成**: ルート鍵は統制された環境内で生成され、しきい値方式を用いて即座に複数のシェアへ分割されます。分割前の元の鍵が保存されることはありません。
2. **独立したカストディアンへの配布**: 各シェアは個別に審査された独立のカストディアンへ配布され、単独のカストディアンが鍵を再構成できるだけのシェアを保有することはありません。
3. **立会いのもとでの再構成イベント**: 承認された操作のために鍵を再構成するには、定義済みの最低人数のカストディアンが物理的に出席・参加する必要があり、そのイベントは記録・立会いされます。

### 4. カストディアンガバナンスと儀式の監査
カストディアンの審査と儀式記録のレビュー:

* **文書化されたカストディアン審査基準**: 鍵カストディアンとして選定される個人は文書化された基準に照らして審査され、カストディアンの一覧は無期限に固定されるのではなくレビューされます。
* **カストディアン職務と日常運用の分離**: 鍵カストディアンは、ルート鍵が最終的に保護する日常システムを管理する担当者とは分離され、単一の侵害された役割が両方を統制するリスクを低減します。
* **儀式記録の継続的監査**: カストディアンの出席状況や再構成の正当性理由を含む過去の鍵儀式の記録は、手順が文書通りに実施されたことを確認するため定められた周期でレビューされます。

### 5. 結論
生体情報であれ何であれ、一人の人物の在席によって保護されるルート鍵は、その一人分の可用性と信頼性しか持ちません。

しきい値暗号方式によって管理権限を複数のカストディアンへ分散することは、CISSPドメイン3およびNIST SP 800-57に沿いつつ、ルート鍵を特定の一個人への強要や、その一個人の喪失に対して強靭なものにします。
