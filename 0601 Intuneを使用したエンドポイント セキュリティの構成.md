---
lab:
  title: '演習ラボ 0601: Intune を使用したエンドポイント セキュリティの構成'
  description: このラボでは、Intune の管理対象デバイスに Microsoft Defender を構成するポリシーを作成します。
  duration: 30 minutes
  level: 200
  islab: true
  primarytopics:
    - Microsoft Defender
---

# 演習ラボ 0601: Intune を使用したエンドポイント セキュリティの構成

## 概要

このラボでは、Intune の管理対象デバイスに Microsoft Defender を構成するポリシーを作成します。

### 前提条件

このラボを開始する前に、0203、0204、0301の各ラボを完了しておく必要があります。

> 注: Entra ID への Windows Hello サインイン認証に使用するテキスト メッセージを受信できる携帯電話も必要です。

### シナリオ

Contoso Developersグループに対してMicrosoft Defenderが正しく構成されるようにします。改ざん防止を有効化し、Windows Securityの一部領域を非表示にして、会社名と電話番号を追加します。また、リアルタイム保護、修復、スキャンの設定も構成します。登録済みのSEA-WS1と未登録のSEA-CL1で設定を確認します。

### タスク 1: IntuneでWindows Securityエクスペリエンスを構成する

1. 手元のPCでMicrosoft Edgeを起動し、**https://intune.microsoft.com**を開いてテナント管理者でサインインします。
2. ナビゲーション ペインで、**エンドポイント セキュリティ**、**ウイルス対策**の順に選択します。
3. **エンドポイント セキュリティ | ウイルス対策**ペインで、**ポリシーの作成**を選択します。
4. **プロファイルの作成**ペインの**プラットフォーム**で、**Windows**を選択します。
5. **プロファイル**で**Windows Securityエクスペリエンス**を選択し、**作成**を選択します。
6. **基本**タブの**名前**に**Windows Security Settings**と入力し、**次へ**を選択します。
7. **構成設定**タブの**Defender**で、次の設定を構成します。
   - TamperProtection (Device): **オン**
8. **Windows Defender Security Center**で、次の設定を構成します。
   - Disable Account Protection UI: **有効**
   - Disable App Browser UI: **有効**
   - Disable Device Security UI: **有効**
   - Disable Family UI: **有効**
   - Disable Health UI: **有効**
   - Enable Customized Toasts: **有効**
9. **会社名**で**構成済み**を選択し、**Contoso IT**と入力します。
10. **電話**で**構成済み**を選択して**555-1234**と入力し、**次へ**を選択します。
11. **スコープ タグ**ページで、**次へ**を選択します。
12. **割り当て**タブの検索ボックスに**Contoso**と入力し、**Contoso Developer Devices**グループを選択して、**次へ**を選択します。
13. **確認と作成**タブで情報を確認し、**保存**を選択します。

### タスク 2: IntuneでMicrosoft Defenderウイルス対策ポリシーを構成する

1. **エンドポイント セキュリティ | ウイルス対策**ペインで、**ポリシーの作成**を選択します。
2. **プロファイルの作成**ペインの**プラットフォーム**で、**Windows**を選択します。
3. **プロファイル**で**Microsoft Defenderウイルス対策**を選択し、**作成**を選択します。
4. **基本**タブの**名前**に**Microsoft Defender Antivirus Settings**と入力し、**次へ**を選択します。
5. **構成設定**タブで、次の設定を構成します。
   - ダウンロードしたすべてのファイルと添付ファイルのスキャンを許可する: **許可**
   - リアルタイム監視を許可する: **許可**
   - スキャン実行前に署名を確認する: **有効**
   - クリーンアップされたマルウェアを保持する日数: **60**
   - クイック スキャンのスケジュール時刻: **60**（午前1時）
   - サンプル送信の同意: **安全なサンプルを自動的に送信する**
6. **構成設定**タブで、**次へ**を2回選択します。
7. **割り当て**タブで**Contoso**と入力し、**Contoso Developer Devices**グループを選択して、**次へ**を選択します。
9. **確認と作成**タブで情報を確認し、**保存**を選択します。

### タスク 3: 管理対象デバイスを同期する

1. Microsoft Intune管理センターで、**デバイス**、**すべてのデバイス**の順に選択します。
2. **デバイス | すべてのデバイス**ペインで**SEA-WS1**を選択し、**SEA-WS1**ブレードのツール バーで**同期**、**はい**の順に選択します。
   > 同期が完了するまで3分から4分待ちます。
3. Microsoft Edgeを閉じます。

### タスク 4: 構成を確認する

1. **SEA-CL1**に切り替えます。
2. 必要に応じて、パスワード**Pa55w.rd**を使用して**Contoso\Administrator**としてサインインします。
3. **Start**を選択して**Windows Security**と入力し、Windows Securityアイコンの下にある**Open**を選択します。
   > すべてのセキュリティ オプションが表示されることを確認します。SEA-CL1はIntuneに登録されていないためです。
4. **Windows Security**を閉じ、SEA-CL1からサインアウトします。
5. **SEA-WS1**に切り替え、PIN **102938**を使用して**Aaron Nicholls**としてサインインします。
6. **Start**を選択して**Windows Security**と入力し、Windows Securityアイコンの下にある**Open**を選択します。
   > Intuneポリシーで制限した領域が表示されないことを確認します。SEA-WS1はIntuneに登録されており、セキュリティ設定が適用されています。
7. **Windows Security**を閉じ、**SEA-WS1**からサインアウトします。

**結果**: この演習を完了すると、Intuneの管理対象デバイスにMicrosoft Defenderを構成するポリシーの作成と適用が完了します。

**ラボ終了**
