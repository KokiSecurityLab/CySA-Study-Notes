# Koki's Technical Paper #062

## Formal Security Models — Bell-LaPadula and Biba Model Application, Multilevel Security Enforcement, and Confidentiality-Integrity Trade-offs

### Summary Digest
This paper defines a formal access-control modeling approach, aligned with CISSP Domain 3, applying Bell-LaPadula confidentiality and Biba integrity models to systems requiring multilevel security enforcement.

Bell-LaPadula's no-read-up, no-write-down rules and Biba's inverse no-write-up, no-read-down rules address confidentiality and integrity separately, since a single model does not enforce both simultaneously.

---
### 1. Informal Access-Control Reasoning Risk
Structural Vulnerabilities of Unmodeled Multilevel Access:

* **Ad Hoc Level-Crossing Decisions**: Systems handling multiple sensitivity levels without a formal model make read and write permission decisions inconsistently, since there is no mathematically defined rule to check a specific access request against.
* **Confidentiality Model Applied Where Integrity Matters**: Applying a confidentiality-focused model to a system where data integrity is the primary concern can permit low-integrity input to flow upward into higher-integrity processes unchecked.
* **Undocumented Security Level Assignments**: Without formally assigned security levels for subjects and objects, there is no basis for a formal model's rules to actually evaluate against.

### 2. Bell-LaPadula and Biba Foundation
Confidentiality and Integrity Model Principles:

* **Bell-LaPadula Simple and Star Property**: The simple security property prevents a subject from reading data at a higher classification level, and the star property prevents a subject from writing data to a lower classification level, together preventing high-to-low information leakage.
* **Biba Simple and Star Integrity Property**: The simple integrity property prevents a subject from reading data at a lower integrity level, and the star integrity property prevents a subject from writing to a higher integrity level, together preventing low-integrity data from contaminating higher-integrity processes.
* **Model Selection by Primary Concern**: The applicable model is selected based on whether confidentiality or integrity is the primary security concern for the specific system, consistent with the classification tiers defined in Technical Paper #027.

### 3. Level Assignment and Enforcement Sequence
Subject-Object Labeling, Rule Application, and Verification:

1. **Security Level Assignment**: Subjects and objects are formally assigned a security or integrity level, providing the labeled basis the model's rules require.
2. **Access Rule Enforcement**: Read and write requests are evaluated against the applicable model's rules, Bell-LaPadula for confidentiality-focused systems or Biba for integrity-focused systems, before being permitted.
3. **Cross-Level Request Logging**: Requests denied due to a level-crossing violation are logged for review, consistent with the audit-logging approach defined in Technical Paper #002, rather than silently discarded.

### 4. Model Governance and Level Assignment Auditing
Level Currency and Enforcement Exception Review:

* **Documented Justification for Trusted Subject Exceptions**: Any subject granted an exception to bypass standard model rules, such as a trusted downgrade process, is documented with explicit justification rather than left as an undocumented special case.
* **Periodic Level Reassignment Review**: Security and integrity level assignments are reviewed on a defined cadence to confirm subjects and objects remain correctly labeled as roles and data change.
* **Continuous Enforcement Log Auditing**: Logged level-crossing denial attempts are reviewed to identify patterns suggesting a misconfigured level assignment rather than a genuine access violation.

### 5. Conclusion
Confidentiality and integrity are different properties enforced by different rules, which is why Bell-LaPadula and Biba point in opposite directions.

Choosing the model matching a system's primary concern, consistent with CISSP Domain 3, is what makes formal access control enforce the property the system was built to protect.

---
# テクニカルペーパーシリーズ #062

## 形式的セキュリティモデル — ベル・ラパドゥラモデルとビバモデルの適用、マルチレベルセキュリティの執行、および機密性と完全性のトレードオフ

### サマリー・ダイジェスト
本論文は、CISSPドメイン3に準拠した形式的アクセス制御モデリング手法を定義し、マルチレベルセキュリティの適用を必要とするシステムにベル・ラパドゥラ機密性モデルとビバ完全性モデルを適用します。

