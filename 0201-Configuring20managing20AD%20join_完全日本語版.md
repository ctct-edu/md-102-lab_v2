---
lab:
  title: 'プラクティス ラボ 0201: Entra 参加の構成と管理'
  description: このラボでは、Entra ID 参加の設定を構成し、Windows デバイスで通常の Entra 参加と Entra ハイブリッド参加の両方のシナリオを実行します。
  duration: 100 minutes
  level: 200
  islab: true
  primarytopics:
- Windows
---

# プラクティス ラボ 0201: Entra 参加の構成と管理

## 概要

このラボでは、Entra ID 参加の設定を構成し、Windows デバイスで通常の Entra 参加と Entra ハイブリッド参加の両方のシナリオを実行します。

### 前提条件

このラボを開始する前に、次のラボを完了しておく必要があります。

- 0102-Synchronizing Identities by using Microsoft Entra Connect

> 注: You will also need a mobile phone that can receive text messages used to secure Windows Hello sign in authentication to Entra ID。

## 演習 1: Entra 参加の構成

### シナリオ

すべてのユーザーがデバイスを Entra ID に参加させられるように、Entra ID のデバイス設定を構成します。また、ユーザーが参加させられるデバイスを最大20台に制限し、すべての Entra 参加済みデバイスで Allan Deyoung をローカル管理者として追加します。最後に、Joni Sherman が SEA-WS1 をテナントへ参加させ、Entra 参加が想定どおりに動作することを確認します。

### タスク 1: Entra 参加のデバイス設定を構成する

1. On **SEA-SVR1**, if necessary, としてサインインします **Contoso\\Administrator** パスワード **Pa55w.rd** and 閉じます Server Manager。

2. On the taskbar 選択します **Microsoft Edge**, in the address bar 入力します **https://entra.microsoft.com**, and then 押します **Enter**。

3. Sign in as user `Admin@yourtenant.onmicrosoft.com`, and use the tenant Admin password. If the **Stay signed in?** prompt appears, 選択します **いいえ**。

> The Microsoft Entra admin c入力します が開きます。

4. Microsoft Entra 管理センターで、 ナビゲーション ペインで、 選択します **デバイス**, and 続いて **すべてのデバイス**。

> 次の点に注意してください: there are no devices found, as you have not joined any devices yet。

5. ****Devices | All devices**** ページで **デバイスの設定** を選択します。

6. On the **Devices|Device settings** ページ, in the details ペイン, under **Users may join devices to Microsoft Entra**, verify that **All** is 選択しました。

> これは、 all Entra users are permitted to join Windows 10 or newer devices to Microsoft Entra. Note that this setting does not apply to Entra hybrid  joined devices, or devices joined by using Windows Autopilot self-deployment mode。

7. In the **Require Multi-factor Authentication to register or join devices with Microsoft Entra** section, verify that the setting is set to **いいえ**。

8. In the **Maximum number of devices per user** section, 選択します **20**。

9. Under **Local administrator settings**, 選択します **Microsoft Entra 参加済みデバイスの追加のローカル管理者を管理する**. The Device Administrators ページ が開きます。

10. **Device Administrators** ページで **+ Add assignments** を選択します。

11. In the Search ボックス, 入力します **Allan Deyoung**, 選択します the **Allan Deyoung** user object, and 続いて **Add**。

> Allan Deyoung will now be added as a Device Administrator on all Entra joined devices。

12. In the navigation breadcrumbs, 選択します the **Devices | Device settings** link at the top of the ページ。

13. **Device settings** ページで **保存** を選択します。

14. In the Entra admin c入力します, ナビゲーション ペインで、 選択します **認証方法**。

15. ****認証方法**** ページで **SMS** を選択します。

16. In the **SMS settings** ページ, 選択します **有効化** (to make SMS available as an authenticatiom method)。

17. **bottom of the ページ** で **保存** を選択します。

### タスク 2: Entra 参加を実行する

1. **SEA-WS1** and としてサインインします **Admin** パスワード **Pa55w.rd** に切り替えます。

2. タスク バーで **Start** and 続いて **Settings** を選択します。

3. ****Settings**** ウィンドウで **Accounts** を選択します。

4. **Accounts** ページで **Access work or school** を選択します。

5. ****Access work or school**** ページで **Connect** を選択します。

6. ****Microsoft account**** ウィンドウで **Join this device to Microsoft Entra ID** を選択します。

7. On the **Sign in** ページ, 入力します **JoniS@yourtenant.onmicrosoft.com** and 続いて **次へ**。

8. On the **Enter password** ページ, 入力します the user password (from the Resources タブ) and 続いて **Sign in**。

9. On the **Make sure this is your organization** ダイアログ ボックス, 選択します **Join**。

10. ****You're all set!**** ページで **Done** を選択します。

