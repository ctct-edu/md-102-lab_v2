---
lab:
  title: 'Practice Lab 0801: Deploying Windows with Autopilot'
  description: In this lab you will learn how provision a Windows 11 device with Autopilot using User-driven mode.
  duration: 30 minutes
  level: 200
  islab: true
  primarytopics:
    - Windows
    - Windows 11
---

# 演習ラボ 0801: Autopilot を使用した Windows の展開

## 概要

このラボでは、ユーザー主導の展開プロファイルを使用し、Autopilot で Windows 11 デバイスをプロビジョニングする方法を学習します。

### 前提条件

このラボを開始する前に、次のラボを完了しておく必要があります。

- 0101-Managing Identities in Entra ID

- 0102-Synchronizing identities by using Entra Connect

### シナリオ

Contoso IT は、Autopilot を使用して新しい Windows 11 デバイスを展開する予定です。デバイスには Windows 11 が既定でインストールされています。ユーザーはデバイスを接続して電源を入れ、OOBE で最小限の質問に回答し、Entra ID 資格情報を使用してサインインできる必要があります。この処理では、デバイスを Entra ID に自動参加させ、Intune に登録します。このエクスペリエンスを構成してテストします。

### タスク 1: Entra ID でのグループの作成

1. Sign in to **SEA-SVR1** as **Contoso\\Administrator** パスワード **Pa55w.rd** および 閉じます **Server Manager**.

2. タスク バーで **Microsoft Edge**.

3. Microsoft Edge で、 アドレス バーに **https://entra.microsoft.com**, と入力して **入力します**. 求められた場合は、 your **`Admin@yourtenant.onmicrosoft.com`** および default tenant password.

4. ナビゲーション ペインで **Entra ID**.

5. 選択します **グループ** を選択してから **すべてのグループ**.

6. 対象: **Groups | All groups** ブレード, 選択します **新しいグループ**.

7. 対象: **新しいグループ** ブレード, in **グループの種類** list, 選択します **セキュリティ**.

8. 対象: **グループ名** box, 入力します **IT Devices**.

9. 対象: **グループの説明** box, 入力します **IT Department Devices**.

10. 対象: **メンバーシップの種類** list, 選択します **動的デバイス**.

11. 選択します **動的クエリの追加**.

12. 対象: **動的メンバーシップ ルール** ブレード 選択します **編集** above **ルール構文** box.

13. 対象: Edit rule syntax テキスト ボックス, add 次の項目 simple membership rule を選択し **OK**.

    ```cmd
    (device.devicePhysicalIDs -any (_ -contains "[ZTDId]"))
    ```
    
14. 選択します **保存** to 閉じます **動的メンバーシップ ルール**, を選択してから **作成** to create group.

### タスク 2: デバイス固有のコンマ区切り値 (CSV) ファイルの生成

1. 切り替え先: **SEA-WS3** および としてサインインし **Admin** パスワード **Pa55w.rd**.

2. 右クリックし **Start**, 選択します **Windows Terminal (Admin)**, を選択してから **Yes** at **User Account Control** prompt.

3. 対象: Windows PowerShell commおよび-line prompt, 入力します 次の項目 cmdlet, と入力して **入力します**:

    ```powershell
    Install-Script -Name Get-WindowsAutoPilotInfo
    ```

4. You will receive three prompts. Each time, 入力します **Y**, と入力して **入力します**.

5. 対象: Windows PowerShell commおよび-line prompt, 入力します 次の項目 cmdlet, と入力して **入力します**:

    ```powershell
    Set-ExecutionPolicy -ExecutionPolicy RemoteSigned
    ```

6. 対象: Windows PowerShell commおよび-line prompt, 入力します 次の項目 cmdlet, と入力して **入力します**:

    ```powershell
    Get-WindowsAutoPilotInfo.ps1 -OutputFile C:\Computer.csv
    ```

7. 対象: Windows PowerShell commおよび-line prompt, 入力します 次の項目 commおよび, press **入力します**, 続いて 確認し file content:

    ```cmd
    type C:\Computer.csv
    ```

8. 閉じます **Windows Terminal**.

### タスク 3: Windows Autopilot 展開プロファイルの操作

1. 対象: **SEA-WS3**, in ウィンドウs taskbar, 選択します **Microsoft Edge**.

2. 対象: **Microsoft Edge**, 移動します: **https://intune.microsoft.com**. Sign in を使用して your **`Admin@yourtenant.onmicrosoft.com`** account.

    >Note: You may be prompted to register for MFA. Follow the same procedures you used earlier in the course to add your phone number.

3. 対象: **Microsoft Intune 管理センター**, 選択します **デバイス**.

4. 対象: **デバイスのオンボード** section, 選択します **登録**. 。

5. 対象: **Windows** タブ, 下へスクロールして **Windows Autopilot**, を選択してから **デバイス**.

