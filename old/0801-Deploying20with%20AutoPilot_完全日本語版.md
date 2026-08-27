---
lab:
  title: '演習ラボ 0801: Autopilot を使用した Windows の展開'
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

このラボでは、ユーザー主導型の展開プロファイルを使用し、Autopilot で Windows 11 デバイスをプロビジョニングする方法を学習します。

### 前提条件

このラボを開始する前に、次のラボを完了しておく必要があります。

- 0101-Managing Identities in Entra ID

- 0102-Synchronizing identities by using Entra Connect

### シナリオ

Contoso IT は、Autopilot を使用して新しい Windows 11 デバイスを展開することを計画しています。デバイスには Windows 11 が既定でインストールされています。ユーザーはデバイスを接続して電源を入れ、OOBE で最小限の質問に回答し、Entra ID 資格情報でサインインできる必要があります。この処理では、デバイスを Entra ID に自動参加させ、Intune に登録します。このエクスペリエンスの構成とテストを担当します。

### タスク 1: Entra ID でのグループの作成

1. Sign in to **SEA-SVR1** as **Contoso\\Administrator** パスワード **Pa55w.rd** and 閉じます **Server Manager**.

2. タスク バーで, **Microsoft Edge**.

3. In Microsoft Edge, の address bar, **https://entra.microsoft.com**, 、続いて press **入力します**. If prompted, sign in with your **`Admin@yourtenant.onmicrosoft.com`** and the default tenant password.

4. の navigation ペイン, 展開します **Entra ID**.

5. **Groups** 、続いて **All groups**.

6. の **Groups | All groups** ブレード, **New group**.

7. の **New Group** ブレード, の **Group 入力します** list, **Security**.

8. の **Group name** box, **IT Devices**.

9. の **Group description** box, **IT Department Devices**.

10. の **Membership 入力します** list, **Dynamic Device**.

11. **Add dynamic query**.

12. の **Dynamic membership rules** ブレード **Edit** above the **Rule syntax** box.

13. の Edit rule syntax テキスト ボックス, add the following simple membership rule and **OK**.

    ```cmd
    (device.devicePhysicalIDs -any (_ -contains "[ZTDId]"))
    ```
    
14. **Save** to 閉じます **Dynamic membership rules**, 、続いて **Create** to create グループ.

### タスク 2: デバイス固有のコンマ区切り値 (CSV) ファイルの生成

1. に切り替えます **SEA-WS3** and としてサインインします **Admin** パスワード of **Pa55w.rd**.

2. 右クリックします **Start**, **Windows Terminal (Admin)**, 、続いて **Yes** at the **User Account Control** prompt.

3. At the Windows PowerShell command-line prompt, 入力します the following cmdlet, 、続いて press **入力します**:

    ```powershell
    Install-Script -Name Get-WindowsAutoPilotInfo
    ```

4. You will receive three prompts. Each time, **Y**, 、続いて press **入力します**.

5. At the Windows PowerShell command-line prompt, 入力します the following cmdlet, 、続いて press **入力します**:

    ```powershell
    Set-ExecutionPolicy -ExecutionPolicy RemoteSigned
    ```

6. At the Windows PowerShell command-line prompt, 入力します the following cmdlet, 、続いて press **入力します**:

    ```powershell
    Get-WindowsAutoPilotInfo.ps1 -OutputFile C:\Computer.csv
    ```

7. At the Windows PowerShell command-line prompt, 入力します the following command, press **入力します**, 、続いて review the file content:

    ```cmd
    入力します C:\Computer.csv
    ```

8. 閉じます **Windows Terminal**.

### タスク 3: Windows Autopilot 展開プロファイルの操作

1. On **SEA-WS3**, の windows taskbar, **Microsoft Edge**.

2. In **Microsoft Edge**, navigate to **https://intune.microsoft.com**. Sign in with your **`Admin@yourtenant.onmicrosoft.com`** account.

    >Note: You may be prompted to register for MFA. Follow the same procedures you used earlier の course to add your phone number.

3. の **Microsoft Intune admin center**, **Devices**.

4. の **Device onboarding** section, **Enrollment**. 

5. の **Windows** タブ, scroll down to **Windows Autopilot**, 、続いて **Devices**.

