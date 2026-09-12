# Koki's Technical Paper #016

## Core Persistence — Deep-Level Logic Integration, Kernel-Level Security Controls, and Root of Trust Verification

### Summary Digest
This paper defines a kernel-level security architecture, aligned with CISSP Domain 3 root-of-trust practices, that integrates configuration-integrity checks into core system processes rather than relying on removable, externally attached tools.

Runtime state is verified against a hardware root of trust, and automated remediation restores a known-good configuration on deviation.

---
### 1. Kernel Security Integration
Structural Vulnerabilities of Externally Deployed Security Tools:

* **Removable Security Controls**: Security tools deployed as separate, externally attached processes can be disabled, uninstalled, or bypassed by an attacker who gains sufficient privilege, leaving the underlying system unprotected.
* **Absence of a Verified Boot Chain**: Systems that do not verify each stage of the boot process against a trusted reference have no guarantee that the operating system loaded at startup matches its intended, unmodified state.
* **Undetected Configuration Drift at the Kernel Level**: Without continuous comparison against a known-good baseline, low-level configuration changes, including those made by a rootkit, can persist undetected for extended periods.

### 2. Methodological Foundation
Root of Trust and Continuous Integrity Verification:

* **Hardware Root of Trust**: A hardware-anchored root of trust, such as a Trusted Platform Module (TPM), provides a verified starting point that later boot and configuration checks can be measured against.
* **Continuous Integrity Measurement**: Runtime configuration is compared against the verified baseline on an ongoing basis, extending the boot-time verification model into continuous operation rather than a single check at startup.
* **Alignment with Baseline Boundary and Behavioral Controls**: Kernel-integrity findings are reconciled with the baseline boundary controls defined in Technical Paper #001 and the behavioral-anomaly indicators defined in Technical Paper #013, keeping detection consistent across the wider security architecture.

### 3. Pipeline Implementation
Root of Trust Verification and Automated Remediation:

1. **Baseline Signature Capture**: A cryptographic signature of the verified, known-good kernel and configuration state is captured and stored as the reference for later comparison.
2. **Continuous Discrepancy Scanning**: Automated scans compare the current runtime state against the stored signature on a defined interval, flagging any deviation for review.
3. **Automated Configuration Remediation**: When a deviation is confirmed, the affected configuration is automatically restored to the verified baseline, and the incident is logged for correlation with related security events (see Technical Paper #006 for post-incident review).

### 4. Boundary Governance
Long-Term Integrity Assurance and Recovery Review:

* **Isolating Kernel Integrity from Application-Layer Compromise**: Kernel-level integrity checks operate independently of application-layer processes, so a compromise at the application level does not automatically extend to the verified kernel state.
* **Bounded Automated Remediation Actions**: Automated remediation is limited to restoring a previously verified configuration rather than making unreviewed changes, keeping recovery actions predictable and auditable.
* **Continuous Root-of-Trust Auditing**: Ongoing auditing of root-of-trust verification results functions as a detective control, supporting compliance evidence without asserting that kernel compromise is fully impossible.

### 5. Conclusion
A root of trust is only useful if the baseline it verifies against is itself known to be accurate and current.

Extending that verification into continuous runtime monitoring, consistent with CISSP Domain 3 practices, is what turns a one-time boot check into an ongoing integrity control.

---
# Koki's Technical Paper #016

## コア・パーシステンス — 深層論理統合、カーネルレベルのセキュリティ統制、およびRoot of Trust検証

### サマリー・ダイジェスト
本論文は、CISSPドメイン3のRoot of Trust実務に準拠したカーネルレベルのセキュリティアーキテクチャを定義し、着脱可能な外部ツールに頼るのではなく、構成整合性チェックをコアシステムのプロセスに組み込みます。

ランタイムの状態はハードウェアのRoot of Trustと照合され、逸脱が検知されると自動修復によって既知の正常な構成へ復元されます。

---
### 1. カーネル・セキュリティ統合
外部展開されたセキュリティツールに伴う構造的脆弱性:

* **除去可能なセキュリティ統制**: 外部に付加された独立プロセスとして展開されたセキュリティツールは、十分な権限を得た攻撃者によって無効化・アンインストール・回避される可能性があり、その結果基盤システムが無防備な状態になります。
* **検証済み起動チェーンの欠如**: 起動プロセスの各段階を信頼済みの参照値と照合しないシステムには、起動時に読み込まれるオペレーティングシステムが意図した未改ざんの状態と一致しているという保証がありません。
* **カーネルレベルでの検知されない構成ドリフト**: 既知の正常なベースラインとの継続的な比較がなければ、ルートキットによるものを含む低レイヤーの構成変更が長期間検知されないまま持続する可能性があります。

### 2. 方法論的基盤
Root of Trustと継続的な整合性検証:

* **ハードウェアRoot of Trust**: TPM（Trusted Platform Module）などハードウェアに固定されたRoot of Trustは、以降の起動チェックや構成チェックの基準となる検証済みの出発点を提供します。
* **継続的な整合性測定**: ランタイム構成を検証済みベースラインと継続的に比較することで、起動時のみの検証モデルを継続的な運用へと拡張します。
* **ベースライン境界統制および行動統制との整合**: カーネル整合性の検知結果をTechnical Paper #001で定義されたベースライン境界統制、およびTechnical Paper #013で定義された行動異常指標と突き合わせ、より広いセキュリティアーキテクチャ全体で検知を一貫させます。

### 3. パイプラインの実装
Root of Trustの検証と自動修復:

1. **ベースライン署名の取得**: 検証済みで既知の正常なカーネルおよび構成状態の暗号学的署名を取得し、以降の比較の基準として保存します。
2. **継続的な不一致スキャン**: 定義済みの間隔で現在のランタイム状態を保存済みの署名と自動比較し、逸脱を検出した場合はレビュー対象としてフラグ付けします。
3. **自動化された構成修復**: 逸脱が確認された場合、該当する構成は自動的に検証済みベースラインへ復元され、そのインシデントは関連するセキュリティイベントとの相関分析のために記録されます（ポストインシデントレビューの詳細はTechnical Paper #006を参照）。

### 4. 境界統治
長期的な整合性保証と復旧レビュー:

* **カーネル整合性とアプリケーション層侵害の分離**: カーネルレベルの整合性チェックはアプリケーション層のプロセスから独立して動作するため、アプリケーション層での侵害が自動的に検証済みのカーネル状態にまで及ぶことはありません。
* **範囲を限定した自動修復アクション**: 自動修復は未レビューの変更を行うのではなく、以前に検証済みの構成へ復元することに限定され、復旧アクションを予測可能かつ監査可能な状態に保ちます。
* **Root of Trustの継続的監査**: Root of Trust検証結果を継続的に監査することは検知的統制として機能し、カーネル侵害が完全に不可能であると主張することなくコンプライアンス上の証跡を提供します。

### 5. 結論
Root of Trustは、それが照合するベースライン自体が正確かつ最新であると確認されている場合にのみ有効です。

その検証を継続的なランタイム監視へと拡張することが、CISSPドメイン3の実務に沿いつつ、一度きりの起動時チェックを継続的な整合性統制へと変えます。
