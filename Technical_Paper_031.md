# Koki's Technical Paper #031

## Supply Chain Risk Management — Managing External Dependencies, Software Composition Analysis, and Vendor Diversification

### Summary Digest
This paper defines a third-party dependency risk framework, aligned with CISSP Domain 1 and NIST SP 800-161, scoring vendor and library risk continuously rather than once at procurement.

Software composition analysis and vendor diversification reduce the impact of a single degraded or compromised dependency on core operations.

---
### 1. Weakest-Link Dependency Risk
Structural Vulnerabilities of Unmonitored External Dependencies:

* **Overweighted Internal Perimeter Focus**: Security programs that concentrate resources on internal controls while leaving third-party vendor and library security largely unassessed leave the organization exposed at whichever external dependency is weakest.
* **Undetected Vulnerable Dependencies**: Applications that incorporate open-source or third-party libraries without ongoing vulnerability scanning can carry known, patchable weaknesses into production for extended periods.
* **Single-Vendor Concentration Risk**: Relying on a single critical vendor for an essential function creates a condition where that vendor's outage or compromise directly disrupts the dependent organization's own operations.

### 2. Vendor Assessment and SCA Foundation
Third-Party Risk Scoring and Dependency Scanning Principles:

* **Structured Vendor Risk Assessment**: Critical vendors are assessed against documented criteria before onboarding and on a recurring basis afterward, consistent with third-party risk management practices in CISSP Domain 1.
* **Software Composition Analysis (SCA)**: Automated tooling scans application dependencies against known-vulnerability databases, flagging outdated or vulnerable library versions for remediation.
* **Alignment with Build Provenance Controls**: Dependency risk scoring is reconciled with the SBOM and build-provenance approach defined in Technical Paper #026, connecting vendor risk to the actual components in use.

### 3. Dependency Mapping and Scanning Sequence
Inventory, Scanning, and Alternative-Source Evaluation:

1. **Dependency Inventory Compilation**: A current inventory of external vendors, libraries, and infrastructure dependencies is compiled and reconciled with the boundary controls defined in Technical Paper #001.
2. **Scheduled Vulnerability Scanning**: Dependencies are scanned against updated vulnerability databases on a defined schedule, rather than only at initial integration, to catch newly disclosed weaknesses.
3. **Alternative-Source Evaluation**: Where feasible, qualified alternative vendors or libraries are identified in advance, reducing the time needed to replace a dependency that is later found to be compromised or unmaintained.

### 4. Vendor Diversification and SLA Governance
Redundancy Planning and Service-Level Review:

* **Diversification Away From Single-Vendor Dependence**: Critical functions are designed, where practical, to support more than one qualified vendor or library, reducing the impact of any one provider's failure.
* **Service-Level Agreement Enforcement**: Vendor performance is measured against documented service-level agreements, with deviations tracked and escalated rather than only noticed informally.
* **Continuous Vendor and Dependency Auditing**: Vendor risk scores and dependency-scan results are reviewed on a defined cadence to identify degrading vendors or accumulating unpatched dependencies before they cause a disruption.

### 5. Conclusion
Most supply-chain risk is invisible until someone actually inventories which vendors and libraries a system depends on.

Continuous scanning and vendor scoring, consistent with CISSP Domain 1 and NIST SP 800-161, replace a one-time procurement decision with an ongoing check.

---
# テクニカルペーパーシリーズ #031

## サプライチェーンリスク管理 — 外部依存関係の管理、ソフトウェア構成分析、およびベンダーの多様化

### サマリー・ダイジェスト
本論文は、CISSPドメイン1およびNIST SP 800-161に準拠したサードパーティ依存関係リスクフレームワークを定義し、調達時の一度きりの評価ではなく、ベンダーおよびライブラリのリスクを継続的にスコアリングします。

ソフトウェア構成分析（SCA）とベンダーの多様化により、単一の劣化または侵害された依存関係がコア業務に与える影響を低減します。

---
### 1. 最弱リンク依存リスク
未監視の外部依存関係に伴う構造的脆弱性:

* **内部境界への偏った注力**: リソースを内部統制に集中させる一方でサードパーティのベンダーやライブラリのセキュリティをほぼ未評価のままにするセキュリティプログラムは、最も脆弱な外部依存関係のところで組織を露出させてしまいます。
* **検知されない脆弱な依存関係**: 継続的な脆弱性スキャンを行わずにオープンソースやサードパーティ製ライブラリを組み込んだアプリケーションは、既知でパッチ適用可能な弱点を長期間本番環境に持ち込んだままになる可能性があります。
* **単一ベンダーへの集中リスク**: 重要な機能を単一の重要ベンダーに依存すると、そのベンダーの停止や侵害が依存元組織自身の業務に直接的な支障をもたらす状況が生まれます。

### 2. ベンダー評価とSCAの基盤
サードパーティリスクスコアリングと依存関係スキャンの原則:

* **構造化されたベンダーリスク評価**: 重要なベンダーは、オンボーディング前および導入後も継続的に、文書化された基準に照らして評価されます。これはCISSPドメイン1のサードパーティリスク管理実務と整合します。
* **ソフトウェア構成分析（SCA）**: 自動化ツールがアプリケーションの依存関係を既知の脆弱性データベースと照合してスキャンし、古くなった、または脆弱なライブラリバージョンを修復対象としてフラグ付けします。
* **ビルド出自証明統制との整合**: 依存関係のリスクスコアリングを、テクニカルペーパーシリーズ #026 で定義したSBOMおよびビルド出自証明のアプローチと突き合わせ、ベンダーリスクを実際に使用中のコンポーネントと結びつけます。

### 3. 依存関係マッピングとスキャンの手順
棚卸し・スキャン・代替ソースの評価:

1. **依存関係の棚卸し**: 外部ベンダー、ライブラリ、インフラ依存関係の最新の一覧を作成し、テクニカルペーパーシリーズ #001 で定義した境界統制と突き合わせます。
2. **定期的な脆弱性スキャン**: 依存関係は、初回統合時のみでなく定められたスケジュールで更新済みの脆弱性データベースと照合してスキャンされ、新たに公表された弱点を捕捉します。
3. **代替ソースの評価**: 実現可能な場合、適格な代替ベンダーやライブラリをあらかじめ特定しておき、後に侵害または保守放棄が判明した依存関係を置き換えるまでの時間を短縮します。

### 4. ベンダー多様化とSLAガバナンス
冗長化計画とサービスレベルのレビュー:

* **単一ベンダー依存からの多様化**: 重要な機能は、実現可能な範囲で複数の適格なベンダーやライブラリに対応できるよう設計され、いずれか一社の障害による影響を低減します。
* **サービスレベル合意（SLA）の適用**: ベンダーの実績は文書化されたサービスレベル合意に照らして測定され、逸脱は非公式に気づかれるのではなく追跡・エスカレーションされます。
* **ベンダーおよび依存関係の継続的監査**: ベンダーリスクスコアと依存関係スキャン結果は定められた周期でレビューされ、支障が生じる前に劣化しつつあるベンダーや未パッチの依存関係の蓄積を特定します。

### 5. 結論
サプライチェーンリスクの大半は、システムがどのベンダーやライブラリに依存しているかを実際に棚卸しするまで見えないままです。

継続的なスキャンとベンダースコアリングは、CISSPドメイン1およびNIST SP 800-161に沿いつつ、一度きりの調達判断を継続的な確認へと置き換えます。
