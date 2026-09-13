# Koki's Technical Paper #030

## Access Control — Implementing Least Privilege in Life, Identity and Access Management, and Ingestion Governance

### Summary Digest
This paper defines an access-control model combining Role-Based
Access Control (RBAC) and need-to-know restrictions, aligned with
CISSP Domain 5 and NIST SP 800-53 access-control practices.

Access requests are evaluated against defined roles and attributes
before being granted, consistent with default-deny rather than
implicit trust.

---
### 1. Implicit Trust Exposure
Structural Vulnerabilities of Undefined Access Models:

* **Undifferentiated Access Once Authenticated**: Systems that grant broad access after a single authentication step, without further role-based restriction, allow an authenticated but low-privilege user to reach resources beyond their actual need.
* **Absence of Need-to-Know Enforcement**: Without a documented need-to-know criterion, sensitive internal data sets may be visible to personnel whose role does not actually require that visibility.
* **Social-Engineering Exploitation of Undefined Roles**: When authorization does not follow a defined role structure, an attacker impersonating a plausible-sounding role can more easily obtain access that a properly scoped RBAC model would have denied.

### 2. RBAC and Need-to-Know Foundation
Role Definitions and Attribute-Based Refinement:

* **Least-Privilege Role Assignment**: Each role is granted only the permissions required for its defined function, consistent with the least-privilege principle in CISSP Domain 5.
* **Need-to-Know Data Segmentation**: Access to sensitive data sets requires a documented, verifiable justification tied to the requester's role, rather than being available to any authenticated user.
* **Attribute-Based Access Refinement**: Where role alone is insufficient, access decisions incorporate additional attributes such as time, location, or request context, consistent with the Attribute-Based Access Control (ABAC) model defined in NIST SP 800-162.
  
### 3. Access List and Session Control Sequence
ACL Configuration, Request Evaluation, and Isolation:

1. **Access Control List Configuration**: Permitted roles and their associated permissions are compiled into access control lists, consistent with the baseline boundary controls defined in Technical Paper #001.
2. **Per-Request Authorization Evaluation**: Each incoming request is evaluated against the applicable role and attribute policy before access is granted, rather than relying on a single session-level check.
3. **Endpoint Segregation and Air-Gapping**: Internal administrative logs are structurally separated from externally facing endpoints, consistent with the human-oversight boundaries defined in Technical Paper #018.

### 4. Session Governance and Revocation Review
Token Lifecycle and Continuous Policy Auditing:

* **Automated Session Token Revocation**: Access tokens are automatically invalidated when an anomaly is detected or a defined session duration expires, rather than remaining valid indefinitely once issued.
* **Migration from Static to Continuous Checks**: Access enforcement moves from a single point-in-time grant toward inline validation at each request, consistent with the continuous-verification approach defined in Technical Paper #008.
* **Continuous RBAC and ACL Auditing**: Role definitions and access control lists are reviewed on a defined cadence to identify permissions that no longer match a role's actual current responsibilities.

### 5. Conclusion
An access-control model only works if roles stay current, since a role
that no longer matches someone's job quietly becomes an
unnecessary grant of access.

Reviewing RBAC assignments and access lists on a defined schedule,
per CISSP Domain 5 and NIST SP 800-53, keeps least privilege from
eroding over time.

---
# テクニカルペーパーシリーズ #030

## アクセス制御 — 最小権限原則の実装､アイデンティティ・アクセス管理､およびデータ取込統制ガバナンス

### サマリー・ダイジェスト
本論文は､CISSPドメイン5およびNIST SP 800-53のアクセス制御実務に
準拠した､ロールベースアクセス制御RBACとニード・トゥ・ノウの制限
を組み合わせたアクセス制御モデルを定義します｡

アクセス要求は､暗黙の信頼ではなくデフォルト拒否の姿勢と整合する形
で､権限を付与される前に定義済みのロールおよび属性と照合されます｡

---
### 1. 暗黙的信頼への露出
未定義のアクセスモデルに伴う構造的脆弱性:

* **認証後の無差別なアクセス**: 単一の認証ステップの後にロールベースの制限を追加せず広範なアクセスを許可するシステムは､認証済みだが低権限のユーザーが実際の必要範囲を超えたリソースに到達することを許してしまいます｡
* **ニード・トゥ・ノウ原則の未適用**: 文書化されたニード・トゥ・ノウ基準がなければ､機密性の高い内部データセットが､その可視性を実際には必要としない役割の担当者にも見える状態になり得ます｡
* **未定義のロールを狙ったソーシャルエンジニアリング**: 認可が定義済みのロール構造に従っていない場合､もっともらしいロールを装った攻撃者が､適切に設計されたRBACモデルであれば拒否されるはずのアクセスをより容易に得てしまいます｡

### 2. RBACとニード・トゥ・ノウの基盤
ロール定義と属性による精緻化:

* **最小権限に基づくロール割り当て**: 各ロールには､CISSPドメイン5の最小権限原則に沿って､その定義された機能に必要な権限のみが付与されます｡
* **ニード・トゥ・ノウによるデータのセグメント化**: 機密データセットへのアクセスには､認証済みユーザーであれば誰でも利用可能というのではなく､要求者のロールに紐づく文書化された検証可能な正当性が必要とされます｡
* **属性に基づくアクセスの精緻化**: ロールのみでは不十分な場合､アクセス判断には時間・場所・リクエストの文脈といった追加の属性が組み込まれます｡これはNIST SP 800-162で定義されている属性ベースアクセス制御ABACモデルと整合します｡

### 3. アクセスリストとセッション制御の手順
ACL設定・リクエスト評価・隔離:

1. **アクセス制御リストの設定**: 許可されたロールとそれに紐づく権限は､Technical Paper #001で定義したベースライン境界統制と整合する形でアクセス制御リストへ集約されます｡
2. **リクエスト単位での認可評価**: 着信する各リクエストは､単一のセッションレベルのチェックに頼るのではなく､アクセスが許可される前に該当するロールおよび属性ポリシーと照合されます｡
3. **エンドポイントの分離とエアギャップ化**: 内部の管理ログは､Technical Paper #018で定義した人的監視の境界と整合する形で､外部向けのエンドポイントから構造的に分離されます｡

### 4. セッションガバナンスと失効レビュー
トークンのライフサイクルと継続的なポリシー監査:

* **自動化されたセッショントークンの失効**: アクセストークンは､発行後に無期限で有効であり続けるのではなく､異常が検知された場合や定義済みのセッション期間が経過した場合に自動的に無効化されます｡
* **静的チェックから継続的チェックへの移行**: アクセス適用は､単一時点での許可からリクエストごとのインライン検証へと移行します｡これはTechnical Paper #008で定義した継続的検証アプローチと整合します｡
* **RBACおよびACLの継続的監査**: ロール定義とアクセス制御リストは定められた周期でレビューされ､そのロールの実際の現在の職責と一致しなくなった権限を特定します｡

### 5. 結論
アクセス制御モデルが機能するのは､ロールが最新の状態に保たれている場
合に限られます｡実際の職務と一致しなくなったロールは､気づかぬうちに
不要なアクセス権限の付与となってしまうためです｡

CISSPドメイン5およびNIST SP 800-53に沿い､RBACの割り当てとアク
セス制御リストを定められたスケジュールでレビューすることが､最小権限
の形骸化を防ぎます｡
