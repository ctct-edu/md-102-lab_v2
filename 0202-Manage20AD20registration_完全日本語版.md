---
lab:
    title: '演習ラボ 0202: Entra ID デバイス登録の管理'
    description: この演習では、Windows デバイスを使用して Entra 登録を実行します。
    duration: 90 minutes
    level: 200
    islab: true
    primarytopics:
        - Windows
---

## 演習ラボ 0202: Entra ID デバイス登録の管理

### 概要

この演習では、Windows デバイスを使用して Entra 登録を実行します。

### 演習 1: Entra デバイス登録の構成

#### シナリオ

複数のユーザーから、個人所有の iOS、Android、Windows の各デバイスを使用して Contoso のクラウド リソースにアクセスしたいという要望が寄せられています。Contoso はこれらの Windows デバイスを所有していないため、ユーザーに Entra 参加を実行させることは避けたいと考えています (Entra 参加できるのは Windows デバイスのみです)。その代わりに、ユーザーが自分のデバイスを Entra に登録できるようにする必要があります。これにより、必要に応じてアプリに会社のポリシーを適用でき、ユーザーは引き続き Contoso のリソースにアクセスできます。ここでは、Windows 11 デバイスを使用して Entra デバイス登録をテストします。

#### タスク 1: Entra ID デバイス登録を構成する
- 手元 PC で、日本語版 Microsoft Edge を起動します。アドレス バーに [**https://entra.microsoft.com**](https://entra.microsoft.com) と入力し、**Enter** キーを押します。
- **Admin@yourtenant.onmicrosoft.com** としてサインインし、テナントの管理者パスワードを使用します。**サインインの状態を維持しますか?** のメッセージが表示された場合は、**いいえ** を選択します。<br>Microsoft Entra 管理センターが開きます。
- Microsoft Entra 管理センターのナビゲーション ペインで **デバイス** を選択し、続いて **すべてのデバイス** を選択します。
- **デバイス | すべてのデバイス** ページで、**デバイスの設定** を選択します。
- **デバイス | デバイスの設定** ページの詳細ペインで、**ユーザーはデバイスを Microsoft Entra に登録できる** が **すべて** に設定され、グレー表示になっていることを確認します。<br>このオプションは、テナントで Microsoft Intune が有効になっている場合、既定でグレー表示となり **すべて** に設定されます。これにより、すべてのユーザーが Windows 10 以降の個人所有デバイス、iOS、Android、macOS の各デバイスを Entra に登録できるようになります。

#### タスク 2: Entra 登録を実行する
- **SEA-WS1** に切り替え、**Admin** としてパスワード **Pa55w.rd** でサインインします。
- タスク バーで **Start** を選択し、続いて **Settings** を選択します。
- **Settings** ウィンドウで、**Accounts** を選択します。
- **Accounts** ページで、**Access work or school** を選択します。
- **Access work or school** ページで、**Connect** を選択します。
- **Microsoft account** ウィンドウの **Email address** ボックスに **JoniS@yourtenant.onmicrosoft.com** を入力し、続いて **Next** を選択します。
- **Enter password** ページで、以前のタスクで使用したユーザー パスワードを入力し、続いて **Sign in** を選択します。
- **You're all set!** ページで、**Done** を選択します。
- **Access work or school** ページで、Joni の **Work or school** アカウントが表示されていることを確認します。
- **Settings** ページを閉じます。

#### タスク 3: Entra 登録を検証する
- SEA-WS1 で **Start** を右クリックし、続いて **Windows Terminal (Admin)** を選択します。**User Account Control** が表示されたら、**Yes** を選択します。
- PowerShell コンソールで次のように入力し、**Enter** キーを押します: `dsregcmd /status`
- 出力の **User State** セクションで、**WorkplaceJoined : YES** が表示されていることを確認します。これは、ユーザーが Azure AD でデバイス登録を実行したことを示しています。
- PowerShell を閉じ、続いて SEA-WS1 からサインアウトします。
- 手元 PC の日本語版 Microsoft Edge に切り替えます。
- Microsoft Entra 管理センターで、**Entra ID** を展開します。
- **デバイス** を選択し、続いて **すべてのデバイス** を選択します。デバイス ペインで、SEA-WS1 が一覧に表示されていることに注目します。
- **参加の種類** が **Microsoft Entra 登録済み** と表示され、所有者が **Joni Sherman** であることを確認します。<br>デバイスが Microsoft Entra 参加済みではなく、Microsoft Entra 登録済みであることに注目してください。Entra 登録済みデバイスは、通常、Entra 参加できないデバイスや、ユーザーが個人所有しているデバイスです。デバイスを登録すると、クラウド ベースのリソースへのアクセスが提供されます。
- Microsoft Edge を閉じます。

#### タスク 4: Windows へのサインインと組織からの切断
- **SEA-WS1** に切り替え、Entra 参加済みや Entra ハイブリッド参加済みのデバイスとは異なり、Entra 登録済みデバイスではローカル アカウントしか選択できないことに注目します。
- SEA-WS1 で、**Admin** としてパスワード **Pa55w.rd** でサインインします。
- **Start** を選択し、続いて **Settings** を選択します。
- **Settings** ウィンドウで、**Accounts** を選択します。
- **Accounts** ページで、**Access work or school** を選択します。
- **Access work or school** ページで、**JoniS** の Work or school アカウントを選択します。
- Disconnect this account の横にある **Disconnect** を選択し、続いて **Yes** を選択します。<br>登録済みデバイスを Entra ID から切断するのに、再起動は不要であることに注目してください。
- 次のラボに備えて、**Start** を選択し、続いて **Power** アイコンを選択して、**Restart** を選択します。  
**結果**: この演習を完了すると、Entra デバイス登録を構成できたことになります。  
**ラボの終了**
