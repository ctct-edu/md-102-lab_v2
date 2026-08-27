---
lab:
  title: 'プラクティス ラボ 0101: Entra ID でのIDの管理'
  description: このラボでは、Entra 管理センターを使用してユーザーの作成と変更、管理者ロールの割り当て、グループの作成と変更、および Entra ID でのライセンス割り当ての管理を行います。
  duration: 60 minutes
  level: 200
  islab: true
---

# プラクティス ラボ 0101: Entra ID でのIDの管理

## WWL Tenants - Terms of Use

If you are being provided with a tenant as a part of an instructor-led training delivery, please note that the tenant is made available for the purpose of supporting the hands-on labs in the instructor-led training。

Tenants should not be shared or used for purposes outside of hands-on labs. The tenant used in this course is a trial tenant and cannot be used or accessed after the class is over and are not eligible for extension。

Tenants must not be converted to a paid subscription. Tenants obtained as a part of this course remain the property of Microsoft Corporation and we reserve the right to obtain access and repossess at any time。

## 概要

このラボでは、Entra 管理センターを使用してユーザーの作成と変更、管理者ロールの割り当て、グループの作成と変更、および Entra ID でのライセンス割り当ての管理を行います。

## 演習 1: Entra ID でのユーザーの作成

### シナリオ

来週入社する新入社員のユーザー アカウントを Azure AD に作成する必要があります。新しいユーザーを次の表に示します。

| Name           | User Name                             | Password   | Job title        | Department |
| -------------- | ------------------------------------- | ---------- | ---------------- | ---------- |
| Edmund Reeve   | `ereeve@yourtenant.onmicrosoft.com`   | Pa55-w.rd! | HR Rep           | HR         |
| Miranda Snider | `msnider@yourtenant.onmicrosoft.com`  | Pa55-w.rd! | Helpdesk Manager | Operations |
| Cody Godinez   | `cgodinez@yourtenant.onmicrosoft.com` | Pa55-w.rd! | Sales Rep        | Sales      |

_注: For location use either your local region or United States._

今後数か月の間に、さらに複数の従業員が採用される予定です。多数の新しいユーザーを追加するにはスクリプトの方が効率的であるため、PowerShell スクリプトを作成し、Cody Godinez のアカウントを作成するときにテストします。

### タスク 1: Microsoft Entra 管理センターを使用してユーザーを作成する

1. **SEA-SVR1** で、**Contoso\\Administrator** としてパスワード **Pa55w.rd** を使用してサインインします。

2. **Server Manager** を閉じます。

3. タスク バーで **Microsoft Edge** を選択します。

4. アドレス バーに **https://entra.microsoft.com** と入力します。

5. At the Sign-in prompt, 入力します **admin@yourtenant.onmicrosoft.com** and 続いて **次へ**。

6. At the Enter password ページ, 入力します the password for the Admin account and 続いて **Sign in**。

> 注: Check with your instructor on the password to use for signing in with the Admin account。

7. **Edge Save password prompt** で **Save & Turn on** を選択します。

8. **Stay signed in prompt** で **はい** を選択します。

9. On the **Let's keep your account secure** dialog, 選択します **次へ**。

10. On the **Install Microsoft Authenticator** dialog, 選択します **次へ**。

11. ****set up your account in app**** ページで **次へ** を選択します。

12. Using the Authenticator app on your mobile device, scan the QR code and 続いて **次へ**。

13. On the **Let's try it out** dialog, take note of the code, 入力します that in to your Authenticator app。

14. On the **Authenticator Added** dialog, 選択します **Done**。

15. Microsoft Entra 管理センターで、 ナビゲーション ペインで、 選択します **ユーザー**。

> 確認します: the users that already exist as members of the Microsoft Entra ID. The **オンプレミスの同期が有効** 列 states **いいえ** for all current users. これは、 each user was created directly in Microsoft Entra ID and not synchronized from an on-premises directory service。

16. ****Users | All users**** ページで **新しいユーザー** 続いて **新しいユーザーの作成** を選択します。

17. On the **新しいユーザーの作成** ページ, 入力します the following:

- User Principal Name: **ereeve**
- Display Name: **Edmund Reeve**

18. Uncheck **パスワードの自動生成**

19. Next to **パスワード**, 入力します **Pa55-w.rd!**。

> 注: If you receive an error message stating that this password in weak or commonly used, 入力します the student password found under the **Resources** タブ of this lab profile. Alternatively, you can 入力します a complex password of your choice。

20. Select **次へ: プロパティ** located at the bottom of the ページ。

21. Next to **名**, 入力します **Edmund**。

22. Next to **姓**, 入力します **Reeve**。

23. Next to **ユーザーの種類**, 次の点を確認します: **メンバー** is 選択しました。

> 注: The **メンバー** user 入力します is the default user 入力します. This user 入力します is used for most users in an organization。

