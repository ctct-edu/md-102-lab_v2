---
lab:
 title: '演習ラボ 0101: Entra ID での ID 管理'
 description: このラボでは、 use Entra admin c入力します に create および modifyユーザー, assign administrative roles, create および modifyグループ, および manageライセンス割り当てs で Entra ID.
 duration: 60 minutes
 level: 200
 islab: true
---

# 演習ラボ 0101: Entra ID での ID 管理

## WWL Tenants - Terms of Use

次の操作を実行します。If you は being provided を使用して tenant として part の instructor-led training delivery, please note that tenant は made利用可能な のために purpose の supporting hおよびs-on labs で instructor-led training.

次の操作を実行します。Tenants should not be shared または used のために purposes outside の hおよびs-on labs. tenant used で this course は trial tenant および cannot be used または accessed after class は over および は not eligible のために extension.

次の操作を実行します。Tenants must not be converted に paid subscription. Tenants obtained として part の this course remain property の Microsoft Corporation および we reserve right に obtain access および repossess at any time.

## 概要

このラボでは、 use Entra admin c入力します に create および modifyユーザー, assign administrative roles, create および modifyグループ, および manageライセンス割り当てs で Entra ID.

## 演習 1: Entra ID でのユーザー作成

### シナリオ

次の作業を行う必要があります。 create userアカウントs で Azure AD のために new employees that します start next week. Newユーザー は 一覧ed で following タブle:

| 名前 | ユーザー名 | Password | 役職 | 部署 |
| -------------- | ------------------------------------- | ---------- | ---------------- | ---------- |
| Edmund Reeve | `ereeve@yourtenant.onmicrosoft.com` | Pa55-w.rd! | HR Rep | HR |
| Mirおよびa Snider | `msnider@yourtenant.onmicrosoft.com` | Pa55-w.rd! | Helpdesk Manager | Operations |
| Cody Godinez | `cgodinez@yourtenant.onmicrosoft.com` | Pa55-w.rd! | Sales Rep | Sales |

_注: For location use either yourローカル region または United States._

次の操作を実行します。You've also been told that several more employees します be hired over next couple の months. You've decided that scripting would be far more efficient method の adding large number の newユーザー. You've decided に create PowerShell script および test it out when you create Cody Godinez'sアカウント.

### タスク 1: Microsoft Entra 管理センターを使用してユーザーを作成する

1. On **SEA-SVR1**, 次のアカウントでサインインします。 **Contoso\\Administrator** パスワード **Pa55w.rd**.

2. 閉じます **Server Manager**.

3. タスク バーで **Microsoft Edge**.

4. アドレス バーに **https://entra.microsoft.com**.

5. At Sign-in prompt, 入力します **admin@yourtenant.onmicrosoft.com** 続いて 選択します **次へ**.

6. At 入力しますパスワード ページ, 入力します theパスワード のために Adminアカウント 続いて 選択します **Sign in**.

 > 注: Check を使用して受講者のinstructor パスワード に use のために signing で を使用して Adminアカウント.

7. At Edge Saveパスワード prompt, 選択します **Save & Turn on**.

8. At Stay signed で prompt, 選択します **はい**.

9. **Let's keep yourアカウント secure** dialog, 選択します **次へ**.

10. **Install Microsoft Au続いてticator** dialog, 選択します **次へ**.

11. **set up yourアカウント で app** ページ, 選択します **次へ**.

12. Using Au続いてticator app on受講者のmobile device, scan QR code 続いて 選択します **次へ**.

13. **Let's try it out** dialog, take note の code, 入力します that で to受講者のAu続いてticator app.

14. **Au続いてticator Added** dialog, 選択します **Done**. 

15. Microsoft Entra 管理センターで, ナビゲーション ペインで, 選択します **ユーザー**.

 > 次の点を確認してください。 theユーザー that already exist として members の Microsoft Entra ID. **オンプレミスの同期が有効** 列 states **いいえ** のために all現在のユーザー. これは、 each user was created directly で Microsoft Entra ID および not synchronized から on-premises directory service.

16. **ユーザー | すべてのユーザー** ページ, 選択します **新しいユーザー** 続いて 選択します **新しいユーザーの作成**.

