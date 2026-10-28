# Koki's Technical Paper #057

## Data Loss Prevention — Content Inspection and Exfiltration Blocking, Classification-Aware Policy Enforcement, and Egress Channel Monitoring

### Summary Digest
This paper defines a DLP architecture, aligned with CISSP Domain 2, inspecting outbound content against classification policy and blocking exfiltration via email, media, and cloud uploads.

Content inspection uses pattern matching and exact data matching against classification tiers defined in Technical Paper #027, rather than treating all outbound data identically.

---
### 1. Unmonitored Egress Channel Risk
Structural Vulnerabilities of Uninspected Outbound Data Paths:

* **Uninspected Email Attachments**: Outbound email that leaves the organization without content inspection can carry sensitive data attached inadvertently or deliberately, with no technical control to catch it before it departs.
* **Unrestricted Removable Media**: Endpoints that permit unrestricted writing to removable storage provide a straightforward exfiltration path that bypasses network-based monitoring entirely.
* **Unsanctioned Cloud Upload Destinations**: Uploads to personal or unsanctioned cloud storage services can move classified data outside organizational control without triggering any alert if upload traffic itself is not inspected.

### 2. Content Inspection and Policy Foundation
Pattern Matching and Classification-Aware Enforcement Principles:

* **Pattern-Based Content Detection**: Outbound content is scanned for patterns consistent with sensitive data types, such as payment card numbers or government identifiers, flagging matches for policy evaluation.
* **Exact Data Matching**: Where feasible, outbound content is compared against fingerprints of known sensitive source documents, catching exfiltration of specific protected files even when reformatted.
* **Classification-Aware Policy Enforcement**: DLP policy enforcement is tied to the classification tiers defined in Technical Paper #027, applying stricter blocking to higher-tier data rather than a single uniform policy.

### 3. Inspection and Blocking Sequence
Channel Monitoring, Policy Matching, and Enforcement Action:

1. **Egress Channel Monitoring**: Email, removable media, and cloud-upload channels are monitored continuously for outbound content, rather than only at designated checkpoints.
2. **Policy Match Evaluation**: Detected content is evaluated against classification-aware DLP policy to determine whether the specific channel and content combination is permitted.
3. **Enforcement Action Application**: Content violating policy is blocked, quarantined for review, or flagged with a warning to the sender, depending on the severity defined for that policy violation.

### 4. DLP Program Governance and Tuning Review
False-Positive Reduction and Policy Currency Review:

* **Documented Business Justification for Exceptions**: Legitimate business needs to transmit otherwise-restricted data require a documented, approved exception rather than an informal workaround that bypasses DLP entirely.
* **False-Positive Rate Monitoring**: DLP policies generating excessive false positives are identified and tuned, since an overly aggressive policy that blocks legitimate work encourages users to seek unmonitored workarounds.
* **Continuous Policy and Pattern Currency Review**: Detection patterns and policy rules are reviewed on a defined cadence to account for new sensitive data types or classification changes.

### 5. Conclusion
A classification scheme only limits exposure if enforced at the points where data can leave the organization, not just where it is labeled.

Tying DLP policy to classification tiers, consistent with CISSP Domain 2, connects a documented label to an actual technical block at the egress channel.

---
# テクニカルペーパーシリーズ #057

## データ損失防止 — コンテンツ検査と情報流出の遮断、分類対応型ポリシー適用、および出口チャネル監視

### サマリー・ダイジェスト
本論文は、CISSPドメイン2に準拠したDLP（データ損失防止）アーキテクチャを定義し、発信コンテンツを分類ポリシーと照合し、メール・媒体・クラウドアップロードを通じた情報流出を遮断します。

コンテンツ検査は、すべての発信データを一律に扱うのではなく、パターンマッチングと テクニカルペーパーシリーズ #027 で定義した分類ティアに照らした正確なデータ照合を用います。

---
### 1. 未監視の出口チャネルリスク
未検査の発信データ経路に伴う構造的脆弱性:

* **未検査のメール添付ファイル**: コンテンツ検査なしに組織を離れる発信メールは、意図せずまたは意図的に添付された機密データを運び得ますが、それが送信される前に捕捉する技術的統制がありません。
* **無制限のリムーバブルメディア**: リムーバブルストレージへの無制限な書き込みを許可するエンドポイントは、ネットワークベースの監視を完全に迂回する単純な情報流出経路を提供してしまいます。
* **未承認のクラウドアップロード先**: 個人用または未承認のクラウドストレージサービスへのアップロードは、アップロードトラフィック自体が検査されない場合、警告を発生させることなく分類対象データを組織の管理外へ移動させ得ます。

### 2. コンテンツ検査とポリシーの基盤
パターンマッチングと分類対応型適用の原則:

* **パターンベースのコンテンツ検知**: 発信コンテンツは、支払いカード番号や政府発行の識別番号など機密データ種別と整合するパターンについてスキャンされ、一致した場合はポリシー評価対象としてフラグ付けされます。
* **正確なデータ照合**: 実現可能な場合、発信コンテンツは既知の機密文書のフィンガープリントと照合され、再フォーマットされた場合でも特定の保護対象ファイルの流出を捕捉します。
* **分類対応型ポリシー適用**: DLPポリシーの適用は、単一の一律ポリシーではなく、テクニカルペーパーシリーズ #027 で定義した分類ティアに紐づけられ、より上位のティアのデータにはより厳格なブロックが適用されます。

### 3. 検査とブロックの手順
チャネル監視・ポリシー照合・適用アクション:

1. **出口チャネルの監視**: メール、リムーバブルメディア、クラウドアップロードの各チャネルは、指定されたチェックポイントのみでなく継続的に発信コンテンツについて監視されます。
2. **ポリシー照合評価**: 検知されたコンテンツは、特定のチャネルとコンテンツの組み合わせが許可されているかを判断するため、分類対応型のDLPポリシーと照合して評価されます。
3. **適用アクションの実行**: ポリシーに違反するコンテンツは、そのポリシー違反に定義された深刻度に応じて、ブロック、レビュー待ちの検疫、または送信者への警告フラグ付けのいずれかとして処理されます。

### 4. DLPプログラムガバナンスとチューニングレビュー
偽陽性の低減とポリシー鮮度のレビュー:

* **例外に対する文書化された業務上の正当性**: 制限対象データを送信する正当な業務上の必要性がある場合、DLPを完全に迂回する非公式な回避策ではなく、文書化され承認された例外が必要です。
* **偽陽性率の監視**: 過度に厳しいポリシーは正規の業務をブロックし利用者に未監視の回避策を探させてしまうため、過剰な偽陽性を発生させるDLPポリシーは特定・調整されます。
* **ポリシーとパターンの継続的な鮮度レビュー**: 検知パターンとポリシールールは、新しい機密データ種別や分類の変化に対応するため、定められた周期でレビューされます。

### 5. 結論
分類スキームが露出を制限できるのは、単にラベル付けされる時点だけでなく、データが組織を離れ得る地点で実際に適用されている場合に限られます。

DLPポリシーを分類ティアに紐づけることは、CISSPドメイン2に沿いつつ、文書化されたラベルを出口地点における実際の技術的なブロックへと結びつけます。