11. On the **Access work or school** ページ, verify that **Connected to Contoso's Azure AD** が表示されている。

12. Close the **Settings** ページ。

### タスク 3: Entra 参加を検証する

1. On SEA-WS1, right-click **Start**, and 続いて **Windows Terminal**。

2. In the PowerShell console, 入力します the following and 押します **Enter**:

   ```powershell
   dsregcmd /status
   ```

3. In the output under **Device State**, verify that **AzureAdJoined : YES** が表示されている。

> これは、 the device is Entra joined。

4. PowerShell を閉じます。

5. Right-click **Start** and 続いて **Computer Management**。

6. In Computer Management, expand **Local Users and Groups**, and 続いて **グループ**。

7. Double-click the **Administrators** group。

> 次の点に注意してください: Joni Sherman has been added as a local Administrator on SEA-WS1. Also notice two security principals represented by their security identifiers (SID). These two SIDs represent the Entra ID global administrator role, and the Entra joined device administrator role。

8. 開いているすべてのウィンドウを閉じ、SEA-WS1 からサインアウトします。

9. **SEA-SVR1** に切り替えます。

10. In Microsoft Edge, in the Microsoft Entra admin c入力します, 選択します **デバイス**, and 続いて **すべてのデバイス**。

> In the Devices ペイン, notice that SEA-WS1 が表示されている。

11. the **参加の種類** が表示されている as **Microsoft Entra joined** and that the owner is **Joni Sherman**ことを確認します。

> Also note that the MDM 列 shows None. これは、 this device is not yet managed by Microsoft Intune。

### タスク 4: Entra ユーザーとして Windows にサインインする

1. Switch to **SEA-WS1** and then としてサインインします **`JoniS@yourtenant.onmicrosoft.com`** ユーザー パスワード you used in the previous task。

2. ****Use Windows Hello with your account** ページ** で **OK** を選択します。

3. ****Let's keep your account secure**** ページで **次へ** を選択します。

4. On the **Install Microsoft Authenticator** ページ, 選択します **Set up a different way to sign in**. **Note** Ensure you 選択します the correct link。

5. On the **Add a sign-in method** ダイアログ ボックス, 選択します **Phone**。

6. On the **Add your phone number** ページ, 選択します your **Country code** and in the **Phone number** フィールド, 入力します your mobile phone number which is able to receive text messages, 続いて **次へ**。

7. When you receive the verification code, 入力します the code on the **Verify your phone number** ページ and 続いて **次へ**。

8. ****Phone number added**** ページで **Done** を選択します。

9. On the **Set up a PIN** ページ, in the **New PIN** and **Confirm PIN** ボックスes, 入力します **`102938`** and 続いて **OK**。

10. ****All set!**** ページで **OK** を選択します。

### タスク 5: Windows デバイスを Entra から削除する

1. On SEA-WS1, whilst still signed in as **Joni Sherman**, 選択します **Start** and 続いて **Settings**。

2. ****Settings**** ウィンドウで **Accounts** を選択します。

3. **Accounts** ページで **Access work or school** を選択します。

4. ****Access work or school**** ページで **Connected to Contoso's Azure AD** を選択します。

5. **Disconnect** and 続いて **はい** を選択します。

6. ****Disconnect from the organization**** ページで **Disconnect** を選択します。

7. On the **Windows Security** ダイアログ ボックス, in the **Email address** ボックス, 入力します **Admin** and in the **パスワード** ボックス, 入力します **Pa55w.rd**. Select **OK**。

8. In the **Restart your PC** ダイアログ ボックス, 選択します **Restart now**. SEA-WS1 が再起動します。

**結果**: After completing this exercise, you will have configured Microsoft Entra device settings, joined a device to Entra, and removed a device from Entra。

## 演習 2: Entra ハイブリッド参加の構成

### シナリオ

Contoso の一部の Windows デバイスは、現在ローカルの Active Directory Domain Services に参加しています。これらのデバイスからクラウド サービスへシームレスにアクセスできるように、Entra ハイブリッド参加を有効にします。Entra Connect Sync を再構成し、SEA-CL2 で処理をテストします。

### タスク 1: 環境を準備する

1. **SEA-SVR1** に切り替えます。

2. **Start**, expand **Windows Administrative Tools**, and 続いて **Active Directory Users and Computers** を選択します。

3. In **Active Directory Users and Computers**, right-click **Contoso.com**, point to **New**, and 続いて **Organizational Unit**。

4. In the **New-Object - Organizational Unit** ダイアログ ボックス, 入力します **`Entra ID clients`** and 続いて **OK**。

5. In the navigation ペイン, 選択します **Seattle Clients**。

6. Right-click **SEA-CL2** and 続いて **Move**。

7. In the **Move** ダイアログ ボックス, 選択します **Entra ID clients** and 続いて **OK**。

8. **Active Directory Users and Computers** を閉じます。