17. **新しいユーザーの作成** ページ, 入力します following:

 - User Principal 名前: **ereeve**
 - Display 名前: **Edmund Reeve**

18. Uncheck **パスワードの自動生成**

19. Next に **パスワード**, 入力します **Pa55-w.rd!**.

 > 注: If you receive error message stating that thisパスワード で weak または commonly used, 入力します studentパスワード found 配下で **Resources** タブ の this lab profile. Alternatively, you できます 入力します complexパスワード of受講者のchoice.

20. 選択します **次へ: プロパティ** located ページ下部で.

21. Next に **名**, 入力します **Edmund**.

22. Next に **姓**, 入力します **Reeve**.

23. Next に **User 入力します**, make note that **メンバー** が選択されていること.

 > 注: **メンバー** user 入力します は default user 入力します. This user 入力します は used のために mostユーザー で an組織.

24. Next に **役職**, 入力します **HR Rep**.

25. Next に **部署**, 入力します **HR**.

26. Next に **利用場所**, 選択します **United States**.

27. 選択します **次へ: 割り当て** located ページ下部で.

28. **割り当て** ページ, note that no割り当てs が選択されていること.

 > By default, noグループ は assigned に user. This は because user は not member の anyグループ until you assign them.

29. 選択します **Next: 確認します + create** located ページ下部で.
 > 確認します information on this ページ に 次のことを確認します。 it は correct.

30. 選択します **作成**.

31. **ユーザー | すべてのユーザー** ページ, 選択します **新しいユーザー** 続いて 選択します **新しいユーザーの作成**.

32. **新しいユーザーの作成** ページ, 入力します following:

 - User Principal 名前: **msnider**
 - Display 名前: **Mirおよびa Snider**

33. Uncheck **パスワードの自動生成**

34. Next に **パスワード**, 入力します **Pa55-w.rd!**.

 > 注: If you receive error message stating that thisパスワード で weak または commonly used, 入力します studentパスワード found 配下で **Resources** タブ の this lab profile. Alternatively, you できます 入力します complexパスワード of受講者のchoice.

35. 選択します **次へ: プロパティ** located ページ下部で.

36. Next に **名**, 入力します **Mirおよびa**.

37. Next に **姓**, 入力します **Snider**.

38. Next に **User 入力します**, make note that **メンバー** が選択されていること.

39. Next に **役職**, 入力します **Helpdesk Manager**.

40. Next に **部署**, 入力します **Operations**.

41. Next に **利用場所**, 選択します **United States**.

42. 選択します **次へ: 割り当て** located ページ下部で.

43. **割り当て** ページ, note that no割り当てs が選択されていること.

44. 選択します **Next: 確認します + create** located ページ下部で.

45. 選択します **作成**.

### タスク 2: PowerShell を使用してユーザーを作成する

# SEA-SVR1 に PowerShell 7.5.4 をインストールする手順

1. On **SEA-SVR1**, で **Microsoft Edge**, open new タブ. 

2. アドレス バーに **https://github.com/PowerShell/PowerShell/releases/download/v7.5.4/PowerShell-7.5.4-win-x64.msi** 

3. タスク バーで **File Explorer**, 続いて navigate to受講者の**Downloads** folder. 

4. Double-click **PowerShell-7.5.4-win-x64.msi** に launch setup wizard. 

 - 選択します **次へ** 
 - Leave **Destination Folder** として is, 続いて 選択します **次へ** 
 - Leave **Optional Actions** として is, 続いて 選択します **次へ** 
 - Leave checkboxes blank 配下で *Use Microsoft Update に help keep受講者のcomputer secure および up に date*, 続いて 選択します **次へ** 
 - 選択します **Install** 

5. **Installation completed successfully** ウィンドウ, check **Launch PowerShell**, 続いて 選択します **Finish**. 

 > **注:** If installer 閉じますd without launching PowerShell, click **Windows Search** bar, 入力します **pwsh**, right-click **PowerShell 7**, および 選択します **Run as管理者**. 

