# Koki's Technical Paper #068

## Wireless Security — WPA3 SAE Handshake Implementation, Rogue Access Point Detection, and Enterprise 802.1X Integration

### Summary Digest
This paper defines a wireless security architecture, aligned with CISSP Domain 4 and WPA3, using SAE (Simultaneous Authentication of Equals) to resist the offline dictionary attacks that affect its predecessor, WPA2.

Enterprise deployments integrate WPA3-Enterprise with 802.1X authentication, consistent with the approach in Technical Paper #066, rather than relying on a single shared passphrase.

---
### 1. Legacy Handshake Exposure Risk
Structural Vulnerabilities of Pre-WPA3 Wireless Protocols:

* **Offline Dictionary Attacks Against WPA2-PSK**: The WPA2 four-way handshake exposes enough information for an attacker to attempt offline password guessing without further interaction with the network, a documented weakness WPA3's SAE handshake was designed to close.
* **Rogue Access Points Mimicking Legitimate SSIDs**: A device broadcasting the same network name as a legitimate access point can trick clients into connecting to it, enabling interception of their traffic through an evil-twin attack.
* **Shared Passphrase Across All Users**: A single shared passphrase used by every device on a personal-mode network provides no way to revoke access for one specific device without changing the passphrase for everyone.

### 2. WPA3 and Enterprise Authentication Foundation
SAE Handshake and 802.1X Integration Principles:

* **Simultaneous Authentication of Equals (SAE)**: The SAE handshake used in WPA3-Personal replaces the WPA2 four-way handshake with a protocol resistant to offline dictionary attacks, since each failed guess requires live interaction with the network. The password element is derived with the hash-to-element (H2E) method, mandatory for Wi-Fi 6E and Wi-Fi 7, which replaces the original hunting-and-pecking method that the 2019 Dragonblood research showed could leak information through timing and cache side channels.
* **WPA3-Enterprise with 802.1X**: Enterprise deployments authenticate individual devices through 802.1X port-based access control, consistent with the approach defined in Technical Paper #066, rather than a single shared credential, with EAP-TLS certificates giving each device a credential of its own.
* **Protected Management Frames**: Protected Management Frames (PMF), mandatory under WPA3, prevent an attacker from forging deauthentication frames to forcibly disconnect legitimate clients, a technique previously usable to support evil-twin attacks; Wi-Fi 7 additionally requires beacon protection.

### 3. Deployment and Rogue Detection Sequence
Handshake Configuration, Enterprise Enrollment, and Monitoring:

* **WPA3 Handshake Configuration**: Access points are configured to require the WPA3 SAE handshake, and WPA3 transition mode is retired once connecting devices support WPA3, since the Dragonblood research demonstrated a downgrade and dictionary attack against networks running in that mode. Devices that support only WPA2 are moved to a separate SSID on an isolated segment, consistent with the segmentation approach defined in Technical Paper #067.
* **Enterprise Device Enrollment**: Devices are enrolled with individual 802.1X credentials, such as per-device EAP-TLS certificates, rather than a shared passphrase, so access can be revoked for one device without affecting the others.
* **Rogue Access Point Monitoring**: A wireless intrusion detection system continuously scans for access points broadcasting legitimate SSIDs without authorization, flagging matches for investigation.

### 4. Wireless Governance and Rogue Response Review
Detection Accuracy and Credential Revocation Auditing:

* **Documented Rogue Response Procedure**: Detected rogue access points trigger a documented investigation and, where confirmed unauthorized, physical location and removal procedure.
* **Per-Device Credential Revocation Tracking**: Individual device credential revocations are tracked and confirmed effective, consistent with the access-revocation approach defined in Technical Paper #054.
* **Continuous WIDS Detection Accuracy Review**: Wireless intrusion detection alerts are reviewed on a defined cadence to tune detection sensitivity and confirm legitimate access points are not falsely flagged.

### 5. Conclusion
A shared passphrase cannot be revoked for one device without disrupting every other device using it, which is exactly the problem individual 802.1X credentials solve.

Requiring the WPA3 SAE handshake and per-device enterprise authentication, consistent with CISSP Domain 4, closes both the offline-guessing weakness and the shared-credential weakness at once, and WPA3 is already the baseline that the 6 GHz band and Wi-Fi 7 require.
日本語版

# テクニカルペーパーシリーズ #068

## 無線セキュリティ — WPA3 SAEハンドシェイクの実装、不正アクセスポイント検知、およびエンタープライズ802.1X統合

### サマリー・ダイジェスト
本論文は、CISSPドメイン4およびWPA3標準に準拠した無線セキュリティアーキテクチャを定義し、前身のWPA2に影響するオフライン辞書攻撃に耐性を持つSAE（同時等価者認証）を用います。

エンタープライズ展開では、単一の共有パスフレーズに頼るのではなく、テクニカルペーパーシリーズ #066 で定義したアプローチと整合する形でWPA3-Enterpriseと802.1X認証を統合します。

