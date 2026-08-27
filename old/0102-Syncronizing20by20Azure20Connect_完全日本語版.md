---
lab:
  title: 'プラクティス ラボ 0102: Microsoft Entra Connect を使用したIDの同期'
  description: このラボでは、Active Directory Domain Services から Entra ID への同期を構成します。
  duration: 20 minutes
  level: 200
  islab: true
  primarytopics:
- Microsoft Entra
- Active Directory
---

# プラクティス ラボ 0102: Microsoft Entra Connect を使用したIDの同期

## 概要

このラボでは、Active Directory Domain Services から Entra ID への同期を構成します。

### シナリオ

Contoso Corporation では現在、AD DS と Entra ID のユーザーを別々のプロセスで管理しています。この方法は時間がかかり、情報の不整合も発生しています。この問題に対処するため、Microsoft Entra Connect 同期ツールを使用して2つのディレクトリを接続します。

#### タスク 1: Microsoft Entra Connect を使用してディレクトリ同期を構成する

1. **SEA-SVR1** で、必要に応じて **Contoso\\Administrator** としてパスワード **Pa55w.rd** を使用してサインインし、**Server Manager** を閉じます。

2. タスク バーで **Microsoft Edge** を選択します。

3. アドレス バーに `https://entra.microsoft.com` と入力します。

4. In the left navigation ペイン, under **Entra ID**, 選択します **Entra Connect**。

5. On the **Microsoft Entra Connect | Get started** ペイン, 選択します the **管理** タブ。

6. ****インフラストラクチャの管理**** ページで **Connect Sync Agent のダウンロード** を選択します。

7. **条項に同意してダウンロード** を選択します。

>**注**: Entra Connect Sync automatically downloads to the **Downloads** folder on SEA-SVR1。

8. **Open downloads folder** and then in the **Downloads** ウィンドウ, double-click **AzureAdConnect.msi** を選択します。

9. In the **Microsoft Entra Connect Sync** wizard, on the **Welcome to Microsoft Entra Connect Sync** ページ, 選択します the **I agree to the license terms and privacy notice** check ボックス, and 続いて **Continue**。

10. ****Ex押します Settings**** ページで **カスタマイズ** を選択します。
    
>**注**: Do not click the Use Ex押します Settings button。

11. ****Install required components**** ページで **Install** を選択します。

12. On the **User sign-in** ページ, ensure that **Password Hash Synchronization** is 選択しました, and 続いて **次へ**。

13. On the **Connect to Microsoft Entra ID** ページ, in the **ユーザー名** ボックスes, 入力します **admin@yourtenant.onmicrosoft.com**, and 続いて **次へ**。

14. In the **Sign in to your account** ウィンドウ, 入力します **admin@yourtenant.onmicrosoft.com**, 選択します **次へ**, then 入力します テナント password, 選択してから **Sign in**。

15. On the **Connect your directories** ページ, ensure that **Contoso.com** が表示されている under **フォレスト**, and 続いて **Add Directory**。

16. In the **AD forest account** ウィンドウ, 選択します the **Create New AD Account** option, and in the **ENTERPRISE ADMIN USERNAME** フィールド, 入力します **Contoso\\Administrator**, and then 入力します **Pa55w.rd** in the **PASSWORD** フィールド. Select **OK**, and 続いて **次へ**。

17. On the **Microsoft Entra sign-in configuration** ページ, ensure that in the **USER PRINCIPAL NAME** ドロップダウン リスト, the **userPrincipalName** value is 選択しました。

18. **Continue without matching all UPN suffixes to verified domains** and 続いて **次へ** を選択します。

19. ****Domain and OU filtering**** ページで **Sync 選択しました domains and OUs** を選択します。

20. Expand **Contoso.com**, clear the checkボックス next to **Contoso.com** and ensure that the only following check ボックスes are 選択しました: **IT**, **Managers**, **Marketing**, **Research**, and **Sales**. Select **次へ**。

21. ****Uniquely identifying your users**** ページで **次へ** を選択します。

22. ****Filter users and devices**** ページで **次へ** を選択します。

23. On the **Optional features** ページ, 確認します available options, but 変更しません. Ensure that **Password hash synchronization** is 選択しました, and 続いて **次へ**。

24. On the **Ready to configure** ページ, ensure that **Start the synchronization process when configuration completes** is 選択しました, and 続いて **Install**。

25. configuration is completeときは、**Exit** を選択します。

> 注: At this time, synchronization of objects from your local Active Directory Domain Services (AD DS) and Entra ID begins. You should wait approximately 3-4 minutes for this process to complete. Or check progress in the Synchronization Service application。

26. 開いているすべてのウィンドウを閉じます。

#### タスク 2: Entra ID で同期を確認する

1. Microsoft Entra 管理センターで、 ナビゲーション ペインで、 選択します **ユーザー**。

2. 表示されている users ローカル AD DS から. Ensure that these users have the value **はい** in the **オンプレミスの同期が有効** 列ことを確認します。

3. In the Navigation ペイン, 選択します **グループ**, 続いて **すべてのグループ**. Verify that 表示されている groups ローカル AD DS から. Ensure that these groups have the value **Windows Server AD** in the **ソース** 列 (you will need to use the horizontal scroll bar and scroll to the right to be able to see the **ソース** 列)。

4. Select the **Managers** group。

5. On the **Managers** group ページ, 選択します **メンバー** and then ensure that 表示されている users。

> Note that you cannot add to or remove members from this group, as it is sourced from the local AD DS。

6. Microsoft Edge を閉じます。

**結果**: この演習を完了すると、 configured Azure AD Connect to synchronize identity from Active Directory Domain Services to Entra ID。

**ラボ終了**