6. In **PowerShell 7** ウィンドウ, 入力します following commおよび, を入力し、 **入力します**. If prompted, 入力します **Y** at NuGet および repository messages:

 ```powershell
 Install-Module Microsoft.Graph -Scope CurrentUser
    ```

7. In **PowerShell 7** ウィンドウ, 入力します following commおよび, を入力し、 **入力します**:

 ```powershell
 Connect-MgGraph -scopes "user.readwrite.all, group.readwrite.all"
    ```

8. 要求されたら で **Let's get you signed in** ウィンドウ, 選択します **Work または Schoolアカウント** 続いて 選択します **Continue**.

9. In **Sign in** ダイアログ ボックス, 次のアカウントでサインインします。 **`admin@yourtenant.onmicrosoft.com`** を使用して administrativeパスワード, 続いて 選択します **Sign in**.

10. **Permissions Requested** prompt that が表示された場合, check **Consent on behalf の your組織** 続いて 選択します **Accept**.

11. **Sign で に all apps, websites, および services on this device?** 選択します, **No, this app only**.

12. In **PowerShell 7** ウィンドウ, 入力します following code に create new profile object, を入力し、 **入力します**. Replace **Pa55w.rd** を使用して complexパスワード of受講者のchoice:

 ```powershell
 $PWProfile = @{
 Password = "Pa55w.rd";
 ForceChangePasswordNextSignIn = $false
    }
    ```
    
