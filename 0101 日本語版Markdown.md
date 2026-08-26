---
lab:
  title: '演習ラボ 0101: Entra ID での ID の管理'
  description: このラボでは、Entra 管理センターを使用してユーザーの作成と変更、管理ロールの割り当て、グループの作成と変更、および Entra ID のライセンス割り当てを管理します。
  duration: 60 minutes
  level: 200
  islab: true
---

# 演習ラボ 0101: Entra ID での ID の管理

## WWL テナント - 利用規約

講師主導型トレーニングの一環としてテナントが提供される場合、そのテナントは講師主導型トレーニングのハンズオン ラボを支援する目的で提供されます。

テナントを共有したり、ハンズオン ラボ以外の目的で使用したりしないでください。このコースで使用するテナントは試用版であり、クラス終了後は使用またはアクセスできず、利用期間を延長することもできません。

テナントを有料サブスクリプションへ変換しないでください。このコースの一環として取得したテナントは Microsoft Corporation の所有物であり、Microsoft はいつでもアクセスして回収する権利を保有します。

## 概要

このラボでは、Entra 管理センターを使用してユーザーの作成と変更、管理ロールの割り当て、グループの作成と変更、および Entra ID のライセンス割り当てを管理します。

## 演習 1: Entra ID でのユーザーの作成

### シナリオ

来週入社する新しい従業員のユーザー アカウントを Azure AD に作成します。新しいユーザーは次の表のとおりです。

| Name           | User Name                             | Password   | Job title        | Department |
| -------------- | ------------------------------------- | ---------- | ---------------- | ---------- |
| Edmund Reeve   | `ereeve@yourtenant.onmicrosoft.com`   | Pa55-w.rd! | HR Rep           | HR         |
| Miranda Snider | `msnider@yourtenant.onmicrosoft.com`  | Pa55-w.rd! | Helpdesk Manager | Operations |
| Cody Godinez   | `cgodinez@yourtenant.onmicrosoft.com` | Pa55-w.rd! | Sales Rep        | Sales      |

_注: For location use either your local region or United States._

今後数か月の間に、さらに複数の従業員を採用する予定です。多数の新規ユーザーを追加するにはスクリプトの方が効率的であるため、PowerShell スクリプトを作成し、Cody Godinez のアカウントを作成するときにテストします。

### タスク 1: Microsoft Entra 管理センターを使用してユーザーを作成する

1. 手元の PC で Microsoft Edge を起動し、アドレス バーに **https://entra.microsoft.com** と入力して **Enter** キーを押します。

5. サインイン プロンプトで **admin@yourtenant.onmicrosoft.com** と入力し、**Next** を選択します。

6. **Enter password** ページで管理者アカウントのパスワードを入力し、**Sign in** を選択します。

   > 注: 管理者アカウントでのサインインに使用するパスワードは、講師に確認してください。

7. Edge のパスワード保存プロンプトで、**Save & Turn on** を選択します。

8. Stay signed in プロンプトで、**Yes** を選択します。

9. **Let's keep your account secure** ダイアログで、**Next** を選択します。

10. **Install Microsoft Authenticator** ダイアログで、**Next** を選択します。

11. **set up your account in app** ページで、**Next** を選択します。

12. モバイル デバイスの Authenticator アプリで QR コードをスキャンし、**Next** を選択します。

13. **Let's try it out** ダイアログに表示されたコードを確認し、Authenticator アプリへ入力します。

14. **Authenticator Added** ダイアログで、**Done** を選択します。 。

15. Microsoft Entra 管理センターのナビゲーション ペインで、**ユーザー** を選択します。

    > Microsoft Entra ID のメンバーとして既に存在するユーザーを確認します。現在のすべてのユーザーについて、**オンプレミスの同期が有効**列に **いいえ** と表示されています。これは、各ユーザーがオンプレミスのディレクトリ サービスから同期されたのではなく、Microsoft Entra ID で直接作成されたことを示します。

16. **ユーザー | すべてのユーザー** ページで、**新しいユーザー**、**新しいユーザーの作成** の順に選択します。

17. **新しいユーザーの作成** ページで、次の値を入力します。

    - User Principal Name: **ereeve**
    - Display Name: **Edmund Reeve**

18. Uncheck **Auto-generated password** を選択します。

19. **Password** の横に **Pa55-w.rd!** を選択します。

    > 注: このパスワードが弱い、または一般的に使用されているというエラーが表示された場合は、このラボ プロファイルの **Resources** タブにある受講者用パスワードを入力します。または、任意の複雑なパスワードを入力します。

20. ページ下部の **Next: Properties** を選択します。

21. **First name** の横に **Edmund** と入力します。

22. **Last name** の横に **Reeve** と入力します。

