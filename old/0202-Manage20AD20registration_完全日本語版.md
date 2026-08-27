### lab:
title: '演習ラボ 0202: Entra ID デバイス登録の管理'
description: このラボでは、Windows デバイスを使用して Entra 登録を実行します。
duration: 90 minutes
level: 200
islab: true
primarytopics:
\- Windows

## 演習ラボ 0202: Entra ID デバイス登録の管理

### 概要

このラボでは、Windows デバイスを使用して Entra 登録を実行します。

### 演習 1: Entra デバイス登録の構成

#### シナリオ

複数のユーザーから、個人所有の iOS、Android、および Windows デバイスを使用して Contoso のクラウド リソースにアクセスしたいという要望がありました。Contoso はこれらの Windows デバイスを所有していないため、ユーザーには Entra 参加を実行させません（Entra に参加できるのは Windows デバイスのみです）。代わりに、ユーザーがデバイスを Entra に登録できるようにする必要があります。これにより、必要に応じてアプリに会社のポリシーを適用しながら、ユーザーによる Contoso リソースへのアクセスを許可できます。Windows 11 デバイスを使用して Entra デバイス登録をテストします。

#### タスク 1: Entra ID デバイス登録を構成する

1. 受講者の手元 PC で日本語版 **Microsoft Edge** を開き、アドレス バーに [**https://entra.microsoft.com**](https://entra.microsoft.com) と入力して **Enter** キーを押します。

2. Admin@yourtenant.onmicrosoft.com として、テナントの Admin パスワードを使用してサインインします。**サインインの状態を維持しますか?** と表示された場合は、**いいえ**を選択します。<br>Microsoft Entra 管理センターが開きます。

3. Microsoft Entra 管理センターのナビゲーション ペインで、**デバイス**、**すべてのデバイス**の順に選択します。

4. **デバイス | すべてのデバイス**ページで、**デバイスの設定**を選択します。

5. **デバイス | デバイスの設定**ページの詳細ペインで、**ユーザーはデバイスを Microsoft Entra に登録できます**が **すべて**に設定され、グレー表示されていることを確認します。<br>テナントで Microsoft Intune が有効になっている場合、このオプションは既定でグレー表示され、**すべて**に設定されます。これにより、すべてのユーザーが Windows 10 以降の個人所有デバイス、iOS、Android、および macOS デバイスを Entra に登録できます。

#### タスク 2: Entra 登録を実行する

1. **SEA-WS1** に切り替え、パスワード **Pa55w.rd** を使用して **Admin** としてサインインします。

2. タスク バーで **Start**、**Settings** の順に選択します。

3. **Settings** ウィンドウで **Accounts** を選択します。

4. **Accounts** ページで **Access work or school** を選択します。

5. **Access work or school** ページで **Connect** を選択します。

6. **Microsoft account** ウィンドウの **Email address** ボックスに **JoniS@yourtenant.onmicrosoft.com** と入力し、**Next** を選択します。

7. **Enter password** ページで、前のタスクで使用したユーザー パスワードを入力し、**Sign in** を選択します。

8. **You're all set\!** ページで **Done** を選択します。

9. **Access work or school** ページに Joni の **Work or school account** が表示されていることを確認します。

10. **Settings** ページを閉じます。

#### タスク 3: Entra 登録を検証する

1. **SEA-WS1** で **Start** を右クリックし、**Windows Terminal (Admin)** を選択します。**User Account Control** で **Yes** を選択します。

2. PowerShell コンソールで次のコマンドを入力し、**Enter** キーを押します: `dsregcmd /status`

3. 出力の **User State** で、**WorkplaceJoined : YES** と表示されていることを確認します。これは、ユーザーが Azure AD でデバイス登録を実行したことを示します。

4. PowerShell を閉じ、**SEA-WS1** からサインアウトします。

5. 受講者の手元 PC に切り替えます。

6. Microsoft Edge の Microsoft Entra 管理センターで、**Entra ID** を展開します。

7. **デバイス**、**すべてのデバイス**の順に選択します。デバイス ペインに **SEA-WS1** が表示されていることを確認します。

8. **参加の種類**が **Microsoft Entra 登録済み**、所有者が **Joni Sherman** と表示されていることを確認します。<br>このデバイスは Microsoft Entra 参加済みではなく、Microsoft Entra 登録済みであることに注意してください。Entra 登録済みデバイスは通常、Entra に参加できないデバイス、またはユーザーが個人所有するデバイスです。デバイスを登録すると、クラウドベースのリソースにアクセスできるようになります。

9. Microsoft Edge を閉じます。

#### タスク 4: Windows にサインインして組織から切断する

1. **SEA-WS1** に切り替え、Entra 参加済みまたは Entra ハイブリッド参加済みデバイスとは異なり、Entra 登録済みデバイスではローカル アカウントのみを選択できることを確認します。

2. **SEA-WS1** で、パスワード **Pa55w.rd** を使用して **Admin** としてサインインします。

3. **Start**、**Settings** の順に選択します。

4. **Settings** ウィンドウで **Accounts** を選択します。

5. **Accounts** ページで **Access work or school** を選択します。

6. **Access work or school** ページで **JoniS** の **Work or School account** を選択します。

7. **Disconnect this account** の横にある **Disconnect** を選択し、**Yes** を選択します。<br>登録済みデバイスを Entra ID から切断するために再起動する必要はありません。

8. 次のラボに備えて、**Start**、**Power** アイコン、**Restart** の順に選択します。

**結果**: この演習では、Entra デバイス登録を構成しました。

**ラボ終了**