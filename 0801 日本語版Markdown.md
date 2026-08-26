---
lab:
  title: '演習ラボ 0801: Autopilot を使用した Windows の展開'
  description: このラボでは、ユーザー駆動モードの Autopilot を使用して Windows 11 デバイスをプロビジョニングする方法を学習します。
  duration: 30 minutes
  level: 200
  islab: true
  primarytopics:
    - Windows
    - Windows 11
---

# 演習ラボ 0801: Autopilot を使用した Windows の展開

## 概要

このラボでは、ユーザー駆動型の展開プロファイルを使用して、Autopilot で Windows 11 デバイスをプロビジョニングする方法を学習します。

### 前提条件

このラボを開始する前に、次のラボを完了しておく必要があります。

- 0101-Managing Identities in Entra ID
- 0102-Synchronizing identities by using Entra Connect

### シナリオ

Contoso IT は、Autopilot を使用して新しい Windows 11 デバイスを展開する予定です。デバイスには Windows 11 が既定の状態でインストールされています。ユーザーはデバイスを接続して電源を入れ、OOBE で最小限の質問に回答した後、Entra ID 資格情報を使用してサインインできる必要があります。この処理によって、デバイスが自動的に Entra ID に参加し、Intune に登録されるようにします。このエクスペリエンスを構成してテストします。

### タスク 1: Entra ID にグループを作成する

1. 手元の PC で Microsoft Edge を起動します。
2. アドレス バーに **https://entra.microsoft.com** と入力し、**Enter** キーを押します。求められた場合は、**Admin@yourtenant.onmicrosoft.com** と既定のテナント パスワードを使用してサインインします。
3. ナビゲーション ペインで **Entra ID** を展開します。
4. **グループ**、**すべてのグループ** の順に選択します。
5. **グループ | すべてのグループ** ブレードで、**新しいグループ** を選択します。
6. **新しいグループ** ブレードの **グループの種類** で、**セキュリティ** を選択します。
7. **グループ名** ボックスに **IT Devices** と入力します。
8. **グループの説明** ボックスに **IT Department Devices** と入力します。
9. **メンバーシップの種類** で、**動的デバイス** を選択します。
10. **動的クエリの追加** を選択します。
11. **動的メンバーシップ ルール** ブレードで、**ルール構文** ボックスの上にある **編集** を選択します。
12. **ルール構文の編集** テキスト ボックスに次のメンバーシップ ルールを追加し、**OK** を選択します。

    ```powershell
    (device.devicePhysicalIDs -any (_ -contains "[ZTDId]"))
    ```

13. **保存** を選択して **動的メンバーシップ ルール** を閉じ、**作成** を選択してグループを作成します。

### タスク 2: デバイス固有のコンマ区切り値（CSV）ファイルを生成する

1. **SEA-WS3** に切り替え、パスワード **Pa55w.rd** を使用して **Admin** としてサインインします。
2. **Start** を右クリックし、**Windows Terminal (Admin)** を選択して、**User Account Control** プロンプトで **Yes** を選択します。
3. Windows PowerShell のコマンド ライン プロンプトで、次のコマンドレットを入力し、**Enter** キーを押します。

   ```powershell
   Install-Script -Name Get-WindowsAutoPilotInfo
   ```

4. 3つのプロンプトが表示されます。毎回 **Y** と入力し、**Enter** キーを押します。
5. Windows PowerShell のコマンド ライン プロンプトで、次のコマンドレットを入力し、**Enter** キーを押します。

   ```powershell
   Set-ExecutionPolicy -ExecutionPolicy RemoteSigned
   ```

6. Windows PowerShell のコマンド ライン プロンプトで、次のコマンドレットを入力し、**Enter** キーを押します。

   ```powershell
   Get-WindowsAutoPilotInfo.ps1 -OutputFile C:\Computer.csv
   ```

7. Windows PowerShell のコマンド ライン プロンプトで、次のコマンドを入力して **Enter** キーを押し、ファイルの内容を確認します。

   ```powershell
   type C:\Computer.csv
   ```

8. **Windows Terminal** を閉じます。

### タスク 3: Windows Autopilot 展開プロファイルを操作する

1. **SEA-WS3** の Windows タスク バーで、**Microsoft Edge** を選択します。
2. **Microsoft Edge** で **https://intune.microsoft.com** に移動し、**Admin@yourtenant.onmicrosoft.com** アカウントでサインインします。

   > 注: MFA の登録を求められる場合があります。コースの前半で使用した手順と同様に、電話番号を追加します。

