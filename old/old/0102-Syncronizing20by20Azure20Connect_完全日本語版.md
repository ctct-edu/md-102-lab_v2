---
lab:
 title: '演習ラボ 0102: Microsoft Entra Connect を使用した ID の同期'
 description: このラボでは、 configure同期 から Active Directory Domain Services に Entra ID.
 duration: 20 minutes
 level: 200
 islab: true
 primarytopics:
 - Microsoft Entra
 - Active Directory
---

# 演習ラボ 0102: Microsoft Entra Connect を使用した ID の同期 

## 概要

このラボでは、 configure同期 から Active Directory Domain Services に Entra ID.

### シナリオ

次の操作を実行します。Contoso Corporation は currently managingユーザー で both AD DS および Entra ID として separate processes. This は time consuming および があります led に inconsistent information. 担当することになりました。 addressing this issue by connecting two directories by using Microsoft Entra Connect同期 tool.

#### タスク 1: Microsoft Entra Connect を使用してディレクトリ同期を構成する

1. On **SEA-SVR1**, 必要に応じて, 次のアカウントでサインインします。 **Contoso\\Administrator** パスワード **Pa55w.rd** および 閉じます **Server Manager**.

2. タスク バーで **Microsoft Edge**.

3. アドレス バーに `https://entra.microsoft.com`

4. In left navigation ペイン, 配下で **Entra ID**, 選択します **Entra Connect**.

5. **Microsoft Entra Connect | Get started** ペイン, 選択します **管理** タブ.

6. In **Manage受講者のinfrastructure** ページ, 選択します **Download Connect Sync Agent**.

7. 選択します **Accept terms & download**. 

 >**注**: Entra Connect Sync automatically downloads に **Downloads** folder on SEA-SVR1.

8. 選択します **Open downloads folder** 続いて で **Downloads** ウィンドウ, double-click **AzureAdConnect.msi**.

9. In **Microsoft Entra Connect Sync** wizard, **Welcome に Microsoft Entra Connect Sync** ページ, 選択します **I agree に theライセンス terms および privacy notice** チェック ボックス, 続いて 選択します **Continue**.

10. **Express Settings** ページ, 選択します **カスタマイズ**
    
 >**注**: Do not click Use Express Settings ボタン.

11. **Install required components** ページ, 選択します **Install**.

12. **User sign-in** ページ, 次のことを確認します。 **Password Hash Synchronization** が選択されていること, 続いて 選択します **次へ**.

13. **Connect に Microsoft Entra ID** ページ, で **USERNAME** boxes, 入力します **admin@yourtenant.onmicrosoft.com**, 続いて 選択します **次へ**.

14. In **Sign で に yourアカウント** ウィンドウ, 入力します **admin@yourtenant.onmicrosoft.com**, 選択します **次へ**, 続いて 入力します受講者のtenantパスワード, および 選択します **Sign in**.

15. **Connect受講者のdirectories** ページ, 次のことを確認します。 **Contoso.com** が表示されていること 配下で **FOREST**, 続いて 選択します **Add Directory**.

16. In **AD forestアカウント** ウィンドウ, 選択します **Create New AD Account** option, および で **ENTERPRISE ADMIN USERNAME** フィールド, 入力します **Contoso\\Administrator**, 続いて 入力します **Pa55w.rd** で **PASSWORD** フィールド. 選択します **OK**, 続いて 選択します **次へ**.

17. **Microsoft Entra sign-in構成** ページ, 次のことを確認します。 で **USER PRINCIPAL NAME** drop-down 一覧, **userPrincipal名前** 値 が選択されていること. 

18. 選択します **Continue without matching all UPN suffixes に verified domains** 続いて 選択します **次へ**.

19. **Domain および OU filtering** ページ, 選択します **Sync 選択しますed domains および OUs**.

20. Expおよび **Contoso.com**, clear checkbox next に **Contoso.com** および 次のことを確認します。 only following チェック ボックスes が選択されていること: **IT**, **Managers**, **Marketing**, **Research**, および **Sales**. 選択します **次へ**.

21. **Uniquely identifying受講者のusers** ページ, 選択します **次へ**.

22. **Filterユーザー およびデバイス** ページ, 選択します **次へ**.

23. **Optional features** ページ, review利用可能な options, but 変更しないでください. 次のことを確認します。 **Password hash同期** が選択されていること, 続いて 選択します **次へ**.

24. **Ready に configure** ページ, 次のことを確認します。 **Start the同期 process when構成 completes** が選択されていること, 続いて 選択します **Install**.

25. When構成 は complete, 選択します **Exit**. 

 > 注: At this time,同期 の objects から yourローカル Active Directory Domain Services (AD DS) および Entra ID begins. You should wait approximately 3-4 minutes のために this process に complete. Or check progress で Synchronization Service application.

26. 閉じます 開いているすべてのウィンドウ.

#### タスク 2: Entra ID で同期を確認する

1. Microsoft Entra 管理センターで, ナビゲーション ペインで, 選択します **ユーザー**.

2. 次のことを確認します。 you seeユーザー から yourローカル AD DS. 次のことを確認します。 theseユーザー があります 値 **はい** で **オンプレミスの同期が有効** 列. 

3. In Navigation ペイン, 選択します **グループ**, 続いて 選択します **All Groups**. 次のことを確認します。 you seeグループ から yourローカル AD DS. 次のことを確認します。 theseグループ があります 値 **Windows Server AD** で **Source** 列 (you します need に use horizontal scroll bar および scroll に right に be able に see **Source** 列).

4. 選択します **Managers** group.

5. **Managers** group ページ, 選択します **メンバー** 続いて 次のことを確認します。 you seeユーザー. 

 > 次の点に注意してください。 you cannot add に または remove members から this group, として it は sourced から theローカル AD DS. 

6. 閉じます Microsoft Edge.

**結果**: この演習を完了すると、 configured Azure AD Connect に synchronize identity から Active Directory Domain Services に Entra ID.

**ラボ終了**