24. Next to **役職**, 入力します **HR Rep**。

25. Next to **部署**, 入力します **HR**。

26. Next to **利用場所**, 選択します **United States**。

27. Select **次へ: 割り当て** located at the bottom of the ページ。

28. On the **割り当て** ページ, note that no assignments are 選択しました。

> By default, no groups are assigned to the user. This is because the user is not a member of any groups until you assign them。

29. Select **次へ: 確認と作成** located at the bottom of the ページ。
> Review the information on this ページ to ensure that it is correct。

30. **作成** を選択します。

31. ****Users | All users**** ページで **新しいユーザー** 続いて **新しいユーザーの作成** を選択します。

32. On the **新しいユーザーの作成** ページ, 入力します the following:

- User Principal Name: **msnider**
- Display Name: **Miranda Snider**

33. Uncheck **パスワードの自動生成**

34. Next to **パスワード**, 入力します **Pa55-w.rd!**。

> 注: If you receive an error message stating that this password in weak or commonly used, 入力します the student password found under the **Resources** タブ of this lab profile. Alternatively, you can 入力します a complex password of your choice。

35. Select **次へ: プロパティ** located at the bottom of the ページ。

36. Next to **名**, 入力します **Miranda**。

37. Next to **姓**, 入力します **Snider**。

38. Next to **ユーザーの種類**, 次の点を確認します: **メンバー** is 選択しました。

39. Next to **役職**, 入力します **Helpdesk Manager**。

40. Next to **部署**, 入力します **Operations**。

41. Next to **利用場所**, 選択します **United States**。

42. Select **次へ: 割り当て** located at the bottom of the ページ。

43. On the **割り当て** ページ, note that no assignments are 選択しました。

44. Select **次へ: 確認と作成** located at the bottom of the ページ。

45. **作成** を選択します。

### タスク 2: PowerShell を使用してユーザーを作成する

# SEA-SVR1 に PowerShell 7.5.4 をインストールする手順

1. On **SEA-SVR1**, in **Microsoft Edge**, open a new タブ。

2. アドレス バーに **https://github.com/PowerShell/PowerShell/releases/download/v7.5.4/PowerShell-7.5.4-win-x64.msi** と入力します。

3. On the taskbar, 選択します **File Explorer**, then navigate to your **Downloads** folder。

4. Double-click **PowerShell-7.5.4-win-x64.msi** to launch the setup wizard。

- **次へ** を選択します。
- Leave the **Destination Folder** as is, 続いて **次へ**
- Leave the **Optional Actions** as is, 続いて **次へ**
- Leave the checkボックスes blank under *Use Microsoft Update to help keep your computer secure and up to date*, 続いて **次へ**
- **Install** を選択します。

5. On the **Installation completed successfully** ウィンドウ, check **Launch PowerShell**, 続いて **Finish**。

> **注:** If the installer 閉じますd without launching PowerShell, click the **Windows Search** bar, 入力します **pwsh**, right-click **PowerShell 7**, 選択してから **Run as administrator**。

6. In the **PowerShell 7** ウィンドウ, 入力します the following command, and then 押します **Enter**. If prompted, 入力します **Y** at the NuGet and repository messages:

    ```powershell
    Install-Module Microsoft.Graph -Scope CurrentUser
    ```

7. In the **PowerShell 7** ウィンドウ, 入力します the following command, and then 押します **Enter**:

    ```powershell
    Connect-MgGraph -scopes "user.readwrite.all, group.readwrite.all"
    ```

8. prompted in the **Let's get you signed in** ウィンドウときは、**Work or School account** and 続いて **Continue** を選択します。

9. In the **Sign in** ダイアログ ボックス, としてサインインします **`admin@yourtenant.onmicrosoft.com`** with the administrative password, and 続いて **Sign in**。

10. On the **Permissions Requested** prompt that appears, check **Consent on behalf of your organization** and 続いて **Accept**。

11. On the **Sign in to all apps, websites, and services on this device?** 選択します, **No, this app only**。

12. In the **PowerShell 7** ウィンドウ, 入力します the following code to create a new profile object, and then 押します **入力します**. Replace **Pa55w.rd** with a complex password of your choice:

    ```powershell
    $PWProfile = @{
        Password = "Pa55w.rd";
        ForceChangePasswordNextSignIn = $false
    }
    ```
    
14. Next, 入力します the following code to create a new user, and then 押します **Enter**. Ensure "yourtenant" matches your assigned tenant name:

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

15. To confirm that the user **Cody Godinez** was created, In the **PowerShell 7** ウィンドウ, 入力します the following command and then 押します **Enter**:

    ```powershell
    Get-MgUser
    ```

> Verify that the list of users from テナント が表示されている。

**結果**: この演習を完了すると、 created new user accounts in Entra ID。

