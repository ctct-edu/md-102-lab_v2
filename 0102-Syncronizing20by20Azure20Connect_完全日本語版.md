---
lab:
    title: '練習ラボ 0102: Microsoft Entra Connect を使用した ID の同期'
    description: このラボでは、Active Directory Domain Services から Entra ID への同期を構成します。
    duration: 20 minutes
    level: 200
    islab: true
    primarytopics:
    - Microsoft Entra
    - Active Directory
---

## 練習ラボ 0102: Microsoft Entra Connect を使用した ID の同期

### 概要

このラボでは、Active Directory Domain Services から Entra ID への同期を構成します。

#### シナリオ

Contoso Corporation は現在、AD DS と Entra ID の両方でユーザーを個別のプロセスとして管理しています。これは時間がかかり、情報の不整合を招いています。あなたは、Microsoft Entra Connect 同期ツールを使用して 2 つのディレクトリを接続することで、この問題に対処するよう任されました。

##### タスク 1: Microsoft Entra Connect でディレクトリ同期を構成する

1. **SEA-SVR1** で、必要に応じて **Contoso\Administrator** としてパスワード **Pa55w.rd** でサインインし、**Server Manager** を閉じます。

2. タスク バーで **Microsoft Edge** を選択します。

3. アドレス バーに https://entra.microsoft.com を入力します。

4. 左側のナビゲーション ペインで、**Entra ID** の下にある **Entra Connect** を選択します。

5. **Microsoft Entra Connect \| はじめに** ペインで、**管理** タブを選択します。

6. **インフラストラクチャの管理** ページで、**Connect Sync Agent のダウンロード** を選択します。

7. **条項に同意してダウンロード** を選択します。

   **注:** Entra Connect Sync は SEA-SVR1 の **Downloads** フォルダーへ自動的にダウンロードされます。

8. **ダウンロード フォルダーを開く** を選択し、続いて **Downloads** ウィンドウで **AzureAdConnect.msi** をダブルクリックします。

9. **Microsoft Entra Connect Sync** ウィザードの **Welcome to Microsoft Entra Connect Sync** ページで、**I agree to the license terms and privacy notice** チェック ボックスをオンにし、続いて **Continue** を選択します。

10. **Express Settings** ページで、**Customize** を選択します。

    **注:** Use Express Settings ボタンはクリックしないでください。

11. **Install required components** ページで、**Install** を選択します。

12. **User sign-in** ページで、**Password Hash Synchronization** が選択されていることを確認し、続いて **Next** を選択します。

13. **Connect to Microsoft Entra ID** ページの **USERNAME** ボックスに **admin@yourtenant.onmicrosoft.com** を入力し、続いて **Next** を選択します。

14. **Sign in to your account** ウィンドウで **admin@yourtenant.onmicrosoft.com** を入力して **Next** を選択し、続いてテナントのパスワードを入力して **Sign in** を選択します。

15. **Connect your directories** ページで、**Contoso.com** が **FOREST** の下に一覧表示されていることを確認し、続いて **Add Directory** を選択します。

16. **AD forest account** ウィンドウで **Create New AD Account** オプションを選択し、**ENTERPRISE ADMIN USERNAME** フィールドに **Contoso\Administrator** を入力し、続いて **PASSWORD** フィールドに **Pa55w.rd** を入力します。**OK** を選択し、続いて **Next** を選択します。

17. **Microsoft Entra sign-in configuration** ページで、**USER PRINCIPAL NAME** ドロップダウン リストで **userPrincipalName** 値が選択されていることを確認します。

18. **Continue without matching all UPN suffixes to verified domains** を選択し、続いて **Next** を選択します。

19. **Domain and OU filtering** ページで、**Sync selected domains and OUs** を選択します。

20. **Contoso.com** を展開し、**Contoso.com** の横のチェック ボックスをオフにして、**IT**、**Managers**、**Marketing**、**Research**、**Sales** のチェック ボックスだけがオンになっていることを確認します。**Next** を選択します。

21. **Uniquely identifying your users** ページで、**Next** を選択します。

22. **Filter users and devices** ページで、**Next** を選択します。

23. **Optional features** ページで、利用可能なオプションを確認しますが、変更は行わないでください。**Password hash synchronization** が選択されていることを確認し、続いて **Next** を選択します。

24. **Ready to configure** ページで、**Start the synchronization process when configuration completes** が選択されていることを確認し、続いて **Install** を選択します。

25. 構成が完了したら、**Exit** を選択します。

    注: この時点で、ローカルの Active Directory Domain Services (AD DS) から Entra ID へのオブジェクトの同期が開始されます。このプロセスが完了するまで約 3 ～ 4 分待つ必要があります。または、Synchronization Service アプリケーションで進行状況を確認します。

26. 開いているすべてのウィンドウを閉じます。

##### タスク 2: Entra ID で同期を検証する

1. Microsoft Entra 管理センターのナビゲーション ペインで、**ユーザー** を選択します。

2. ローカルの AD DS のユーザーが表示されることを確認します。これらのユーザーの **オンプレミスの同期が有効** 列の値が **はい** になっていることを確認します。

3. ナビゲーション ペインで **グループ** を選択し、続いて **すべてのグループ** を選択します。ローカルの AD DS のグループが表示されることを確認します。これらのグループの **ソース** 列の値が **Windows Server AD** になっていることを確認します (**ソース** 列を表示するには、水平スクロール バーを使用して右へスクロールする必要があります)。

4. **Managers** グループを選択します。

5. **Managers** グループ ページで **メンバー** を選択し、ユーザーが表示されることを確認します。

   注: このグループはローカルの AD DS が提供元であるため、このグループにメンバーを追加したり、このグループからメンバーを削除したりすることはできません。

6. Microsoft Edge を閉じます。

**結果**: この演習を完了すると、Active Directory Domain Services から Entra ID へ ID を同期するように Azure AD Connect を正常に構成できたことになります。

**ラボ終了**
