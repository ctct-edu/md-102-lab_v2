---
lab:
    title: '演習ラボ 0204: Microsoft Intune へのデバイスの登録'
    description: この演習では、Windows クライアントを Entra ID に参加させ、そのデバイスが自動的に Microsoft Intune に登録されたことを確認します。
    duration: 108 minutes
    level: 200
    islab: true
    primarytopics:
        - Microsoft Intune
        - Windows
---

## 演習ラボ 0204: Microsoft Intune へのデバイスの登録

### 概要

この演習では、Windows クライアントを Entra ID に参加させ、そのデバイスが自動的に Microsoft Intune に登録されたことを確認します。

#### 前提条件

このラボを実施する前に、次のラボを完了しておく必要があります。
- 0101-Managing Identities in Entra ID
- 0102-Synchronizing identities by using Entra Connect
- 0203-Manage Device Enrollment into Intune<br>注: Entra ID への Windows Hello サインイン認証を保護するために使用するテキスト メッセージを受信できる携帯電話も必要になります。

#### シナリオ

Aaron Nicholls に適切なライセンスを割り当てたので、ここからは Windows デバイスを Entra ID に参加させ、それを自動的に Microsoft Intune に登録させるプロセスをテストします。

#### タスク 1: Windows デバイスを Microsoft Intune に自動的に登録する
1. **SEA-WS1** に **Admin** としてパスワード **Pa55w.rd** でサインインします。
2. **Start** を選択し、続いて **Settings** を選択します。
3. **Settings** で、**Accounts** を選択します。
4. **Accounts** ページで、**Access work or school** を選択します。
5. **Access work or school** ページで、**Connect** を選択します。
6. **Microsoft account** ウィンドウで、**Join this device to Microsoft Entra ID** を選択します。
7. **Sign in** ページで **Aaron@yourtenant.onmicrosoft.com** と入力し、続いて **Next** を選択します。
8. **Enter password** ページで **Pa55w.rd** を入力し、続いて **Sign in** を選択します。
9. **Make sure this is your organization** ダイアログ ボックスで、**Join** を選択します。
10. **You're all set!** ページで情報を読み、続いて **Done** を選択します。
11. **Access work or school** セクションで、**Connected to Contoso's Azure AD** が表示されていることを確認します。
12. **Connected to Contoso's Azure AD** を選択し、続いて **Info** を選択します。
13. Contoso が管理する領域に関する情報を確認し、下にスクロールして、続いて **Sync** を選択します。これにより、Intune とのデバイス同期が強制的に実行されます。
14. **Settings** ウィンドウを閉じます。

#### タスク 2: Entra ID と Intune へのデバイス登録を検証する
1. **SEA-WS1** のタスク バーで **Start** を選択し、**cert** と入力して、**Manage computer certificates** を選択します。**User Account Control** が表示されたら、**Yes** を選択します。
2. **Certificates** コンソールのナビゲーション ペインで **Personal** を展開し、**Certificates** ノードを選択します。詳細ペインに次の証明書が一覧表示されていることを確認します。
    - Microsoft Intune MDM Device CA
    - MS-Organization-Access
    - MS-Organization-P2P-Access [2026]<br>これは、デバイスが Entra 参加済みかつ Intune 登録済みであることを示しています。
3. Certificates ウィンドウを閉じます。
4. **Start** を右クリックし、続いて **Windows Terminal** を選択します。
5. PowerShell コンソールで次のように入力し、**Enter** キーを押します: `dsregcmd /status`
6. 出力の **Device State** セクションで、**AzureAdJoined : YES** が表示されていることを確認します。これは、デバイスが Azure AD に参加していることを示しています。
7. 出力の **Tenant Details** セクションで、次の 3 つのエントリが存在することを確認します。

    ```
    mdmUrl : https://enrollment.manage.microsoft.com/enrollmentserver/discovery.svc
    mdmTouUrl : https://portal.manage.microsoft.com/TermsofUse.aspx
    mdmComplianceUrl : https://portal.manage.microsoft.com/?portalAction=Compliance
    ```
    <br>注: これらのエントリは、デバイスが Intune に登録されていることを示しています。

#### タスク 3: Entra ユーザーとしてサインインする
1. **SEA-WS1** からサインアウトします。
2. **Other user** を選択し、**Aaron@yourtenant.onmicrosoft.com** としてパスワード **Pa55w.rd** でサインインします。
3. **Use Windows Hello with your account** ページで、**OK** を選択します。
4. **Let's keep your account secure** ページで、**Next** を選択します。
5. **Install Microsoft Authenticator** ページで、**Set up a different way to sign in** を選択します。**注**: 正しいリンクを選択していることを確認してください。
6. **Add a sign-in method** ダイアログ ボックスで、**Phone** を選択します。
7. **Add your phone number** ページで **Country code** を選択し、**Phone number** フィールドに、テキスト メッセージを受信できる携帯電話の番号を入力して、続いて **Next** を選択します。
8. 確認コードを受信したら、そのコードを **Verify your phone number** ページに入力し、続いて **Next** を選択します。
9. **Phone number added** ページで、**Done** を選択します。
10. **Set up a PIN** ページの **New PIN** ボックスと **Confirm PIN** ボックスに **102938** と入力し、続いて **OK** を選択します。
11. **All set!** ページで、**OK** を選択します。
12. **SEA-WS1** からサインアウトします。

#### タスク 4: Intune コンソールでデバイス登録を確認する
1. 手元 PC で、日本語版 Microsoft Edge を起動します。アドレス バーに [**https://intune.microsoft.com**](https://intune.microsoft.com) と入力し、続いて **Enter** キーを押します。テナントの管理者アカウントでサインインします。
2. ナビゲーション ペインで、**デバイス** を選択します。
3. **デバイス | 概要** ブレードの **プラットフォーム別のデバイス管理** で、**Windows** の下に **1** が表示されていることを確認します。表示までにしばらく時間がかかる場合があります。
4. **デバイス | 概要** ブレードで **すべてのデバイス** を選択し、**SEA-WS1** が一覧に表示されていることを確認します。
5. SEA-WS1 について、**管理者** 列に **Intune** が、**所有権** 列に **企業** が表示されていることに注目します。<br>_注: このビューには、Intune に登録されているデバイスが一覧表示されます。Entra と Intune の間で自動登録を構成したため、Entra に参加または登録されたデバイスはすべて、自動的に Intune に登録されることを思い出してください。登録の設定より前に参加されたデバイスは、Entra に参加または登録されているだけで、Intune には登録されていません。_
6. Microsoft Edge で新しいタブを開き、アドレス バーに [**https://entra.microsoft.com**](https://entra.microsoft.com) と入力し、続いて **Enter** キーを押します。
7. Microsoft Entra 管理センターのナビゲーション ペインで **デバイス** を選択し、続いて **すべてのデバイス** を選択します。<br>SEA-WS1 に注目します。参加の種類列に **Microsoft Entra 参加済み** が、MDM 列に **Microsoft Intune** が表示されていることに注目します。
8. 開いているすべてのウィンドウを閉じます。  
**結果**: この演習を完了すると、Windows クライアントを Entra ID に参加させ、そのデバイスが自動的に Microsoft Intune に登録されたことを確認できたことになります。  
**ラボの終了**
