# Koki's Technical Paper #044

## Zero-Trust Mesh — Service Mesh mTLS Enforcement, Mesh-Wide Authorization Policy, and Anomaly-Triggered Quarantine

### Summary Digest
This paper defines a service-mesh security architecture, aligned with CISSP Domain 4 and the workload-identity approach in Technical Paper #035, enforcing mutual TLS through a sidecar proxy rather than application code.

Mesh-wide authorization policies and anomaly-triggered quarantine, consistent with Technical Paper #008, contain lateral movement without a single centralized gatekeeper.

---
### 1. Centralized Mesh Control Risk
Structural Vulnerabilities of Single-Point Mesh Authority:

* **Single Control-Plane Dependency**: A mesh architecture that routes every authorization decision through one centralized control-plane node creates a single point of failure whose compromise or outage affects every service in the mesh.
* **Inconsistent Per-Service mTLS Adoption**: Requiring each development team to implement mutual TLS individually in application code produces inconsistent coverage, since some services may be misconfigured or skipped entirely.
* **Undetected Lateral Movement Between Trusted Services**: Without mesh-wide behavioral monitoring, a compromised service can communicate with any other service it has network reachability to, since service-to-service trust alone does not account for anomalous request patterns.

### 2. Sidecar Proxy and Mesh Policy Foundation
mTLS Sidecar Enforcement and Authorization Policy Principles:

* **Sidecar Proxy mTLS Termination**: A sidecar proxy deployed alongside each service handles mutual TLS negotiation and certificate presentation, consistent with the workload identities issued under the approach defined in Technical Paper #035, without requiring changes to application code.
* **Mesh-Wide Authorization Policy**: Access between services is governed by centrally defined but locally enforced authorization policies, specifying exactly which services may call which others, consistent with the least-privilege principle in CISSP Domain 5.
* **Alignment with Micro-Segmentation Controls**: Mesh authorization boundaries are reconciled with the micro-segmentation approach defined in Technical Paper #008, keeping service-to-service policy consistent with the wider zero-trust architecture.

### 3. Policy Enforcement and Quarantine Sequence
Sidecar Injection, Policy Evaluation, and Isolation:

1. **Automatic Sidecar Injection**: Each service instance is automatically paired with a sidecar proxy at deployment time, consistent with the deployment-approval process defined in Technical Paper #021.
2. **Per-Request Policy Evaluation**: Each service-to-service request is evaluated against the applicable mesh authorization policy by the sidecar before being forwarded, rather than trusted based on network location alone.
3. **Anomaly-Triggered Quarantine**: A service exhibiting request patterns inconsistent with its established baseline is automatically isolated from the mesh pending review, consistent with the behavioral-anomaly approach defined in Technical Paper #013.

### 4. Mesh Governance and Control-Plane Resilience
Control-Plane Redundancy and Policy Audit Review:

* **Redundant Control-Plane Deployment**: The mesh control plane is deployed with redundancy across multiple instances, so that a single control-plane node failure does not disable policy enforcement mesh-wide.
* **Separation of Data Plane from Control Plane**: Sidecar proxies continue enforcing their last-known policy even during a temporary control-plane disruption, consistent with the fail-safe principle rather than failing open.
* **Continuous Authorization Policy Auditing**: Mesh authorization policies are reviewed on a defined cadence to identify overly permissive rules or services that no longer require a previously granted communication path.

### 5. Conclusion
Enforcing mutual TLS through a sidecar proxy, rather than in each service's own code, makes consistent mesh-wide coverage achievable across independently developed services.

Pairing that with anomaly-triggered quarantine, consistent with CISSP Domain 4 and Technical Papers #008 and #013, contains lateral movement without a single centralized authority.

---
# テクニカルペーパーシリーズ #044

## ゼロトラスト・メッシュ — サービスメッシュにおけるmTLS適用、メッシュ全体の認可ポリシー、および異常検知に基づく隔離

### サマリー・ダイジェスト
本論文は、CISSPドメイン4および テクニカルペーパーシリーズ #035 のワークロードアイデンティティに準拠したサービスメッシュアーキテクチャを定義し、アプリケーションコードではなくサイドカープロキシで相互TLSを適用します。

