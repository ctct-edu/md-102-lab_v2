### lab:
title: '演習ラボ 0204: Microsoft Intune へのデバイス登録'
description: このラボでは、Windows クライアントを Entra ID に参加させ、デバイスが Microsoft Intune に自動登録されたことを確認します。
duration: 108 minutes
level: 200
islab: true
primarytopics:
\- Microsoft Intune
\- Windows

## 演習ラボ 0204: Microsoft Intune へのデバイス登録

### 概要

このラボでは、Windows クライアントを Entra ID に参加させ、デバイスが Microsoft Intune に自動登録されたことを確認します。

#### 前提条件

このラボの前に、次のラボを完了しておく必要があります。
- 0101-Managing Identities in Entra ID
- 0102-Synchronizing identities by using Entra Connect
- 0203-Manage Device Enrollment into Intune<br>注: Entra ID に対する Windows Hello サインイン認証をセキュリティで保護するため、テキスト メッセージを受信できる携帯電話も必要です。

#### シナリオ

Aaron Nicholls に適切なライセンスを割り当てました。ここでは、Windows デバイスを Entra ID に参加させ、Microsoft Intune に自動登録するプロセスをテストします。

#### タスク 1: Windows デバイスを Microsoft Intune に自動登録する

1. **SEA-WS1** に、パスワード **Pa55w.rd** を使用して **Admin** としてサインインします。

2. **Start**、**Settings** の順に選択します。

3. **Settings** で **Accounts** を選択します。

4. **Accounts** ページで **Access work or school** を選択します。

5. **Access work or school** ページで **Connect** を選択します。

6. **Microsoft account** ウィンドウで **Join this device to Microsoft Entra ID** を選択します。

7. **Sign in** ページに **Aaron@yourtenant.onmicrosoft.com** と入力し、**Next** を選択します。

8. **Enter password** ページに **Pa55w.rd** と入力し、**Sign in** を選択します。

9. **Make sure this is your organization** ダイアログ ボックスで **Join** を選択します。

10. **You're all set\!** ページの情報を確認し、**Done** を選択します。

11. **Access work or school** セクションに **Connected to Contoso's Azure AD** と表示されていることを確認します。

12. **Connected to Contoso's Azure AD**、**Info** の順に選択します。

13. Contoso が管理する領域に関する情報を確認し、下にスクロールして **Sync** を選択します。これにより、Intune とのデバイス同期が強制的に実行されます。

14. **Settings** ウィンドウを閉じます。

#### タスク 2: Entra ID と Intune へのデバイス登録を検証する

1. **SEA-WS1** のタスク バーで **Start** を選択し、「**cert**」と入力して **Manage computer certificates** を選択します。**User Account Control** で **Yes** を選択します。

2. **Certificates** コンソールのナビゲーション ペインで **Personal** を展開し、**Certificates** ノードを選択します。詳細ペインに次の証明書が表示されていることを確認します。
   - Microsoft Intune MDM Device CA
   - MS-Organization-Access
   - MS-Organization-P2P-Access \[2026\]<br>これは、デバイスが Entra に参加し、Intune に登録されていることを示します。

3. **Certificates** ウィンドウを閉じます。

4. **Start** を右クリックし、**Windows Terminal** を選択します。

5. PowerShell コンソールで次のコマンドを入力し、**Enter** キーを押します: `dsregcmd /status`

6. 出力の **Device State** で **AzureAdJoined : YES** と表示されていることを確認します。これは、デバイスが Azure AD に参加していることを示します。

7. 出力の **Tenant Details** に次の 3 つのエントリが存在することを確認します:<br>`mdmUrl : https://enrollment.manage.microsoft.com/enrollmentserver/discovery.svc`<br>`mdmTouUrl : https://portal.manage.microsoft.com/TermsofUse.aspx`<br>`mdmComplianceUrl : https://portal.manage.microsoft.com/?portalAction=Compliance`<br>注: これらのエントリは、デバイスが Intune に登録されていることを示します。

#### タスク 3: Entra ユーザーとしてサインインする

1. **SEA-WS1** からサインアウトします。

2. **Other user** を選択し、パスワード **Pa55w.rd** を使用して **Aaron@yourtenant.onmicrosoft.com** としてサインインします。

3. **Use Windows Hello with your account** ページで **OK** を選択します。

4. **Let's keep your account secure** ページで **Next** を選択します。

5. **Install Microsoft Authenticator** ページで **Set up a different way to sign in** を選択します。**注**: 正しいリンクを選択してください。

6. **Add a sign-in method** ダイアログ ボックスで **Phone** を選択します。

7. **Add your phone number** ページで **Country code** を選択し、**Phone number** フィールドにテキスト メッセージを受信できる携帯電話番号を入力して **Next** を選択します。

8. 確認コードを受信したら、**Verify your phone number** ページにコードを入力し、**Next** を選択します。

9. **Phone number added** ページで **Done** を選択します。

10. **Set up a PIN** ページの **New PIN** ボックスと **Confirm PIN** ボックスに **102938** と入力し、**OK** を選択します。

11. **All set\!** ページで **OK** を選択します。

12. **SEA-WS1** からサインアウトします。

#### タスク 4: Intune コンソールでデバイス登録を確認する

1. 受講者の手元 PC で日本語版 **Microsoft Edge** を開き、[**https://intune.microsoft.com**](https://intune.microsoft.com) にアクセスします。テナント管理者アカウントでサインインします。

2. ナビゲーション ペインで **デバイス**を選択します。

3. **デバイス | 概要**ブレードの**プラットフォーム別のデバイス管理**で、**Windows** の下に **1** と表示されていることを確認します。表示まで時間がかかる場合があります。

4. **デバイス | 概要**ブレードで **すべてのデバイス**を選択し、**SEA-WS1** が表示されていることを確認します。

5. SEA-WS1 の**管理者**列に **Intune**、**所有権**列に**企業**と表示されていることを確認します。<br>_注: このビューには、Intune に登録されているデバイスが表示されます。Entra と Intune の間で自動登録を構成したため、Entra に参加または登録されたデバイスは Intune に自動登録されます。登録を設定する前に参加したデバイスは、Entra に参加または登録されているだけで、Intune には登録されていません。_

6. **Microsoft Edge** で新しいタブを開き、[**https://entra.microsoft.com**](https://entra.microsoft.com) にアクセスします。

7. Microsoft Entra 管理センターのナビゲーション ペインで、**デバイス**、**すべてのデバイス**の順に選択します。<br>**SEA-WS1** を確認します。**参加の種類**列に **Microsoft Entra 参加済み**、MDM 列に **Microsoft Intune** と表示されていることを確認します。

8. 開いているすべてのウィンドウを閉じます。

**結果**: この演習では、Windows クライアントを Entra ID に参加させ、デバイスが Microsoft Intune に自動登録されたことを確認しました。

**ラボ終了**