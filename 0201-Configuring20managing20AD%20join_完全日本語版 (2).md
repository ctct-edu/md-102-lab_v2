---
lab:
 title: '演習ラボ 0201: Entra 参加の構成と管理'
 description: このラボでは、 configure Entra ID Join設定 および perform both stおよびard および Entra hybrid join scenarios のために Windowsデバイス.
 duration: 100 minutes
 level: 200
 islab: true
 primarytopics:
 - Windows
---

# 演習ラボ 0201: Entra 参加の構成と管理

## 概要

このラボでは、 configure Entra ID Join設定 および perform both stおよびard および Entra hybrid join scenarios のために Windowsデバイス.

### 前提条件

このラボを開始する前に、次のラボを完了しておく必要があります。

- 0102-Microsoft Entra Connect を使用した ID の同期

 > 注: You します also need mobile phone that できます receive text messages used に secure Windows Hello sign で au続いてtication に Entra ID.

## 演習 1: Entra 参加の構成

### シナリオ

次の作業を行う必要があります。 configure Entra ID device設定 に 次のことを確認します。 allユーザー は allowed に joinデバイス に Entra ID. You also need に 次のことを確認します。ユーザー できます only join maximum の 20デバイス および that Allan Deyoung は added として local管理者 on all Entra joinedデバイス. Finally, you します 次のことを確認します。 Entra join works として expected by having Joni Sherman join SEA-WS1 に tenant.

### タスク 1: Entra 参加のデバイス設定を構成する

1. On **SEA-SVR1**, 必要に応じて, 次のアカウントでサインインします。 **Contoso\\Administrator** パスワード **Pa55w.rd** および 閉じます Server Manager.

2. タスク バーで **Microsoft Edge**, で address bar 入力します **https://entra.microsoft.com**, を入力し、 **入力します**.

3. Sign で として user `Admin@yourtenant.onmicrosoft.com`, および use tenant Adminパスワード. If **Stay signed in?** prompt が表示された場合, 選択します **いいえ**. 

 > Microsoft Entra admin c入力します が開きます.

4. Microsoft Entra 管理センターで, ナビゲーション ペインで, 選択します **デバイス**, 続いて 選択します **すべてのデバイス**.

 > 次の点に注意してください。 there は noデバイス found, として you があります not joined anyデバイス yet.

5. **Devices | Allデバイス** ページ, 選択します **Device設定**.

6. **Devices|Device設定** ページ, で details ペイン, 配下で **Users may joinデバイス に Microsoft Entra**, 次のことを確認します。 **All** が選択されていること. 

 > これは、 all Entraユーザー は permitted に join Windows 10 または newerデバイス に Microsoft Entra. 次の点に注意してください。 this setting does not apply に Entra hybrid joinedデバイス, orデバイス joined by using Windows Autopilot self-deployment mode.

7. In **Require Multi-factor Au続いてtication に register または joinデバイス を使用して Microsoft Entra** section, 次のことを確認します。 setting は set に **いいえ**. 

8. In **Maximum number ofデバイス per user** section, 選択します **20**.

9. Under **Local管理者設定**, 選択します **Manage Additional local管理者s on all Entra joinedデバイス**. Device Administrators ページ が開きます.

10. In Device Administrators ページ, 選択します **+ Add割り当てs**.

11. In Search box, 入力します **Allan Deyoung**, 選択します **Allan Deyoung** user object, 続いて 選択します **Add**. 

 > Allan Deyoung します now be added として Device Administrator on all Entra joinedデバイス.

12. In navigation breadcrumbs, 選択します **Devices | Device設定** リンク ページ上部で.

13. Device設定 ページ, 選択します **Save**.

14. In Entra admin c入力します, ナビゲーション ペインで, 選択します **Au続いてtication methods**.

15. In **Au続いてtication methods** ページ, 選択します **SMS**.

16. In **SMS設定** ページ, 選択します **Enable** (to make SMS利用可能な として au続いてticatiom method).

17. At bottom の ページ, 選択します **Save**.

### タスク 2: Entra 参加を実行する

1. 切り替えます。 **SEA-WS1** および 次のアカウントでサインインします。 **Admin** パスワード **Pa55w.rd**.

2. タスク バーで **Start** 続いて 選択します **Settings**.

3. In **Settings** ウィンドウ, 選択します **Accounts**.

4. Accounts ページ, 選択します **Access work または school**.

5. In **Access work または school** ページ, 選択します **Connect**.

6. In **Microsoftアカウント** ウィンドウ, 選択します **Join this device に Microsoft Entra ID**.

7. **Sign in** ページ, 入力します **JoniS@yourtenant.onmicrosoft.com** 続いて 選択します **次へ**.

8. **入力しますパスワード** ページ, 入力します userパスワード (から Resources タブ) 続いて 選択します **Sign in**.

9. **Make sure this は your組織** ダイアログ ボックス, 選択します **Join**.

10. **You're all set!** ページ, 選択します **Done**.

11. **Access work または school** ページ, 次のことを確認します。 **Connected に Contoso's Azure AD** が表示されていること.

