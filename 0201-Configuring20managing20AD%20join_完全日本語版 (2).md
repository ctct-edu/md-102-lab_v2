---
lab:
    title: '練習ラボ 0201: Entra 参加の構成と管理'
    description: このラボでは、Entra ID 参加の設定を構成し、Windows デバイスに対して標準の Entra 参加と Entra ハイブリッド参加の両方のシナリオを実行します。
    duration: 100 minutes
    level: 200
    islab: true
    primarytopics:
    - Windows
---

## 練習ラボ 0201: Entra 参加の構成と管理

### 概要

このラボでは、Entra ID 参加の設定を構成し、Windows デバイスに対して標準の Entra 参加と Entra ハイブリッド参加の両方のシナリオを実行します。

#### 前提条件

このラボの前に、次のラボを完了しておく必要があります。

- 0102-Synchronizing Identities by using Microsoft Entra Connect

  注: Entra ID への Windows Hello のサインイン認証を保護するために使用する、テキスト メッセージを受信できる携帯電話も必要です。

### 演習 1: Entra 参加の構成

#### シナリオ

すべてのユーザーがデバイスを Entra ID に参加させることを許可されるように、Entra ID デバイスの設定を構成する必要があります。また、ユーザーが参加できるデバイスは最大 20 台までとし、すべての Entra 参加済みデバイスで Allan Deyoung をローカル管理者として追加する必要もあります。最後に、Joni Sherman が SEA-WS1 をテナントに参加させることで、Entra 参加が期待どおりに機能することを確認します。

#### タスク 1: Entra 参加のデバイス設定を構成する

1. **SEA-SVR1** で、必要に応じて **Contoso\Administrator** としてパスワード **Pa55w.rd** でサインインし、Server Manager を閉じます。

