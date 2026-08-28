---
lab:
    title: '演習ラボ 0101: Entra ID での ID の管理'
    description: このラボでは、Entra 管理センターを使用して、Entra ID でユーザーの作成と変更、管理者ロールの割り当て、グループの作成と変更、およびライセンス割り当ての管理を行います。
    duration: 60 minutes
    level: 200
    islab: true
---

## 演習ラボ 0101: Entra ID での ID の管理

### WWL テナント - 利用規約

インストラクター主導のトレーニングの一環としてテナントが提供される場合、そのテナントはインストラクター主導トレーニングのハンズオン ラボを支援する目的で提供されるものであることにご注意ください。

テナントを共有したり、ハンズオン ラボ以外の目的で使用したりしないでください。このコースで使用するテナントは試用版テナントであり、クラス終了後は使用およびアクセスできず、延長の対象にもなりません。

テナントを有料サブスクリプションへ変換することはできません。このコースの一環として取得したテナントは Microsoft Corporation の資産であり、当社はいつでもアクセスを取得し、回収する権利を留保します。

### 概要

このラボでは、Entra 管理センターを使用して、Entra ID でユーザーの作成と変更、管理者ロールの割り当て、グループの作成と変更、およびライセンス割り当ての管理を行います。

### 演習 1: Entra ID でのユーザーの作成

#### シナリオ

来週入社する新入社員のために、Azure AD でユーザー アカウントを作成する必要があります。新しいユーザーは次の表に記載されています。

<table>
<tr>
<th>名前</th>
<th>ユーザー名</th>
<th>パスワード</th>
<th>役職</th>
<th>部署</th>
</tr>
<tr>
<td>Edmund Reeve</td>
<td>ereeve@yourtenant.onmicrosoft.com</td>
<td>Pa55-w.rd!</td>
<td>HR Rep</td>
<td>HR</td>
</tr>
<tr>
<td>Miranda Snider</td>
<td>msnider@yourtenant.onmicrosoft.com</td>
<td>Pa55-w.rd!</td>
<td>Helpdesk Manager</td>
<td>Operations</td>
</tr>
<tr>
<td>Cody Godinez</td>
<td>cgodinez@yourtenant.onmicrosoft.com</td>
<td>Pa55-w.rd!</td>
<td>Sales Rep</td>
<td>Sales</td>
</tr>
</table>

_注: 場所には、お住まいの地域または米国のいずれかを使用してください。_

さらに、今後数か月でさらに数名の従業員が採用されることも伝えられています。多数の新しいユーザーを追加するには、スクリプトを使用する方がはるかに効率的な方法だと判断しました。そこで PowerShell スクリプトを作成し、Cody Godinez のアカウントを作成する際にそれを試してみることにしました。

#### タスク 1: Microsoft Entra 管理センターを使用したユーザーの作成

1. **SEA-SVR1** に、**Contoso\Administrator** としてパスワード **Pa55w.rd** でサインインします。

2. **Server Manager** を閉じます。

3. タスク バーで、**Microsoft Edge** を選択します。