---
### 1. レガシーハンドシェイクへの露出リスク
WPA3以前の無線プロトコルに伴う構造的脆弱性:

* **WPA2-PSKに対するオフライン辞書攻撃**: WPA2の4ウェイハンドシェイクは、攻撃者がネットワークとのそれ以上のやり取りなしにオフラインでパスワード推測を試みるのに十分な情報を露出させます。これはWPA3のSAEハンドシェイクが解消するよう設計された、文書化された弱点です。
* **正規SSIDを模倣する不正アクセスポイント**: 正規のアクセスポイントと同じネットワーク名をブロードキャストするデバイスは、クライアントをだましてそれに接続させ、エビルツイン攻撃を通じてそのトラフィックの傍受を可能にします。
* **全ユーザー共通の共有パスフレーズ**: パーソナルモードのネットワークですべてのデバイスが使用する単一の共有パスフレーズは、全員のパスフレーズを変更することなく特定の1台のアクセスを失効させる手段を提供しません。

### 2. WPA3とエンタープライズ認証の基盤
SAEハンドシェイクと802.1X統合の原則:

* **同時等価者認証（SAE）**: WPA3-Personalで使用されるSAEハンドシェイクは、WPA2の4ウェイハンドシェイクを、失敗した推測1回ごとにネットワークとのライブなやり取りを必要とするオフライン辞書攻撃耐性のあるプロトコルに置き換えます。パスワード要素の導出には、Wi-Fi 6EとWi-Fi 7で必須とされるハッシュ・トゥ・エレメント（H2E）方式を用います。これは、2019年のDragonblood研究がタイミングやキャッシュのサイドチャネルを通じて情報を漏えいし得ると示した、従来のハンティング・アンド・ペッキング方式に代わるものです。
* **802.1XによるWPA3-Enterprise**: エンタープライズ展開では、単一の共有資格情報ではなく、テクニカルペーパーシリーズ #066 で定義したアプローチと整合する形で802.1Xポートベースアクセス制御を通じて個々のデバイスを認証し、EAP-TLS証明書によって各デバイスに固有の資格情報を持たせます。
* **保護管理フレーム**: WPA3で必須とされる保護管理フレーム（PMF）は、攻撃者が偽造した認証解除フレームを用いて正規のクライアントを強制的に切断することを防ぎます。これは以前はエビルツイン攻撃を支えるために利用できた手法であり、Wi-Fi 7ではさらにビーコン保護も必須とされています。

### 3. 展開と不正検知の手順
ハンドシェイク設定・エンタープライズ登録・監視:

* **WPA3ハンドシェイクの設定**: アクセスポイントはWPA3 SAEハンドシェイクを要求するよう設定され、接続するデバイスがWPA3に対応した時点でWPA3トランジションモードは廃止されます。Dragonblood研究が、このモードで運用されるネットワークに対するダウングレード攻撃と辞書攻撃を実証しているためです。WPA2のみに対応するデバイスは、テクニカルペーパーシリーズ #067 で定義したセグメンテーションのアプローチと整合する形で、隔離されたセグメント上の別のSSIDへ移されます。
* **エンタープライズデバイスの登録**: デバイスは共有パスフレーズではなく、デバイスごとのEAP-TLS証明書のような個別の802.1X資格情報で登録され、他のデバイスに影響を与えることなく1台のアクセスだけを失効できるようにします。
* **不正アクセスポイントの監視**: 無線侵入検知システムは、正規のSSIDを無許可でブロードキャストしているアクセスポイントを継続的にスキャンし、一致した場合は調査対象としてフラグ付けします。

### 4. 無線ガバナンスと不正対応レビュー
検知精度と資格情報失効の監査:

* **文書化された不正対応手順**: 検知された不正アクセスポイントは文書化された調査を発動させ、無許可であることが確認された場合は物理的な特定と撤去の手順に進みます。
* **デバイスごとの資格情報失効の追跡**: 個々のデバイスの資格情報失効は、テクニカルペーパーシリーズ #054 で定義したアクセス失効アプローチと整合する形で追跡され、有効であることが確認されます。
* **WIDS検知精度の継続的レビュー**: 無線侵入検知のアラートは、検知感度を調整し正規のアクセスポイントが誤ってフラグ付けされていないことを確認するため、定められた周期でレビューされます。

### 5. 結論
共有パスフレーズは、それを使用している他のすべてのデバイスに影響を与えることなく特定の1台だけを失効させることができず、これはまさに個別の802.1X資格情報が解決する問題です。

WPA3のSAEハンドシェイクとデバイスごとのエンタープライズ認証の両方を要求することは、CISSPドメイン4に沿いつつ、オフライン推測の弱点と共有資格情報の弱点を同時に解消し、WPA3はすでに6 GHz帯とWi-Fi 7が求める基準となっています。
