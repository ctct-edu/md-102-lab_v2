---
lab:
  title: 'Practice Lab 0201: Configuring and managing Entra Join'
  description: このラボでは、Entra ID 参加の設定を構成し、Windows デバイスで標準の Entra 参加と Entra ハイブリッド参加の両方を実行します。
  duration: 100 minutes
  level: 200
  islab: true
  primarytopics:
    - Windows
---

# 演習ラボ 0201: Entra Join の構成と管理

## 概要

このラボでは、Entra ID 参加の設定を構成し、Windows デバイスで標準の Entra 参加と Entra ハイブリッド参加の両方を実行します。

### 前提条件

このラボを開始する前に、次のラボを完了しておく必要があります。

- 0102-Synchronizing Identities by using Microsoft Entra Connect

  > 注: Entra ID への Windows Hello サインイン認証を保護するために使用するテキスト メッセージを受信できる携帯電話も必要です。

## 演習 1: Entra Join の構成

### シナリオ

すべてのユーザーがデバイスを Entra ID に参加させられるように、Entra ID のデバイス設定を構成します。また、ユーザーが参加させられるデバイスを最大20台に制限し、Allan Deyoung をすべての Entra 参加済みデバイスのローカル管理者として追加します。最後に、Joni Sherman が SEA-WS1 をテナントへ参加させ、Entra 参加が想定どおりに機能することを確認します。

### タスク 1: Entra 参加のデバイス設定を構成する

1. 手元の PC で Microsoft Edge を起動し、アドレス バーに **https://entra.microsoft.com** と入力して **Enter** キーを押します。

2. テナント管理者のパスワードを使用して、`Admin@yourtenant.onmicrosoft.com` としてサインインします。サインイン状態の維持を確認するプロンプトが表示された場合は、**いいえ**を選択します。 

   > Microsoft Entra 管理センターが開きます。

2. Microsoft Entra 管理センターのナビゲーション ペインで、**デバイス**、**すべてのデバイス**の順に選択します。

   > まだデバイスを参加させていないため、デバイスが見つからないことを確認します。

2. **デバイス | すべてのデバイス**ページで、**デバイスの設定**を選択します。

2. **デバイス | デバイスの設定**ページの詳細ペインで、**ユーザーはデバイスを Microsoft Entra に参加させることができます**の下にある **すべて**が選択されていることを確認します。 

   > これは、すべての Entra ユーザーが Windows 10 以降のデバイスを Microsoft Entra に参加させられることを示します。この設定は、Entra ハイブリッド参加済みデバイス、または Windows Autopilot の自己展開モードで参加したデバイスには適用されません。

2. **Microsoft Entra でデバイスを登録または参加させるには多要素認証が必要**セクションで、設定が **いいえ**になっていることを確認します。 

2. **ユーザーあたりのデバイスの最大数**セクションで、**20** を選択します。

2. **ローカル管理者の設定**で、**Microsoft Entra 参加済みのすべてのデバイスの追加のローカル管理者を管理する**を選択します。デバイス管理者ページが開きます。

2. デバイス管理者ページで、**割り当ての追加**を選択します。

2. 検索ボックスに **Allan Deyoung** と入力し、**Allan Deyoung** ユーザー オブジェクトを選択して、**追加**を選択します。 

    > Allan Deyoung が、すべての Entra 参加済みデバイスのデバイス管理者として追加されます。

2. ページ上部のナビゲーション階層リンクで、**デバイス | デバイスの設定**を選択します。

2. デバイスの設定ページで、**保存**を選択します。

2. Entra 管理センターのナビゲーション ペインで、**認証方法**を選択します。

2. **認証方法**ページで、**SMS** を選択します。

2. **SMS settings** ページで **Enable** を選択し、SMS を認証方法として使用できるようにします。

2. ページ下部の **保存**を選択します。

### タスク 2: Entra 参加を実行する

1. **SEA-WS1** に切り替え、パスワード **Pa55w.rd** を使用して **Admin** としてサインインします。

2. タスク バーで **Start**、**Settings** の順に選択します。

3. **Settings** ウィンドウで **Accounts** を選択します。

4. Accounts ページで **Access work or school** を選択します。

5. **Access work or school** ページで **Connect** を選択します。

6. **Microsoft account** ウィンドウで **Join this device to Microsoft Entra ID** を選択します。

7. **Sign in** ページで **JoniS@yourtenant.onmicrosoft.com** と入力し、**Next** を選択します。

8. **Enter password** ページで Resources タブにあるユーザー パスワードを入力し、**Sign in** を選択します。

9. **Make sure this is your organization** ダイアログで **Join** を選択します。

10. **You're all set!** ページで **Done** を選択します。

