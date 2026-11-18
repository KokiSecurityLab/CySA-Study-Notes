# Koki's Technical Paper #001

## FIM & Tripwires — File Integrity Monitoring, Ingestion Auditing, and Perimeter Intrusion Detection Systems

### Summary Digest
This paper defines a File Integrity Monitoring (FIM) and tripwire framework, aligned with CISSP Domain 7 and CySA+ security-operations practices, to detect unauthorized changes and configuration drift on perimeter systems.

Cryptographic baseline hashing and default-deny controls enable continuous validation of file changes, so modifications made outside an approved change process are flagged before they reach production systems.

---
### 1. Ingress Vulnerability Assessment
Structural Risks of Perimeter Configuration Drift and Unauthorized Access:

* **Unmonitored Configuration Drift**: Systems that do not track changes to configuration files on perimeter devices, such as firewall rule sets and remote-access settings, cannot distinguish an approved change from an attacker quietly weakening a control.
* **Unauthorized Registry and System File Modification**: Attackers modify the Windows Registry (MITRE ATT&CK T1112) and system files in predictable locations to establish persistence or disable defenses, and a firewall alone does not inspect those changes.
* **Self-Modifying Malware Evading Signatures**: In November 2025, Google Threat Intelligence Group reported PROMPTFLUX, an experimental malware family that uses an LLM API to rewrite its own source code and saves each new version to the Startup folder for persistence; signature-based detection struggles against code that keeps changing, but a write to a monitored Startup folder remains a detectable file event.

### 2. Cryptographic Baseline Hashing
Cryptographic Baseline Verification and Access Control Alignment:

* **SHA-256 Baseline Hashing**: Each monitored file is recorded with a SHA-256 hash along with attributes such as owner, permissions, and size, so any later change to its content or metadata appears as a measurable difference from the baseline.
* **Default-Deny Policy Enforcement**: Perimeter access moves from a permissive posture to a default-deny posture, so only explicitly authorized connections and changes reach protected assets, which limits how many events the FIM baseline must explain.
* **Control Framework Alignment**: The approach maps to NIST SP 800-53 control SI-7 (Software, Firmware, and Information Integrity) and to PCI DSS v4.0 Requirement 11.5.2, which calls for a change-detection mechanism such as FIM on critical files, supporting the security operations objectives of CISSP Domain 7.

### 3. Staged Integrity Verification Sequence
Three-Stage Deployment for File Integrity Tracking:

* **Baseline Configuration Capture**: Hashes and attributes for trusted system binaries, configuration files, and persistence locations such as Startup folders and scheduled-task directories are captured on a known-good system and stored where the monitored host cannot alter them.
* **Continuous Integrity Monitoring**: Tools such as the Wazuh FIM module, which supports real-time monitoring, or scheduled scanners such as AIDE compare current file states against the baseline, with high-risk paths watched in real time and the rest scanned often enough to meet the PCI DSS minimum of at least weekly comparison.
* **Alert Triage and Automated Response**: Each detected change is checked against approved change records, unexplained changes raise an alert, and files confirmed as malicious can be quarantined or removed through automated actions such as Wazuh Active Response, pending analyst review.

### 4. Trust-Boundary Enforcement
Trust-Boundary Enforcement and System Integrity Maintenance:

* **From Integrity Tracking to a Defensive Control**: Linking FIM alerts to the change-management process turns integrity tracking into an enforcement point, because every change must either match an approved change or be investigated.
* **Protecting the Baseline Itself**: The baseline database and the FIM agent's configuration are protected from modification by the hosts they monitor, since an attacker who can rewrite the baseline can make any change look approved.
* **Continuous Provenance Auditing**: Records of who changed which file, when, and through which process are retained as an audit trail, functioning as a detective control that supports compliance and incident-response requirements.

### 5. Conclusion
Continuous file-integrity monitoring, tied to SHA-256 baseline hashing, gives CISSP Domain 7 security operations an early signal when protected files change outside an approved process, including writes to persistence locations such as Startup folders.

Default-deny access control at the perimeter keeps that signal meaningful by limiting how much unauthenticated traffic ever reaches the monitored files, so each alert is more likely to reflect a real problem, consistent with CySA+ practice.

---
# テクニカルペーパーシリーズ #001

## FIM＆トリップワイヤー — ファイル整合性監視、取り込み監査、および境界侵入検知

### サマリー・ダイジェスト
本論文は、CISSPドメイン7およびCySA+のセキュリティ運用実務に準拠したファイル整合性監視（FIM）とトリップワイヤーの枠組みを定義し、境界システムにおける不正な変更と構成ドリフトの検出を図るものです。

