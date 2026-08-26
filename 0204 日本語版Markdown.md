---
lab:
  title: '演習ラボ 0204: Intune へのデバイス登録'
  description: このラボでは、Windows デバイスを Microsoft Intune に登録し、登録状態を確認します。
  duration: 108 minutes
  level: 200
  islab: true
  primarytopics:
    - Microsoft Intune
    - Windows
---

# Practice Lab 0204: Enrolling devices into Microsoft Intune

## 概要

このラボでは、Windows クライアントを Entra ID に参加させ、デバイスが Microsoft Intune に自動登録されたことを確認します。

### 前提条件

このラボを開始する前に、次のラボを完了しておく必要があります。

- 0101-Managing Identities in Entra ID

- 0102-Synchronizing identities by using Entra Connect

- 0203-Manage Device Enrollment into Intune

  > 注: Entra ID への Windows Hello サインイン認証を保護するために使用するテキスト メッセージを受信できる携帯電話も必要です。

### シナリオ

Aaron Nicholls に適切なライセンスを割り当てました。次に、Windows デバイスを Entra ID に参加させ、そのデバイスを Microsoft Intune に自動登録する処理をテストします。

### Task 1: Automatically enroll a Windows device to Microsoft Intune

1. Sign in to **SEA-WS1** as **Admin** with the password of **Pa55w.rd**.

2. **Start**、**Settings** の順に選択します。

3. **Settings** で **Accounts** を選択します。

4. Accounts ページで **Access work or school** を選択します。

5. **Access work or school** ページで **Connect** を選択します。

6. **Microsoft account** ウィンドウで **Join this device to Microsoft Entra ID** を選択します。

7. **Sign in** ページで **`Aaron@yourtenant.onmicrosoft.com`** と入力し、**Next** を選択します。

8. **Enter password** ページで **Pa55w.rd** と入力し、**Sign in** を選択します。

9. **Make sure this is your organization** ダイアログで **Join** を選択します。

10. **You're all set!** ページの情報を確認し、**Done** を選択します。

11. **Access work or school** セクションに **Connected to Contoso's Azure AD** と表示されていることを確認します。

12. **Connected to Contoso's Azure AD**、**Info** の順に選択します。

13. Contoso が管理する領域の情報を確認し、下にスクロールして **Sync** を選択します。これにより、Intune とのデバイス同期が強制的に実行されます。

14. **Settings** ウィンドウを閉じます。

### Task 2: Validate device enrollment into Entra ID and Intune

1. **SEA-WS1** のタスク バーで **Start** を選択し、**cert** と入力して **Manage computer certificates** を選択します。**User Account Control** で **Yes** を選択します。
  
2. **Certificates** コンソールのナビゲーション ペインで **Personal** を展開し、**Certificates** ノードを選択します。詳細ペインに次の証明書が表示されていることを確認します。

-   Microsoft Intune MDM Device CA
-   MS-Organization-Access
-   MS-Organization-P2P-Access \[2026\]

    これは、デバイスが Entra に参加し、Intune に登録されていることを示します。

3. Certificates ウィンドウを閉じます。

4. **Start** を右クリックし、**Windows Terminal** を選択します。

5. PowerShell コンソールで次のコマンドを入力し、**Enter** キーを押します。 

   ```powershell
   dsregcmd /status
   ```

6. **Device State** の出力に **AzureAdJoined : YES** と表示されていることを確認します。これは、デバイスが Azure AD に参加していることを示します。

7. **Tenant Details** の出力に、次の3つのエントリが存在することを確認します。

   ```cmd
   mdmUrl : https://enrollment.manage.microsoft.com/enrollmentserver/discovery.svc
   mdmTouUrl : https://portal.manage.microsoft.com/TermsofUse.aspx
   mdmComplianceUrl : https://portal.manage.microsoft.com/?portalAction=Compliance
   ```

   > Note: These entries indicate that the device is enrolled in Intune.

### Task 3: Sign in as an Entra user

1. Sign out of **SEA-WS1**.

2. **Other user** を選択し、パスワード **Pa55w.rd** を使用して **`Aaron@yourtenant.onmicrosoft.com`** としてサインインします。

2. **Use Windows Hello with your account** ページで **OK** を選択します。

3. **Let's keep your account secure** ページで **Next** を選択します。

4. **Install Microsoft Authenticator** ページで **Set up a different way to sign in** を選択します。**注**: 正しいリンクを選択してください。

5. **Add a sign-in method** ダイアログで **Phone** を選択します。

6. **Add your phone number** ページで **Country code** を選択し、**Phone number** フィールドにテキスト メッセージを受信できる携帯電話番号を入力して、**Next** を選択します。

7. 確認コードを受信したら、**Verify your phone number** ページにコードを入力し、**Next** を選択します。

8. **Phone number added** ページで **Done** を選択します。

9. **Set up a PIN** ページの **New PIN** と **Confirm PIN** ボックスに **102938** と入力し、**OK** を選択します。

10. **All set!** ページで **OK** を選択します。

11. Sign out of **SEA-WS1**.

### タスク 4: Intune コンソールでデバイス登録を確認する

1. Switch to **SEA-SVR1** as **Contoso\Administrator** with the password of **Pa55w.rd**. 

2. Microsoft Edge のアドレス バーに **https://intune.microsoft.com** と入力して **Enter** キーを押し、テナント管理者アカウントでサインインします。

3. ナビゲーション ペインで **デバイス**を選択します。

4. **デバイス | 概要**ブレードの **プラットフォームごとのデバイスの管理**で、**Windows** の下に **1** と表示されていることを確認します。表示されるまで時間がかかる場合があります。

5. **デバイス | 概要**ブレードで **すべてのデバイス**を選択し、**SEA-WS1** が一覧に表示されていることを確認します。

6. Note that for SEA-WS1, the **Managed by** column displays **Intune** and the **Ownership** column displays **Corporate**. 

   _注: このビューには Intune へ登録されたデバイスが表示されます。Entra と Intune の間で自動登録を構成したため、Entra に参加または登録されるデバイスは Intune に自動登録されます。登録の設定前に参加したデバイスは、Entra に参加または登録されるだけで、Intune には登録されません。_

7. **Microsoft Edge** で新しいタブを開き、アドレス バーに **https://entra.microsoft.com** と入力して **Enter** キーを押します。

8. Microsoft Entra 管理センターのナビゲーション ペインで、**デバイス**、**すべてのデバイス**の順に選択します。

   > SEA-WS1 を確認します。参加の種類列に **Microsoft Entra joined**、MDM 列に **Microsoft Intune** と表示されていることを確認します。

9. 開いているすべてのウィンドウを閉じます。

**結果**: この演習を完了すると、Windows クライアントが Entra ID に正常に参加し、デバイスが Microsoft Intune に自動登録されたことを確認できます。

**ラボ終了**
