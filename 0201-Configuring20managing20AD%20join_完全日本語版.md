### lab:
title: '演習ラボ 0201: Entra Join の構成と管理'
description: このラボでは、Entra ID Join 設定を構成し、標準 Join および Entra Hybrid Join を実行します。
duration: 100 minutes
level: 200
islab: true
primarytopics:
- Windows

## 演習ラボ 0201: Entra Join の構成と管理

### 概要
このラボでは、Entra ID Join および Entra Hybrid Join を構成して検証します。

### 演習 1: Entra Join の構成

#### タスク 1: Entra Join デバイス設定の構成
1. SEA-SVR1 に Contoso\Administrator / Pa55w.rd でサインインします。

2. Microsoft Edge で https://entra.microsoft.com を開きます。

3. Microsoft Entra 管理センターで デバイス > すべてのデバイス > デバイス設定 を開きます。

4. Users may join devices to Microsoft Entra が All であることを確認します。

5. Maximum number of devices per user を 20 に設定します。

6. Allan Deyoung をデバイス管理者として追加します。

7. SMS 認証方法を有効化して保存します。

#### タスク 2: Entra Join の実行
1. SEA-WS1 に Admin / Pa55w.rd でサインインします。

2. Start > Settings > Accounts > Access work or school を開きます。

3. Connect を選択し、Join this device to Microsoft Entra ID を実行します。

4. JoniS@yourtenant.onmicrosoft.com でサインインします。

5. Join を選択してデバイス参加を完了します。

#### タスク 3: Entra Join の検証
1. Windows Terminal を開きます。

2. 次のコマンドを実行します。

```powershell
dsregcmd /status
```

3. Device State に AzureAdJoined : YES が表示されることを確認します。

4. Administrators グループを確認し、Joni Sherman が含まれていることを確認します。

5. Microsoft Entra 管理センターで SEA-WS1 が表示されることを確認します。

#### タスク 4: Entra ユーザーで Windows にサインイン
1. JoniS@yourtenant.onmicrosoft.com でサインインします。

2. 電話番号認証と PIN 102938 の構成を完了します。

#### タスク 5: Entra から Windows デバイスを削除
1. Access work or school を開きます。

2. Connected to Contoso's Azure AD を選択して切断します。

3. Windows Security で Admin / Pa55w.rd を入力します。

4. Restart now を選択して再起動します。

### 演習 2: Entra Hybrid Join の構成

#### タスク 1: 環境の準備
1. Active Directory Users and Computers を開きます。

2. Entra ID clients OU を作成します。

3. SEA-CL2 を Entra ID clients OU に移動します。

#### タスク 2: Entra Connect Sync で Entra Hybrid Join を構成
1. Azure AD Connect を起動します。

2. Configure device options を選択します。

3. Configure Hybrid Microsoft Entra ID join を構成します。

4. Authentication Service として Microsoft Entra ID を選択します。

5. Contoso\Administrator / Pa55w.rd を使用して構成を完了します。

#### タスク 3: 新しい OU を同期
1. Customize synchronization options を実行します。

2. Entra ID clients OU を同期対象として選択します。

3. Configure を選択して同期を開始します。

#### タスク 4: Entra Hybrid Join の検証
1. SEA-CL2 を再起動します。

2. Windows Terminal (Admin) を開きます。

3. 次のコマンドを実行します。

```powershell
dsregcmd /status
Start-ADSyncSyncCycle -PolicyType Delta
```

4. Device State に AzureAdJoined : YES および DomainJoined : YES が表示されることを確認します。

5. Microsoft Entra 管理センターで SEA-CL2 の Join Type が Microsoft Entra hybrid joined であることを確認します。

ラボ終了