暗号学的なベースラインハッシュとデフォルト拒否型のアクセス制御によりファイルの変更を継続的に検証し、承認された変更プロセス以外で行われた変更を、本番環境に到達する前に検出します。

---
### 1. 入力脆弱性評価
境界における構成ドリフトと不正アクセスに伴う構造的リスク:

* **未監視の構成ドリフト**: ファイアウォールのルールセットやリモートアクセス設定など、境界機器の構成ファイルへの変更を追跡していないシステムは、承認された変更と、攻撃者がひそかに統制を弱める変更とを区別できません。
* **レジストリとシステムファイルの不正な改ざん**: 攻撃者は、永続化の確立や防御の無効化のために、Windowsレジストリ（MITRE ATT&CK T1112）や決まった場所にあるシステムファイルを改ざんします。こうした変更は、ファイアウォールだけでは検査されません。
* **シグネチャを回避する自己改変型マルウェア**: Google Threat Intelligence Groupは2025年11月、LLMのAPIを使って自らのソースコードを書き換え、新しい版をスタートアップフォルダーに保存して永続化を図る実験的なマルウェア「PROMPTFLUX」を報告しました。コードが変わり続けるとシグネチャによる検知は難しくなりますが、監視対象のスタートアップフォルダーへの書き込みは、ファイルイベントとして検知できます。

### 2. 暗号学的ベースラインハッシュ
暗号学的ベースライン検証とアクセス制御の整合:

* **SHA-256によるベースラインハッシュ**: 監視対象の各ファイルは、所有者、権限、サイズなどの属性とともにSHA-256ハッシュで記録されます。その後の内容やメタデータの変更は、ベースラインとの測定可能な差分として現れます。
* **デフォルト拒否ポリシーの適用**: 境界のアクセスを許可的な状態からデフォルト拒否の状態へ移行させ、明示的に承認された接続と変更のみが保護対象資産に到達するようにします。これにより、FIMのベースラインが説明すべきイベントの数を抑えます。
* **統制フレームワークとの整合**: 本アプローチは、NIST SP 800-53の統制SI-7（ソフトウェア、ファームウェア、および情報の完全性）と、重要ファイルに対するFIMなどの変更検知メカニズムを求めるPCI DSS v4.0の要件11.5.2に対応しており、CISSPドメイン7のセキュリティ運用の目的を支えます。

### 3. 整合性検証の段階的手順
ファイル整合性追跡のための3段階の展開:

* **ベースライン構成の取得**: 信頼できるシステムバイナリ、構成ファイル、およびスタートアップフォルダーやスケジュールタスクのディレクトリといった永続化に使われる場所について、既知の正常なシステム上でハッシュと属性を取得し、監視対象のホストが改変できない場所に保管します。
* **継続的な整合性監視**: リアルタイム監視に対応するWazuhのFIMモジュールや、定期スキャン型のAIDEなどのツールが、現在のファイルの状態をベースラインと比較します。リスクの高いパスはリアルタイムで監視し、それ以外はPCI DSSが求める少なくとも週1回の比較を満たす頻度でスキャンします。
* **アラートの切り分けと自動対応**: 検出された変更はそれぞれ承認済みの変更記録と照合され、説明のつかない変更はアラートとなります。悪意があると確認されたファイルは、Wazuh Active Responseなどの自動対応によって隔離または削除され、アナリストのレビューを待ちます。

### 4. 信頼境界の強制
信頼境界の強制とシステム整合性の維持:

* **整合性追跡から防御統制への発展**: FIMのアラートを変更管理プロセスと結び付けることで、整合性の追跡は強制ポイントとなります。すべての変更は、承認済みの変更と一致するか、調査の対象となるかのどちらかになるためです。
* **ベースライン自体の保護**: ベースラインのデータベースとFIMエージェントの設定は、監視対象のホストから改変されないよう保護されます。ベースラインを書き換えられる攻撃者は、どんな変更でも承認済みに見せかけられるためです。
* **継続的なプロベナンス監査**: 誰が、いつ、どのプロセスを通じてどのファイルを変更したかの記録は監査証跡として保持され、コンプライアンスおよびインシデント対応の要件を支える検知的統制として機能します。

### 5. 結論
継続的なファイル整合性監視は、SHA-256のベースラインハッシュと組み合わさることで、保護対象ファイルが承認済みプロセス以外の経路で変更された際に、スタートアップフォルダーのような永続化に使われる場所への書き込みも含めて、CISSPドメイン7のセキュリティ運用に早期の兆候を提供します。

境界におけるデフォルト拒否型のアクセス制御は、未認証トラフィックが監視対象ファイルに到達する範囲を制限することで、その兆候の意味を保ち、一つひとつのアラートが実際の問題を示す可能性を高め、CySA+の実務と整合した状態を維持します。
