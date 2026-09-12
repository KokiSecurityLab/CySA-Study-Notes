# Koki's Technical Paper #020

## Binary Ethics — Programming "Good Intent" into AI, Secure Development Lifecycle Guardrails, and Prompt Injection Mitigation

### Summary Digest
This paper defines a guardrail-classifier architecture for AI systems, aligned with CISSP Domain 8 and NIST AI RMF, screening prompts and generated output against policy before a response is returned.

Content that violates policy is blocked or routed for review, keeping refusal decisions auditable, not implicit in model weights alone.

---
### 1. Guardrail Bypass Risk
Structural Vulnerabilities of Unfiltered Model Output:

* **Absence of Output-Side Policy Enforcement**: Systems that filter only inbound prompts, without also screening generated output, remain exposed to policy-violating content that a model produces on its own without an explicit malicious prompt.
* **Prompt Injection Targeting Model Behavior**: Adversarial inputs crafted to override a model's intended instructions, documented as LLM01 in the OWASP Top 10 for LLM Applications, can cause a model to bypass its own configured guardrails.
* **Reliance on Training-Time Alignment Alone**: Depending solely on the behavior instilled during model training, without a separate runtime enforcement layer, leaves no independent control if the underlying model's behavior degrades or drifts after deployment.

### 2. Independent Runtime Enforcement Layer
Layered Guardrail and Policy Enforcement Principles:

* **Runtime Classifier Enforcement**: A dedicated classifier evaluates both incoming prompts and generated output against a defined policy, operating independently of the underlying model's own training-time alignment.
* **Defense-in-Depth Guardrail Layering**: Multiple, independently maintained guardrail checks are applied in sequence, so that a bypass of one check does not automatically result in an unfiltered output.
* **Alignment with Human-Oversight Controls**: Content flagged by the guardrail layer as ambiguous or high-risk is escalated according to the human-review process defined in Technical Paper #018, rather than being resolved automatically.

### 3. Bidirectional Policy Screening
Prompt and Output Screening Workflow:

1. **Inbound Prompt Screening**: Incoming prompts are evaluated against the policy classifier before being passed to the underlying model, flagging requests that clearly violate policy prior to generation.
2. **Outbound Output Screening**: Generated output is evaluated against the same policy classifier before being returned to the requester, catching policy violations that were not present in the original prompt.
3. **Logged Escalation for Ambiguous Cases**: Content that the classifier flags as ambiguous, rather than clearly compliant or clearly violating, is logged and routed to human review consistent with Technical Paper #018.

### 4. Decoupled Policy Update Path
Policy Update and Bypass Review:

* **Independent Update Path for Guardrail Policy**: Guardrail policy definitions are updated through a process separate from model retraining, allowing policy changes to be deployed without waiting for a full model update cycle.
* **Isolation of Guardrail Logic from Model Weights**: Guardrail enforcement runs as a separate component from the underlying model, so a change in model behavior after an update does not silently remove existing policy checks.
* **Continuous Bypass-Attempt Auditing**: Ongoing review of flagged prompt-injection attempts and near-miss guardrail bypasses functions as a detective control, informing updates to the classifier rather than assuming the current policy remains sufficient indefinitely.

### 5. Conclusion
A model's training-time alignment and a runtime guardrail layer catch different failure modes; neither alone covers what the other is built to catch.

Keeping guardrail updates independent of model retraining, consistent with CISSP Domain 8 and NIST AI RMF, lets policy changes reach production without a full redeployment.

---
# テクニカルペーパーシリーズ #020

## バイナリ・エシックス — AIへの「善意」のプログラミング、セキュアな開発ライフサイクルのガードレール、およびプロンプトインジェクション対策

### サマリー・ダイジェスト
本論文は、CISSPドメイン8およびNIST AI RMFに準拠したガードレール分類器アーキテクチャをAIシステム向けに定義し、応答を返す前にプロンプトと生成出力の両方をポリシーと照合します。

ポリシーに違反するコンテンツはブロックまたはレビューへ回され、拒否判断はモデルの重みに暗黙的に組み込まれるのではなく、監査可能な状態に保たれます。

---
### 1. ガードレール回避リスク
未フィルタリングのモデル出力に伴う構造的脆弱性:

* **出力側でのポリシー適用の欠如**: 着信するプロンプトのみをフィルタリングし生成出力を検査しないシステムは、明示的な悪意あるプロンプトがなくとも、モデルが自ら生成してしまうポリシー違反コンテンツにさらされたままとなります。
* **モデルの挙動を狙ったプロンプトインジェクション**: モデルの意図された指示を上書きするよう作られた敵対的な入力は、OWASP LLM Top 10でLLM01として文書化されており、モデルに自らの設定済みガードレールを回避させ得ます。
* **学習時アライメントのみへの依存**: 独立した実行時の適用層を持たず、学習時にモデルへ植え付けられた挙動のみに依存すると、デプロイ後にモデルの挙動が劣化・変質した場合に独立した統制が存在しません。

### 2. 学習とは独立した実行時適用層
多層的なガードレールとポリシー適用の原則:

* **実行時分類器による適用**: 専用の分類器が、着信プロンプトと生成出力の両方を定義済みのポリシーと照合して評価し、モデル自体の学習時アライメントとは独立して動作します。
* **多層防御によるガードレールの重ね合わせ**: 独立して維持される複数のガードレールチェックを順に適用し、いずれか1つの回避が自動的に未フィルタリングの出力につながらないようにします。
* **人的監視統制との整合**: ガードレール層が曖昧または高リスクと判定したコンテンツは、自動的に解決するのではなく、Technical Paper #018で定義した人的レビュープロセスに沿ってエスカレーションされます。

### 3. 双方向のポリシースクリーニング
プロンプトと出力のスクリーニングワークフロー:

1. **入力プロンプトのスクリーニング**: 着信プロンプトは基盤モデルへ渡される前にポリシー分類器と照合され、生成前の時点で明確にポリシーへ違反するリクエストにフラグを立てます。
2. **出力のスクリーニング**: 生成された出力は要求元へ返される前に同じポリシー分類器と照合され、元のプロンプトには存在しなかったポリシー違反を検出します。
3. **曖昧な事案のログ記録とエスカレーション**: 分類器が明確な準拠・違反のいずれとも判定できず曖昧と判定したコンテンツは記録され、Technical Paper #018と整合する形で人的レビューへ回されます。

### 4. モデルから切り離されたポリシー更新経路
ポリシー更新と回避事例のレビュー:

* **ガードレールポリシーの独立した更新経路**: ガードレールのポリシー定義はモデルの再学習とは別のプロセスで更新され、モデルの完全な更新サイクルを待たずにポリシー変更を展開できます。
* **ガードレールロジックとモデルの重みの分離**: ガードレールの適用は基盤モデルとは別のコンポーネントとして動作するため、更新後にモデルの挙動が変化しても、既存のポリシーチェックが気づかぬうちに失われることはありません。
* **回避試行の継続的監査**: フラグ付けされたプロンプトインジェクションの試みやガードレール回避の未遂事例を継続的にレビューすることは検知的統制として機能し、現行ポリシーが今後も十分であると前提するのではなく、分類器の更新につなげます。

### 5. 結論
モデルの学習時アライメントと実行時のガードレール層はそれぞれ異なる失敗モードを捉えるものであり、どちらか一方だけでもう一方の役割を代替することはできません。

ガードレールの更新をモデルの再学習から独立させておくことは、CISSPドメイン8およびNIST AI RMFに沿いつつ、完全な再デプロイを待たずにポリシー変更を本番へ反映することを可能にします。
