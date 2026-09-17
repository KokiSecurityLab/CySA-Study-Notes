# Koki's Technical Paper #039

## The Last Patch — Secure SDLC Finalization, Release Gate Penetration Testing, and Software Assurance Maturity

### Summary Digest
This paper defines a release-gate framework for Secure SDLC finalization, aligned with CISSP Domains 6 and 8 and OWASP SAMM, requiring testing before production release.

Findings from that testing are resolved and re-verified before release, consistent with the vulnerability approach in Technical Paper #004, rather than shipped alongside known issues.

---
### 1. Unverified Release Risk
Structural Vulnerabilities of Untested Production Releases:

* **Release Without a Defined Security Gate**: Deploying a version to production without a documented, mandatory security checkpoint allows known or undiscovered vulnerabilities to reach live users unaddressed.
* **Fragmented Security Coverage Across Development Phases**: Applying security controls only at isolated points, such as code review alone, without coverage across the full SDLC leaves gaps at phases such as design or deployment.
* **Untracked Post-Release Configuration Drift**: Without continuous monitoring after release, configuration changes made in production can silently diverge from the tested and verified release baseline.

### 2. SAMM Maturity and Testing Foundation
OWASP SAMM Practices and Release Gate Criteria:

* **Structured Maturity Assessment via OWASP SAMM**: Security practices across governance, design, implementation, verification, and operations are assessed against the OWASP Software Assurance Maturity Model (SAMM), identifying which SDLC phases require additional controls.
* **Mandatory Pre-Release Penetration Testing**: A defined penetration-testing gate, consistent with CISSP Domain 6 security assessment practices, must be passed before any version is approved for production deployment.
* **Alignment with Vulnerability Management Controls**: Findings from release-gate testing are processed through the same vulnerability-scoring and remediation approach defined in Technical Paper #004, rather than tracked separately.

### 3. Release Gate and Verification Sequence
Testing, Remediation, and Sign-Off Stages:

1. **Pre-Release Penetration Testing**: The candidate release undergoes structured penetration testing against defined scope and severity criteria before proceeding further.
2. **Finding Remediation and Re-Verification**: Identified vulnerabilities are remediated and the affected components are re-tested, confirming resolution before the release proceeds.
3. **Documented Release Sign-Off**: A named approver confirms that testing results meet the defined release criteria, consistent with the deployment-approval process defined in Technical Paper #021, before production release.

### 4. SDLC Governance and Maturity Review
Cross-Phase Coverage and Maturity Progression:

* **Coverage Across All SDLC Phases**: Security controls are mapped to each SAMM business function so that no development phase relies solely on controls intended for a different phase.
* **Post-Release Configuration Monitoring**: Production configuration is continuously compared against the tested release baseline, consistent with the integrity-verification approach defined in Technical Paper #001.
* **Continuous SAMM Maturity Reassessment**: The organization's SAMM maturity scores are reassessed on a defined cadence to identify phases where security practice has not kept pace with development velocity.

### 5. Conclusion
A release gate only reduces risk if passing it actually requires fixing what testing finds, rather than documenting the finding and shipping anyway.

Structuring that gate around OWASP SAMM and CISSP Domain 6 practices gives "finalized" a specific, testable meaning instead of a general sense that the work is done.

---
# テクニカルペーパーシリーズ #039

## ザ・ラスト・パッチ — セキュアSDLCの最終化、リリースゲートにおけるペネトレーションテスト、およびソフトウェア保証成熟度

### サマリー・ダイジェスト
本論文は、CISSPドメイン6・8およびOWASP SAMMに準拠したセキュアSDLC最終化のためのリリースゲートフレームワークを定義し、本番リリース前のテストを義務付けます。

そのテストで見つかった問題は、既知の問題を抱えたまま出荷するのではなく、テクニカルペーパーシリーズ #004 で定義した脆弱性対応アプローチに沿って解決・再検証されます。

---
### 1. 未検証リリースのリスク
未検証の本番リリースに伴う構造的脆弱性:

* **セキュリティゲートを欠いたリリース**: 文書化された必須のセキュリティチェックポイントを経ずに本番環境へバージョンをデプロイすると、既知または未発見の脆弱性が未対処のまま実際のユーザーに到達してしまいます。
* **開発フェーズ間で断片化したセキュリティカバレッジ**: コードレビューのみなど孤立した時点でのみセキュリティ統制を適用し、SDLC全体をカバーしないと、設計やデプロイなどのフェーズに隙間が生じます。
* **追跡されないリリース後の構成ドリフト**: リリース後の継続的な監視がなければ、本番環境で行われた構成変更が、テスト・検証済みのリリースベースラインから気づかぬうちに乖離する可能性があります。

### 2. SAMM成熟度とテストの基盤
OWASP SAMMの実務とリリースゲートの基準:

* **OWASP SAMMによる構造的な成熟度評価**: ガバナンス・設計・実装・検証・運用にわたるセキュリティ実務を、OWASP Software Assurance Maturity Model（SAMM）に照らして評価し、追加統制が必要なSDLCフェーズを特定します。
* **リリース前ペネトレーションテストの義務化**: CISSPドメイン6のセキュリティ評価実務と整合する、定義済みのペネトレーションテストゲートを通過しなければ、いかなるバージョンも本番デプロイの承認を得られません。
* **脆弱性管理統制との整合**: リリースゲートテストで見つかった事案は、個別に追跡されるのではなく、テクニカルペーパーシリーズ #004 で定義した脆弱性スコアリング・修復アプローチを通じて処理されます。

### 3. リリースゲートと検証の手順
テスト・修復・サインオフの各段階:

1. **リリース前ペネトレーションテスト**: リリース候補は、次の段階へ進む前に、定義済みの範囲と深刻度基準に沿った構造化されたペネトレーションテストを受けます。
2. **検出事案の修復と再検証**: 特定された脆弱性は修復され、該当コンポーネントは再テストされ、リリースが進む前に解消を確認します。
3. **文書化されたリリースサインオフ**: 指名された承認者が、テスト結果が定義済みのリリース基準を満たしていることを確認します。これは　テクニカルペーパーシリーズ　#021で定義したデプロイ承認プロセスと整合し、本番リリース前に行われます。

### 4. SDLCガバナンスと成熟度レビュー
フェーズ横断のカバレッジと成熟度の進展:

* **全SDLCフェーズにわたるカバレッジ**: セキュリティ統制はSAMMの各ビジネス機能に対応付けられ、どの開発フェーズも別のフェーズ向けの統制のみに依存することがないようにします。
* **リリース後の構成監視**: 本番環境の構成は、テクニカルペーパーシリーズ #001 で定義した整合性検証アプローチと整合する形で、テスト済みのリリースベースラインと継続的に比較されます。
* **SAMM成熟度の継続的再評価**: 組織のSAMM成熟度スコアは定められた周期で再評価され、開発速度にセキュリティ実務が追いついていないフェーズを特定します。

### 5. 結論
リリースゲートがリスクを低減するのは、テストで見つかった問題を記録して出荷を続けるのではなく、それを通過するために実際に修正が求められる場合に限られます。

このゲートをOWASP SAMMおよびCISSPドメイン6の実務に沿って構成することは、「完了」に対して、作業が終わったという漠然とした感覚ではなく、具体的でテスト可能な意味を与えます。
