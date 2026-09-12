# Koki's Technical Paper #005

## Python & TypeScript — Programming Synergy in AI Security, Structured Output Validation, and LLM Ingestion Control

### Summary Digest
This paper defines a secure integration pattern pairing TypeScript's static typing with Python-based AI inference services, aligned with CISSP Domain 8 and the OWASP LLM Top 10, to validate prompts and model outputs at each boundary.

Structured-output validation prevents unverified model responses from being executed as trusted application logic.

---
### 1. AI Ingestion and Output Risk
Structural Risks of Unvalidated Prompts and Model Output:

* **Prompt Injection via Unvalidated User Input**: User-supplied text forwarded directly into a model prompt without sanitization can override intended system instructions, a risk documented as LLM01 in the OWASP Top 10 for LLM Applications.
* **Unverified Structured Output Consumption**: Treating a model's JSON or function-call output as inherently trustworthy allows a manipulated response to trigger unintended application behavior, corresponding to LLM02 (Insecure Output Handling).
* **Type Ambiguity in Cross-Language Model Responses**: Passing loosely-typed model output directly into a dynamically-typed Python execution path without schema validation increases the risk that malformed fields reach downstream logic unexamined.

### 2. Static Typing and Schema Validation
Static Typing and Schema Validation Alignment for AI Interfaces:

* **Compile-Time Contract Enforcement**: A TypeScript-based interface layer defines strict types for both outbound prompts and expected model response shapes, catching structural mismatches before a request or response reaches Python services.
* **Schema Validation of Model Output**: Model responses, particularly structured tool-call or function-call output, are validated against a defined JSON schema before being accepted as input to any downstream action.
* **Alignment with CISSP Domain 8 and OWASP LLM Guidance**: Input and output validation controls for the AI interface are mapped to CISSP Domain 8 secure-development practices and the OWASP Top 10 for LLM Applications.

### 3. Frontend-to-Backend Validation Sequence
Three-Stage Validation for AI Request and Response Handling:

1. **Outbound Prompt Schema Enforcement**: The TypeScript layer validates user input against an allowed-input schema before it is incorporated into a prompt sent to the model.
2. **Inbound Output Schema Validation**: Model responses are parsed against a strict response schema in Python before any structured field is used to trigger an application action.
3. **Rejection and Logging of Non-Conforming Responses**: Responses that fail schema validation are rejected and logged for review rather than passed to execution logic (see Technical Paper #002 for related SIEM correlation).

### 4. Dependency and Interface Control
Trust Boundary Enforcement Between Model Output and Application Logic:

* **Model Output Treated as Untrusted Input**: Structured output from the model is treated with the same trust level as external user input, requiring validation before it can affect application state.
* **Restricted Tool-Call Execution Scope**: Function-calling actions requested by the model are restricted to a pre-approved allow-list of operations, preventing an unexpected or manipulated call from reaching sensitive functions.
* **Continuous Interface Contract Auditing**: The schema contract between the TypeScript interface and Python execution layer is reviewed on an ongoing basis to identify drift introduced by model or application updates.

### 5. Conclusion
Treating prompts and model output as inputs requiring validation, not trusted internal data, closes a gap generic validation patterns often miss in AI-integrated applications.

Applying CISSP Domain 8 practices alongside the OWASP LLM Top 10 gives this TypeScript-Python pairing a concrete basis for handling unpredictable model behavior.

---
# テクニカルペーパーシリーズ #005

## Python＆TypeScript — AIセキュリティにおけるプログラミングシナジー、構造化出力の検証、およびLLM入力制御

### サマリー・ダイジェスト
本論文は、CISSPドメイン8およびOWASP LLM Top 10に準拠し、TypeScriptの静的型付けとPythonベースのAI推論サービスを組み合わせた安全な統合パターンを定義し、各境界でプロンプトとモデル出力を検証します。

構造化出力の検証により、未検証のモデル応答が信頼済みのアプリケーションロジックとして実行されることを防ぎます。

---
### 1. AI入出力に関するリスク
未検証のプロンプトとモデル出力に伴う構造的リスク:

* **未検証ユーザー入力によるプロンプトインジェクション**: サニタイズされていないユーザー入力をそのままモデルへのプロンプトに組み込むと、意図したシステム指示が上書きされる恐れがあります。これはOWASP LLM Top 10のLLM01（プロンプトインジェクション）に該当します。
* **未検証の構造化出力の消費**: モデルが返すJSONや関数呼び出し出力を無条件に信頼すると、改変された応答が意図しないアプリケーション動作を引き起こす恐れがあります。これはLLM02（不適切な出力処理）に相当します。
* **言語間でのモデル応答における型の曖昧性**: 型の緩いモデル出力をスキーマ検証なしに動的型付けのPython実行経路へ直接渡すと、不正な形式のフィールドが未検査のまま下流ロジックに到達するリスクが高まります。

### 2. 静的型付けとスキーマ検証
AIインターフェースにおける静的型付けとスキーマ検証の整合:

* **コンパイル時の契約強制**: TypeScriptベースのインターフェース層が送信するプロンプトと想定されるモデル応答の形状の両方に厳格な型を定義し、リクエストや応答がPythonサービスに到達する前に構造上の不一致を検出します。
* **モデル出力のスキーマ検証**: 特に構造化されたツール呼び出しや関数呼び出しの出力を、下流アクションへの入力として受け入れる前に定義済みのJSONスキーマと照合します。
* **CISSPドメイン8およびOWASP LLMガイダンスとの整合**: AIインターフェースの入出力検証統制を、CISSPドメイン8のセキュア開発実務およびOWASP LLM Top 10に対応付けます。

### 3. フロントエンド-バックエンド検証手順
AIリクエストおよび応答処理のための3段階検証:

1. **送信プロンプトのスキーマ強制**: TypeScript層は、モデルへ送信するプロンプトに組み込まれる前のユーザー入力を許可済みスキーマと照合します。
2. **受信出力のスキーマ検証**: モデル応答は、構造化されたフィールドがアプリケーションの動作を引き起こす前に、Python側で厳格な応答スキーマと照合されます。
3. **非準拠応答の拒否とログ記録**: スキーマ検証に失敗した応答は実行ロジックへ渡されずに拒否・記録されます（SIEM連携の詳細はTechnical Paper #002を参照）。

### 4. 依存関係とインターフェース制御
モデル出力とアプリケーションロジック間の信頼境界の強制:

* **モデル出力を未信頼入力として扱う**: モデルからの構造化出力は外部ユーザー入力と同等の信頼レベルで扱われ、アプリケーションの状態に影響を与える前に検証が必要とされます。
* **ツール呼び出しの実行範囲の制限**: モデルが要求する関数呼び出しは事前承認済みの許可リストに限定され、予期しない、または改変された呼び出しが機微な機能へ到達することを防ぎます。
* **インターフェース契約の継続的監査**: TypeScriptインターフェースとPython実行層の間のスキーマ契約を継続的にレビューし、モデルまたはアプリケーションの更新によって生じる乖離を特定します。

### 5. 結論
プロンプトとモデル出力の両方を、信頼済みの内部データではなく検証が必要な入力として扱うことで、AI連携アプリケーションで見落とされがちな一般的な入力検証の隙間を解消します。

CISSPドメイン8の実務とOWASP LLM Top 10を組み合わせることで、このTypeScriptとPythonの連携は、事前に完全には予測できないモデルの挙動を扱うための具体的な基盤を得ます。
