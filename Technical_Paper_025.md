# Koki's Technical Paper #025

## Deepfake Detection — Biometric Resonance & Artifact Metrics, Liveness Verification, and Content Provenance Cross-Checking

### Summary Digest
This paper defines a deepfake-detection framework combining physiological liveness signals with visual artifact analysis, aligned with CISSP Domain 5 and ISO/IEC 30107 presentation-attack-detection practices.

Content lacking a detectable pulse signal or exhibiting known synthetic-media artifacts is flagged for additional verification rather than accepted as a genuine video source.

---
### 1. Synthetic Media Exposure
Structural Risks of Unverified Video and Audio Sources:

* **Statistical Fidelity of Generative Media**: Modern generative models can reproduce facial and vocal characteristics with a level of statistical fidelity that makes visual inspection alone an unreliable authentication method.
* **Absence of Physiological Signal Verification**: Systems that authenticate a video source using only facial-recognition matching, without checking for physiological signals such as pulse-driven color variation, cannot distinguish a high-fidelity synthetic face from a live one.
* **Impersonation of Trusted Individuals**: Synthetic media impersonating a known, trusted individual can be used to support social-engineering attempts, such as a fraudulent video call requesting an urgent action.

### 2. Physiological and Artifact Signal Foundation
Remote Pulse Detection and Visual Artifact Analysis:

* **Remote Photoplethysmography (rPPG) Signal Analysis**: Subtle color variation in facial video caused by blood flow is measured as a physiological liveness signal; synthetic video frequently lacks this signal or reproduces it inconsistently.
* **GAN-Fingerprint and Blending-Boundary Detection**: Generated media often carries statistical artifacts characteristic of the generation process, including inconsistent blending boundaries around the face, which can be detected through established forensic image-analysis techniques.
* **Alignment with Content Provenance Verification**: Physiological and artifact-based findings are reconciled with the content-provenance verification approach defined in Technical Paper #011, combining detection-based and provenance-based evidence.

### 3. Liveness and Provenance Verification Sequence
Signal Extraction, Artifact Scoring, and Cross-Verification:

1. **Physiological Signal Extraction**: The rPPG pulse signal and other physiological indicators are extracted from the incoming video stream and compared against expected characteristics of live human tissue.
2. **Artifact Scoring**: Facial and audio artifacts are scored against known generative-model signatures maintained in a reference set, flagging content with a high artifact score for further review.
3. **Provenance Cross-Check**: Where available, content-provenance credentials are checked against the C2PA-based approach defined in Technical Paper #011, providing a second, independent line of evidence.

### 4. Detection Model Governance
Model Currency and False-Result Review:

* **Isolation of Flagged Content Pending Review**: Content flagged by either the physiological or artifact-based check is held for human review before being treated as authentic, consistent with the escalation approach defined in Technical Paper #018.
* **Regular Retraining Against New Generation Techniques**: The detection model is retrained on a defined cadence against newly published generative techniques, since a model trained only on older synthetic media loses accuracy as generation methods improve.
* **Continuous False-Positive and False-Negative Auditing**: Detection accuracy is reviewed against confirmed authentic and confirmed synthetic samples on an ongoing basis, informing adjustments to the underlying detection model.

### 5. Conclusion
A convincing face is not the same as a live one; liveness detection has to rely on a signal generative models do not reliably reproduce.

Combining physiological analysis with provenance checks, consistent with CISSP Domain 5 and ISO/IEC 30107, gives this system two independent forms of evidence.

---
# テクニカルペーパーシリーズ　#025

## ディープフェイク検知 — 生体共鳴とアーティファクト指標、実体検知（ライブネス）検証、およびコンテンツ出自の相互確認

### サマリー・ダイジェスト
本論文は、CISSPドメイン5およびISO/IEC 30107のプレゼンテーション攻撃検知（PAD）実務に準拠し、生理的な実体検知信号と視覚的アーティファクト分析を組み合わせたディープフェイク検知フレームワークを定義します。

検知可能な脈拍信号を欠く、または既知の合成メディアアーティファクトを示すコンテンツは、真正な映像として受け入れるのではなく追加検証の対象としてフラグ付けされます。

---
### 1. 合成メディアへの露出
未検証の映像・音声ソースに伴う構造的リスク:

* **生成メディアの統計的忠実度**: 現代の生成モデルは、視覚的な確認だけでは信頼性のある認証手段とは言えないほどの統計的忠実度で顔や声の特徴を再現できます。
* **生理的信号検証の欠如**: 脈拍に由来する色の変化などの生理的信号を確認せず、顔認識の一致のみで映像ソースを認証するシステムは、高精度な合成顔と生きている人物とを区別できません。
* **信頼された人物へのなりすまし**: 既知の信頼された人物を模した合成メディアは、緊急の対応を要求する偽の映像通話など、ソーシャルエンジニアリングの試みを後押しするために利用され得ます。

### 2. 生理的信号とアーティファクト検知の基盤
遠隔脈拍検知と視覚的アーティファクト分析:

* **遠隔光電式容積脈波（rPPG）信号分析**: 血流に由来する顔の映像内の微細な色変化を生理的な実体検知信号として測定します。合成映像はこの信号を欠く、または不整合な形でしか再現できないことが多くあります。
* **GANフィンガープリントとブレンディング境界の検知**: 生成メディアには生成プロセス特有の統計的アーティファクトが残ることが多く、顔周辺のブレンディング境界の不整合を含め、確立されたフォレンジック画像分析技術で検出できます。
* **コンテンツ出自検証との整合**: 生理的信号およびアーティファクトに基づく所見を、Technical Paper #011で定義したコンテンツ出自検証アプローチと突き合わせ、検知ベースの根拠と出自ベースの根拠を組み合わせます。

### 3. 実体検知と出自検証の手順
信号抽出・アーティファクトスコアリング・相互検証:

1. **生理的信号の抽出**: 着信映像ストリームからrPPG脈拍信号などの生理的指標を抽出し、生きている人体組織に期待される特性と比較します。
2. **アーティファクトスコアリング**: 顔・音声のアーティファクトを、参照セットとして維持されている既知の生成モデルシグネチャと照合してスコアリングし、スコアの高いコンテンツを追加レビュー対象としてフラグ付けします。
3. **出自の相互確認**: 利用可能な場合、コンテンツの出自証明を、Technical Paper #011で定義したC2PAベースのアプローチと照合し、独立した第二の根拠を提供します。

### 4. 検知モデルのガバナンス
モデルの鮮度と誤判定のレビュー:

* **フラグ付けコンテンツのレビュー待機中の隔離**: 生理的チェックまたはアーティファクトチェックのいずれかでフラグ付けされたコンテンツは、真正なものとして扱われる前に、Technical Paper #018で定義したエスカレーションアプローチに沿って人的レビューのために保留されます。
* **新しい生成技術に対する定期的な再学習**: 検知モデルは、新たに公表された生成技術に対して定められた周期で再学習されます。古い合成メディアのみで学習したモデルは、生成手法の進化とともに精度が低下するためです。
* **偽陽性・偽陰性の継続的監査**: 検知精度は、確認済みの真正サンプルおよび確認済みの合成サンプルに照らして継続的にレビューされ、基盤となる検知モデルの調整に活用されます。

### 5. 結論
説得力のある顔だからといって、それが生きている人物であるとは限りません。だからこそ実体検知は、生成モデルが確実には再現できない信号に依拠する必要があります。

生理的信号分析とコンテンツの出自確認を組み合わせることは、CISSPドメイン5およびISO/IEC 30107に沿いつつ、このシステムに独立した2種類の根拠を与えます。