12. 閉じます **Settings** ページ.

### タスク 3: Entra 参加を検証する

1. On SEA-WS1, right-click **Start**, 続いて 選択します **Windows Terminal**.

2. In PowerShell console, 入力します following および press **入力します**:

 ```powershell
 dsregcmd /status
   ```

3. In output 配下で **Device State**, 次のことを確認します。 **AzureAdJoined : YES** が表示されていること.

 > これは、 device は Entra joined.

4. 閉じます PowerShell.

5. Right-click **Start** 続いて 選択します **Computer Management**.

6. In Computer Management, expおよび **Local Users および Groups**, 続いて 選択します **グループ**.

7. Double-click **Administrators** group.

 > 次の点に注意してください。 Joni Sherman があります been added として aローカル Administrator on SEA-WS1. Also notice two security principals represented by their security identifiers (SID). These two SIDs represent Entra ID global管理者 role, および Entra joined device管理者 role. 

8. 閉じます 開いているすべてのウィンドウ および sign out の SEA-WS1.

9. 切り替えます。 **SEA-SVR1**.

10. In Microsoft Edge, Microsoft Entra 管理センターで, 選択します **デバイス**, 続いて 選択します **すべてのデバイス**. 

 > In Devices ペイン, notice that SEA-WS1 が表示されていること. 

11. 次のことを確認します。 **Join 入力します** が表示されていること として **Microsoft Entra joined** および that owner は **Joni Sherman**. 

 > Also note that MDM 列 shows None. これは、 this device は not yet managed by Microsoft Intune.

### タスク 4: Entra ユーザーとして Windows にサインインする

1. 切り替えます。 **SEA-WS1** 続いて 次のアカウントでサインインします。 **`JoniS@yourtenant.onmicrosoft.com`** ユーザー パスワードを使用します you used で previous task. 

2. At **Use Windows Hello を使用して yourアカウント** ページ, 選択します **OK**.

3. **Let's keep yourアカウント secure** ページ, 選択します **次へ**.

4. **Install Microsoft Au続いてticator** ページ, 選択します **Set up different way に sign in**. **Note** Ensure you 選択します correct リンク.

5. **Add sign-in method** ダイアログ ボックス, 選択します **Phone**.

6. **Add受講者のphone number** ページ, 選択します受講者の**Country code** および で **Phone number** フィールド, 入力します受講者のmobile phone number which は able に receive text messages, 続いて 選択します **次へ**.

7. When you receive verification code, 入力します code **Verify受講者のphone number** ページ 続いて 選択します **次へ**.

8. **Phone number added** ページ, 選択します **Done**.

9. **Set up PIN** ページ, で **New PIN** および **Confirm PIN** boxes, 入力します **`102938`** 続いて 選択します **OK**.

10. **All set!** ページ, 選択します **OK**.

### タスク 5: Windows デバイスを Entra から削除する

1. On SEA-WS1, whilst still signed で として **Joni Sherman**, 選択します **Start** 続いて 選択します **Settings**.

2. In **Settings** ウィンドウ, 選択します **Accounts**.

3. Accounts ページ, 選択します **Access work または school**.

4. In **Access work または school** ページ, 選択します **Connected に Contoso's Azure AD**.

5. 選択します **Disconnect** 続いて 選択します **はい**.

6. **Disconnect から the組織** ページ, 選択します **Disconnect**.

7. **Windows Security** ダイアログ ボックス, で **Email address** box, 入力します **Admin** および で **パスワード** box, 入力します **Pa55w.rd**. 選択します **OK**.

8. In **Restart受講者のPC** ダイアログ ボックス, 選択します **Restart now**. SEA-WS1 restarts.

**結果**: After completing this exercise, you します があります configured Microsoft Entra device設定, joined device に Entra, および removed device から Entra.

## 演習 2: Entra ハイブリッド参加の構成

### シナリオ

次の操作を実行します。Some Contoso Windowsデバイス は currently joined に theローカル Active Directory Domain Services. To enable thoseデバイス に seamlessly access cloud services you plan に enable Entra hybrid join. You します test Entra hybrid join by re-configuring Entra Connect sync および testing out process on SEA-CL2.

### タスク 1: 環境を準備する

1. 切り替えます。 **SEA-SVR1**.

2. 選択します **Start**, expおよび **Windows Administrative Tools**, 続いて 選択します **Active Directory Users および Computers**.

3. In **Active Directory Users および Computers**, right-click **Contoso.com**, point に **New**, 続いて 選択します **Organizational Unit**.

4. In **New-Object - Organizational Unit** ダイアログ ボックス, 入力します **`Entra ID clients`** 続いて 選択します **OK**.

5. ナビゲーション ペインで, 選択します **Seattle Clients**.

6. Right-click **SEA-CL2** 続いて 選択します **Move**.

7. In **Move** ダイアログ ボックス, 選択します **Entra ID clients** 続いて 選択します **OK**.

8. 閉じます **Active Directory Users および Computers**.

