# Koki's Technical Paper #065

## Trusted Computing Base — Reference Monitor Concept Application, Security Kernel Design, and TCB Boundary Verification

### Summary Digest
This paper defines the Trusted Computing Base (TCB) and reference monitor concept, aligned with CISSP Domain 3, requiring the security kernel to be tamperproof, always invoked, and verifiable.

Everything outside the documented TCB boundary is treated as unable to bypass enforcement, consistent with the least-common-mechanism principle in Technical Paper #061.
---

### 1. Unbounded TCB Risk
Structural Vulnerabilities of an Undefined Trust Boundary:

* **Undocumented TCB Scope**: A system without an explicitly documented TCB boundary has no basis for determining which components must meet the highest assurance requirements and which do not.
* **Bypassable Enforcement Points**: A reference monitor implementation that can be circumvented through an alternate code path violates the always-invoked property, allowing a request to reach protected resources without being checked.
* **Unverifiably Large Security Kernel**: A security kernel implementation large and complex enough that no one can practically verify its correctness undermines the small-enough-to-verify property the reference monitor concept requires.

### 2. Reference Monitor Property Foundation
Tamperproof, Always-Invoked, and Verifiable Design Principles:

* **Tamperproof Enforcement**: The security kernel implementing the reference monitor concept is protected from unauthorized modification, consistent with the integrity-verification approach defined in Technical Paper #001.
* **Always Invoked, No Bypass Path**: Every access request to a protected resource passes through the reference monitor without exception, eliminating alternate paths that could reach the resource unchecked.
* **Small Enough to Verify**: The security kernel is kept as small and simple as its function allows, consistent with the economy-of-mechanism principle defined in Technical Paper #061, so its correctness can actually be independently assessed.

### 3. TCB Boundary Definition and Verification Sequence
Scope Documentation, Enforcement Testing, and Independent Review:

1. **TCB Boundary Documentation**: The specific hardware, firmware, and software components composing the TCB are explicitly documented, distinguishing them from components outside the trust boundary.
2. **Enforcement Path Testing**: All identified access paths to protected resources are tested to confirm each one passes through the reference monitor without an undocumented bypass.
3. **Independent Kernel Verification**: The security kernel's implementation is independently reviewed against its documented specification to confirm it correctly implements the intended enforcement logic.

### 4. TCB Governance and Boundary Change Review
Boundary Currency and Modification Control:

* **Controlled TCB Modification Process**: Any change to a component within the documented TCB boundary follows a stricter change-control process than changes outside it, consistent with the deployment-approval process defined in Technical Paper #021.
* **Boundary Drift Detection**: The actual system configuration is periodically compared against the documented TCB boundary to detect components that have drifted into or out of the trust boundary without formal review.
* **Continuous Reference Monitor Property Auditing**: The tamperproof, always-invoked, and verifiable properties are periodically re-assessed as the system evolves, rather than assumed to hold indefinitely from initial design.

### 5. Conclusion
A security kernel that can be bypassed, modified undetected, or is too complex to verify does not satisfy the reference monitor concept, whatever it is called.

Documenting the TCB boundary and testing all three reference monitor properties, consistent with CISSP Domain 3, turns the concept into something verifiable rather than assumed.

---
# テクニカルペーパーシリーズ #065

## 信頼できるコンピューティングベース — リファレンスモニタ概念の適用、セキュリティカーネル設計、およびTCB境界の検証

### サマリー・ダイジェスト
本論文は、CISSPドメイン3に準拠した信頼できるコンピューティングベース（TCB）とリファレンスモニタの概念を定義し、セキュリティカーネルが改ざん耐性を持ち、常に呼び出され、検証可能であることを要求します。

文書化されたTCB境界の外側にあるものはすべて、テクニカルペーパーシリーズ #061 で定義した最小共通機構の原則と整合する形で、その執行を回避できないものとして扱われます。

---
### 1. 境界未確定のTCBリスク
未定義の信頼境界に伴う構造的脆弱性:

* **文書化されていないTCBの範囲**: 明示的に文書化されたTCB境界を持たないシステムには、どのコンポーネントが最高水準の保証要件を満たすべきで、どれがそうでないかを判断する根拠がありません。
* **回避可能な執行ポイント**: 代替のコード経路を通じて回避可能なリファレンスモニタの実装は「常に呼び出される」という特性に違反し、チェックされないまま保護対象リソースへリクエストが到達することを許してしまいます。
* **検証不能なほど大きいセキュリティカーネル**: 誰も実際にはその正しさを検証できないほど大きく複雑なセキュリティカーネルの実装は、リファレンスモニタの概念が要求する「検証できるほど小さい」という特性を損ないます。

### 2. リファレンスモニタ特性の基盤
改ざん耐性・常時呼び出し・検証可能性の設計原則:

* **改ざん耐性のある執行**: リファレンスモニタの概念を実装するセキュリティカーネルは、テクニカルペーパーシリーズ #001 で定義した整合性検証アプローチと整合する形で、不正な変更から保護されます。
* **常時呼び出しと回避経路の不在**: 保護対象リソースへのすべてのアクセス要求は例外なくリファレンスモニタを経由し、チェックされずにそのリソースへ到達し得る代替経路を排除します。
* **検証できるほどの小ささ**: セキュリティカーネルは、テクニカルペーパーシリーズ #061 で定義した機構の経済性の原則と整合する形で、その機能が許す範囲で可能な限り小さく単純に保たれ、その正しさを実際に独立して評価できるようにします。

### 3. TCB境界の定義と検証の手順
範囲の文書化・執行テスト・独立レビュー:

1. **TCB境界の文書化**: TCBを構成する特定のハードウェア・ファームウェア・ソフトウェアのコンポーネントは、信頼境界の外側にあるコンポーネントと区別する形で明示的に文書化されます。
2. **執行経路のテスト**: 保護対象リソースへの特定されたすべてのアクセス経路は、それぞれが文書化されていない迂回なしにリファレンスモニタを経由することを確認するためテストされます。
3. **独立したカーネル検証**: セキュリティカーネルの実装は、意図された執行ロジックを正しく実装しているかを確認するため、文書化された仕様に照らして独立してレビューされます。

### 4. TCBガバナンスと境界変更のレビュー
境界の鮮度と変更管理:

* **統制されたTCB変更プロセス**: 文書化されたTCB境界内のコンポーネントへの変更は、テクニカルペーパーシリーズ #021 で定義したデプロイ承認プロセスと整合する形で、境界外の変更よりも厳格な変更管理プロセスに従います。
* **境界ドリフトの検知**: 実際のシステム構成は、正式なレビューを経ずに信頼境界の内外へドリフトしたコンポーネントを検知するため、文書化されたTCB境界と定期的に比較されます。
* **リファレンスモニタ特性の継続的監査**: 改ざん耐性・常時呼び出し・検証可能性という各特性は、初期設計から無期限に維持されると想定するのではなく、システムが進化する中で定期的に再評価されます。

### 5. 結論
回避可能であったり、検知されずに改変されたり、複雑すぎて検証できないセキュリティカーネルは、それが何と呼ばれていようとも、実際にはリファレンスモニタの概念を満たしていません。

TCB境界を文書化し、3つのリファレンスモニタ特性すべてをテストすることは、CISSPドメイン3に沿いつつ、その概念を想定ではなく検証可能なものへと変えます。
