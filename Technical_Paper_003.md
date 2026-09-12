# Koki's Technical Paper #003

## CASB Essentials — Multi-Cloud Security Control, Reverse Proxy Deflection, and Data Tokenization Protocols

### Summary Digest
This paper defines a reverse-proxy-based Cloud Access Security Broker (CASB) architecture, aligned with CISSP Domain 3 and CASP+ practices, to filter non-compliant payloads before they reach cloud workloads.

Traffic is isolated at the outermost perimeter and processed as unauthenticated until verified, reducing the impact of hostile requests on core systems.

---
### 1. Reverse Proxy Deflection
The Structural Framework of Non-Absorption Ingestion Strategies:

* **The Hazards of Absorbing Unverified Traffic**: Systems that process inbound requests before verification inherit the risk profile of every connecting node, increasing exposure to compromise.
* **Default-Deny Posture for Unauthenticated Traffic**: The reverse proxy treats all inbound data as untrusted by default, rejecting requests that fail authentication before they reach backend services.
* **Separation of Traffic Metadata from Payload Handling**: Isolating connection metadata from payload inspection allows the gateway to log and analyze attack characteristics without exposing backend systems to the payload itself.

### 2. Session Isolation and Data Protection Design
Response Minimization and Tokenization Controls:

* **Minimal Response Disclosure**: Withholding non-essential response data from unauthenticated sources limits the information available to automated scanning and reconnaissance tools.
* **Session Isolation on Repeated Failure**: Nodes that repeatedly fail authentication are routed to an isolated handling path, preventing them from consuming resources allocated to verified sessions (see Technical Paper #013 for related response-timing controls).
* **Inline Data Tokenization**: Sensitive data fields are replaced with non-reversible tokens before leaving the trust boundary, limiting exposure if a downstream system is compromised.

### 3. Policy Configuration, Inspection, and Rejection
Three-Stage Deployment for Reverse Proxy Enforcement:

1. **Baseline Policy Configuration**: Define allow-lists, authentication requirements, and tokenization rules for each cloud service integrated with the CASB.
2. **Real-Time Traffic Inspection**: Inspect inbound and outbound traffic against the configured policy, flagging requests that do not meet authentication or data-handling requirements.
3. **Automated Request Rejection and Logging**: Reject non-compliant requests at the perimeter and log the rejection for correlation with related security events (see Technical Paper #002 for SIEM integration).

### 4. Reconnaissance Cost and Propagation Control
Resource Preservation and Threat Containment:

* **Limiting Response to Non-Compliant Requests**: Declining to process malformed or unauthenticated requests reduces the resources spent responding to reconnaissance and scanning activity.
* **Preventing Propagation of Malicious Content**: The proxy is configured to strip or block known malicious payload patterns so that the CASB does not become a conduit for malware or scripts.
* **Policy Enforcement Review Cadence**: CASB policy enforcement is reviewed on a defined cadence, producing records that support compliance reporting and incident investigation.

### 5. Conclusion
Rejecting unauthenticated traffic at the proxy, rather than absorbing it into backend logic, keeps a CASB's default posture defensible under CISSP Domain 3 and CASP+ review.

Inline tokenization adds a second layer, so that traffic which does pass inspection carries no data of direct value if intercepted downstream.

---
# テクニカルペーパーシリーズ #003

## CASBの基本概念 — マルチクラウドセキュリティ制御、リバースプロキシによる脅威遮断、およびデータトークン化プロトコル

### サマリー・ダイジェスト
本論文は、CISSPドメイン3およびCASP+の実務に準拠したリバースプロキシ型のCASB（Cloud Access Security Broker）アーキテクチャを定義し、保護対象のクラウドワークロードに到達する前に非準拠のペイロードを遮断します。

トラフィックは最も外側の境界で隔離され、検証されるまで未認証として扱われるため、悪意あるリクエストがコアシステムに与える影響を低減します。

---
### 1. リバースプロキシによる脅威遮断
外部データを吸収しない入力防護の構造的枠組み:

* **未検証トラフィックを処理することのリスク**: 検証前に着信リクエストを処理するシステムは、接続してくるすべてのノードのリスクプロファイルを引き継ぐことになり、侵害への露出が増大します。
* **未認証トラフィックに対するデフォルト拒否**: リバースプロキシは着信データを既定で未信頼として扱い、認証に失敗したリクエストをバックエンドサービスに到達する前に拒否します。
* **トラフィックのメタデータとペイロード処理の分離**: 接続メタデータとペイロード検査を分離することで、ゲートウェイはバックエンドシステムをペイロードにさらすことなく攻撃の特徴を記録・分析できます。

### 2. セッション隔離とデータ保護の設計
応答の最小化とトークン化による制御:

* **応答内容の最小開示**: 未認証の送信元に対して不要な応答情報を返さないことで、自動スキャンや偵察ツールが利用できる情報を制限します。
* **認証失敗時のセッション分離**: 認証に繰り返し失敗するノードを分離された処理経路へルーティングし、検証済みセッションに割り当てられたリソースを消費させないようにします（応答タイミング制御の詳細はTechnical Paper #013を参照）。
* **インライン型データトークン化**: 機密データフィールドは信頼境界を離れる前に復元不能なトークンへ置き換えられ、下流システムが侵害された場合の露出を制限します。

### 3. ポリシー設定・検査・拒否
リバースプロキシ適用のための3段階の展開:

1. **ベースラインポリシーの設定**: CASBと連携する各クラウドサービスについて、許可リスト、認証要件、トークン化ルールを定義します。
2. **リアルタイムトラフィック検査**: 着信・発信トラフィックを設定済みポリシーと照合し、認証またはデータ取り扱い要件を満たさないリクエストを検出します。
3. **自動拒否とログ記録**: 非準拠のリクエストを境界で拒否し、関連するセキュリティイベントとの相関分析のためにログを記録します（SIEM連携の詳細はTechnical Paper #002を参照）。

### 4. 偵察コストと伝播の制御
リソース保全と脅威の封じ込め:

* **非準拠リクエストへの応答制限**: 不正な形式や未認証のリクエストの処理を見送ることで、偵察・スキャン活動への対応に費やすリソースを削減します。
* **悪意あるコンテンツの伝播防止**: 既知の悪意あるペイロードパターンを除去またはブロックするようプロキシを設定し、CASBがマルウェアやスクリプトの媒介とならないようにします。
* **ポリシー適用状況の定期レビュー**: CASBのポリシー適用状況を定めたレビュー周期で確認し、コンプライアンス報告とインシデント調査を裏付ける記録を残します。

### 5. 結論
バックエンドロジックに取り込むのではなく、プロキシの段階で未認証トラフィックを拒否することにより、CISSPドメイン3およびCASP+の観点からも説明可能なCASBの既定姿勢を保てます。

インライン型トークン化はさらにもう一層の防御を加え、検査を通過したトラフィックであっても、下流で傍受された場合に直接的な価値を持つデータを含まない状態にします。