### タスク 2: Entra Connect Sync で Entra ハイブリッド参加を構成する

1. On **SEA-SVR1**, on the **Desktop**, double-click **Azure AD Connect**。

2. In the **Microsoft Entra Connect Sync** ウィンドウ 選択します **Configure**。

3. ****Additional tasks**** ページで **Configure device options** 選択してから **次へ** を選択します。

4. ****Overview**** ページで **次へ** を選択します。

5. ****Connect to Microsoft Entra ID**** ページで **次へ** を選択します。

6. On the **Sign in to your account** ウィンドウ, 選択します the tenant admin account, and then 入力します テナントのパスワード 選択してから **Sign in**。

7. ****Device options**** ページで **Configure Hybrid Microsoft Entra ID join**, and 続いて **次へ** を選択します。

8. ****Device operating systems**** ページで **Windows 10 or later domain-joined devices**, and 続いて **次へ** を選択します。

9. On the **SCP configuration** ページ, 選択します the check ボックス next to **Contoso.com**。

10. **Microsoft Entra ID** from the **Authentication Service** ドロップダウン 選択してから **Add** を選択します。

11. In the **Enterprise Admin Credentials** ウィンドウ 入力します **Contoso\\Administrator** as **User name** and **Pa55w.rd** as **パスワード**. Select **OK** 選択してから **次へ**。

12. In the **Ready to configure** ページ, 選択します **Configure** to run the configuration。

13. the configuration is completeときは、**Exit** を選択します。

14. **SEA-CL2** に切り替えます。

15. At the sign-in ページ, 選択します the **Power** button and 続いて **Restart**。

> **Note** Restarting **SEA-CL2** will enable quicker discovery of the SCP created by reconfiguring Entra Connect Sync。

16. After **SEA-CL2** has restarted, としてサインインします **Contoso\\Administrator** パスワード **Pa55w.rd**。

### タスク 3: 新しい OU を同期するように Entra Connect Sync を再構成する

1. On **SEA-SVR1**, on the **Desktop**, double-click **Azure AD Connect**。

2. In the **Microsoft Entra Connect Sync** ウィンドウ 選択します **Configure**。

3. ****Additional tasks**** ページで **Customize synchronization options** 選択してから **次へ** を選択します。

4. ****Connect to Microsoft Entra ID**** ページで **次へ** を選択します。

5. One the **Sign in to your account** ウィンドウ, 選択します the tenant admin account, and then 入力します テナントのパスワード 選択してから **Sign in**。

6. ****Connect your directories**** ページで **次へ** を選択します。

7. On the **Domain and OU filtering** ページ, ensure that **Sync 選択しました domains and OUs** is 選択しました and then expand **Contoso.com**。

8. Select the check ボックス next to **Entra ID clients**. **Do not make any other changes** and 続いて **次へ**。

9. In the **Optional features** ページ, 変更しません and 続いて **次へ**。

10. In the **Ready to configure** ウィンドウ, 選択します **Configure** to run the configuration and start synchronization。

11. the configuration is completeときは、**Exit** を選択します。

> **注**: Entra Connect Sync synchronizes automatically now when you modify the OUs being synced. You can use the **Synchronization Service** to monitor sync status。

### タスク 4: Entra ハイブリッド参加を確認する

1. **SEA-CL2** に切り替えます。

2. Right-click **Start**, 選択します **Shut down or sign out**, and 続いて **Restart**。

_注: The reboot will trigger the Entra hybrid join on SEA-CL2._
   
3. After **SEA-CL2** has restarted, としてサインインします **Contoso\\Administrator** パスワード **Pa55w.rd**。
    
4. On the taskbar, right-click **Start** 選択してから **Windows Terminal (Admin)**。

5. In the **Windows PowerShell** ウィンドウ, 入力します the following command, and then 押します **Enter**:

   ```powershell
   dsregcmd /status
   ```

6. In the output under **Device State**, verify that **AzureAdJoined : YES** and **DomainJoined : YES** が表示されている。

> **注**: If the device is not yet joined to Entra ID, switch back to **SEA-SRV1** and run the command below. Once completed, switch back to SEA-CL2 and restart the computer once more。
   
   ```powershell
   Start-ADSyncSyncCycle -PolicyType Delta
   ```

7. Close all ウィンドウs on SEA-CL2 and sign out。

8. Switch to **SEA-SVR1** and switch to the Microsoft Entra admin c入力します。

9. **デバイス** > **すべてのデバイス** を選択します。

10. **SEA-CL2** has **Microsoft Entra hybrid joined** as value for the row **参加の種類**. 必要に応じて, 選択します the **更新** button if SEA-CL2 is not listedことを確認します。

11. Close all ウィンドウs on **SEA-SVR1**。

**結果**: この演習を完了すると、 configured and validated Entra hybrid join。

**ラボ終了**