23. **User type** の横で **Member** が選択されていることを確認します。

    > 注: **Member** は既定のユーザー タイプであり、組織内のほとんどのユーザーに使用されます。

24. **Job title** の横に **HR Rep** と入力します。

25. **Department** の横に **HR** と入力します。

26. **Usage location** の横で **United States** を選択します。

27. ページ下部の **Next: Assignments** を選択します。

28. **割り当て** ページで、割り当てが選択されていないことを確認します。

    > 既定ではユーザーにグループは割り当てられません。グループを割り当てるまで、ユーザーはどのグループのメンバーにもなりません。

29. ページ下部の **Next: Review + create** を選択します。
    > このページの情報が正しいことを確認します。

30. **作成** を選択します。

31. **ユーザー | すべてのユーザー** ページで、**新しいユーザー**、**新しいユーザーの作成** の順に選択します。

32. **新しいユーザーの作成** ページで、次の値を入力します。

    - User Principal Name: **msnider**
    - Display Name: **Miranda Snider**

33. Uncheck **Auto-generated password** を選択します。

34. **Password** の横に **Pa55-w.rd!** を選択します。

    > 注: このパスワードが弱い、または一般的に使用されているというエラーが表示された場合は、このラボ プロファイルの **Resources** タブにある受講者用パスワードを入力します。または、任意の複雑なパスワードを入力します。

35. ページ下部の **Next: Properties** を選択します。

36. **First name** の横に **Miranda** と入力します。

37. **Last name** の横に **Snider** と入力します。

38. **User type** の横で **Member** が選択されていることを確認します。

39. **Job title** の横に **Helpdesk Manager** と入力します。

40. **Department** の横に **Operations** と入力します。

41. **Usage location** の横で **United States** を選択します。

42. ページ下部の **Next: Assignments** を選択します。

43. **割り当て** ページで、割り当てが選択されていないことを確認します。

44. ページ下部の **Next: Review + create** を選択します。

45. **作成** を選択します。

### タスク 2: PowerShell を使用してユーザーを作成する

# SEA-SVR1 に PowerShell 7.5.4 をインストールする手順

1. **SEA-SVR1** の **Microsoft Edge** で新しいタブを開きます。  。

2. アドレス バーに **https://github.com/PowerShell/PowerShell/releases/download/v7.5.4/PowerShell-7.5.4-win-x64.msi** と入力します。  。

3. タスク バーで **File Explorer** を選択し、**Downloads** フォルダーへ移動します。  。

4. **PowerShell-7.5.4-win-x64.msi** をダブルクリックして、セットアップ ウィザードを起動します。  。

   - **Next** を選択します。  
   - **Destination Folder** は変更せず、**Next** を選択します。  
   - **Optional Actions** は変更せず、**Next** を選択します。  
   - *Use Microsoft Update to help keep your computer secure and up to date* のチェック ボックスをオフのままにし、**Next** を選択します。  
   - **Install** を選択します。  

5. **Installation completed successfully** ウィンドウで **Launch PowerShell** をオンにし、**Finish** を選択します。  。

   > **注:** インストーラーが PowerShell を起動せずに終了した場合は、**Windows Search** バーを選択して **pwsh** と入力し、**PowerShell 7** を右クリックして **Run as administrator** を選択します。  

6. **PowerShell 7** ウィンドウで次のコマンドを入力し、**Enter** キーを押します。NuGet またはリポジトリに関するメッセージが表示された場合は **Y** と入力します。

    ```powershell
    Install-Module Microsoft.Graph -Scope CurrentUser
    ```

7. **PowerShell 7** ウィンドウで次のコマンドを入力し、**Enter** キーを押します。

    ```powershell
    Connect-MgGraph -scopes "user.readwrite.all, group.readwrite.all"
    ```

8. **Let's get you signed in** ウィンドウが表示されたら、**Work or School account**、**Continue** の順に選択します。

9. **Sign in** ダイアログで管理者パスワードを使用して **`admin@yourtenant.onmicrosoft.com`** としてサインインし、**Sign in** を選択します。

10. **Permissions Requested** プロンプトで **Consent on behalf of your organization** をオンにし、**Accept** を選択します。

11. **Sign in to all apps, websites, and services on this device?** で、**No, this app only** を選択します。

12. **PowerShell 7** ウィンドウで次のコードを入力して新しいプロファイル オブジェクトを作成し、**Enter** キーを押します。**Pa55w.rd** は任意の複雑なパスワードへ置き換えます。

    ```powershell
    $PWProfile = @{
        Password = "Pa55w.rd";
        ForceChangePasswordNextSignIn = $false
    }
    ```
    
14. 次に、以下のコードを入力して新しいユーザーを作成し、**Enter** キーを押します。"yourtenant" が割り当てられたテナント名と一致することを確認します。

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

