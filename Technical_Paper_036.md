# Koki's Technical Paper #036

## Social Engineering — Detecting Manipulation as Logical Bugs, Email Authentication Controls, and Automated Pretext Flagging

### Summary Digest
This paper defines a technical detection layer for social-engineering attempts, aligned with CISSP Domain 4 and SPF/DKIM/DMARC email authentication, flagging manipulation patterns as measurable anomalies rather than relying on judgment alone.

Automated linguistic and sender-behavior analysis, combined with system-enforced verification holds, complements the awareness training defined in Technical Paper #010.

---
### 1. Undetected Manipulation Pattern Risk
Structural Vulnerabilities of Judgment-Only Defenses:

* **Spoofed Sender Domains Passing Basic Filters**: Email systems that do not enforce sender-authentication standards allow a spoofed or look-alike domain to reach a user's inbox indistinguishable from a legitimate sender at a glance.
* **Urgency and Authority Language Left Unflagged**: Messages combining urgency, authority claims, and a request for atypical action share a recognizable linguistic pattern that goes undetected when no automated analysis is applied to message content.
* **Unenforced Secondary Verification for High-Risk Requests**: Financial or credential-related requests that lack a system-enforced hold for secondary verification depend entirely on the recipient remembering to check independently.

### 2. Email Authentication and Pattern-Detection Foundation
SPF/DKIM/DMARC Enforcement and Linguistic Anomaly Scoring:

* **Sender Authentication via SPF, DKIM, and DMARC**: Inbound mail is validated against Sender Policy Framework (SPF), DomainKeys Identified Mail (DKIM), and Domain-based Message Authentication (DMARC) records, rejecting or flagging messages that fail authentication.
* **Automated Linguistic Pattern Scoring**: Message content is scored for combinations of urgency, authority assertion, and requests for atypical action, consistent with patterns documented in business-email-compromise research, flagging high-scoring messages for review.
* **Alignment with Awareness Training Findings**: Detection patterns are informed by the incident data and human-factor findings described in Technical Paper #010, keeping automated detection grounded in observed manipulation tactics rather than assumptions.

### 3. Detection and Hold Sequence
Authentication Checks, Scoring, and Transaction Hold:

1. **Inbound Authentication Verification**: Every inbound message is checked against SPF, DKIM, and DMARC records before delivery, with failures routed to quarantine rather than the primary inbox.
2. **Content-Pattern Scoring**: Delivered messages are scored for linguistic manipulation patterns, and high-scoring messages are flagged with a visible warning before the recipient can act on them.
3. **System-Enforced Verification Hold**: Requests matching a high-risk category, such as a wire transfer or credential reset, are held pending the out-of-band confirmation process defined in Technical Paper #010, rather than proceeding immediately.

### 4. Detection Model Governance and False-Result Review
Scoring Threshold Calibration and Bypass Auditing:

* **Separation of Detection Logic from Delivery Decisions**: The scoring and authentication engine operates independently of the mail-delivery path, so a flaw in one component does not silently disable the other.
* **Documented Threshold Justification**: Scoring thresholds that determine when a message is flagged or held are documented and reviewed, rather than set arbitrarily without a basis in observed data.
* **Continuous False-Positive and Bypass Auditing**: False-positive rates and confirmed bypasses of the detection system are reviewed on a defined cadence, informing adjustments to authentication enforcement and scoring criteria.

### 5. Conclusion
Treating manipulation as a pattern with measurable properties lets a system flag it, rather than relying on a person to catch it every time.

Pairing that detection with the verification procedures in Technical Paper #010, per CISSP Domain 4, covers what a system catches and what still needs judgment.

---
# テクニカルペーパーシリーズ #036

## ソーシャルエンジニアリング — 論理バグとしての操作検知、メール認証統制、および自動化されたプリテキスト検出

### サマリー・ダイジェスト
本論文は、CISSPドメイン4およびSPF/DKIM/DMARCのメール認証に準拠した、ソーシャルエンジニアリング検知のための技術層を定義し、判断のみに頼らず操作パターンを測定可能な異常として検出します。