6. の **Windows Autopilot devices** ブレード の メニュー バー, **Import**, 選択します the **folder icon** 、続いて browse to **C:\\**, **Computer.csv**, **開きます**, 、続いて **Import**. 

   _Note: The import process can take up to 15 minutes, but normally takes around 5 minutes._  

   _**Important**: After 処理 is complete, デバイス may not show automatically. If this is the case, 選択します the **Refresh** button. If デバイス still does not appear, 選択します the **Sync** button, 数分待ち, 、続いて **Refresh**._

7. **X** to 閉じます the **Windows Autopilot devices** ブレード. 

8. の Windows enrollment ブレード, 詳細ペインで, **Deployment Profiles**.

9. の **Windows AutoPilot deployment profiles** ブレード, **+ Create profile** 、続いて **Windows PC**.

10. の **Basics** タブ, の **Name** テキスト ボックス, **Contoso profile1**.

11. For **Convert all targeted devices to Autopilot** **No**, 、続いて **Next**.

12. の **Out-of-box experience (OOBE)** タブ, ensure that the **Deployment mode** is set to **User-Driven**.

13. Ensure that **Join to Entra ID as** is set to **Microsoft Entra joined**.

14. Ensure that the following options are set:

    - Microsoft Software License Terms: **Hide**

    - Privacy settings: **Hide**

    - Hide change account options: **Hide**

    - User account 入力します: **Administrator**.

    - Allow pre-provisioned deployment: **No**

    - Language (Region): **Operating system default**

    - Automatically configure keyboard: **Yes**

    - Apply device name template: **No**

15. **Next**.

16. の **Assignments** タブ, で **Included groups** **Add groups**.

17. 選択します the **IT Devices** group and click **選択します**. **Next**.

18. の **Review + create** タブ, 情報を確認し 、続いて **Create**.

19. 閉じます **Microsoft Edge**

### タスク 4: PC のリセット

1. On **SEA-WS3**, **Start**, **reset** and **Reset this PC**.

2. の **System > Recovery** ページ, **Reset PC**.

3. **Remove everything**, 、続いて **Local reinstall**.

4. **Next** 、続いて **Reset**.

   >Note: Normally this task is not required for new deployment of physical devices. デバイス’s autopilot info is either provided by the manufacturer or can be obtained from デバイス prior to the OOBE. For the purposes of this lab, we must initiate a reset to simulate a new device OOBE.

   >Note: この処理には 30-45 分かかる場合があり、処理中に数回再起動します. 

### タスク 5: Autopilot 展開の確認

1. At the **Let's set things up for your work or school** ページ, **`Aaron@yourtenant.onmicrosoft.com`** and **Next**.

2. At the Password ページ, **Pa55w.rd1234!** and **Sign in**.

3. At the **Use Windows Hello with your account**, **OK**.

4. At the **Verify your identity** ページ, 選択します the Text verification method.

5. At the **入力します code** ページ, 入力します the code that has been texted to your mobile device 、続いて **Verify**.

6. の **Setup up a PIN** dialog box, の **New PIN** and **Confirm PIN** fields, **102938**, 、続いて **OK**.

7. の **All set!** ページ, **OK**.

8. **Start** and **Settings**. 


9. **Accounts**, 、続いて **Access work or school**. Verify デバイス is connected to Contoso's Azure AD.

10. **Connected to Contoso's Azure AD** and **Info**.

11. の **Managed by Contoso** ページ, scroll down 、続いて **Sync**.

12. On **SEA-WS3**, 閉じます the **Settings** ウィンドウ.

13. に切り替えます **SEA-SVR1**.

14. の Microsoft Entra admin center, 展開します **Entra ID**, 展開します **Devices** 、続いて **All devices**. 

    > Note that the new device displays with an icon that indicates an Autopilot device. Also note that the Join 入力します is **Microsoft Entra joined** with Aaron Nicholls as the owner.

15. 選択します the Autopilot device 、続いて **Manage**. 

16. 次の点を確認します: you can Retire, Wipe, Sync, and Restart デバイス.

17. 選択します the ellipsis at the end of the メニュー バー and take notice of the additional management capabilities.

    > Additional capabilities include Fresh Start, Autopilot Reset, Quick scan, Full scan, as well as others.

18. 閉じます Microsoft Edge.

**結果**: この演習を完了すると、 provisioned a Windows device with Autopilot using User-driven mode.

**ラボ終了**