3. **Microsoft Intune 管理センター**で、**デバイス** を選択します。
4. **デバイスのオンボーディング** セクションで、**登録** を選択します。
5. **Windows** タブで **Windows Autopilot** まで下にスクロールし、**デバイス** を選択します。
6. **Windows Autopilot デバイス** ブレードのメニュー バーで **インポート** を選択し、**フォルダー アイコン**を選択します。**C:\** を参照し、**Computer.csv**、**Open**、**インポート** の順に選択します。

   > 注: インポート処理には最長15分かかる場合がありますが、通常は約5分で完了します。

   > **重要**: 処理が完了してもデバイスが自動的に表示されない場合は、**更新** を選択します。それでも表示されない場合は、**同期** を選択して数分待ち、再度 **更新** を選択します。

7. **X** を選択して、**Windows Autopilot デバイス** ブレードを閉じます。
8. Windows登録ブレードの詳細ペインで、**展開プロファイル** を選択します。
9. **Windows Autopilot 展開プロファイル** ブレードで、**プロファイルの作成**、**Windows PC** の順に選択します。
10. **基本** タブの **名前** テキスト ボックスに **Contoso profile1** と入力します。
11. **対象となるすべてのデバイスを Autopilot に変換する**で **いいえ** を選択し、**次へ** を選択します。
12. **Out-of-box experience (OOBE)** タブで、**展開モード**が **User-Driven** に設定されていることを確認します。
13. **Entra ID への参加方法**が **Microsoft Entra joined** に設定されていることを確認します。
14. 次のオプションが設定されていることを確認します。
    - Microsoft Software License Terms: **Hide**
    - Privacy settings: **Hide**
    - Hide change account options: **Hide**
    - User account type: **Administrator**
    - Allow pre-provisioned deployment: **No**
    - Language (Region): **Operating system default**
    - Automatically configure keyboard: **Yes**
    - Apply device name template: **No**
15. **次へ** を選択します。
16. **割り当て** タブの **包含されたグループ** で、**グループの追加** を選択します。
17. **IT Devices** グループを選択し、**選択**、**次へ** の順に選択します。
18. **確認と作成** タブで情報を確認し、**作成** を選択します。
19. **Microsoft Edge** を閉じます。

### タスク 4: PCをリセットする

1. **SEA-WS3** で **Start** を選択し、**reset** と入力して **Reset this PC** を選択します。
2. **System > Recovery** ページで、**Reset PC** を選択します。
3. **Remove everything**、**Local reinstall** の順に選択します。
4. **Next**、**Reset** の順に選択します。

   > 注: 通常、このタスクは物理デバイスを新規展開する際には不要です。デバイスのAutopilot情報は製造元から提供されるか、OOBEの前にデバイスから取得できます。このラボでは、新しいデバイスのOOBEをシミュレートするためにリセットを開始します。

   > 注: この処理には30分から45分かかる場合があり、処理中に数回再起動します。

### タスク 5: Autopilot 展開を確認する

1. **Let's set things up for your work or school** ページで **Aaron@yourtenant.onmicrosoft.com** と入力し、**Next** を選択します。
2. Password ページで **Pa55w.rd1234\!** と入力し、**Sign in** を選択します。
3. **Use Windows Hello with your account** で、**OK** を選択します。
4. **Verify your identity** ページで、Textによる確認方法を選択します。
5. **Enter code** ページで、モバイル デバイスにテキスト送信されたコードを入力し、**Verify** を選択します。
6. **Setup up a PIN** ダイアログの **New PIN** フィールドと **Confirm PIN** フィールドに **102938** と入力し、**OK** を選択します。
7. **All set\!** ページで、**OK** を選択します。
8. **Start** を選択し、**Settings** を選択します。
9. **Accounts**、**Access work or school** の順に選択し、デバイスが Contoso's Azure AD に接続されていることを確認します。
10. **Connected to Contoso's Azure AD** を選択し、**Info** を選択します。
11. **Managed by Contoso** ページで下にスクロールし、**Sync** を選択します。
12. **SEA-WS3** で、**Settings** ウィンドウを閉じます。
13. 手元の PC の Microsoft Entra 管理センターに切り替えます。
14. Microsoft Entra 管理センターで **Entra ID**、**デバイス** の順に展開し、**すべてのデバイス** を選択します。

    > 新しいデバイスにAutopilotデバイスを示すアイコンが表示されることを確認します。また、参加の種類が **Microsoft Entra joined**、所有者が Aaron Nicholls であることを確認します。

15. Autopilotデバイスを選択し、**管理** を選択します。
16. デバイスに対して、廃止、ワイプ、同期、再起動を実行できることを確認します。
17. メニュー バーの末尾にある省略記号を選択し、追加の管理機能を確認します。

    > 追加機能には、Fresh Start、Autopilot Reset、Quick scan、Full scanなどがあります。

**結果**: この演習を完了すると、ユーザー駆動モードのAutopilotを使用してWindowsデバイスがプロビジョニングされます。

**ラボ終了**
