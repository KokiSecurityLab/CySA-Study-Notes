# Koki's Technical Paper #024

## AI "Soul" Design — Cognitive Synchronization and Context Window Integrity, Configuration Baseline Assurance, and Session State Governance

### Summary Digest
This paper defines a configuration-baseline framework for deployed AI systems, aligned with CISSP Domain 3 and NIST AI RMF, verifying instructions and context state stay consistent across sessions and nodes.

Indirect prompt injection and context poisoning are treated as configuration-drift conditions, detected through baseline hashing rather than content-level filtering alone.

---
### 1. Configuration Drift Exposure
Structural Risks of Inconsistent System State Across Sessions:

* **Context Window Persistence of Injected Instructions**: Content embedded in retrieved documents or prior conversation turns can persist within the context window and continue to influence model behavior across multiple turns, a risk distinct from a single malicious prompt.
* **Configuration Inconsistency Across Inference Nodes**: Deployments that serve the same model from multiple nodes without a shared, versioned configuration source can silently apply different system instructions or guardrail policies depending on which node handles a given request.
* **Undetected Drift Between Deployed and Documented Configuration**: Without a verified baseline, a system prompt or policy change applied directly in production can diverge from what is documented, leaving no reliable record of the system's actual configured behavior.

### 2. Baseline Hashing Foundation
Configuration Fingerprinting and Cross-Node Consistency:

* **Cryptographic Configuration Fingerprinting**: The system instructions, guardrail policy set, and model version in use are hashed to produce a verifiable fingerprint, consistent with the baseline-hashing approach defined in Technical Paper #001.
* **Cross-Node Configuration Reconciliation**: All inference nodes serving a given deployment are checked against the same configuration fingerprint, so that a request routed to any node receives a consistent system state.
* **Session-Scoped Context Tracking**: The context window's accumulated content is tracked separately from the verified system-instruction baseline, so that persisted conversational content cannot be mistaken for part of the trusted configuration.

### 3. Fingerprint Verification Sequence
Capture, Compare, and Reset on Mismatch:

1. **Configuration Fingerprint Capture**: At deployment time, a fingerprint of the verified system instructions and guardrail configuration is generated and stored as the reference baseline.
2. **Per-Session Fingerprint Comparison**: At session start and at defined intervals, the active configuration fingerprint is compared against the stored baseline across all serving nodes.
3. **Automated Session Reset on Mismatch**: A session whose fingerprint no longer matches the baseline is terminated and reinitialized from the verified configuration, consistent with the automated-remediation approach defined in Technical Paper #016.

### 4. Context Window Trust Boundaries
Separating Verified Configuration From Accumulated Content:

* **System Instructions Isolated From Retrieved Content**: The verified system-instruction baseline is kept structurally separate from retrieved documents and prior turns within the context window, so accumulated content cannot silently override verified configuration.
* **Restricted Configuration Change Path**: Changes to system instructions or guardrail policy are applied only through the same version-controlled deployment process defined in Technical Paper #021, not through in-session modification.
* **Continuous Fingerprint Drift Auditing**: Ongoing review of fingerprint-mismatch events across nodes and sessions functions as a detective control, identifying deployments where configuration is drifting more frequently than expected.

### 5. Conclusion
A model's context window can accumulate influence from retrieved content and prior turns in ways that a single-prompt injection filter does not fully cover.

Verifying the underlying configuration fingerprint, consistent with CISSP Domain 3 and NIST AI RMF, catches that drift independently of whatever the visible conversation content contains.

---
# テクニカルペーパーシリーズ　#024

## AI「ソウル」設計 — 認知同期とコンテキストウィンドウの整合性、構成ベースラインの保証、およびセッション状態のガバナンス

### サマリー・ダイジェスト
本論文は、CISSPドメイン3およびNIST AI RMFに準拠した構成ベースラインフレームワークを定義し、システム指示とコンテキスト状態がセッションおよびノード間で一貫していることを検証します。