6. 対象: **Windows Autopilot devices** ブレード on メニュー バー, 選択します **インポート**, 選択します **folder icon** 続いて 参照します: **C:\\**, 選択します **Computer.csv**, 選択します **Open**, を選択してから **インポート**. 。

   _Note: The import process can take up to 15 minutes, but normally takes around 5 minutes._  

   _**Important**: After the process is complete, the device may not show automatically. If this is the case, select the **Refresh** button. If the device still does not appear, select the **Sync** button, wait a few minutes, and then select **Refresh**._

7. 選択します **X** to 閉じます **Windows Autopilot devices** ブレード. 。

8. 対象: Windows enrollment ブレード, in 詳細ペイン, 選択します **展開プロファイル**.

9. 対象: **Windows Autopilot 展開プロファイル** ブレード, 選択します **+ Create profile** を選択してから **Windows PC**.

10. 対象: **基本** タブ, in **名前** テキスト ボックス, 入力します **Contoso profile1**.

11. For **対象となるすべてのデバイスを Autopilot に変換する** 選択します **いいえ**, を選択してから **次へ**.

12. 対象: **Out-of-box experience (OOBE)** タブ, 確認し **展開モード** が次に設定されていることを確認します: **ユーザー主導**.

13. 確認し **Entra ID への参加方法** が次に設定されていることを確認します: **Microsoft Entra 参加済み**.

14. 確認し 次の項目 options を設定します:

    - Microsoft Software License Terms: **Hide**

    - Privacy settings: **Hide**

    - Hide change account options: **Hide**

    - User account type: **Administrator**.

    - Allow pre-provisioned deployment: **No**

    - Language (Region): **Operating system default**

    - Automatically configure keyboard: **Yes**

    - Apply device name template: **No**

15. 選択します **次へ**.

16. 対象: **割り当て** タブ, で **包含されたグループ** 選択します **グループの追加**.

17. 選択します **IT Devices** group および 選択します **選択**. 選択します **次へ**.

18. 対象: **確認と作成** タブ, 確認し information を選択してから **作成**.

19. 閉じます **Microsoft Edge**

### タスク 4: PC のリセット

1. 対象: **SEA-WS3**, 選択します **Start**, 入力します **reset** を選択し **Reset this PC**.

2. 対象: **System > Recovery** ページ, 選択します **Reset PC**.

3. 選択します **Remove everything**, を選択してから **Local reinstall**.

4. 選択します **Next** を選択してから **Reset**.

   >Note: Normally this task is not required for new deployment of physical devices. The device’s autopilot info is either provided by the manufacturer or can be obtained from the device prior to the OOBE. For the purposes of this lab, we must initiate a reset to simulate a new device OOBE.

   >Note: This process can take 30-45 minutes and will reboot several times during the process. 

### タスク 5: Autopilot 展開の確認

1. 対象: **Let's set things up for your work or school** ページ, 入力します **`Aaron@yourtenant.onmicrosoft.com`** を選択し **Next**.

2. 対象: Password ページ, 入力します **Pa55w.rd1234!** を選択し **Sign in**.

3. 対象: **Use Windows Hello を使用して your account**, 選択します **OK**.

4. 対象: **Verify your identity** ページ, 選択します Text verification method.

5. 対象: **入力します code** ページ, 入力します code that has been texted to your mobile device を選択してから **Verify**.

6. 対象: **Setup up a PIN** ダイアログ ボックス, in **New PIN** および **Confirm PIN** fields, 入力します **102938**, を選択してから **OK**.

7. 対象: **All set!** ページ, 選択します **OK**.

8. 選択します **Start** を選択し **Settings**. 。


9. 選択します **Accounts**, を選択してから **Access work or school**. Verify device is connected to Contoso's Azure AD.

10. 選択します **Connected to Contoso's Azure AD** を選択し **Info**.

11. 対象: **Managed by Contoso** ページ, scroll down を選択してから **Sync**.

12. 対象: **SEA-WS3**, 閉じます **Settings** ウィンドウ.

13. 切り替え先: **SEA-SVR1**.

14. 対象: Microsoft Entra admin c入力します, 展開し **Entra ID**, 展開し **Devices** を選択してから **All devices**. 。

    > Note that the new device displays with an icon that indicates an Autopilot device. Also note that the Join Type is **Microsoft Entra joined** with Aaron Nicholls as the owner.

15. 選択します Autopilot device を選択してから **Manage**. 。

16. Notice that you can Retire, Wipe, Sync, および Restart device.

17. 選択します ellipsis at end of メニュー バー および take notice of additional management capabilities.

    > Additional capabilities include Fresh Start, Autopilot Reset, Quick scan, Full scan, as well as others.

18. 閉じます Microsoft Edge.

**結果**: この演習を完了すると、ユーザー主導モードの Autopilot を使用して Windows デバイスをプロビジョニングできるようになります。

**ラボ終了**
