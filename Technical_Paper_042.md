# Koki's Technical Paper #042

## Cognitive Cryptography — Biometric-Derived Key Generation, Fuzzy Extractor Cryptosystems, and Template Protection Standards

### Summary Digest
This paper defines a biometric cryptosystem deriving cryptographic key material from behavioral biometrics using fuzzy-extractor techniques, aligned with CISSP Domain 3 and ISO/IEC 24745 template-protection guidance.

Because biometric data cannot be revoked like a password, derived keys use cancelable-biometric transforms so a compromised template does not permanently compromise the trait.

---
### 1. Biometric Key Derivation Risk
Structural Vulnerabilities of Naive Biometric-to-Key Mapping:

* **Non-Reproducible Raw Biometric Signals**: Behavioral biometric measurements vary slightly between readings, so a cryptographic scheme that requires an exact match will fail to reproduce the same key from legitimate input without an explicit error-tolerance mechanism.
* **Irrevocability of Compromised Biometric Templates**: A traditional password can be reset after compromise, but a raw biometric trait cannot, meaning a naive scheme that derives keys directly from unprotected biometric data creates a permanent exposure if the template is ever leaked.
* **Limited Entropy in Behavioral Signals**: Behavioral biometric measurements such as typing rhythm carry finite, measurable entropy, which is lower than a well-generated cryptographic key and must be accounted for rather than assumed to be unlimited.

### 2. Fuzzy Extractor and Template Protection Foundation
Error-Tolerant Key Derivation and Cancelable Biometrics:

* **Fuzzy Extractor Key Derivation**: A fuzzy extractor scheme, consistent with established biometric cryptosystem research, tolerates small variations in repeated biometric measurements while still reliably reproducing the same derived key.
* **Cancelable Biometric Transforms**: The biometric trait is transformed before key derivation using a revocable, non-invertible transform, consistent with ISO/IEC 24745 biometric information protection, so a compromised transform can be revoked and reissued without discarding the underlying trait.
* **Alignment with Continuous Authentication Signals**: Key-derivation inputs are drawn from the same behavioral-biometric baseline defined in Technical Paper #013, keeping the two systems consistent rather than maintaining separate, conflicting behavioral profiles.

### 3. Enrollment and Derivation Sequence
Baseline Enrollment, Transform Application, and Key Extraction:

1. **Baseline Biometric Enrollment**: An initial set of behavioral biometric measurements is collected to establish the reference template used for later key derivation.
2. **Cancelable Transform Application**: The enrolled template is passed through a revocable transform before any cryptographic material is derived, so the underlying raw trait is never stored directly.
3. **Fuzzy-Extractor Key Reconstruction**: At each use, new biometric input is combined with stored helper data to reconstruct the same derived key, tolerating natural variation without revealing the original template.

### 4. Template Governance and Revocation Review
Compromise Response and Transform Rotation:

* **Defined Revocation Procedure**: A documented procedure exists for revoking and reissuing a cancelable transform if a template is suspected compromised, rather than treating biometric compromise as unrecoverable.
* **Separation of Helper Data from Raw Biometric Storage**: Helper data used in key reconstruction is stored separately from any raw biometric reference, limiting what an attacker gains from compromising either store alone.
* **Continuous Entropy and False-Match Auditing**: The effective entropy and false-match rate of the derivation scheme are reviewed on a defined cadence against current research, since assumptions about biometric uniqueness can weaken as measurement or spoofing techniques advance.

### 5. Conclusion
A biometric trait is a poor password substitute because it cannot be changed, so derivation must pass through a revocable transform rather than skip that step.

Combining fuzzy extractors with cancelable biometrics, consistent with CISSP Domain 3 and ISO/IEC 24745, makes biometric-derived keys practical rather than a permanent liability once compromised.

---
# テクニカルペーパーシリーズ #042

## 認知暗号学 — 生体情報からの鍵導出、ファジーエクストラクタ暗号システム、およびテンプレート保護標準

### サマリー・ダイジェスト
本論文は、CISSPドメイン3およびISO/IEC 24745のテンプレート保護指針に準拠し、ファジーエクストラクタ技術を用いて行動生体情報から暗号鍵素材を導出する生体暗号システムを定義します。