14. Next, 入力します following code に create new user, を入力し、 **入力します**. Ensure "yourtenant" matches受講者のassigned tenant name:

 ```powershell
 New-MgUser `
 -Display名前 "Cody Godinez" `
 -Given名前 "Cody" -Surname "Godinez" `
 -MailNickname "cgodinez" `
 -UsageLocation "US" `
 -UserPrincipal名前 "cgodinez@yourtenant.onmicrosoft.com" `
 -PasswordProfile $PWProfile -AccountEnabled `
 -部署 "Sales" -JobTitle "Sales Rep"
    ```

15. To confirm that user **Cody Godinez** was created, In **PowerShell 7** ウィンドウ, 入力します following commおよび を入力し、 **入力します**:

 ```powershell
 Get-MgUser
    ```

> 次のことを確認します。 一覧 ofユーザー から受講者のtenant が表示されていること. 

**結果**: この演習を完了すると、 created new userアカウントs で Entra ID.

## 演習 2: Entra ID での管理ロールの割り当て

### シナリオ

次の作業を行う必要があります。 review および modify the現在の administrative roles for受講者のtenant.

次の操作を実行します。You があります been provided 一覧 ofユーザー should があります administrative roles assigned として indicated で following タブle. 

| 名前 | 必要な操作: | 必要な管理ロール: |
| -------------- | ---------------------------------------- | --------------------------- |
| Allan Deyoung | テナントを管理する | Global管理者 |
| Edmund Reeve | ユーザー、グループ、パスワードのリセットを管理する | User管理者 |
| Mirおよびa Snider | パスワードのリセットを管理する | Helpdesk管理者 |

### タスク 1: 管理ロールを確認して割り当てる

1. On SEA-SVR1, switch に Microsoft Edge.

2. Microsoft Entra 管理センターで, で Navigation ペイン, 選択します **ロールと管理者**.

 > 次の点に注意してください。 you できます scroll down 一覧 または use 検索ボックス に find **ロール** you は looking for.

3. Using 検索ボックス, search のために **グローバル管理者**.

4. 選択します **グローバル管理者** (選択します name, not checkbox).

5. In **グローバル管理者** ペイン, 選択します **+ Add割り当てs**.

6. Under **選択します members**, 選択します **No member 選択しますed**, 続いて search のために および 選択します **Allan Deyoung**.

7. 選択します **選択します**, 続いて 選択します **次へ**, および finally 選択します **割り当て**.

8. In navigation breadcrumbs, 選択します **ロールと管理者 | すべてのロール**.

9. Using 検索ボックス, search のために **ユーザー管理者**.

10. 選択します **ユーザー管理者** (選択します name, not checkbox).

11. In **ユーザー管理者** ペイン, 選択します **+ Add割り当てs**.

12. Under **選択します members**, 選択します **No member 選択しますed**, 続いて search のために および 選択します **Edmund Reeve**.

13. 選択します **選択します**, 続いて 選択します **次へ**, および finally 選択します **割り当て**.

14. In navigation breadcrumbs, 選択します **ロールと管理者 | すべてのロール**.

15. Using 検索ボックス, search のために **ヘルプデスク管理者**.

16. 選択します **ヘルプデスク管理者** (選択します name, not checkbox).

17. In **ヘルプデスク管理者** ペイン, 選択します **+ Add割り当てs**

18. Under **選択します members**, 選択します **No member 選択しますed**, 続いて search のために および 選択します **Mirおよびa Snider**.

19. 選択します **選択します**, 続いて 選択します **次へ**, および finally 選択します **割り当て**.

20. ナビゲーション ペインで, 選択します **ホーム**.

**結果**: この演習を完了すると、 assigned administrative roles toユーザー.

## 演習 3: グループの作成と管理、およびライセンス割り当ての検証

### シナリオ

次の作業を行う必要があります。 add three newユーザー に Security group および assignライセンスs として indicated で following タブle. 

| 名前 | 所属グループ: | 割り当てるライセンス |
| -------------- | ---------------- | ------------------------------------------------------------ |
| Edmund Reeve | Contoso_Managers | Office 365 E5, 入力しますprise Mobility + Security E5 via group membership |
| Mirおよびa Snider | Contoso_Managers | Office 365 E5, 入力しますprise Mobility + Security E5 via group membership |
| Cody Godinez | Contoso_Sales | Office 365 E5, 入力しますprise Mobility + Security E5 via group membership direct割り当て |

次の操作を実行します。You also been asked に modify Company brおよびing のために sign-in ページ.

### タスク 1: Microsoft Entra 管理センターを使用してグループを作成する

1. On **SEA-SVR1**, Microsoft Entra 管理センターで, ナビゲーション ペインで, 選択します **グループ**.

2. 選択します **新しいグループ**.

3. **新しいグループ** ページ, 入力します following:

 - Group 入力します: **セキュリティ**
 - Group name: **Contoso_Managers**
 - Membership 入力します: **割り当て済み**

4. Under Members, 選択します **No members 選択しますed**.

5. In Add members ページ add **Edmund Reeve**, **Mirおよびa Snider**, 続いて click **選択します**.

6. 選択します **作成**.

### タスク 2: PowerShell を使用してグループを作成する

1. On SEA-SVR1, switch に PowerShell 7.

2. In **PowerShell 7** ウィンドウ, 入力します following code に create new group, を入力し、 **入力します**:

 ```powershell
 New-MgGroup -Display名前 "Contoso_Sales" -Description "Contoso Sales teamユーザー" -MailEnabled:$false -Mailnickname "Contoso_Sales" -SecurityEnabled
    ```

3. In **PowerShell 7** ウィンドウ, 入力します following commおよび, を入力し、 **入力します**:

 ```powershell
 Get-MgGroup
    ```

4. 次のことを確認します。 you get 一覧 ofグループ in受講者のtenant, including Contoso_Sales group you just created.

5. In **PowerShell 7** ウィンドウ, 入力します following code に define variable として Contoso_Sales group, を入力し、 **入力します**:

 ```powershell
 $group = Get-MgGroup | Where-Object {$_.Display名前 -eq "Contoso_Sales"}
    ```

6. In **PowerShell 7** ウィンドウ, 入力します following code に define another variable として user, を入力し、 **入力します**:

 ```powershell
 $user = Get-MgUser | Where-Object {$_.Display名前 -eq "Cody Godinez"}
    ```

7. In **PowerShell 7** ウィンドウ, 入力します following code に add Cody に Contoso_Sales using set variables, を入力し、 **入力します**:

 ```powershell
 New-MgGroupMember -GroupId $group.Id -DirectoryObjectId $user.Id
    ```

8. In **PowerShell 7** ウィンドウ, 入力します following code, を入力し、 **入力します**:

 ```powershell
 Get-MgGroupMember -GroupId $group.Id | FL
    ```

9. 次のことを確認します。 you see **Cody Godinez** として 値 で **AdditionalProperties**.

10. 閉じます PowerShell 7.

### タスク 3: ライセンスを確認して会社のブランドを変更する

1. Microsoft Entra 管理センターで, ナビゲーション ペインで, 選択します **課金** > **ライセンス**.

2. **ライセンス** ページ, で c入力します navigation ペイン, 配下で **管理**, 選択します **すべての製品**.

 > 次の点を確認してください。 the現在のライセンスs利用可能な および assigned のために **入力しますprise Mobility + Security E5** および **Office 365 E5**.

3. Microsoft Entra 管理センターで, で Navigation ペイン,配下で **Entra ID**, 選択します **Custom brおよびing**.

4. **Company Brおよびing** ページ, 配下で **既定のサインイン エクスペリエンス**, 選択します **カスタマイズ**.

5. **既定のサインイン エクスペリエンスのカスタマイズ** ページ, navigate に **サインイン フォーム** タブ および configure following設定:

 - Sign-in ページ text: **Contoso Corp. Sign-in Page**

6. 選択します **確認します + Create**, review the設定 続いて 選択します **作成**.

7. Microsoft Entra 管理センターで, で Navigation ペイン, 選択します **ユーザー**.

8. In user 一覧, 選択します **Cody Godinez** (選択します name, not checkbox).

9. In Cody Godinez Profile ページ, で c入力します navigation menu, 選択します **ライセンス**.

 > 次の点に注意してください。 Cody does not があります any現在のライセンス割り当てs. And that licensing must now be performed で 365 Admin c入力します.

10. Open new タブ で **Microsoft Edge**, で address bar, 入力します **https://admin.microsoft.com**.

11. ナビゲーション ペインで left, 選択します **ユーザー** > **アクティブなユーザー**.

12. In user 一覧, 選択します **Cody Godinez** (選択します name, not checkbox).

13. 選択します **Licenses および apps** タブ.

14. 選択します チェック ボックスes next に **入力しますprise Mobility + Security E5** および **Office 365 E5 (no Teams)**.

15. 選択します **変更の保存**.

16. Once changes があります been saved, 選択します **X** で upper-right corner に 閉じます **Cody Godinez** ペイン. 

17. Microsoft 365 管理センターで, で Navigation ペイン, 選択します **課金** > **ライセンス**.

18. In **サブスクリプション** 一覧, 選択します **入力しますprise Mobility + Security E5**.

19. 選択します **グループ** タブ, 続いて 選択します **+ Assignライセンスs**.

20. Navigate into **入力します group name** textbox, および 選択します **Contoso_Managers** group.

21. 選択します **ライセンスの割り当て**.

22. **Contoso_Managers にライセンスを割り当てました** ペイン, 選択します **X** で upper-right corner に 閉じます it.

23. In upper-left corner の **入力しますprise Mobility + Security E5** ページ, 選択します **ライセンスに戻る** リンク.

24. In **サブスクリプション** 一覧, 選択します **Office 365 E5 (no Teams)**.

25. 選択します **グループ** タブ, 続いて 選択します **+ Assignライセンスs**.

26. Navigate into **入力します group name** textbox, および 選択します **Contoso_Managers** group.

27. 選択します **ライセンスの割り当て**.

28. **Contoso_Managers にライセンスを割り当てました** ペイン, 選択します **X** で upper-right corner に 閉じます it.

29. Microsoft 365 管理センターで, で Navigation ペイン, 選択します **課金** > **ライセンス**.

30. In **サブスクリプション** 一覧, 選択します **Office 365 E5 (no Teams)**.

 > 次の点を確認してください。 theユーザー that は assigned Office 365 E5ライセンス. Edmund および Mirおよびa both receive theirライセンス割り当て から their membership で Contoso_Managers group. You できます 選択します **グループ** タブ see if theライセンスs assigned correctly. It may take 3-5 minutes のために theライセンスs に reprocess.

31. 閉じます Microsoft Edge.

**結果**: この演習を完了すると、 created および managedグループ, modified company brおよびing, および assignedライセンスs.

**ラボ終了**
