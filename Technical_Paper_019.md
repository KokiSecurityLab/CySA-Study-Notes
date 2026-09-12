# Koki's Technical Paper #019

## AI: Ally or Adversary? — Information Integrity and AI Ethics, Synthetic Content Disclosure, and Overreliance Mitigation

### Summary Digest
This paper examines AI systems as a source and a mitigant of information-integrity risk, aligned with CISSP Domain 3, the OWASP LLM Top 10, and EU AI Act Article 50.

AI-generated content for external distribution is labeled and reviewed before publication; internal decision outputs are treated as advisory, not authoritative.

---
### 1. AI-Generated Misinformation Risk
Structural Risks of Unlabeled and Unreviewed AI Output:

* **Undisclosed Synthetic Content**: AI-generated text, images, or audio distributed without disclosure can be mistaken for authentic human-created content, complicating downstream fact-checking and source verification.
* **Overreliance on Model Output**: Treating AI-generated summaries or analysis as authoritative without independent verification allows a plausible-sounding but incorrect output, documented as LLM09 (Overreliance) in the OWASP Top 10 for LLM Applications, to propagate unchecked.
* **Scaled Generation of Coordinated Content**: The low cost of generating large volumes of AI-written content can be used to produce coordinated messaging at a scale that would be impractical to produce manually.

### 2. Methodological Foundation
Disclosure Standards and Verification Principles:

* **Synthetic Content Labeling**: AI-generated content intended for public distribution is labeled as such, consistent with the transparency obligations described in EU AI Act Article 50.
* **Content Provenance Credentials**: Where feasible, AI-generated media is tagged with content credentials, such as those defined by the Coalition for Content Provenance and Authenticity (C2PA), to preserve a verifiable record of its origin.
* **Alignment with Source-Verification Controls**: Information-integrity checks are reconciled with the source-provenance verification approach defined in Technical Paper #011, keeping AI-content review consistent with the wider data-integrity architecture.

### 3. Pipeline Implementation
Review and Disclosure Workflow:

1. **Generation-Time Tagging**: Content produced by an AI system is tagged with its generation source and confidence indicators at the point of creation, before any human review step.
2. **Human Review Prior to Publication**: AI-generated content intended for external audiences is reviewed by a designated human reviewer before publication, consistent with the escalation approach defined in Technical Paper #018.
3. **Disclosure Application**: Approved content is published with the required synthetic-content disclosure applied, and the review decision is logged for later audit.

### 4. Boundary Governance
Overreliance Mitigation and Disclosure Compliance Review:

* **Explicit Advisory Status for Automated Analysis**: AI-generated analysis used in internal decision-making is explicitly labeled as advisory input rather than a final determination, keeping accountability with the human decision-maker.
* **Separation of Content Generation from Publication Approval**: The system or process that generates AI content operates separately from the approval step that authorizes its publication, so generation volume cannot itself bypass review.
* **Continuous Disclosure Compliance Auditing**: Ongoing review of published content confirms that synthetic-content labeling requirements were applied consistently, rather than assuming compliance without verification.

### 5. Conclusion
An AI system's usefulness for detecting misinformation does not offset the risk that its own output, left unlabeled, becomes a source of the same problem.

Disclosure requirements under EU AI Act Article 50, combined with human review before publication, keep that distinction visible rather than left to guess.

---
# Koki's Technical Paper #019

## AI：味方か、それとも敵か？ — 情報の完全性とAI倫理、合成コンテンツの開示、および過信リスクの緩和

### サマリー・ダイジェスト
本論文は、CISSPドメイン3、OWASP LLM Top 10、およびEU AI法第50条に準拠し、AIシステムを情報完全性リスクの発生源であると同時にその緩和手段でもある存在として検討します。

外部配布用のAI生成コンテンツは公開前にラベル付けとレビューを行い、内部の意思決定に用いる出力は権威ある結論ではなく参考情報として扱います。

---
### 1. AI生成による誤情報リスク
未開示・未レビューのAI出力に伴う構造的リスク:

* **未開示の合成コンテンツ**: 開示なしに配布されたAI生成のテキスト・画像・音声は、真正な人間作成のコンテンツと誤認される可能性があり、下流でのファクトチェックやソース検証を複雑にします。
* **モデル出力への過信**: AI生成の要約や分析を独立した検証なしに権威あるものとして扱うと、もっともらしいが誤った出力が野放しに拡散してしまいます。これはOWASP LLM Top 10でLLM09（過信）として文書化されているリスクです。
* **協調的コンテンツの規模的生成**: 大量のAI生成コンテンツを生成する際のコストの低さは、手動では非現実的な規模での協調的なメッセージング生成に悪用され得ます。

### 2. 方法論的基盤
開示基準と検証の原則:

* **合成コンテンツのラベル付け**: 公開配布を意図したAI生成コンテンツには、EU AI法第50条が定める透明性義務に沿ってその旨のラベルを付与します。
* **コンテンツの出自証明**: 可能な場合、AI生成メディアにはCoalition for Content Provenance and Authenticity（C2PA）が定めるようなコンテンツ来歴情報を付与し、発信元の検証可能な記録を保持します。
* **ソース検証統制との整合**: 情報完全性のチェックを、Technical Paper #011で定義したソース出自検証アプローチと突き合わせ、AIコンテンツのレビューをより広いデータ完全性アーキテクチャと一貫させます。

### 3. パイプラインの実装
レビューと開示のワークフロー:

1. **生成時点でのタグ付け**: AIシステムが生成したコンテンツには、人間によるレビュー工程の前に、生成元と信頼度指標のタグが付与されます。
2. **公開前の人的レビュー**: 外部向けのAI生成コンテンツは、公開前に指定されたレビュー担当者によるレビューを受けます。これはTechnical Paper #018で定義したエスカレーションの考え方と整合します。
3. **開示の適用**: 承認済みのコンテンツは必要な合成コンテンツ開示を付与された上で公開され、レビュー判断は後の監査のために記録されます。

### 4. 境界統治
過信の緩和と開示コンプライアンスのレビュー:

* **自動分析への明示的な参考情報としての位置づけ**: 内部の意思決定に用いるAI生成の分析結果は最終判断ではなく参考情報として明示的にラベル付けされ、説明責任は人間の意思決定者に残されます。
* **コンテンツ生成と公開承認の分離**: AIコンテンツを生成する仕組みは、その公開を許可する承認工程とは別に動作するため、生成量そのものがレビューを迂回することはありません。
* **開示コンプライアンスの継続的監査**: 公開済みコンテンツを継続的にレビューし、合成コンテンツのラベル付け要件が一貫して適用されていることを、検証なしに前提とするのではなく確認します。

### 5. 結論
AIシステムが誤情報の検知に役立つとしても、その出力自体がラベル付けされないまま同じ問題の発生源になり得るリスクは相殺されません。

EU AI法第50条に基づく開示要件を公開前の人的レビューと組み合わせることで、その区別を読者の推測任せにせず可視化された状態に保ちます。