15. ユーザー **Cody Godinez** が作成されたことを確認するため、**PowerShell 7** ウィンドウで次のコマンドを入力し、**Enter** キーを押します。

    ```powershell
    Get-MgUser
    ```

> テナント内のユーザー一覧が表示されることを確認します。 

**結果**: この演習を完了すると、Entra ID に新しいユーザー アカウントが正常に作成されます。

## 演習 2: Entra ID での管理ロールの割り当て

### シナリオ

テナントの現在の管理ロールを確認し、変更します。

次の表に示す管理ロールをユーザーへ割り当てます。  

| Name           | Must be able to:                         | Administrative Role needed: |
| -------------- | ---------------------------------------- | --------------------------- |
| Allan Deyoung  | Manage the tenant                        | Global administrator        |
| Edmund Reeve   | Manage users, group, and password resets | User administrator          |
| Miranda Snider | Manage password resets                   | Helpdesk administrator      |

### タスク 1: 管理ロールを確認して割り当てる

1. 手元の PC の Microsoft Edge に切り替えます。

2. Microsoft Entra 管理センターのナビゲーション ペインで、 **Roles & admins** を選択します。

    > 一覧をスクロールするか、検索ボックスを使用して目的の **ロール** を検索できます。

3. 検索ボックスを使用して検索します: **Global administrator** を選択します。

4. **グローバル管理者**を選択します。チェック ボックスではなく名前を選択します。

5. **Global administrator** で **+ Add assignments** を選択します。

6. Under **Select members**, **No member selected**, then search for and **Allan Deyoung** を選択します。

7. **選択**、**次へ**、**割り当て** の順に選択します。

8. navigation breadcrumbs で、 **Roles & administrators | All roles** を選択します。

9. 検索ボックスを使用して検索します: **User administrator** を選択します。

10. **ユーザー管理者**を選択します。チェック ボックスではなく名前を選択します。

11. **User administrator** で **+ Add assignments** を選択します。

12. Under **Select members**, **No member selected**, then search for and **Edmund Reeve** を選択します。

13. **選択**、**次へ**、**割り当て** の順に選択します。

14. navigation breadcrumbs で、 **Roles & administrators | All roles** を選択します。

15. 検索ボックスを使用して検索します: **Helpdesk administrator** を選択します。

16. **ヘルプデスク管理者**を選択します。チェック ボックスではなく名前を選択します。

17. **Helpdesk administrator** で **+ Add assignments** を選択します。

18. Under **Select members**, **No member selected**, then search for and **Miranda Snider** を選択します。

19. **選択**、**次へ**、**割り当て** の順に選択します。

20. ナビゲーション ペインで **Home** を選択します。

**結果**: この演習を完了すると、管理ロールがユーザーへ正常に割り当てられます。

## 演習 3: グループの作成と管理、およびライセンス割り当ての検証

### シナリオ

3人の新しいユーザーをセキュリティ グループに追加し、次の表に従ってライセンスを割り当てます。  

| Name           | Member of:       | License to assign                                            |
| -------------- | ---------------- | ------------------------------------------------------------ |
| Edmund Reeve   | Contoso_Managers | Office 365 E5, Enterprise Mobility + Security E5 via group membership |
| Miranda Snider | Contoso_Managers | Office 365 E5, Enterprise Mobility + Security E5 via group membership |
| Cody Godinez   | Contoso_Sales    | Office 365 E5, Enterprise Mobility + Security E5 via group membership direct assignment |

さらに、サインイン ページの会社ブランドを変更します。

### タスク 1: Microsoft Entra 管理センターを使用してグループを作成する

1. 手元の PC の Microsoft Entra 管理センターのナビゲーション ペインで、**グループ** を選択します。

2. **新しいグループ** を選択します。

3. **新しいグループ** ページで、次の値を入力します。

    - Group type: **Security**
    - Group name: **Contoso_Managers**
    - Membership type: **Assigned**

4. Under Members, **No members selected** を選択します。

5. Add members ページで **Edmund Reeve** と **Miranda Snider** を追加し、**Select** を選択します。

6. **作成** を選択します。

### タスク 2: PowerShell を使用してグループを作成する

1. On SEA-SVR1, switch to PowerShell 7。

2. **PowerShell 7** ウィンドウで次のコードを入力して新しいグループを作成し、**Enter** キーを押します。

    ```powershell
    New-MgGroup -DisplayName "Contoso_Sales" -Description "Contoso Sales team users" -MailEnabled:$false -Mailnickname "Contoso_Sales" -SecurityEnabled
    ```

3. **PowerShell 7** ウィンドウで次のコマンドを入力し、**Enter** キーを押します。

    ```powershell
    Get-MgGroup
    ```

4. 作成した Contoso_Sales グループを含む、テナント内のグループ一覧が表示されることを確認します。