## 演習 2: Entra ID での管理者ロールの割り当て

### シナリオ

テナントの現在の管理者ロールを確認し、変更する必要があります。

次の表に示すとおり、管理者ロールを割り当てる必要があるユーザーの一覧が提供されています。

| Name           | Must be able to:                         | Administrative Role needed: |
| -------------- | ---------------------------------------- | --------------------------- |
| Allan Deyoung  | Manage the tenant                        | Global administrator        |
| Edmund Reeve   | Manage users, group, and password resets | User administrator          |
| Miranda Snider | Manage password resets                   | Helpdesk administrator      |

### タスク 1: 管理者ロールを確認して割り当てる

1. On SEA-SVR1, switch to Microsoft Edge。

2. Microsoft Entra 管理センターで、 ナビゲーション ペインで、 選択します **ロールと管理者**。

> Note that you can scroll down the list or use the search ボックス to find the **Role** you are looking for。

3. Using the search ボックス, search for **グローバル管理者**。

4. Select **グローバル管理者** (選択します the name, not the checkボックス)。

5. In the **グローバル管理者** ペイン, 選択します **+ Add assignments**。

6. Under **メンバーの選択**, 選択します **メンバーが選択されていません**, then search for 選択してから **Allan Deyoung**。

7. **選択**, 続いて **次へ**, and finally 選択します **割り当て** を選択します。

8. In the navigation breadcrumbs, 選択します **Roles & administrators | All roles**。

9. Using the search ボックス, search for **ユーザー管理者**。

10. Select **ユーザー管理者** (選択します the name, not the checkボックス)。

11. In the **ユーザー管理者** ペイン, 選択します **+ Add assignments**。

12. Under **メンバーの選択**, 選択します **メンバーが選択されていません**, then search for 選択してから **Edmund Reeve**。

13. **選択**, 続いて **次へ**, and finally 選択します **割り当て** を選択します。

14. In the navigation breadcrumbs, 選択します **Roles & administrators | All roles**。

15. Using the search ボックス, search for **ヘルプデスク管理者**。

16. Select **ヘルプデスク管理者** (選択します the name, not the checkボックス)。

17. In the **ヘルプデスク管理者** ペイン, 選択します **+ Add assignments**

18. Under **メンバーの選択**, 選択します **メンバーが選択されていません**, then search for 選択してから **Miranda Snider**。

19. **選択**, 続いて **次へ**, and finally 選択します **割り当て** を選択します。

20. In the navigation ペイン, 選択します **ホーム**。

**結果**: この演習を完了すると、 assigned administrative roles to users。

## 演習 3: グループの作成と管理、およびライセンス割り当ての検証

### シナリオ

3人の新しいユーザーをセキュリティ グループに追加し、次の表に示すライセンスを割り当てる必要があります。

| Name           | Member of:       | License to assign                                            |
| -------------- | ---------------- | ------------------------------------------------------------ |
| Edmund Reeve   | Contoso_Managers | Office 365 E5, Enterprise Mobility + Security E5 via group membership |
| Miranda Snider | Contoso_Managers | Office 365 E5, Enterprise Mobility + Security E5 via group membership |
| Cody Godinez   | Contoso_Sales    | Office 365 E5, Enterprise Mobility + Security E5 via group membership direct assignment |

さらに、サインイン ページの会社のブランドを変更するよう依頼されています。

### タスク 1: Microsoft Entra 管理センターを使用してグループを作成する

1. On **SEA-SVR1**, in the Microsoft Entra admin c入力します, ナビゲーション ペインで、 選択します **グループ**。

2. **新しいグループ** を選択します。

3. On the **新しいグループ** ページ, 入力します the following:

- Group 入力します: **セキュリティ**
- Group name: **Contoso_Managers**
- Membership 入力します: **割り当て済み**

4. Under Members, 選択します **メンバーが選択されていません**。

5. In the Add members ページ add **Edmund Reeve**, **Miranda Snider**, and then click **選択**。

6. **作成** を選択します。

### タスク 2: PowerShell を使用してグループを作成する

1. On SEA-SVR1, switch to PowerShell 7。

2. In the **PowerShell 7** ウィンドウ, 入力します the following code to create a new group, and then 押します **Enter**:

    ```powershell
    New-MgGroup -DisplayName "Contoso_Sales" -Description "Contoso Sales team users" -MailEnabled:$false -Mailnickname "Contoso_Sales" -SecurityEnabled
    ```

3. In the **PowerShell 7** ウィンドウ, 入力します the following command, and then 押します **Enter**:

    ```powershell
    Get-MgGroup
    ```

4. you get the list of groups in テナント, including the Contoso_Sales group you just createdことを確認します。

5. In the **PowerShell 7** ウィンドウ, 入力します the following code to define a variable as the Contoso_Sales group, and then 押します **Enter**:

    ```powershell
    $group = Get-MgGroup | Where-Object {$_.DisplayName -eq "Contoso_Sales"}
    ```