メッシュ全体の認可ポリシーと異常検知に基づく隔離は、テクニカルペーパーシリーズ #008 と整合し、単一の中央集権的なゲートキーパーに頼らず横方向の移動を封じ込めます。

---
### 1. 中央集権的メッシュ制御のリスク
単一権限型メッシュ統制に伴う構造的脆弱性:

* **単一のコントロールプレーン依存**: すべての認可判断を単一の中央集権的なコントロールプレーンノード経由で処理するメッシュアーキテクチャは、その侵害や停止がメッシュ内の全サービスに影響する単一障害点を生み出します。
* **サービスごとに一貫しないmTLS導入**: 各開発チームにアプリケーションコード内で個別に相互TLSを実装させると、一部のサービスが誤設定されたり実装自体が省略されたりして、カバレッジが不均一になります。
* **信頼されたサービス間での検知されない横方向移動**: メッシュ全体での行動監視がなければ、侵害されたサービスはネットワーク到達可能な他のあらゆるサービスと通信できてしまいます。サービス間の信頼だけでは異常なリクエストパターンを考慮できないためです。

### 2. サイドカープロキシとメッシュポリシーの基盤
mTLSサイドカー適用と認可ポリシーの原則:

* **サイドカープロキシによるmTLS終端**: 各サービスに併設されたサイドカープロキシが相互TLSのネゴシエーションと証明書提示を処理します。これは テクニカルペーパーシリーズ #035 で定義したアプローチに基づいて発行されたワークロードアイデンティティと整合し、アプリケーションコードの変更を必要としません。
* **メッシュ全体の認可ポリシー**: サービス間のアクセスは、中央で定義されローカルで適用される認可ポリシーによって統治され、どのサービスがどの他サービスを呼び出せるかを正確に規定します。これはCISSPドメイン5の最小権限原則と整合します。
* **マイクロセグメンテーション統制との整合**: メッシュの認可境界は テクニカルペーパーシリーズ #008 で定義したマイクロセグメンテーションアプローチと突き合わされ、サービス間ポリシーをより広いゼロトラストアーキテクチャと一貫させます。

### 3. ポリシー適用と隔離の手順
サイドカー注入・ポリシー評価・隔離:

1. **自動サイドカー注入**: 各サービスインスタンスは、テクニカルペーパーシリーズ #021 で定義したデプロイ承認プロセスと整合する形で、デプロイ時に自動的にサイドカープロキシと組み合わされます。
2. **リクエスト単位のポリシー評価**: サービス間の各リクエストは、単にネットワーク上の所在地に基づいて信頼されるのではなく、転送前にサイドカーによって該当するメッシュ認可ポリシーと照合されます。
3. **異常検知に基づく隔離**: 確立されたベースラインと整合しないリクエストパターンを示すサービスは、テクニカルペーパーシリーズ #013 で定義した行動異常アプローチと整合する形で、レビューを待つ間メッシュから自動的に隔離されます。

### 4. メッシュガバナンスとコントロールプレーンの耐障害性
コントロールプレーンの冗長性とポリシー監査レビュー:

* **冗長化されたコントロールプレーンの展開**: メッシュのコントロールプレーンは複数インスタンスにわたる冗長構成でデプロイされ、単一のコントロールプレーンノードの障害がメッシュ全体のポリシー適用を無効化することはありません。
* **データプレーンとコントロールプレーンの分離**: サイドカープロキシは、フェイルオープンではなくフェイルセーフの原則と整合し、一時的なコントロールプレーンの障害中も直近の既知のポリシーを適用し続けます。
* **認可ポリシーの継続的監査**: メッシュの認可ポリシーは定められた周期でレビューされ、過度に許可的なルールや、以前付与された通信経路をもはや必要としないサービスを特定します。

### 5. 結論
各サービス自身のコードにではなく、サイドカープロキシを通じて相互TLSを適用することが、独立して開発された多数のサービス全体で一貫したメッシュ全体のカバレッジを実現可能にします。

これに異常検知に基づく隔離を組み合わせることは、CISSPドメイン4 および テクニカルペーパーシリーズ #008・#013 に沿いつつ、単一の中央集権的な権限に依存せずに横方向の移動を封じ込めます。