自動化された言語分析および送信者挙動分析に、高リスクリクエストへのシステム強制確認保留を組み合わせ、テクニカルペーパーシリーズ #010 の意識向上教育を補完します。

---
### 1. 検知されない操作パターンのリスク
判断のみに頼る防御の構造的脆弱性:

* **基本フィルターを通過するなりすまし送信ドメイン**: 送信者認証標準を適用しないメールシステムは、なりすましや類似ドメインが、一見して正規の送信者と区別できない状態でユーザーの受信箱に届くことを許してしまいます。
* **フラグ付けされない緊急性・権威性を装う言い回し**: 緊急性・権威の主張・異例の行動の要求を組み合わせたメッセージは認識可能な言語パターンを共有していますが、メッセージ内容への自動分析が行われなければ検知されないままとなります。
* **高リスクリクエストに対する未適用の二次確認**: システムによる二次確認の強制保留を欠く送金や資格情報関連のリクエストは、受信者が独自に確認することを覚えているかどうかに完全に依存してしまいます。

### 2. メール認証とパターン検知の基盤
SPF/DKIM/DMARCの適用と言語的異常のスコアリング:

* **SPF・DKIM・DMARCによる送信者認証**: 着信メールはSender Policy Framework（SPF）、DomainKeys Identified Mail（DKIM）、Domain-based Message Authentication（DMARC）のレコードと照合され、認証に失敗したメッセージは拒否またはフラグ付けされます。
* **自動化された言語パターンのスコアリング**: メッセージ内容は、ビジネスメール詐欺（BEC）研究で文書化されているパターンと整合する、緊急性・権威の主張・異例の行動要求の組み合わせについてスコアリングされ、高スコアのメッセージはレビュー対象としてフラグ付けされます。
* **意識向上教育の知見との整合**: 検知パターンは、テクニカルペーパーシリーズ #010 で述べたインシデントデータおよび人的要因の知見に基づいて策定され、自動検知を想定ではなく観測された操作手口に根ざしたものにします。

### 3. 検知と保留の手順
認証チェック・スコアリング・取引保留:

1. **着信認証の検証**: 着信する各メッセージは配送前にSPF・DKIM・DMARCのレコードと照合され、失敗した場合は主受信箱ではなく検疫対象へルーティングされます。
2. **コンテンツパターンのスコアリング**: 配送されたメッセージは言語的な操作パターンについてスコアリングされ、高スコアのメッセージには受信者が対応する前に目に見える警告が付与されます。
3. **システム強制の確認保留**: 送金や資格情報リセットなど高リスクカテゴリに該当するリクエストは、即座に処理されるのではなく、テクニカルペーパーシリーズ #010 で定義した複数経路での確認プロセスの完了を待って保留されます。

### 4. 検知モデルガバナンスと誤判定のレビュー
スコアしきい値の較正と回避事例の監査:

* **検知ロジックと配送判断の分離**: スコアリングおよび認証エンジンはメール配送経路とは独立して動作するため、一方の欠陥がもう一方を気づかぬうちに無効化することはありません。
* **文書化されたしきい値の根拠**: メッセージがフラグ付けまたは保留される基準となるスコアしきい値は文書化・レビューされ、観測データに基づかない恣意的な設定を避けます。
* **偽陽性と回避事例の継続的監査**: 検知システムの偽陽性率と確認済みの回避事例は定められた周期でレビューされ、認証の適用やスコアリング基準の調整に活用されます。

### 5. 結論
操作の試みを測定可能な特性を持つパターンとして扱うことで、毎回人間が見抜くことに頼るのではなく、システムがそれにフラグを立てられるようになります。

その検知を テクニカルペーパーシリーズ #010 で定義した確認手続きと組み合わせることは、CISSPドメイン4に沿いつつ、システムが検知できる事案と、依然として人の判断を要する事案の両方をカバーします。