6. In the **PowerShell 7** ウィンドウ, 入力します the following code to define another variable as the user, and then 押します **Enter**:

    ```powershell
    $user = Get-MgUser | Where-Object {$_.DisplayName -eq "Cody Godinez"}
    ```

7. In the **PowerShell 7** ウィンドウ, 入力します the following code to add Cody to Contoso_Sales using set variables, and then 押します **Enter**:

    ```powershell
    New-MgGroupMember -GroupId $group.Id -DirectoryObjectId $user.Id
    ```

8. In the **PowerShell 7** ウィンドウ, 入力します the following code, and then 押します **Enter**:

    ```powershell
    Get-MgGroupMember -GroupId $group.Id | FL
    ```

9. 表示されている **Cody Godinez** as value in **AdditionalProperties**ことを確認します。

10. PowerShell 7 を閉じます。

### タスク 3: ライセンスを確認して会社のブランドを変更する

1. Microsoft Entra 管理センターで、 ナビゲーション ペインで、 選択します **課金** > **ライセンス**。

2. On the **ライセンス** ページ, in the c入力します navigation ペイン, under **管理**, 選択します **すべての製品**。

> 確認します: the current licenses available and assigned for **Enterprise Mobility + Security E5** and **Office 365 E5**。

3. Microsoft Entra 管理センターで、 ナビゲーション ペインで、under **Entra ID**, 選択します **会社のブランド**。

4. On the **会社のブランド** ページ, under **既定のサインイン エクスペリエンス**, 選択します **カスタマイズ**。

5. On the **既定のサインイン エクスペリエンスのカスタマイズ** ページ, navigate to the **サインイン フォーム** タブ and configure the following settings:

- Sign-in ページ text: **Contoso Corp. Sign-in Page**

6. **確認と作成**, 確認します the settings and 続いて **作成** を選択します。

7. Microsoft Entra 管理センターで、 ナビゲーション ペインで、 選択します **ユーザー**。

8. In the user list, 選択します **Cody Godinez** (選択します the name, not the checkボックス)。

9. In the Cody Godinez Profile ページ, in the c入力します navigation menu, 選択します **ライセンス**。

> 次の点に注意してください: Cody does not have any current license assignments. And that licensing must now be performed in the 365 Admin c入力します。

10. Open a new タブ in **Microsoft Edge**, in the address bar, 入力します **https://admin.microsoft.com**。

11. In the navigation ペイン on the left, 選択します **ユーザー** > **アクティブなユーザー**。

12. In the user list, 選択します **Cody Godinez** (選択します the name, not the checkボックス)。

13. Select the **ライセンスとアプリ** タブ。

14. Select the check ボックスes next to **Enterprise Mobility + Security E5** and **Office 365 E5 (no Teams)**。

15. **変更の保存** を選択します。

16. Once the changes have been saved, 選択します the **X** in the upper-right corner to 閉じます the **Cody Godinez** ペイン。

17. Microsoft 365 管理センターで、 ナビゲーション ペインで、 選択します **課金** > **ライセンス**。

18. In the **サブスクリプション** list, 選択します **Enterprise Mobility + Security E5**。

19. Select the **グループ** タブ, and 続いて **+ Assign licenses**。

20. Navigate into the **グループ名を入力** textボックス, 選択してから the **Contoso_Managers** group。

21. **ライセンスの割り当て** を選択します。

22. On the **You assigned licenses to Contoso_Managers** ペイン, 選択します the **X** in the upper-right corner to 閉じます it。

23. In the upper-left corner of the **Enterprise Mobility + Security E5** ページ, 選択します the **ライセンスに戻る** link。

24. In the **サブスクリプション** list, 選択します **Office 365 E5 (no Teams)**。

25. Select the **グループ** タブ, and 続いて **+ Assign licenses**。

26. Navigate into the **グループ名を入力** textボックス, 選択してから the **Contoso_Managers** group。

27. **ライセンスの割り当て** を選択します。

28. On the **You assigned licenses to Contoso_Managers** ペイン, 選択します the **X** in the upper-right corner to 閉じます it。

29. Microsoft 365 管理センターで、 ナビゲーション ペインで、 選択します **課金** > **ライセンス**。

30. In the **サブスクリプション** list, 選択します **Office 365 E5 (no Teams)**。

> 確認します: the users that are assigned the Office 365 E5 license. Edmund and Miranda both receive their license assignment from their membership in the Contoso_Managers group. You can 選択します the **グループ** タブ see if the licenses assigned correctly. It may take 3-5 minutes for the licenses to reprocess。

31. Microsoft Edge を閉じます。

**結果**: この演習を完了すると、 created and managed groups, modified company branding, and assigned licenses。

**ラボ終了**