間接的なプロンプトインジェクションとコンテキストポイズニングは、コンテンツレベルのフィルタリングだけに頼るのではなく、ベースラインハッシュを通じて検知される構成ドリフトの一種として扱われます。

---
### 1. 構成ドリフトへの露出
セッション間でのシステム状態の不一致に伴う構造的リスク:

* **コンテキストウィンドウに残留する注入済み指示**: 取得された文書や過去の会話ターンに埋め込まれた内容はコンテキストウィンドウ内に残留し、単発の悪意あるプロンプトとは異なり、複数ターンにわたってモデルの挙動に影響を与え続ける可能性があります。
* **推論ノード間での構成の不一致**: 同一モデルを複数ノードから提供する構成で、共有されたバージョン管理済みの構成ソースを持たない場合、どのノードがリクエストを処理するかによって異なるシステム指示やガードレールポリシーが気づかぬうちに適用される可能性があります。
* **デプロイ済み構成と文書化された構成の間の未検知ドリフト**: 検証済みのベースラインがなければ、本番環境で直接適用されたシステムプロンプトやポリシーの変更が文書化された内容から乖離し、システムの実際の設定挙動についての信頼できる記録が残らなくなります。

### 2. ベースラインハッシュの基盤
構成のフィンガープリント化とノード間の一貫性:

* **暗号学的な構成フィンガープリント化**: 使用中のシステム指示、ガードレールポリシーセット、モデルバージョンをハッシュ化して検証可能なフィンガープリントを生成します。これはTechnical Paper #001で定義したベースラインハッシュのアプローチと整合します。
* **ノード間での構成の突き合わせ**: あるデプロイを提供するすべての推論ノードを同一の構成フィンガープリントと照合し、どのノードへルーティングされたリクエストも一貫したシステム状態を受け取れるようにします。
* **セッション単位でのコンテキスト追跡**: コンテキストウィンドウに蓄積された内容は、検証済みのシステム指示ベースラインとは別に追跡され、蓄積された会話内容が信頼済み構成の一部と誤認されないようにします。

### 3. フィンガープリント検証の手順
取得・比較・不一致時のリセット:

1. **構成フィンガープリントの取得**: デプロイ時に、検証済みのシステム指示とガードレール構成のフィンガープリントを生成し、参照ベースラインとして保存します。
2. **セッションごとのフィンガープリント比較**: セッション開始時および定義済みの間隔で、稼働中の構成フィンガープリントを、提供中の全ノードにわたって保存済みのベースラインと比較します。
3. **不一致時の自動セッションリセット**: フィンガープリントがベースラインと一致しなくなったセッションは終了され、検証済み構成から再初期化されます。これはTechnical Paper #016で定義した自動修復アプローチと整合します。

### 4. コンテキストウィンドウの信頼境界
検証済み構成と蓄積されたコンテンツの分離:

* **取得コンテンツからのシステム指示の隔離**: 検証済みのシステム指示ベースラインは、コンテキストウィンドウ内の取得文書や過去のやり取りとは構造的に分離されており、蓄積されたコンテンツが検証済み構成を気づかぬうちに上書きすることはありません。
* **構成変更経路の制限**: システム指示やガードレールポリシーの変更は、セッション内での修正ではなく、Technical Paper #021で定義したものと同一のバージョン管理されたデプロイプロセスを通じてのみ適用されます。
* **フィンガープリントドリフトの継続的監査**: ノードおよびセッション全体にわたるフィンガープリント不一致イベントを継続的にレビューすることは検知的統制として機能し、想定より頻繁に構成がドリフトしているデプロイを特定します。

### 5. 結論
モデルのコンテキストウィンドウは、取得された文書や過去のやり取りからの影響を蓄積し得るため、単一のプロンプトインジェクションフィルターだけでは十分に捉えきれません。

基盤となる構成のフィンガープリントを検証することは、CISSPドメイン3およびNIST AI RMFに沿いつつ、目に見える会話内容が何であってもそのドリフトを独立して検知します。
