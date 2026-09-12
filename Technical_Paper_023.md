arkdown
# Koki's Technical Paper #023

## AI Hallucinations — Theory of Information Gravity via Grounding, Generative Output Governance, and RAG Integrity Verification

### Summary Digest
This paper defines a RAG verification framework, aligned with CISSP Domain 8 and NIST AI RMF, that scores each generated claim by how well retrieved passages support it.

Claims below a defined support threshold, termed an information-gravity score, are withheld or flagged for review rather than returned as fact.

---
### 1. Ungrounded Generation Risk
Structural Risks of Unverified Language-Model Output:

* **High-Confidence Fabrication**: Language models can produce fluent, confidently-phrased statements that are factually incorrect, a documented failure mode commonly referred to as hallucination, without any signal in the output format itself indicating reduced reliability.
* **Retrieval Bypass Under Load or Failure**: Systems that fall back to generating from parametric knowledge alone when a retrieval step fails or times out lose the grounding that RAG is intended to provide, without necessarily surfacing that degradation to the user.
* **Superficially Plausible Unsupported Claims**: Generated text that closely mimics the style of grounded, well-cited content can be mistaken for verified output even when no retrieved passage actually supports the specific claim being made.

### 2. Faithfulness Scoring Foundation
Retrieval Grounding and Claim-Support Measurement:

* **Mandatory Retrieval Before Generation**: The language model is required to retrieve relevant source passages before generating a response, consistent with the Retrieval-Augmented Generation (RAG) approach.
* **Information-Gravity Scoring**: Each generated claim is scored for how directly it is supported by the retrieved passages, using entailment-based comparison between the claim and the source text rather than the model's own stated confidence.
* **Alignment with Human-Escalation Controls**: Claims that score below a defined support threshold are escalated according to the human-review process defined in Technical Paper #018, rather than being returned to the user unmodified.

### 3. Retrieval, Scoring, and Filtering Sequence
Three-Stage Fact-Checking Pipeline:

1. **Source Retrieval and Ranking**: Relevant passages are retrieved from an authenticated knowledge base and ranked by relevance before being passed to the generation step.
2. **Claim-Level Support Scoring**: Each factual claim in the generated response is compared against the retrieved passages, and an information-gravity score is calculated based on the degree of textual and semantic support found.
3. **Threshold-Based Filtering**: Claims scoring below the defined threshold are removed, rephrased as uncertain, or routed to human review before the response is returned.

### 4. Retrieval Pipeline Governance
Knowledge-Base Integrity and Scoring Model Review:

* **Restricting Generation to Authenticated Sources**: The retrieval step draws only from a defined, access-controlled knowledge base, consistent with the source-verification approach defined in Technical Paper #011, rather than an open-ended external search.
* **Logged Retrieval-to-Claim Mapping**: The specific passages used to support each claim are logged alongside the response, providing an audit trail that connects generated text back to its source material.
* **Continuous Scoring-Model Calibration**: The information-gravity scoring model is periodically reviewed against manually verified examples to confirm it still distinguishes supported from unsupported claims accurately.

### 5. Conclusion
A model's fluency says nothing about whether a specific claim is actually supported by a retrieved source, which is why support must be measured separately.

Scoring claims against retrieved passages, per CISSP Domain 8 and NIST AI RMF, gives grounds to withhold a claim rather than present it as fact.

---
# テクニカルペーパーシリーズ #023

## AIハルシネーション — グラウンディングによる情報重力理論、生成出力ガバナンス、およびRAG完全性検証

### サマリー・ダイジェスト
本論文は、CISSPドメイン8およびNIST AI RMFに準拠したRAG（検索拡張生成）検証フレームワークを定義し、生成された各主張を、取得済みの文書によってどれだけ裏付けられているかでスコアリングします。

定義済みの裏付けしきい値を下回る主張は「情報重力スコア」と呼ばれる指標に基づき、事実として返されるのではなく保留またはレビュー対象としてフラグ付けされます。

---

### 1. 未接地な生成のリスク
未検証の言語モデル出力に伴う構造的リスク:

* **高い確信度を伴う捏造**: 言語モデルは、事実に反する内容であっても流暢で確信度の高い言い回しの文章を生成することがあります。これは一般に「ハルシネーション」と呼ばれる文書化された失敗モードであり、出力の見た目自体には信頼性低下を示す手がかりがありません。
* **負荷・障害時の検索バイパス**: 検索ステップが失敗またはタイムアウトした際にパラメトリック知識のみからの生成へフォールバックするシステムは、RAGが本来提供するはずの裏付けを失いますが、その劣化がユーザーに必ずしも明示されるとは限りません。
* **表面的にもっともらしい未裏付けの主張**: 根拠のある、よく引用された内容の文体を巧妙に模倣した生成テキストは、実際にはその特定の主張を裏付ける取得済み文書が存在しない場合でも、検証済みの出力と誤認される可能性があります。

### 2. 忠実性スコアリングの基盤
検索による裏付けと主張支持度の測定:

* **生成前の検索の必須化**: 言語モデルは、応答を生成する前に関連する情報源を検索することを義務付けられます。これはRAG（検索拡張生成）のアプローチと整合します。
* **情報重力スコアリング**: 生成された各主張は、モデル自身が述べる確信度ではなく、主張と情報源テキストとの含意関係に基づく比較を用いて、取得済み文書によってどれだけ直接的に裏付けられているかでスコアリングされます。
* **人的エスカレーション統制との整合**: 定義済みの裏付けしきい値を下回る主張は、無修正のままユーザーへ返されるのではなく、Technical Paper #018で定義した人的レビュープロセスに沿ってエスカレーションされます。

### 3. 検索・スコアリング・フィルタリングの手順
3段階のファクトチェックパイプライン:

1. **情報源の検索とランキング**: 生成ステップへ渡される前に、認証済みのナレッジベースから関連する文書を検索し、関連度に応じてランキングします。
2. **主張単位の支持度スコアリング**: 生成された応答内の各事実主張を取得済み文書と照合し、見つかったテキスト的・意味的な裏付けの程度に基づいて情報重力スコアを算出します。
3. **しきい値に基づくフィルタリング**: 定義済みのしきい値を下回る主張は、応答が返される前に削除、不確実である旨への言い換え、または人的レビューへの回付が行われます。

### 4. 検索パイプラインのガバナンス
ナレッジベースの完全性とスコアリングモデルのレビュー:

* **生成対象を認証済みソースに限定**: 検索ステップは、無制限な外部検索ではなく、Technical Paper #011で定義したソース検証アプローチと整合する、定義済みでアクセス制御されたナレッジベースのみを参照します。
* **検索結果と主張の対応関係の記録**: 各主張を裏付けるために使用された具体的な文書は応答とともに記録され、生成テキストを情報源まで遡って追跡できる監査証跡を提供します。
* **スコアリングモデルの継続的な較正**: 情報重力スコアリングモデルは、手動で検証済みの事例と照合して定期的にレビューされ、裏付けのある主張とない主張を引き続き正確に区別できているかを確認します。

### 5. 結論
モデルの流暢さは、ある主張が実際に取得済みの情報源によって裏付けられているかどうかについて何も示さないため、その裏付けは別途測定する必要があります。

取得済みの文書と主張を照合してスコアリングすることは、CISSPドメイン8およびNIST AI RMFに沿いつつ、主張を事実として提示するのではなく保留する根拠をこのシステムに与えます。
