# Koki's Technical Paper #035

## Zero Trust Life — Sovereignty Through Verification, Cryptographic Identity Assertion, and Context-Aware Ingestion Perimeters

### Summary Digest
This paper defines a workload-identity verification framework for service-to-service communication, aligned with CISSP Domain 4, NIST SP 800-207, and the SPIFFE/SPIRE workload-identity standard.

Mutual TLS with short-lived, cryptographically verifiable service identities replaces network-location-based trust between internal services.

---
### 1. Implicit Network-Location Trust Risk
Structural Vulnerabilities of Perimeter-Based Service Trust:

* **Trust Based on Network Location Alone**: Internal services that trust a request simply because it originates from inside the network perimeter allow any component that reaches that network segment to communicate freely with sensitive backend services.
* **Long-Lived Static Service Credentials**: Services authenticating to one another with long-lived, static credentials or shared secrets create a persistent target that, once obtained, remains valid until manually rotated.
* **Undifferentiated Lateral Communication**: Without service-level identity verification, a compromised service can communicate with any other reachable service on the same network segment, expanding the impact of a single compromise.

### 2. Workload Identity and mTLS Foundation
SPIFFE/SPIRE Identity Issuance and Mutual Authentication:

* **SPIFFE-Based Workload Identity**: Each service is issued a cryptographically verifiable identity document consistent with the SPIFFE (Secure Production Identity Framework For Everyone) standard, rather than being identified only by network address.
* **Mutual TLS Between Services**: Service-to-service connections require both parties to present and verify a valid identity certificate, consistent with mutual TLS (mTLS), rather than authenticating only the server side of the connection.
* **Alignment with Zero-Trust Session Verification**: Workload identity verification is reconciled with the continuous, per-request verification approach defined in Technical Paper #008, extending zero-trust principles from user sessions to service-to-service traffic.

### 3. Identity Issuance and Rotation Sequence
Certificate Issuance, Short-Lived Rotation, and Verification:

1. **Automated Identity Issuance**: A workload identity provider, consistent with the SPIRE reference implementation, issues short-lived identity certificates to services at startup based on verified attestation of the workload itself.
2. **Scheduled Certificate Rotation**: Identity certificates are rotated automatically on a short, defined interval, reducing the window during which a stolen certificate would remain valid.
3. **Per-Connection Mutual Verification**: Each new connection between services triggers mutual certificate verification before any application data is exchanged, rather than relying on a session established once and reused indefinitely.

### 4. Service Identity Governance and Segmentation
Communication Policy and Certificate Lifecycle Review:

* **Default-Deny Service Communication Policy**: Services are permitted to communicate only with explicitly authorized peers under a default-deny policy, consistent with the default-deny approach defined in Technical Paper #001.
* **Segmented Failure Domains**: Services are grouped into isolated segments so that a compromise of one service's identity does not automatically grant reach into unrelated segments.
* **Continuous Certificate and Policy Auditing**: Issued identities and communication policies are reviewed on a defined cadence to revoke unused identities and correct overly broad communication permissions.

### 5. Conclusion
A service that trusts a caller based on network location, rather than a cryptographic proof of identity, is still running on implicit trust.

Replacing network location with SPIFFE-based workload identity and mutual TLS, per CISSP Domain 4 and NIST SP 800-207, extends zero-trust verification to service-to-service traffic.

---
# テクニカルペーパーシリーズ #035

## ゼロトラスト・ライフ — 検証による主権確立、暗号学的アイデンティティアサーション、およびコンテキスト認識型データ取込境界

### サマリー・ダイジェスト
本論文は、CISSPドメイン4、NIST SP 800-207、およびSPIFFE/SPIREワークロードアイデンティティ標準に準拠した、サービス間通信のためのワークロードアイデンティティ検証フレームワークを定義します。

短命で暗号学的に検証可能なサービスアイデンティティを用いた相互TLSが、ネットワークの所在地に基づく内部サービス間の信頼を置き換えます。