ベル・ラパドゥラの「上へ読まず、下へ書かず」というルールと、その逆であるビバの「上へ書かず、下へ読まず」というルールは、単一のモデルでは両方を同時に強制できないため、機密性と完全性をそれぞれ別個に扱います。

---
### 1. 非形式的なアクセス制御判断のリスク
モデル化されていないマルチレベルアクセスに伴う構造的脆弱性:

* **場当たり的なレベル越境の判断**: 形式的モデルを持たずに複数の機微レベルを扱うシステムは、特定のアクセス要求を照合すべき数学的に定義されたルールがないため、読み取り・書き込み許可の判断に一貫性がなくなります。
* **完全性が重要な場面での機密性モデルの適用**: データの完全性が主な懸念であるシステムに機密性重視のモデルを適用すると、低完全性の入力が未検査のままより高い完全性を持つプロセスへ上向きに流れ込むことを許してしまう可能性があります。
* **文書化されていないセキュリティレベルの割り当て**: 主体（サブジェクト）と客体（オブジェクト）に正式なセキュリティレベルが割り当てられていなければ、形式的モデルのルールが実際に評価する対象となる基盤がありません。

### 2. ベル・ラパドゥラとビバの基盤
機密性・完全性モデルの原則:

* **ベル・ラパドゥラの単純性質とスター性質**: 単純セキュリティ性質は主体がより高い分類レベルのデータを読み取ることを防ぎ、スター性質は主体がより低い分類レベルへデータを書き込むことを防ぎ、両者が合わさって高から低への情報漏えいを防ぎます。
* **ビバの単純完全性性質とスター完全性性質**: 単純完全性性質は主体がより低い完全性レベルのデータを読み取ることを防ぎ、スター完全性性質は主体がより高い完全性レベルへ書き込むことを防ぎ、両者が合わさって低完全性データがより高い完全性のプロセスを汚染することを防ぎます。
* **主な懸念事項に基づくモデル選択**: 適用すべきモデルは、テクニカルペーパーシリーズ #027 で定義した分類ティアと整合する形で、その特定のシステムにとって機密性と完全性のどちらが主な懸念事項かに基づいて選択されます。

### 3. レベル割り当てと執行の手順
主体・客体のラベル付け・ルール適用・検証:

1. **セキュリティレベルの割り当て**: 主体と客体には正式にセキュリティレベルまたは完全性レベルが割り当てられ、モデルのルールが必要とするラベル付けされた基盤を提供します。
2. **アクセスルールの執行**: 読み取り・書き込み要求は、許可される前に、機密性重視のシステムであればベル・ラパドゥラ、完全性重視のシステムであればビバという該当するモデルのルールと照合して評価されます。
3. **レベル越境要求のログ記録**: レベル越境の違反により拒否された要求は、黙って破棄されるのではなく、テクニカルペーパーシリーズ  #002 で定義した監査ログのアプローチと整合する形でレビュー対象として記録されます。

### 4. モデルガバナンスとレベル割り当ての監査
レベルの鮮度と適用除外のレビュー:

* **信頼された主体の例外に対する文書化された正当性**: 信頼されたダウングレードプロセスなど、標準のモデルルールを回避する例外を許可された主体は、文書化されていない特例として放置されるのではなく、明示的な正当性とともに文書化されます。
* **定期的なレベル再割り当てレビュー**: セキュリティおよび完全性レベルの割り当ては、役割やデータが変化する中で主体・客体が引き続き正しくラベル付けされているかを確認するため、定められた周期でレビューされます。
* **執行ログの継続的監査**: 記録されたレベル越境の拒否試行はレビューされ、実際のアクセス違反ではなく、誤設定されたレベル割り当てを示唆するパターンを特定します。

### 5. 結論
機密性と完全性は異なるルールによって強制される異なる性質であり、だからこそベル・ラパドゥラとビバは正反対の方向を向いています。

システムの実際の主な関心事に一致するモデルを選ぶことは、CISSPドメイン3に沿いつつ、形式的アクセス制御が、そのシステムが本来保護するために構築された性質を強制するものにします。