11. **Access work or school** ページに **Connected to Contoso's Azure AD** と表示されていることを確認します。

12. **Settings** ページを閉じます。

### タスク 3: Entra 参加を検証する

1. SEA-WS1 で **Start** を右クリックし、**Windows Terminal** を選択します。

2. PowerShell コンソールで次のコマンドを入力し、**Enter** キーを押します。

   ```powershell
   dsregcmd /status
   ```

3. **Device State** の出力に **AzureAdJoined : YES** と表示されていることを確認します。

   > これは、デバイスが Entra に参加していることを示します。

4. PowerShell を閉じます。

5. **Start** を右クリックし、**Computer Management** を選択します。

6. Computer Management で **Local Users and Groups** を展開し、**Groups** を選択します。

7. **Administrators** グループをダブルクリックします。

   > 次を確認します: Joni Sherman has been added as a local Administrator on SEA-WS1. Also notice two security principals represented by their security identifiers (SID). These two SIDs represent the Entra ID global administrator role, and the Entra joined device administrator role. 

8. 開いているすべてのウィンドウを閉じ、SEA-WS1 からサインアウトします。

9. 手元の PC の Microsoft Entra 管理センターに切り替えます。

10. Microsoft Entra 管理センターで、**デバイス**、**すべてのデバイス**の順に選択します。 

    > デバイス ペインに SEA-WS1 が表示されていることを確認します。 

11. **参加の種類**が **Microsoft Entra joined**、所有者が **Joni Sherman** であることを確認します。 

    > MDM 列に None と表示されていることも確認します。これは、デバイスがまだ Microsoft Intune で管理されていないことを示します。

### タスク 4: Entra ユーザーとして Windows にサインインする

1. **SEA-WS1** に切り替え、前のタスクで使用したユーザー パスワードを使用して **`JoniS@yourtenant.onmicrosoft.com`** としてサインインします。

2. At the **Use Windows Hello with your account** page, **OK**.

3. **Let's keep your account secure** ページで **Next** を選択します。

4. **Install Microsoft Authenticator** ページで **Set up a different way to sign in** を選択します。**注**: 正しいリンクを選択してください。

5. **Add a sign-in method** ダイアログで **Phone** を選択します。

6. **Add your phone number** ページで **Country code** を選択し、**Phone number** フィールドにテキスト メッセージを受信できる携帯電話番号を入力して、**Next** を選択します。

7. 確認コードを受信したら、**Verify your phone number** ページにコードを入力し、**Next** を選択します。

8. **Phone number added** ページで **Done** を選択します。

9. **Set up a PIN** ページの **New PIN** と **Confirm PIN** ボックスに **`102938`** と入力し、**OK** を選択します。

10. **All set!** ページで **OK** を選択します。

### タスク 5: Entra から Windows デバイスを削除する

1. On SEA-WS1, whilst still signed in as **Joni Sherman**, **Start** 続いて **Settings**.

2. **Settings** ウィンドウで **Accounts** を選択します。

3. Accounts ページで **Access work or school** を選択します。

4. **Access work or school** ページで **Connected to Contoso's Azure AD** を選択します。

5. Select **Disconnect** 続いて **Yes**.

6. **Disconnect from the organization** ページで **Disconnect** を選択します。

7. **Windows Security** ダイアログの **Email address** ボックスに **Admin**、**Password** ボックスに **Pa55w.rd** と入力し、**OK** を選択します。

8. **Restart your PC** ダイアログで **Restart now** を選択します。SEA-WS1 が再起動します。

**結果**: この演習を完了すると、Microsoft Entra のデバイス設定を構成し、デバイスを Entra に参加させた後、Entra から削除できます。

## 演習 2: Entra ハイブリッド参加の構成

### シナリオ

一部の Contoso Windows デバイスは、現在ローカルの Active Directory Domain Services に参加しています。クラウド サービスへシームレスにアクセスできるように、Entra ハイブリッド参加を有効にします。Entra Connect Sync を再構成し、SEA-CL2 で処理をテストします。

### タスク 1: 環境を準備する

1. 手元の PC の Microsoft Entra 管理センターに切り替えます。

2. **Start** を選択し、 **Windows Administrative Tools**, 続いて **Active Directory Users and Computers**.

3. In **Active Directory Users and Computers**, right-click **Contoso.com**, point to **New**, 続いて **Organizational Unit**.

4. **New-Object - Organizational Unit** ダイアログで **`Entra ID clients`** と入力し、**OK** を選択します。

5. ナビゲーション ペインで **Seattle Clients** を選択します。

6. **SEA-CL2** 続いて **Move**.

7. **Move** ダイアログで **Entra ID clients** を選択し、**OK** を選択します。

