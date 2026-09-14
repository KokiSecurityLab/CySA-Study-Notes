# Koki's Technical Paper #034

## Automated Defense — Implementing SOAR for Protection, Machine-Speed Triage, and Cloud Security Operations

### Summary Digest
This paper defines a Security Orchestration, Automation, and Response (SOAR) framework, aligned with CISSP Domain 7, that executes pre-approved playbooks to contain confirmed indicators of compromise without waiting for manual analyst action.

Automated token revocation and micro-segmentation reduce containment time from hours to seconds for well-defined, high-confidence detections.

---
### 1. Manual-Triage Latency Risk
Structural Vulnerabilities of Analyst-Dependent Response:

* **Coverage Gaps During Off-Hours**: Environments that depend entirely on human analysts for containment have reduced response capability during off-hours or maintenance windows, leaving confirmed threats unaddressed for longer.
* **SIEM Alerts Without Automated Action**: A SIEM platform that generates alerts but has no automated response path still depends on an analyst to manually execute containment, adding delay between detection and action.
* **Analyst Fatigue and Inconsistent Response**: High alert volume handled entirely through manual review increases the chance that a given incident is triaged inconsistently or missed due to reviewer fatigue.

### 2. SOAR Playbook Foundation
Orchestration Triggers and Automated Action Principles:

* **Event-Driven Playbook Triggers**: The SOAR platform ingests alerts from the SIEM defined in Technical Paper #002 and triggers a corresponding playbook automatically when a match against defined criteria is confirmed.
* **Pre-Approved Automated Actions**: Playbook actions, such as token revocation or host isolation, are pre-approved and scoped in advance, so execution does not require real-time human sign-off for well-defined, high-confidence cases.
* **Human Escalation for Ambiguous Cases**: Alerts that do not clearly match a pre-approved playbook are routed to human review, consistent with the escalation approach defined in Technical Paper #018, rather than triggering an automated action by default.

### 3. Automated Containment Sequence
Detection, Token Revocation, and Isolation Stages:

1. **High-Confidence Detection Matching**: Incoming alerts are matched against playbook trigger criteria, and only those meeting a defined confidence threshold proceed to automated action.
2. **Automated Credential Revocation**: Network authorization tokens associated with a confirmed compromised account or session are revoked immediately upon trigger, without waiting for manual approval.
3. **Host and Segment Isolation**: The affected host or network segment is automatically isolated, consistent with the containment approach defined in Technical Paper #033, pending further investigation.

### 4. Playbook Governance and Execution Auditing
Action Scope Review and Logged Accountability:

* **Scoped Playbook Authority**: Each playbook is limited to a specific, pre-approved set of actions, preventing automation from taking an action beyond what was explicitly reviewed and authorized.
* **Complete Logging of Automated Actions**: Every action a SOAR playbook takes is logged with its trigger, timestamp, and outcome, consistent with the accountability-logging approach defined in Technical Paper #018.
* **Continuous Playbook Accuracy Review**: False-positive and false-negative rates for each playbook are reviewed on a defined cadence, adjusting trigger criteria that generate too many unnecessary automated actions.

### 5. Conclusion
Automation only helps if it acts on cases well-defined enough to automate, which is why ambiguous alerts still need a human reviewer.

Reducing containment time from hours to seconds for high-confidence detections, per CISSP Domain 7, is what SOAR changes, not the need for judgment elsewhere.

---
# テクニカルペーパーシリーズ #034

## 自動化された防御 — 保護のためのSOAR実装、マシンスピードの選別、およびクラウドセキュリティ運用

### サマリー・ダイジェスト
本論文は、CISSPドメイン7に準拠したSOAR（セキュリティオーケストレーション・自動化・対応）フレームワークを定義し、手動でのアナリスト対応を待たずに、確認済みの侵害指標を封じ込めるため事前承認済みのプレイブックを実行します。

自動化されたトークン失効とマイクロセグメンテーションにより、明確に定義された高信頼度の検知については、封じ込め時間を時間単位から秒単位へ短縮します。

---
### 1. 手動選別の遅延リスク
アナリスト依存型対応に伴う構造的脆弱性:

* **時間外におけるカバレッジの欠落**: 封じ込めを完全に人間のアナリストに依存する環境は、時間外やメンテナンス期間中の対応能力が低下し、確認済みの脅威への対処がより長く放置されます。
* **自動対応を伴わないSIEMアラート**: アラートを生成するだけで自動対応経路を持たないSIEMプラットフォームは、封じ込めの手動実行を依然としてアナリストに依存しており、検知から対応までの遅延を生みます。
* **アナリストの疲労と一貫性のない対応**: 高いアラート量をすべて手動レビューで処理すると、レビュー担当者の疲労により、ある事案の選別が一貫性を欠いたり見落とされたりする可能性が高まります。

### 2. SOARプレイブックの基盤
オーケストレーションのトリガーと自動アクションの原則:

* **イベント駆動型のプレイブックトリガー**: SOARプラットフォームは テクニカルペーパーシリーズ　#002　で定義したSIEMからアラートを取り込み、定義済みの基準との一致が確認されると対応するプレイブックを自動的に起動します。
* **事前承認済みの自動アクション**: トークン失効やホスト隔離などのプレイブックアクションは事前に承認・範囲設定されており、明確に定義された高信頼度の事案についてはリアルタイムでの人間の承認を必要としません。
* **曖昧な事案の人的エスカレーション**: 事前承認済みのプレイブックに明確に一致しないアラートは、既定で自動アクションを起動するのではなく、テクニカルペーパーシリーズ　#018　で定義したエスカレーションアプローチに沿って人的レビューへ回されます。

### 3. 自動封じ込めの手順
検知・トークン失効・隔離の各段階:

1. **高信頼度の検知照合**: 着信アラートはプレイブックのトリガー基準と照合され、定義済みの信頼度しきい値を満たすもののみが自動アクションへ進みます。
2. **自動化された資格情報の失効**: 確認済みの侵害アカウントまたはセッションに紐づくネットワーク認可トークンは、手動承認を待たずにトリガー時点で即座に失効させられます。
3. **ホストおよびセグメントの隔離**: 影響を受けたホストまたはネットワークセグメントは、テクニカルペーパーシリーズ　#033　で定義した封じ込めアプローチと整合する形で、さらなる調査を待つ間自動的に隔離されます。

### 4. プレイブックガバナンスと実行監査
アクション範囲のレビューと記録された説明責任:

* **範囲設定されたプレイブック権限**: 各プレイブックは特定の事前承認済みアクションのセットに限定され、明示的にレビュー・承認された範囲を超えた自動アクションが実行されることを防ぎます。
* **自動アクションの完全なログ記録**: SOARプレイブックが実行する各アクションは、そのトリガー・タイムスタンプ・結果とともに、テクニカルペーパーシリーズ　#018　で定義した説明責任のログ記録アプローチと整合する形で記録されます。
* **プレイブック精度の継続的レビュー**: 各プレイブックの偽陽性率・偽陰性率は定められた周期でレビューされ、不要な自動アクションを過剰に発生させているトリガー基準を調整します。

### 5. 結論
自動化が役立つのは、実際に自動化するのに十分なほど明確に定義された事案に対してのみであり、だからこそ曖昧なアラートは依然として人間のレビュー担当者に届く必要があります。

高信頼度の検知に対する封じ込め時間を時間単位から秒単位へ短縮すること、これがCISSPドメイン7に沿ったSOARの変化であり、それ以外の判断に対するアナリストの必要性をなくすものではありません。
