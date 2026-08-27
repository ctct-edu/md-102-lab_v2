### lab:
title: '演習ラボ 0101: Entra ID の ID 管理'
description: このラボでは、Entra 管理センターを使用してユーザーの作成と変更、管理ロールの割り当て、グループの作成と変更、ライセンス割り当ての管理を行います。
duration: 60 minutes
level: 200
islab: true

## 演習ラボ 0101: Entra ID の ID 管理

### 概要
このラボでは、Entra 管理センターを使用してユーザー管理、ロール管理、グループ管理、およびライセンス管理を実施します。

### 演習 1: Entra ID でのユーザー作成

#### タスク 1: Microsoft Entra 管理センターを使用したユーザー作成
1. SEA-SVR1 に Contoso\Administrator / Pa55w.rd でサインインします。

2. Server Manager を閉じます。

3. Microsoft Edge を開き、https://entra.microsoft.com にアクセスします。

4. admin@yourtenant.onmicrosoft.com でサインインします。

5. ユーザー Edmund Reeve および Miranda Snider を原文の値で作成します。

#### タスク 2: PowerShell によるユーザー作成
1. PowerShell 7.5.4 をインストールします。

2. 次のコマンドを実行します。

```powershell
Install-Module Microsoft.Graph -Scope CurrentUser
Connect-MgGraph -scopes "user.readwrite.all, group.readwrite.all"
```

3. Cody Godinez ユーザーを作成し、Get-MgUser で確認します。

### 演習 2: 管理ロールの割り当て

#### タスク 1: 管理ロールの確認と割り当て
1. グローバル管理者を Allan Deyoung に割り当てます。

2. ユーザー管理者を Edmund Reeve に割り当てます。

3. ヘルプデスク管理者を Miranda Snider に割り当てます。

### 演習 3: グループ管理とライセンス割り当て

#### タスク 1: グループ作成
1. Contoso_Managers セキュリティ グループを作成します。

#### タスク 2: PowerShell によるグループ作成
```powershell
New-MgGroup -DisplayName "Contoso_Sales"
Get-MgGroup
```

#### タスク 3: ライセンス確認と会社のブランド変更
1. Contoso Corp. Sign-in Page を構成します。

2. Cody Godinez に Enterprise Mobility + Security E5 と Office 365 E5 (no Teams) を割り当てます。

ラボ終了