5. **PowerShell 7** ウィンドウで次のコードを入力して Contoso_Sales グループを変数として定義し、**Enter** キーを押します。

    ```powershell
    $group = Get-MgGroup | Where-Object {$_.DisplayName -eq "Contoso_Sales"}
    ```

6. **PowerShell 7** ウィンドウで次のコードを入力してユーザーを別の変数として定義し、**Enter** キーを押します。

    ```powershell
    $user = Get-MgUser | Where-Object {$_.DisplayName -eq "Cody Godinez"}
    ```

7. **PowerShell 7** ウィンドウで次のコードを入力し、設定した変数を使用して Cody を Contoso_Sales へ追加して、**Enter** キーを押します。

    ```powershell
    New-MgGroupMember -GroupId $group.Id -DirectoryObjectId $user.Id
    ```

8. **PowerShell 7** ウィンドウで次のコードを入力し、**Enter** キーを押します。

    ```powershell
    Get-MgGroupMember -GroupId $group.Id | FL
    ```

9. **AdditionalProperties** の値として **Cody Godinez** が表示されることを確認します。

10. PowerShell 7 を閉じます。

### タスク 3: ライセンスを確認して会社のブランドを変更する

1. Microsoft Entra 管理センターのナビゲーション ペインで、 **Billing** > **Licenses** を選択します。

2. **Licenses** ページの中央のナビゲーション ペインにある **Manage** で、**All products** を選択します。

   > **Enterprise Mobility + Security E5** と **Office 365 E5** の使用可能なライセンス数と割り当て済みライセンス数を確認します。

3. Microsoft Entra 管理センターのナビゲーション ペインで、under **Entra ID**, **Custom branding** を選択します。

4. **Company Branding** で、 under **Default sign-in experience**, **Customize** を選択します。

5. **Customize default sign-in experience** ページで **Sign-in form** タブへ移動し、次の設定を構成します。

   - Sign-in page text: **Contoso Corp. Sign-in Page**

6. **Review + Create** を選択して設定を確認し、**Create** を選択します。

7. Microsoft Entra 管理センターのナビゲーション ペインで、 **Users** を選択します。

8. ユーザー一覧で **Cody Godinez** を選択します。チェック ボックスではなく名前を選択します。

9. Cody Godinez の Profile ページで、中央のナビゲーション メニューから **Licenses** を選択します。

   > 次の点を確認します: Cody does not have any current license assignments. And that licensing must now be performed in the 365 Admin center.

10. Open a new tab in **Microsoft Edge**, アドレス バーに, **https://admin.microsoft.com** を選択します。

11. 左側のナビゲーション ペインで、**Users** > **Active users** の順に選択します。

12. ユーザー一覧で **Cody Godinez** を選択します。チェック ボックスではなく名前を選択します。

13. **Licenses and apps** タブを選択します。

14. **Enterprise Mobility + Security E5** と **Office 365 E5 (no Teams)** の横にあるチェック ボックスをオンにします。

15. **Save changes** を選択します。

16. 変更が保存されたら、右上隅の **X** を選択して **Cody Godinez** ペインを閉じます。

17. Microsoft 365 admin center で、 in the Navigation pane, **Billing** > **Licenses** を選択します。

18. **Subscriptions** の一覧で、**Enterprise Mobility + Security E5** を選択します。

19. **Groups** タブを選択し、**Assign licenses** を選択します。

20. Navigate into the **Enter a group name** textbox, and 次を選択します: **Contoso_Managers** group。

21. **Assign Licenses** を選択します。

22. **You assigned licenses to Contoso_Managers** で、 次を選択します: **X** in the upper-right corner to close it。

23. upper-left corner of the **Enterprise Mobility + Security E5** page で、 次を選択します: **Back to licenses** link。

24. **Subscriptions** の一覧で、**Office 365 E5 (no Teams)** を選択します。

25. **Groups** タブを選択し、**Assign licenses** を選択します。

26. Navigate into the **Enter a group name** textbox, and 次を選択します: **Contoso_Managers** group。

27. **Assign Licenses** を選択します。

28. **You assigned licenses to Contoso_Managers** で、 次を選択します: **X** in the upper-right corner to close it。

29. Microsoft 365 admin center で、 in the Navigation pane, **Billing** > **Licenses** を選択します。

30. **Subscriptions** の一覧で、**Office 365 E5 (no Teams)** を選択します。

   > Office 365 E5 ライセンスが割り当てられたユーザーを確認します。Edmund と Miranda は、Contoso_Managers グループのメンバーシップを通じてライセンスを受け取ります。**Groups** タブで割り当てを確認できます。ライセンスの再処理には3分から5分かかる場合があります。

31. Microsoft Edge を閉じます。

**結果**: この演習を完了すると、グループの作成と管理、会社ブランドの変更、ライセンスの割り当てが正常に完了します。

**ラボ終了**
