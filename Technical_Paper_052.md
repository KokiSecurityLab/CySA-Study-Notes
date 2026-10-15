# Koki's Technical Paper #052

## Risk Assessment — Quantitative Risk Metrics, NIST SP 800-30 Methodology, and Annualized Loss Expectancy Calculation

### Summary Digest
This paper defines a quantitative risk-assessment methodology, aligned with CISSP Domain 1 and NIST SP 800-30, calculating loss expectancy from asset value, exposure factor, and rate of occurrence.

Risk-treatment decisions are ranked by calculated ALE rather than by subjective severity labels, consistent with the governance approach in Technical Paper #051.

---
### 1. Inconsistent Risk Prioritization Risk
Structural Vulnerabilities of Ad Hoc Risk Ranking:

* **Risk Ranked by Intuition Rather Than Calculation**: Prioritizing remediation based on which risk feels most severe, without a consistent calculation method, produces inconsistent results between different reviewers assessing the same risk.
* **Missing Asset Valuation**: Risk assessments that skip formally valuing the asset at stake have no basis for calculating the actual financial exposure a given threat represents.
* **Undocumented Threat-Vulnerability Pairing**: Failing to explicitly pair each identified vulnerability with the specific threat that could exploit it, consistent with NIST SP 800-30 methodology, can produce a risk register that lists issues without a clear cause-and-effect basis for the calculated risk.

### 2. Quantitative Formula and NIST Methodology Foundation
ALE Calculation and Threat-Vulnerability Pairing Principles:

* **Single Loss Expectancy Calculation**: SLE is calculated as Asset Value (AV) multiplied by Exposure Factor (EF), providing the expected monetary loss from a single occurrence of the identified risk.
* **Annualized Loss Expectancy Calculation**: ALE is calculated as SLE multiplied by Annualized Rate of Occurrence (ARO), consistent with CISSP Domain 1 quantitative risk analysis, expressing risk as an expected annual monetary figure.
* **NIST SP 800-30 Threat-Vulnerability Pairing**: Each risk entry explicitly pairs a specific threat source with a specific vulnerability it could exploit, consistent with the NIST SP 800-30 risk assessment methodology, rather than listing threats and vulnerabilities separately.

### 3. Assessment Calculation and Prioritization Sequence
Valuation, Calculation, and Ranked Output Stages:

1. **Asset Valuation**: Each in-scope asset is assigned a documented value reflecting its replacement cost and business value, forming the basis for subsequent loss calculations.
2. **SLE and ALE Calculation**: For each paired threat-vulnerability combination, SLE and ALE are calculated using the documented asset value, exposure factor, and rate of occurrence.
3. **Risk Register Prioritization**: Calculated ALE values are used to rank entries in the risk register, directing remediation attention toward the highest calculated financial exposure first.

### 4. Assessment Governance and Estimate Review
Input Documentation and Recalculation Cadence:

* **Documented Basis for Each Input Value**: Asset value, exposure factor, and rate-of-occurrence figures are documented with their source or estimation method, rather than entered without a traceable basis.
* **Qualitative Supplementation Where Data Is Limited**: Where reliable historical data for calculating ARO is unavailable, a documented qualitative estimate supplements the quantitative figure rather than substituting an unfounded number.
* **Continuous Risk Register Recalculation**: Risk register entries are recalculated on a defined cadence as asset values, threat data, or exposure factors change, consistent with the governance review approach defined in Technical Paper #051.

### 5. Conclusion
A risk ranked by calculation can be explained and reproduced by someone else; a risk ranked by impression cannot.

Applying the SLE and ALE formulas consistently, aligned with CISSP Domain 1 and NIST SP 800-30, gives a risk register a shared, defensible basis for what gets fixed first.

---
# テクニカルペーパーシリーズ #052

## リスクアセスメント — 定量的リスク指標、NIST SP 800-30方法論、および年間予想損失額の算出