---
### 1. 暗黙的なネットワーク所在地信頼のリスク
境界型サービス信頼に伴う構造的脆弱性:

* **ネットワーク所在地のみに基づく信頼**: リクエストが単にネットワーク境界の内側から発信されたという理由だけで信頼する内部サービスは、そのネットワークセグメントに到達できるあらゆるコンポーネントが機密性の高いバックエンドサービスと自由に通信することを許してしまいます。
* **長寿命な静的サービス資格情報**: 長寿命の静的資格情報や共有シークレットを用いてサービス間で相互認証を行うと、一度取得されれば手動でローテーションされるまで有効であり続ける持続的な標的が生まれます。
* **無差別な横方向の通信**: サービスレベルのアイデンティティ検証がなければ、侵害されたサービスは同じネットワークセグメント上の到達可能な他のあらゆるサービスと通信でき、単一の侵害の影響範囲が拡大します。

### 2. ワークロードアイデンティティとmTLSの基盤
SPIFFE/SPIREによるアイデンティティ発行と相互認証:

* **SPIFFEに基づくワークロードアイデンティティ**: 各サービスには、ネットワークアドレスのみで識別されるのではなく、SPIFFE（Secure Production Identity Framework For Everyone）標準に準拠した暗号学的に検証可能なアイデンティティ文書が発行されます。
* **サービス間の相互TLS**: サービス間通信では、接続の一方のみを認証するのではなく、相互TLS（mTLS）に準拠して双方が有効なアイデンティティ証明書を提示・検証することが求められます。
* **ゼロトラストのセッション検証との整合**: ワークロードアイデンティティ検証を テクニカルペーパーシリーズ　#008　で定義した継続的なリクエスト単位の検証アプローチと突き合わせ、ゼロトラストの原則をユーザーセッションからサービス間通信にまで拡張します。

### 3. アイデンティティ発行とローテーションの手順
証明書発行・短命ローテーション・検証:

1. **自動化されたアイデンティティ発行**: SPIREのリファレンス実装と整合するワークロードアイデンティティプロバイダが、起動時にワークロード自体の検証済みアテステーションに基づいて短命のアイデンティティ証明書をサービスへ発行します。
2. **定期的な証明書ローテーション**: アイデンティティ証明書は短く定義された間隔で自動的にローテーションされ、盗まれた証明書が有効であり続ける期間を短縮します。
3. **接続ごとの相互検証**: サービス間の新規接続はそれぞれ、一度確立されたセッションを無期限に再利用するのではなく、アプリケーションデータが交換される前に相互証明書検証を発生させます。

### 4. サービスアイデンティティのガバナンスとセグメント化
通信ポリシーと証明書ライフサイクルのレビュー:

* **デフォルト拒否型のサービス通信ポリシー**: サービスは、テクニカルペーパーシリーズ　#001　で定義したデフォルト拒否アプローチと整合する形で、明示的に許可された通信相手とのみ通信を許されます。
* **セグメント化された障害ドメイン**: サービスは隔離されたセグメントにグループ化され、あるサービスのアイデンティティが侵害されても、無関係なセグメントへの到達が自動的に許されることはありません。
* **証明書とポリシーの継続的監査**: 発行済みのアイデンティティと通信ポリシーは定められた周期でレビューされ、未使用のアイデンティティを失効させ、過度に広範な通信許可を是正します。

### 5. 結論
呼び出し元のネットワーク上の所在地に基づいて信頼するサービスは、暗号学的なアイデンティティの証明に基づいていない限り、依然として暗黙の信頼の上で動作していることになります。

ネットワークの所在地を、SPIFFEに基づくワークロードアイデンティティと相互TLSに置き換えることは、CISSPドメイン4およびNIST SP 800-207に沿いつつ、ゼロトラスト検証をサービス間通信にまで拡張します。