4. アドレス バーに [**https://entra.microsoft.com**](https://entra.microsoft.com) を入力します。

5. サインインの画面で、**admin@yourtenant.onmicrosoft.com** を入力し、**次へ** を選択します。

6. パスワードの入力ページで、Admin アカウントのパスワードを入力し、**サインイン** を選択します。

   > **注**: Admin アカウントでサインインする際に使用するパスワードについては、インストラクターに確認してください。

7. Microsoft Edge のパスワード保存の確認画面で、**保存してオンにする** を選択します。

8. サインインの状態を維持しますか？の画面で、**はい** を選択します。

9. **アカウントのセキュリティ保護** ダイアログで、**次へ** を選択します。

10. **Microsoft Authenticator のインストール** ダイアログで、**次へ** を選択します。

11. アプリでアカウントを設定するページで、**次へ** を選択します。

12. モバイル デバイスの Authenticator アプリを使用して QR コードをスキャンし、**次へ** を選択します。

13. 試してみましょうダイアログで、コードを控え、それを Authenticator アプリに入力します。

14. **Authenticator が追加されました** ダイアログで、**完了** を選択します。

15. Microsoft Entra 管理センターのナビゲーション ペインで、**ユーザー** を選択します。

    > **注**: Microsoft Entra ID のメンバーとして既に存在するユーザーを確認します。**オンプレミスの同期が有効** 列は、現在のすべてのユーザーで **いいえ** と表示されます。これは、各ユーザーがオンプレミスのディレクトリ サービスから同期されたのではなく、Microsoft Entra ID で直接作成されたことを示しています。

16. **ユーザー | すべてのユーザー** ページで、**新しいユーザー** を選択し、続いて **新しいユーザーの作成** を選択します。

17. **新しいユーザーの作成** ページで、次の情報を入力します。

    - ユーザー プリンシパル名: **ereeve**
    - 表示名: **Edmund Reeve**
    - **パスワードの自動生成** のチェックを外します
    - **パスワード** の横に、**Pa55-w.rd!** を入力します。

      > **注**: パスワードが脆弱である、または一般的に使用されているというエラー メッセージが表示された場合は、このラボ プロファイルの **Resources** タブにある受講者用パスワードを入力してください。または、任意の複雑なパスワードを入力することもできます。

18. ページ下部にある **次へ: プロパティ** を選択します。

19. **名** の横に、**Edmund** を入力します。

20. **姓** の横に、**Reeve** を入力します。

21. **ユーザーの種類** の横で、**メンバー** が選択されていることを確認します。

    > **注**: **メンバー** のユーザーの種類は既定のユーザーの種類です。このユーザーの種類は、組織内のほとんどのユーザーに使用されます。

22. **役職** の横に、**HR Rep** を入力します。

23. **部署** の横に、**HR** を入力します。

24. **利用場所** の横で、**United States** を選択します。

25. ページ下部にある **次へ: 割り当て** を選択します。

26. **割り当て** ページで、割り当てが選択されていないことを確認します。

    > 既定では、ユーザーにグループは割り当てられていません。これは、割り当てを行うまで、ユーザーがどのグループのメンバーでもないためです。

27. ページ下部にある **次へ: 確認と作成** を選択します。

    > このページの情報を確認し、正しいことを確かめます。

28. **作成** を選択します。

29. **ユーザー | すべてのユーザー** ページで、**新しいユーザー** を選択し、続いて **新しいユーザーの作成** を選択します。

30. **新しいユーザーの作成** ページで、次の情報を入力します。

    - ユーザー プリンシパル名: **msnider**
    - 表示名: **Miranda Snider**
    - **パスワードの自動生成** のチェックを外します
    - **パスワード** の横に、**Pa55-w.rd!** を入力します。

      > **注**: パスワードが脆弱である、または一般的に使用されているというエラー メッセージが表示された場合は、このラボ プロファイルの **Resources** タブにある受講者用パスワードを入力してください。または、任意の複雑なパスワードを入力することもできます。

31. ページ下部にある **次へ: プロパティ** を選択します。

32. **名** の横に、**Miranda** を入力します。

33. **姓** の横に、**Snider** を入力します。

34. **ユーザーの種類** の横で、**メンバー** が選択されていることを確認します。

35. **役職** の横に、**Helpdesk Manager** を入力します。

36. **部署** の横に、**Operations** を入力します。

37. **利用場所** の横で、**United States** を選択します。

38. ページ下部にある **次へ: 割り当て** を選択します。

39. **割り当て** ページで、割り当てが選択されていないことを確認します。

40. ページ下部にある **次へ: 確認と作成** を選択します。

41. **作成** を選択します。

#### タスク 2: PowerShell を使用したユーザーの作成

## SEA-SVR1 に PowerShell 7.5.4 をインストールする手順

1. **SEA-SVR1** の **Microsoft Edge** で、新しいタブを開きます。

2. アドレス バーに [**https://github.com/PowerShell/PowerShell/releases/download/v7.5.4/PowerShell-7.5.4-win-x64.msi**](https://github.com/PowerShell/PowerShell/releases/download/v7.5.4/PowerShell-7.5.4-win-x64.msi) を入力します。

3. タスク バーで **File Explorer** を選択し、**Downloads** フォルダーに移動します。

4. **PowerShell-7.5.4-win-x64.msi** をダブルクリックして、セットアップ ウィザードを起動します。

5. **Next** を選択します。

6. **Destination Folder** は変更せず、**Next** を選択します。

7. **Optional Actions** は変更せず、**Next** を選択します。

8. _Use Microsoft Update to help keep your computer secure and up to date_ の下のチェック ボックスは空白のままにして、**Next** を選択します。

9. **Install** を選択します。

10. **Installation completed successfully** ウィンドウで、**Launch PowerShell** をオンにし、**Finish** を選択します。

    > **注**: インストーラーが PowerShell を起動せずに閉じた場合は、**Windows Search** バーをクリックして **pwsh** と入力し、**PowerShell 7** を右クリックして **Run as administrator** を選択します。

11. **PowerShell 7** ウィンドウで、次のコマンドを入力し、**Enter** キーを押します。NuGet とリポジトリのメッセージが表示された場合は、**Y** を入力します。

    ```powershell
    Install-Module Microsoft.Graph -Scope CurrentUser
    ```

12. **PowerShell 7** ウィンドウで、次のコマンドを入力し、**Enter** キーを押します。

    ```powershell
    Connect-MgGraph -scopes "user.readwrite.all, group.readwrite.all"
    ```

13. **Let's get you signed in** ウィンドウで確認が表示されたら、**Work or School account** を選択し、続いて **Continue** を選択します。

14. **Sign in** ダイアログ ボックスで、**admin@yourtenant.onmicrosoft.com** として管理者パスワードでサインインし、**Sign in** を選択します。

15. 表示される **Permissions Requested** の確認画面で、**Consent on behalf of your organization** をオンにし、**Accept** を選択します。

16. **Sign in to all apps, websites, and services on this device?** で、**No, this app only** を選択します。

17. **PowerShell 7** ウィンドウで、新しいプロファイル オブジェクトを作成するために次のコードを入力し、**Enter** キーを押します。**Pa55w.rd** は任意の複雑なパスワードに置き換えてください。

    ```powershell
    $PWProfile = @{
        Password = "Pa55w.rd";
        ForceChangePasswordNextSignIn = $false
    }
    ```

18. 次に、新しいユーザーを作成するために次のコードを入力し、**Enter** キーを押します。"yourtenant" が割り当てられたテナント名と一致していることを確認してください。

    ```powershell
    New-MgUser `
        -DisplayName "Cody Godinez" `
        -GivenName "Cody" -Surname "Godinez" `
        -MailNickname "cgodinez" `
        -UsageLocation "US" `
        -UserPrincipalName "cgodinez@yourtenant.onmicrosoft.com" `
        -PasswordProfile $PWProfile -AccountEnabled `
        -Department "Sales" -JobTitle "Sales Rep"
    ```

19. ユーザー **Cody Godinez** が作成されたことを確認するために、**PowerShell 7** ウィンドウで次のコマンドを入力し、**Enter** キーを押します。

    ```powershell
    Get-MgUser
    ```

    テナントのユーザーの一覧が表示されることを確認します。

**結果**: この演習を完了すると、Entra ID で新しいユーザー アカウントを正常に作成できています。

### 演習 2: Entra ID での管理者ロールの割り当て

#### シナリオ

テナントの現在の管理者ロールを確認し、変更する必要があります。

次の表に示すとおり、管理者ロールを割り当てる必要があるユーザーの一覧が提供されています。

<table>
<tr>
<th>名前</th>
<th>実行できる必要がある操作:</th>
<th>必要な管理者ロール:</th>
</tr>
<tr>
<td>Allan Deyoung</td>
<td>テナントの管理</td>
<td>グローバル管理者</td>
</tr>
<tr>
<td>Edmund Reeve</td>
<td>ユーザー、グループ、パスワード リセットの管理</td>
<td>ユーザー管理者</td>
</tr>
<tr>
<td>Miranda Snider</td>
<td>パスワード リセットの管理</td>
<td>ヘルプデスク管理者</td>
</tr>
</table>

#### タスク 1: 管理者ロールの確認と割り当て

1. **SEA-SVR1** で、**Microsoft Edge** に切り替えます。

2. Microsoft Entra 管理センターのナビゲーション ペインで、**ロールと管理者** を選択します。

   > **注**: 一覧をスクロールするか、検索ボックスを使用して、目的の **ロール** を見つけることができます。

3. 検索ボックスを使用して、**グローバル管理者** を検索します。

4. **グローバル管理者** を選択します (チェック ボックスではなく、名前を選択します)。

5. **グローバル管理者** ペインで、**+ 割り当ての追加** を選択します。

6. **メンバーの選択** の下で、**メンバーが選択されていません** を選択し、**Allan Deyoung** を検索して選択します。

7. **選択** を選択し、続いて **次へ** を選択し、最後に **割り当て** を選択します。

8. ナビゲーションのパンくずリストで、**ロールと管理者 | すべてのロール** を選択します。

9. 検索ボックスを使用して、**ユーザー管理者** を検索します。

10. **ユーザー管理者** を選択します (チェック ボックスではなく、名前を選択します)。

11. **ユーザー管理者** ペインで、**+ 割り当ての追加** を選択します。

12. **メンバーの選択** の下で、**メンバーが選択されていません** を選択し、**Edmund Reeve** を検索して選択します。

13. **選択** を選択し、続いて **次へ** を選択し、最後に **割り当て** を選択します。

14. ナビゲーションのパンくずリストで、**ロールと管理者 | すべてのロール** を選択します。

15. 検索ボックスを使用して、**ヘルプデスク管理者** を検索します。

16. **ヘルプデスク管理者** を選択します (チェック ボックスではなく、名前を選択します)。

17. **ヘルプデスク管理者** ペインで、**+ 割り当ての追加** を選択します。

18. **メンバーの選択** の下で、**メンバーが選択されていません** を選択し、**Miranda Snider** を検索して選択します。

19. **選択** を選択し、続いて **次へ** を選択し、最後に **割り当て** を選択します。

20. ナビゲーション ペインで、**ホーム** を選択します。

**結果**: この演習を完了すると、ユーザーに管理者ロールを正常に割り当てられています。

### 演習 3: グループの作成と管理、およびライセンス割り当ての検証

#### シナリオ

3 人の新しいユーザーをセキュリティ グループに追加し、次の表に示すとおりライセンスを割り当てる必要があります。

<table>
<tr>
<th>名前</th>
<th>所属:</th>
<th>割り当てるライセンス</th>
</tr>
<tr>
<td>Edmund Reeve</td>
<td>Contoso_Managers</td>
<td>Office 365 E5、Enterprise Mobility + Security E5 (グループ メンバーシップ経由)</td>
</tr>
<tr>
<td>Miranda Snider</td>
<td>Contoso_Managers</td>
<td>Office 365 E5、Enterprise Mobility + Security E5 (グループ メンバーシップ経由)</td>
</tr>
<tr>
<td>Cody Godinez</td>
<td>Contoso_Sales</td>
<td>Office 365 E5、Enterprise Mobility + Security E5 (グループ メンバーシップ経由の直接割り当て)</td>
</tr>
</table>

また、サインイン ページの会社のブランドを変更するよう依頼されています。

#### タスク 1: Microsoft Entra 管理センターを使用したグループの作成

1. **SEA-SVR1** の Microsoft Entra 管理センターで、ナビゲーション ペインで **グループ** を選択します。

2. **新しいグループ** を選択します。

3. **新しいグループ** ページで、次の情報を入力します。

   - グループの種類: **セキュリティ**
   - グループ名: **Contoso_Managers**
   - メンバーシップの種類: **割り当て済み**

4. **メンバー** の下で、**メンバーが選択されていません** を選択します。

5. **メンバーの追加** ページで、**Edmund Reeve** と **Miranda Snider** を追加し、**選択** をクリックします。

6. **作成** を選択します。

#### タスク 2: PowerShell を使用したグループの作成

1. **SEA-SVR1** で、**PowerShell 7** に切り替えます。

2. **PowerShell 7** ウィンドウで、新しいグループを作成するために次のコードを入力し、**Enter** キーを押します。

   ```powershell
   New-MgGroup -DisplayName "Contoso_Sales" -Description "Contoso Sales team users" -MailEnabled:$false -Mailnickname "Contoso_Sales" -SecurityEnabled
   ```

3. **PowerShell 7** ウィンドウで、次のコマンドを入力し、**Enter** キーを押します。

   ```powershell
   Get-MgGroup
   ```

4. テナント内のグループの一覧に、今作成した **Contoso_Sales** グループが含まれていることを確認します。

5. **PowerShell 7** ウィンドウで、**Contoso_Sales** グループを変数として定義するために次のコードを入力し、**Enter** キーを押します。

   ```powershell
   $group = Get-MgGroup | Where-Object {$_.DisplayName -eq "Contoso_Sales"}
   ```

6. **PowerShell 7** ウィンドウで、ユーザーを別の変数として定義するために次のコードを入力し、**Enter** キーを押します。

   ```powershell
   $user = Get-MgUser | Where-Object {$_.DisplayName -eq "Cody Godinez"}
   ```

7. **PowerShell 7** ウィンドウで、設定した変数を使用して Cody を **Contoso_Sales** に追加するために次のコードを入力し、**Enter** キーを押します。

   ```powershell
   New-MgGroupMember -GroupId $group.Id -DirectoryObjectId $user.Id
   ```

8. **PowerShell 7** ウィンドウで、次のコードを入力し、**Enter** キーを押します。

   ```powershell
   Get-MgGroupMember -GroupId $group.Id | FL
   ```

9. **AdditionalProperties** の値として **Cody Godinez** が表示されることを確認します。

10. **PowerShell 7** を閉じます。

#### タスク 3: ライセンスの確認と会社のブランドの変更

1. Microsoft Entra 管理センターのナビゲーション ペインで、**課金** > **ライセンス** を選択します。

2. **ライセンス** ページの中央のナビゲーション ペインで、**管理** の下の **すべての製品** を選択します。

   > **Enterprise Mobility + Security E5** と **Office 365 E5** について、現在利用可能なライセンスと割り当て済みのライセンスを確認します。

3. Microsoft Entra 管理センターのナビゲーション ペインで、**Entra ID** の下の **会社のブランド** を選択します。

4. **会社のブランド** ページで、**既定のサインイン エクスペリエンス** の下の **カスタマイズ** を選択します。

5. **既定のサインイン エクスペリエンスのカスタマイズ** ページで、**サインイン フォーム** タブに移動し、次の設定を構成します。

   - サインイン ページのテキスト: **Contoso Corp. Sign-in Page**

6. **確認と作成** を選択し、設定を確認して **作成** を選択します。

7. Microsoft Entra 管理センターのナビゲーション ペインで、**ユーザー** を選択します。

8. ユーザーの一覧で、**Cody Godinez** を選択します (チェック ボックスではなく、名前を選択します)。

9. **Cody Godinez** の **プロファイル** ページで、中央のナビゲーション メニューの **ライセンス** を選択します。

   > Cody に現在割り当てられているライセンスがないことに注意してください。また、ライセンスの割り当ては、365 管理センターで行う必要があります。

10. **Microsoft Edge** で新しいタブを開き、アドレス バーに [**https://admin.microsoft.com**](https://admin.microsoft.com) を入力します。

11. 左側のナビゲーション ペインで、**ユーザー** > **アクティブなユーザー** を選択します。

12. ユーザーの一覧で、**Cody Godinez** を選択します (チェック ボックスではなく、名前を選択します)。

13. **ライセンスとアプリ** タブを選択します。

14. **Enterprise Mobility + Security E5** と **Office 365 E5 (no Teams)** の横のチェック ボックスをオンにします。

15. **変更の保存** を選択します。

16. 変更が保存されたら、右上隅の **X** を選択して **Cody Godinez** ペインを閉じます。

17. Microsoft 365 管理センターのナビゲーション ペインで、**課金** > **ライセンス** を選択します。

18. **サブスクリプション** の一覧で、**Enterprise Mobility + Security E5** を選択します。

19. **グループ** タブを選択し、続いて **+ ライセンスの割り当て** を選択します。

20. **グループ名を入力** テキスト ボックスに移動し、**Contoso_Managers** グループを選択します。

21. **ライセンスの割り当て** を選択します。

22. **Contoso_Managers にライセンスを割り当てました** ペインで、右上隅の **X** を選択して閉じます。

23. **Enterprise Mobility + Security E5** ページの左上隅で、**ライセンスに戻る** リンクを選択します。

24. **サブスクリプション** の一覧で、**Office 365 E5 (no Teams)** を選択します。

25. **グループ** タブを選択し、続いて **+ ライセンスの割り当て** を選択します。

26. **グループ名を入力** テキスト ボックスに移動し、**Contoso_Managers** グループを選択します。

27. **ライセンスの割り当て** を選択します。

28. **Contoso_Managers にライセンスを割り当てました** ペインで、右上隅の **X** を選択して閉じます。

29. Microsoft 365 管理センターのナビゲーション ペインで、**課金** > **ライセンス** を選択します。

30. **サブスクリプション** の一覧で、**Office 365 E5 (no Teams)** を選択します。

    > **Office 365 E5** ライセンスが割り当てられているユーザーを確認します。Edmund と Miranda はどちらも、**Contoso_Managers** グループのメンバーシップからライセンスの割り当てを受けています。**グループ** タブを選択すると、ライセンスが正しく割り当てられているかどうかを確認できます。ライセンスが再処理されるまでに 3～5 分かかる場合があります。

31. **Microsoft Edge** を閉じます。

**結果**: この演習を完了すると、グループの作成と管理、会社のブランドの変更、およびライセンスの割り当てが正常に行えています。

**ラボ終了**