### サマリー・ダイジェスト
本論文は、CISSPドメイン1およびNIST SP 800-30に準拠した定量的リスク評価手法を定義し、資産価値・暴露係数・発生率から損失予想額を算出します。

リスク対応の判断は、主観的な深刻度ラベルではなく、テクニカルペーパーシリーズ #051 で定義したガバナンスアプローチと整合する形で算出されたALEに基づいて優先順位付けされます。

---
### 1. 一貫性を欠くリスク優先順位付けのリスク
場当たり的なリスクランク付けに伴う構造的脆弱性:

* **計算ではなく直感によるリスクランク付け**: どのリスクが最も深刻に感じられるかに基づいて修復の優先順位を決め、一貫した計算方法を用いない場合、同じリスクを評価する担当者間で結果に一貫性がなくなります。
* **資産評価の欠落**: 対象となる資産を正式に評価する手順を省略したリスク評価には、特定の脅威が表す実際の金銭的露出を計算する根拠がありません。
* **文書化されていない脅威・脆弱性のペアリング**: NIST SP 800-30の方法論と整合する形で、特定された各脆弱性をそれを悪用し得る特定の脅威と明示的に対応付けなければ、算出されたリスクの明確な因果関係の根拠を欠いたリスクレジスターになりかねません。

### 2. 定量計算式とNIST方法論の基盤
ALE算出と脅威・脆弱性ペアリングの原則:

* **単一予想損失額の算出**: SLEは資産価値（AV）に暴露係数（EF）を乗じて算出され、特定されたリスクが一度発生した場合の予想金銭損失を示します。
* **年間予想損失額の算出**: ALEはSLEに年間発生率（ARO）を乗じて算出され、CISSPドメイン1の定量的リスク分析と整合する形で、リスクを年間の予想金額として表現します。
* **NIST SP 800-30に基づく脅威・脆弱性のペアリング**: 各リスク項目は、脅威と脆弱性を別々に列挙するのではなく、NIST SP 800-30のリスク評価方法論と整合する形で、特定の脅威源とそれが悪用し得る特定の脆弱性を明示的に対応付けます。

### 3. 評価の算出と優先順位付けの手順
評価・算出・順位付けされた出力の各段階:

1. **資産評価**: 対象範囲内の各資産には、その再調達コストと事業価値を反映した文書化された価値が割り当てられ、以降の損失算出の基礎となります。
2. **SLEおよびALEの算出**: 対応付けられた脅威・脆弱性の組み合わせごとに、文書化された資産価値・暴露係数・発生率を用いてSLEおよびALEが算出されます。
3. **リスクレジスターの優先順位付け**: 算出されたALEの値はリスクレジスター内の項目の順位付けに用いられ、算出された金銭的露出が最も大きいものから修復対応の注意を向けます。

### 4. 評価ガバナンスと見積もりのレビュー
入力値の文書化と再計算の頻度:

* **各入力値の文書化された根拠**: 資産価値・暴露係数・発生率の数値は、追跡可能な根拠を伴わずに入力されるのではなく、その出典または見積もり方法とともに文書化されます。
* **データが限られる場合の定性的な補完**: AROを算出するための信頼できる履歴データが利用できない場合、根拠のない数値を代用するのではなく、文書化された定性的な見積もりが定量的な数値を補完します。
* **リスクレジスターの継続的な再計算**: リスクレジスターの項目は、テクニカルペーパーシリーズ #051 で定義したガバナンスレビューアプローチと整合する形で、資産価値・脅威データ・暴露係数の変化に応じて定められた周期で再計算されます。

### 5. 結論
計算によって順位付けされたリスクは他者が説明・再現できますが、印象によって順位付けされたリスクはそうできません。

SLEおよびALEの公式を一貫して適用することは、CISSPドメイン1およびNIST SP 800-30に沿いつつ、何を最初に修正すべきかについて共有可能で説明可能な根拠をリスクレジスターに与えます。