生体情報はパスワードのように取り消せないため、導出された鍵はキャンセラブル・バイオメトリクス変換と組み合わされ、テンプレートが侵害されても元の特徴そのものが恒久的に侵害されることを防ぎます。

---
### 1. 生体鍵導出のリスク
生体情報から鍵への安易なマッピングに伴う構造的脆弱性:

* **再現性のない生の生体信号**: 行動生体測定値は測定のたびにわずかに変動するため、厳密な一致を要求する暗号方式は、明示的な誤差許容の仕組みなしには正規の入力から同じ鍵を再現できません。
* **侵害された生体テンプレートの取り消し不可能性**: 従来のパスワードは侵害後にリセットできますが、生の生体特徴はそうできません。つまり、保護されていない生体データから直接鍵を導出する安易な方式は、テンプレートが一度でも漏洩すると恒久的な露出を生み出します。
* **行動信号における限られたエントロピー**: タイピングリズムなどの行動生体測定値は有限で測定可能なエントロピーしか持たず、それは適切に生成された暗号鍵よりも低いため、無制限であると想定するのではなく考慮に入れる必要があります。

### 2. ファジーエクストラクタとテンプレート保護の基盤
誤差許容型の鍵導出とキャンセラブル・バイオメトリクス:

* **ファジーエクストラクタによる鍵導出**: 確立された生体暗号システム研究と整合するファジーエクストラクタ方式は、繰り返される生体測定のわずかな変動を許容しつつ、同じ導出鍵を確実に再現します。
* **キャンセラブル・バイオメトリクス変換**: 生体特徴は、鍵導出前にISO/IEC 24745の生体情報保護と整合する取り消し可能かつ非可逆な変換を経ており、変換が侵害されても元の特徴を破棄することなく取り消し・再発行できます。
* **継続的認証の信号との整合**: 鍵導出の入力は、テクニカルペーパーシリーズ #013 で定義した行動生体ベースラインと同じものから取得され、別々の矛盾した行動プロファイルを維持するのではなく2つのシステムを整合させます。

### 3. 登録と導出の手順
ベースライン登録・変換適用・鍵抽出:

1. **ベースラインとなる生体情報の登録**: 後の鍵導出に用いる参照テンプレートを確立するため、初期の行動生体測定値のセットが収集されます。
2. **キャンセラブル変換の適用**: 登録されたテンプレートは、暗号素材が導出される前に取り消し可能な変換を経るため、元の生の特徴が直接保存されることはありません。
3. **ファジーエクストラクタによる鍵の再構成**: 使用のたびに、新たな生体入力は保存済みのヘルパーデータと組み合わされて同じ導出鍵を再構成し、元のテンプレートを明かすことなく自然な変動を許容します。

### 4. テンプレートガバナンスと失効レビュー
侵害対応と変換のローテーション:

* **定義済みの失効手順**: テンプレートが侵害された疑いがある場合にキャンセラブル変換を失効・再発行する文書化された手順が存在し、生体情報の侵害を回復不能なものとして扱うことはありません。
* **ヘルパーデータと生の生体保存の分離**: 鍵再構成に用いるヘルパーデータは、生の生体参照データとは別に保存され、いずれか一方のみが侵害された場合に攻撃者が得られるものを制限します。
* **エントロピーと誤一致率の継続的監査**: 導出方式の実効エントロピーと誤一致率は、最新の研究に照らして定められた周期でレビューされます。測定技術やなりすまし技術の進歩により、生体の一意性に関する前提が弱まる可能性があるためです。

### 5. 結論
生体特徴は変更できないため、パスワードの代替としては不向きであり、だからこそ鍵導出は取り消し可能な変換を経る必要があり、その手順を省略することはできません。

ファジーエクストラクタとキャンセラブル・バイオメトリクスを組み合わせることは、CISSPドメイン3およびISO/IEC 24745に沿いつつ、生体由来の鍵を、侵害された際の恒久的な負債ではなく実用的なものにします。