### タスク 2: Entra Connect Sync で Entra ハイブリッド参加を構成する

1. On **SEA-SVR1**, **Desktop**, double-click **Azure AD Connect**.

2. In **Microsoft Entra Connect Sync** ウィンドウ 選択します **Configure**.

3. **Additional tasks** ページ, 選択します **Configure device options** および 選択します **次へ**.

4. **Overview** ページ, 選択します **次へ**.

5. **Connect に Microsoft Entra ID** ページ, 選択します **次へ**.

6. **Sign で に yourアカウント** ウィンドウ, 選択します tenant adminアカウント, 続いて 入力します tenantパスワード および 選択します **Sign in**.

7. **Device options** ページ, 選択します **Configure Hybrid Microsoft Entra ID join**, 続いて 選択します **次へ**.

8. **Device operating systems** ページ, 選択します **Windows 10 または later domain-joinedデバイス**, 続いて 選択します **次へ**.

9. **SCP構成** ページ, 選択します チェック ボックス next に **Contoso.com**. 

10. 選択します **Microsoft Entra ID** から **Au続いてtication Service** ドロップダウン および 選択します **Add**. 

11. In **入力しますprise Admin Credentials** ウィンドウ 入力します **Contoso\\Administrator** として **User name** および **Pa55w.rd** として **パスワード**. 選択します **OK** および 選択します **次へ**.

12. In **Ready に configure** ページ, 選択します **Configure** に run the構成.

13. 構成が完了したら, 選択します **Exit**.

14. 切り替えます。 **SEA-CL2**.

15. At sign-in ページ, 選択します **Power** ボタン 続いて 選択します **Restart**.

 > **Note** Restarting **SEA-CL2** します enable quicker discovery の SCP created by reconfiguring Entra Connect Sync.

16. After **SEA-CL2** があります restarted, 次のアカウントでサインインします。 **Contoso\\Administrator** パスワード **Pa55w.rd**.

### タスク 3: 新しい OU を同期するように Entra Connect Sync を再構成する

1. On **SEA-SVR1**, **Desktop**, double-click **Azure AD Connect**.

2. In **Microsoft Entra Connect Sync** ウィンドウ 選択します **Configure**.

3. **Additional tasks** ページ, 選択します **Customize同期 options** および 選択します **次へ**.

4. **Connect に Microsoft Entra ID** ページ, 選択します **次へ**.

5. One **Sign で に yourアカウント** ウィンドウ, 選択します tenant adminアカウント, 続いて 入力します tenantパスワード および 選択します **Sign in**.

6. **Connect受講者のdirectories** ページ, 選択します **次へ**.

7. **Domain および OU filtering** ページ, 次のことを確認します。 **Sync 選択しますed domains および OUs** が選択されていること 続いて expおよび **Contoso.com**.

8. 選択します チェック ボックス next に **Entra ID clients**. **Do not make any other changes** 続いて 選択します **次へ**.

9. In **Optional features** ページ, 変更しないでください 続いて 選択します **次へ**.

10. In **Ready に configure** ウィンドウ, 選択します **Configure** に run the構成 および start同期.

11. 構成が完了したら, 選択します **Exit**.

 > **注**: Entra Connect Sync synchronizes automatically now when you modify OUs being synced. You できます use **Synchronization Service** に monitor sync status.

### タスク 4: Entra ハイブリッド参加を確認する

1. 切り替えます。 **SEA-CL2**.

2. Right-click **Start**, 選択します **Shut down または sign out**, 続いて 選択します **Restart**.

 _注: reboot します trigger Entra hybrid join on SEA-CL2._
   
3. After **SEA-CL2** があります restarted, 次のアカウントでサインインします。 **Contoso\\Administrator** パスワード **Pa55w.rd**.
    
4. taskbar, right-click **Start** および 選択します **Windows Terminal (Admin)**.

5. In **Windows PowerShell** ウィンドウ, 入力します following commおよび, を入力し、 **入力します**:

 ```powershell
 dsregcmd /status
   ```

6. In output 配下で **Device State**, 次のことを確認します。 **AzureAdJoined : YES** および **DomainJoined : YES** が表示されていること.

 > **注**: If device は not yet joined に Entra ID, switch back に **SEA-SRV1** および run commおよび below. Once completed, switch back に SEA-CL2 および restart computer once more.
   
 ```powershell
 Start-ADSyncSyncCycle -Policy入力します Delta
   ```

7. 閉じます すべてのウィンドウ on SEA-CL2 および sign out.

8. 切り替えます。 **SEA-SVR1** および switch に Microsoft Entra admin c入力します.

9. 選択します **デバイス** > **すべてのデバイス**. 

10. 次のことを確認します。 **SEA-CL2** があります **Microsoft Entra hybrid joined** として 値 のために row **Join 入力します**. 必要に応じて, 選択します **更新** ボタン if SEA-CL2 は not 一覧ed.

11. 閉じます すべてのウィンドウ on **SEA-SVR1**.

**結果**: この演習を完了すると、 configured および validated Entra hybrid join.

**ラボ終了**