2. タスク バーで **Microsoft Edge** を選択し、アドレス バーに [**https://entra.microsoft.com**](https://entra.microsoft.com) を入力して、**Enter** キーを押します。

3. ユーザー **Admin@yourtenant.onmicrosoft.com** として、テナントの Admin パスワードを使用してサインインします。**サインインの状態を維持しますか?** のプロンプトが表示された場合は、**いいえ** を選択します。

   Microsoft Entra 管理センターが開きます。

4. Microsoft Entra 管理センターのナビゲーション ペインで、**デバイス** を選択し、続いて **すべてのデバイス** を選択します。

   まだデバイスを参加させていないため、デバイスが見つからないことに注意してください。

5. **デバイス \| すべてのデバイス** ページで、**デバイスの設定** を選択します。

6. **デバイス \| デバイスの設定** ページの詳細ペインで、**ユーザーはデバイスを Microsoft Entra に参加させることができます** の下で **すべて** が選択されていることを確認します。

   これは、すべての Entra ユーザーが Windows 10 以降のデバイスを Microsoft Entra に参加させることを許可されていることを示しています。この設定は、Entra ハイブリッド参加済みデバイス、または Windows Autopilot の自己展開モードを使用して参加したデバイスには適用されないことに注意してください。

7. **デバイスを Microsoft Entra に登録または参加させるときに多要素認証を要求する** セクションで、設定が **いいえ** になっていることを確認します。

8. **ユーザーごとのデバイスの最大数** セクションで、**20** を選択します。

9. **ローカル管理者の設定** の下で、**すべての Entra 参加済みデバイスで追加のローカル管理者を管理する** を選択します。デバイス管理者ページが開きます。

10. デバイス管理者ページで、**+ 割り当ての追加** を選択します。

11. 検索ボックスに **Allan Deyoung** を入力し、**Allan Deyoung** ユーザー オブジェクトを選択して、続いて **追加** を選択します。

    これで、Allan Deyoung がすべての Entra 参加済みデバイスのデバイス管理者として追加されます。

12. ナビゲーションのパンくずリストで、ページ上部にある **デバイス \| デバイスの設定** リンクを選択します。

13. デバイスの設定ページで、**保存** を選択します。

14. Entra 管理センターのナビゲーション ペインで、**認証方法** を選択します。

15. **認証方法** ページで、**SMS** を選択します。

16. **SMS 設定** ページで、**有効化** を選択します (SMS を認証方法として使用できるようにします)。

17. ページの下部で、**保存** を選択します。

#### タスク 2: Entra 参加を実行する

1. **SEA-WS1** に切り替え、**Admin** としてパスワード **Pa55w.rd** でサインインします。

2. タスク バーで **Start** を選択し、続いて **Settings** を選択します。

3. **Settings** ウィンドウで、**Accounts** を選択します。

4. Accounts ページで、**Access work or school** を選択します。

5. **Access work or school** ページで、**Connect** を選択します。

6. **Microsoft account** ウィンドウで、**Join this device to Microsoft Entra ID** を選択します。

7. **Sign in** ページで **JoniS@yourtenant.onmicrosoft.com** を入力し、続いて **Next** を選択します。

8. **Enter password** ページで、ユーザーのパスワード (Resources タブに記載) を入力し、続いて **Sign in** を選択します。

9. **Make sure this is your organization** ダイアログ ボックスで、**Join** を選択します。

10. **You're all set!** ページで、**Done** を選択します。

11. **Access work or school** ページで、**Connected to Contoso's Azure AD** が表示されていることを確認します。

12. **Settings** ページを閉じます。

#### タスク 3: Entra 参加を検証する

1. SEA-WS1 で **Start** を右クリックし、続いて **Windows Terminal** を選択します。

2. PowerShell コンソールで、次を入力して **Enter** キーを押します。

   ```
   dsregcmd /status
   ```

3. **Device State** の下の出力で、**AzureAdJoined : YES** が表示されていることを確認します。

   これは、デバイスが Entra 参加済みであることを示しています。

4. PowerShell を閉じます。

5. **Start** を右クリックし、続いて **Computer Management** を選択します。

6. Computer Management で **Local Users and Groups** を展開し、続いて **Groups** を選択します。

7. **Administrators** グループをダブルクリックします。

   Joni Sherman が SEA-WS1 のローカル Administrator として追加されていることに注意してください。また、セキュリティ識別子 (SID) で表される 2 つのセキュリティ プリンシパルにも注目してください。これら 2 つの SID は、Entra ID のグローバル管理者ロールと、Entra 参加済みデバイスの管理者ロールを表しています。

8. 開いているすべてのウィンドウを閉じ、SEA-WS1 からサインアウトします。

9. **SEA-SVR1** に切り替えます。

10. Microsoft Edge の Microsoft Entra 管理センターで、**デバイス** を選択し、続いて **すべてのデバイス** を選択します。

    デバイス ペインで、SEA-WS1 が一覧表示されていることに注意してください。

11. **参加の種類** が **Microsoft Entra 参加済み** として一覧表示され、所有者が **Joni Sherman** であることを確認します。

    また、MDM 列に **なし** が表示されていることにも注意してください。これは、このデバイスがまだ Microsoft Intune によって管理されていないことを示しています。

#### タスク 4: Entra ユーザーとして Windows にサインインする

1. **SEA-WS1** に切り替え、続いて前のタスクで使用したユーザーのパスワードを使用して **JoniS@yourtenant.onmicrosoft.com** としてサインインします。

2. **アカウントで Windows Hello を使用する** ページで、**OK** を選択します。

3. **アカウントのセキュリティ保護** ページで、**次へ** を選択します。

4. **Microsoft Authenticator アプリのインストール** ページで、**別のサインイン方法を設定する** を選択します。**注:** 正しいリンクを選択していることを確認してください。

5. **サインイン方法の追加** ダイアログ ボックスで、**電話** を選択します。

6. **電話番号の追加** ページで **国コード** を選択し、**電話番号** フィールドにテキスト メッセージを受信できる携帯電話の番号を入力して、続いて **次へ** を選択します。

7. 確認コードを受信したら、**電話番号の確認** ページでそのコードを入力し、続いて **次へ** を選択します。

8. **電話番号が追加されました** ページで、**完了** を選択します。

9. **PIN のセットアップ** ページの **新しい PIN** ボックスと **PIN の確認** ボックスに **102938** を入力し、続いて **OK** を選択します。

10. **完了しました** ページで、**OK** を選択します。

#### タスク 5: Windows デバイスを Entra から削除する

1. SEA-WS1 で、**Joni Sherman** としてサインインしたまま、**Start** を選択し、続いて **Settings** を選択します。

2. **Settings** ウィンドウで、**Accounts** を選択します。

3. Accounts ページで、**Access work or school** を選択します。

4. **Access work or school** ページで、**Connected to Contoso's Azure AD** を選択します。

5. **Disconnect** を選択し、続いて **Yes** を選択します。

6. **Disconnect from the organization** ページで、**Disconnect** を選択します。

7. **Windows Security** ダイアログ ボックスの **Email address** ボックスに **Admin** を入力し、**Password** ボックスに **Pa55w.rd** を入力します。**OK** を選択します。

8. **Restart your PC** ダイアログ ボックスで、**Restart now** を選択します。SEA-WS1 が再起動します。

**結果**: この演習を完了すると、Microsoft Entra デバイスの設定を構成し、デバイスを Entra に参加させ、デバイスを Entra から削除できたことになります。

### 演習 2: Entra ハイブリッド参加の構成

#### シナリオ

一部の Contoso Windows デバイスは、現在ローカルの Active Directory Domain Services に参加しています。これらのデバイスがクラウド サービスにシームレスにアクセスできるようにするため、Entra ハイブリッド参加を有効にする予定です。Entra Connect sync を再構成し、SEA-CL2 でプロセスをテストすることで、Entra ハイブリッド参加をテストします。

#### タスク 1: 環境を準備する

1. **SEA-SVR1** に切り替えます。

2. **Start** を選択し、**Windows Administrative Tools** を展開して、続いて **Active Directory Users and Computers** を選択します。

3. **Active Directory Users and Computers** で **Contoso.com** を右クリックし、**New** をポイントして、続いて **Organizational Unit** を選択します。

4. **New-Object - Organizational Unit** ダイアログ ボックスで **Entra ID clients** を入力し、続いて **OK** を選択します。

5. ナビゲーション ペインで、**Seattle Clients** を選択します。

6. **SEA-CL2** を右クリックし、続いて **Move** を選択します。

7. **Move** ダイアログ ボックスで **Entra ID clients** を選択し、続いて **OK** を選択します。

8. **Active Directory Users and Computers** を閉じます。

#### タスク 2: Entra Connect sync で Entra ハイブリッド参加を構成する

1. **SEA-SVR1** の **Desktop** で、**Azure AD Connect** をダブルクリックします。

2. **Microsoft Entra Connect Sync** ウィンドウで、**Configure** を選択します。

3. **Additional tasks** ページで、**Configure device options** を選択し、**Next** を選択します。

4. **Overview** ページで、**Next** を選択します。

5. **Connect to Microsoft Entra ID** ページで、**Next** を選択します。

6. **Sign in to your account** ウィンドウで、テナント管理者アカウントを選択し、続いてテナントのパスワードを入力して **Sign in** を選択します。

7. **Device options** ページで、**Configure Hybrid Microsoft Entra ID join** を選択し、続いて **Next** を選択します。

8. **Device operating systems** ページで、**Windows 10 or later domain-joined devices** を選択し、続いて **Next** を選択します。

9. **SCP configuration** ページで、**Contoso.com** の横のチェック ボックスをオンにします。

10. **Authentication Service** ドロップダウンから **Microsoft Entra ID** を選択し、**Add** を選択します。

11. **Enterprise Admin Credentials** ウィンドウで、**User name** として **Contoso\Administrator** を、**Password** として **Pa55w.rd** を入力します。**OK** を選択し、**Next** を選択します。

12. **Ready to configure** ページで、構成を実行するために **Configure** を選択します。

13. 構成が完了したら、**Exit** を選択します。

14. **SEA-CL2** に切り替えます。

15. サインイン ページで **Power** ボタンを選択し、続いて **Restart** を選択します。

    **注:** **SEA-CL2** を再起動すると、Entra Connect Sync を再構成することで作成された SCP をより早く検出できるようになります。

16. **SEA-CL2** が再起動したら、**Contoso\Administrator** としてパスワード **Pa55w.rd** でサインインします。

#### タスク 3: 新しい OU を同期するように Entra Connect Sync を再構成する

1. **SEA-SVR1** の **Desktop** で、**Azure AD Connect** をダブルクリックします。

2. **Microsoft Entra Connect Sync** ウィンドウで、**Configure** を選択します。

3. **Additional tasks** ページで、**Customize synchronization options** を選択し、**Next** を選択します。

4. **Connect to Microsoft Entra ID** ページで、**Next** を選択します。

5. **Sign in to your account** ウィンドウで、テナント管理者アカウントを選択し、続いてテナントのパスワードを入力して **Sign in** を選択します。

6. **Connect your directories** ページで、**Next** を選択します。

7. **Domain and OU filtering** ページで、**Sync selected domains and OUs** が選択されていることを確認し、続いて **Contoso.com** を展開します。

8. **Entra ID clients** の横のチェック ボックスをオンにします。**他の変更は行わず**、続いて **Next** を選択します。

9. **Optional features** ページで、変更を行わずに **Next** を選択します。

10. **Ready to configure** ウィンドウで、構成を実行して同期を開始するために **Configure** を選択します。

11. 構成が完了したら、**Exit** を選択します。

    **注:** 同期される OU を変更すると、Entra Connect Sync は自動的に同期を行います。**Synchronization Service** を使用して同期の状態を監視できます。

#### タスク 4: Entra ハイブリッド参加を検証する

1. **SEA-CL2** に切り替えます。

2. **Start** を右クリックし、**Shut down or sign out** を選択して、続いて **Restart** を選択します。

   _注: この再起動により、SEA-CL2 で Entra ハイブリッド参加がトリガーされます。_

3. **SEA-CL2** が再起動したら、**Contoso\Administrator** としてパスワード **Pa55w.rd** でサインインします。

4. タスク バーで **Start** を右クリックし、**Windows Terminal (Admin)** を選択します。

5. **Windows PowerShell** ウィンドウで、次のコマンドを入力し、続いて **Enter** キーを押します。

   ```
   dsregcmd /status
   ```

6. **Device State** の下の出力で、**AzureAdJoined : YES** と **DomainJoined : YES** が表示されていることを確認します。

   **注:** デバイスがまだ Entra ID に参加していない場合は、**SEA-SRV1** に戻って以下のコマンドを実行します。完了したら SEA-CL2 に戻り、コンピューターをもう一度再起動します。

   ```powershell
   Start-ADSyncSyncCycle -PolicyType Delta
   ```

7. SEA-CL2 上のすべてのウィンドウを閉じ、サインアウトします。

8. **SEA-SVR1** に切り替え、Microsoft Entra 管理センターに切り替えます。

9. **デバイス** > **すべてのデバイス** を選択します。

10. **SEA-CL2** の **参加の種類** 行の値が **Microsoft Entra ハイブリッド参加済み** になっていることを確認します。SEA-CL2 が一覧に表示されない場合は、必要に応じて **更新** ボタンを選択します。

11. **SEA-SVR1** 上のすべてのウィンドウを閉じます。

**結果**: この演習を完了すると、Entra ハイブリッド参加を正常に構成して検証できたことになります。

**ラボ終了**