8. **Active Directory Users and Computers**.

### タスク 2: Entra Connect Sync で Entra ハイブリッド参加を構成する

1. **SEA-SVR1** の **Desktop** で **Azure AD Connect** をダブルクリックします。

2. **Microsoft Entra Connect Sync** ウィンドウで **Configure** を選択します。

3. **Additional tasks** ページで **Configure device options**、**Next** の順に選択します。

4. **Overview** ページで **Next** を選択します。

5. **Connect to Microsoft Entra ID** ページで **Next** を選択します。

6. **Sign in to your account** ウィンドウでテナント管理者アカウントを選択し、テナント パスワードを入力して **Sign in** を選択します。

7. **Device options** ページで **Configure Hybrid Microsoft Entra ID join**、**Next** の順に選択します。

8. **Device operating systems** ページで **Windows 10 or later domain-joined devices**、**Next** の順に選択します。

9. **SCP configuration** ページで **Contoso.com** の横にあるチェック ボックスをオンにします。

10. Select **Microsoft Entra ID** from the **Authentication Service** dropdown and **Add**. 

11. **Enterprise Admin Credentials** ウィンドウで、**User name** に **Contoso\\Administrator**、**Password** に **Pa55w.rd** と入力します。**OK**、**Next** の順に選択します。

12. **Ready to configure** ページで **Configure** を選択して構成を実行します。

13. 構成が完了したら、 **Exit**.

14. **SEA-CL2**.

15. サインイン ページで **Power** ボタンを選択し、**Restart** を選択します。

    > **Note** Restarting **SEA-CL2** will enable quicker discovery of the SCP created by reconfiguring Entra Connect Sync.

16. **SEA-CL2** has restarted, sign in as **Contoso\\Administrator** with the password of **Pa55w.rd**.

### タスク 3: 新しい OU を同期するよう Entra Connect Sync を再構成する

1. **SEA-SVR1** の **Desktop** で **Azure AD Connect** をダブルクリックします。

2. **Microsoft Entra Connect Sync** ウィンドウで **Configure** を選択します。

3. **Additional tasks** ページで **Customize synchronization options**、**Next** の順に選択します。

4. **Connect to Microsoft Entra ID** ページで **Next** を選択します。

5. **Sign in to your account** ウィンドウでテナント管理者アカウントを選択し、テナント パスワードを入力して **Sign in** を選択します。

6. **Connect your directories** ページで **Next** を選択します。

7. **Domain and OU filtering** ページで **Sync selected domains and OUs** が選択されていることを確認し、**Contoso.com** を展開します。

8. **Entra ID clients** の横にあるチェック ボックスをオンにします。ほかの変更は行わず、**Next** を選択します。

9. **Optional features** ページでは変更を行わず、**Next** を選択します。

10. **Ready to configure** ウィンドウで **Configure** を選択し、構成を実行して同期を開始します。

11. 構成が完了したら、 **Exit**.

    > **Note**: Entra Connect Sync synchronizes automatically now when you modify the OUs being synced. You can use the **Synchronization Service** to monitor sync status.

### タスク 4: Entra ハイブリッド参加を確認する

1. **SEA-CL2**.

2. **Start**, **Shut down or sign out**, 続いて **Restart**.

    _Note: The reboot will trigger the Entra hybrid join on SEA-CL2._
   
3. **SEA-CL2** has restarted, sign in as **Contoso\\Administrator** with the password of **Pa55w.rd**.
    
4. タスク バーで **Start** を右クリックし、**Windows Terminal (Admin)** を選択します。

5. **Windows PowerShell** ウィンドウで次のコマンドを入力し、**Enter** キーを押します。

   ```powershell
   dsregcmd /status
   ```

6. **Device State** の出力に **AzureAdJoined : YES** と **DomainJoined : YES** が表示されていることを確認します。

   > **Note**: If the device is not yet joined to Entra ID, switch back to **SEA-SRV1** and run the command below. Once completed, switch back to SEA-CL2 and restart the computer once more.
   
   ```powershell
   Start-ADSyncSyncCycle -PolicyType Delta
   ```

7. Close all windows on SEA-CL2 and sign out.

8. **SEA-SVR1** and switch to the Microsoft Entra admin center.

9. Select **Devices** > **All devices**. 

10. **SEA-CL2** の **Join Type** の値が **Microsoft Entra hybrid joined** であることを確認します。SEA-CL2 が一覧にない場合は、必要に応じて **Refresh** ボタンを選択します。

11. Close all windows on **SEA-SVR1**.

**結果**: この演習を完了すると、Entra ハイブリッド参加の構成と検証が正常に完了します。

**ラボ終了**
