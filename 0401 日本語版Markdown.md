---
lab:
  title: '演習ラボ 0401: Intune を使用したクラウド アプリの展開'
  description: このラボでは、Intune と Company Portal Web サイトを使用してクラウドベースのアプリを作成し、展開します。
  duration: 5 minutes
  level: 200
  islab: true
---

# 演習ラボ 0401: Intune を使用したクラウド アプリの展開

## 概要

このラボでは、Intune と Company Portal Web サイトを使用してクラウドベースのアプリを作成し、展開します。

### 前提条件

このラボを開始する前に、次のラボを完了しておく必要があります。

- 0101-Managing Identities in Entra ID
- 0102-Synchronizing identities by using Entra Connect
- 0203-Manage Device Enrollment into Intune
- 0204-Enrolling devices into Intune

  注: Entra ID への Windows Hello サインイン認証を保護するために使用するテキスト メッセージを受信できる携帯電話も必要です。

## 演習 1: Microsoft Store アプリを Intune に追加する

### シナリオ

Microsoft Intune を使用して、Contoso Corporation のデスクトップとアプリを管理しています。Research 部門は、作業のためにさまざまなサーバーへ接続することが多く、必要に応じて Research のメンバーが Windows App をインストールできるようにすることを希望しています。Windows App は Microsoft Store から入手できますが、ユーザーが Company Portal Web サイトからアクセスできるように、アプリを Intune へ追加します。Research のメンバーである Aaron Nicholls が、ポータルへの公開後にインストール処理をテストします。

### タスク 1: Windows App を Intune に追加する

1. 手元の PC で Microsoft Edge を起動し、アドレス バーに **https://intune.microsoft.com** と入力して **Enter** キーを押します。
2. テナント管理者のパスワードを使用して、**`admin@yourtenant.onmicrosoft.com`** としてサインインします。
3. **Microsoft Intune 管理センター** ページで、**アプリ** を選択します。
4. **アプリ** ページのナビゲーション ペインで、**すべてのアプリ** を選択します。
5. 詳細ペインで、**作成** を選択します。
6. **アプリの種類の選択** ページでドロップダウン メニューを選択し、**Microsoft Store app (new)** を選択して、**選択** を選択します。
7. **アプリの追加** ページで、**Search the Microsoft Store app (new)** を選択します。**Windows App** を検索して選択し、**選択** を選択します。
8. **アプリ情報** ページで次の情報を確認し、**次へ** を選択します。
   - 名前: **Windows App**
   - 発行元: **Microsoft Corp.**
   - カテゴリ: **Business**
   - おすすめアプリとして表示する: **はい**
9. **次へ** を 2 回選択し、**作成** を選択します。
10. Windows App のページが開きます。

    > **プロパティ**、**デバイスのインストール状態**、**ユーザーのインストール状態**の各ノードを確認します。

### タスク 2: アプリにグループを割り当てる

1. **Windows App** ページの **管理** で、**プロパティ** を選択します。
2. 詳細ペインで **割り当て** セクションまで下にスクロールし、**編集** を選択します。
3. **割り当て** ページの **登録済みデバイスで使用可能** で、**グループの追加** を選択します。
4. **グループの選択** ページで **Research** グループを検索して選択し、**選択** を選択します。
5. **確認と保存** を選択し、**保存** を選択します。

### タスク 3: Intune コンソールからポリシー同期を強制する

1. **Microsoft Intune 管理センター**で **デバイス** を選択し、**すべてのデバイス** を選択します。
2. 詳細ペインで **SEA-WS1** を選択します。
3. **SEA-WS1** ブレードで **同期** を選択し、求められたら **はい** を選択します。

   > Intune はデバイスへ接続し、すべてのポリシーを同期するよう指示します。これには最長5分かかる場合があります。

### タスク 4: Company Portal Web サイトからアプリをインストールする

1. **SEA-WS1** に切り替えます。
2. PIN **102938** を使用して **Aaron Nicholls** としてサインインします。
3. タスク バーで **Microsoft Edge** を選択します。
4. 必要に応じて、**Welcome to Microsoft Edge** ページで **Confirm and continue** を選択します。Welcome ページを閉じます。
5. アドレス バーで **https://portal.manage.microsoft.com** を開き、**Enter** キーを押します。
6. **Aaron Nicholls** としてサインインします。
7. Contoso Web ポータルで、**View Devices** を選択します。
8. Devices ページで、**Tap here to tell us which device you're using or add a new device** を選択します。
9. **Which device are you using** ダイアログで **SEA-WS1** の横にあるオプションを選択し、**Select** を選択します。

   > メッセージが「Apps will be installed onto: SEA-WS1」に変わることを確認します。

10. 左上隅のナビゲーション ボタンを選択し、**Apps** を選択します。

    > Apps ページに Windows App が表示されていることを確認します。表示されるまで数分かかる場合があります。

11. **Windows App** を選択します。
12. Windows App ページで、**Install** を選択します。
13. 求められた場合は、**Install Windows App** ダイアログで **Always allow portal.manage.microsoft.com to open links of this type in the associated app** をオンにし、**Open** を選択します。

    > アプリのインストールには数分かかる場合があります。

14. アプリのインストール後、開いているすべてのウィンドウを閉じます。
15. **Start** を選択し、Start メニューに **Windows App** が表示されていることを確認します。

**結果**: この演習を完了すると、Microsoft Store アプリを Intune に追加し、正常にインストールできます。

## 演習 2: Intune から Microsoft 365 Apps を構成して展開する

### シナリオ

Contoso の Research 部門のすべてのユーザーには Microsoft 365 Apps が必要です。64ビット版の Microsoft Excel、Outlook、PowerPoint、Word を Windows デバイスへ展開します。また、更新チャネルが Current Channel に構成されていることを確認します。

### タスク 1: SEA-WS1 にインストールされているアプリを確認する

1. **SEA-WS1** のタスク バーで **Start** を選択し、**Settings** アプリを選択します。
2. **Settings** アプリで **Apps** を選択し、**Apps & features** を選択します。

   > **Microsoft 365 Apps for enterprise - en-us** が一覧にないことを確認します。

3. 開いているすべてのウィンドウを閉じます。

### タスク 2: Microsoft 365 Apps を Intune に追加する

1. 手元の PC の **Microsoft Intune 管理センター**で、**アプリ** を選択します。
2. **アプリ | 概要** ブレードで **すべてのアプリ** を選択し、詳細ペインで **作成** を選択します。
3. **アプリの種類の選択** ブレードの **Microsoft 365 Apps** で **Windows 10 以降** を選択し、**選択** を選択します。
4. **Microsoft 365 Apps の追加** ブレードで次のオプションを構成し、**次へ** を選択します。
   - スイート名: **Microsoft 365 Apps (Research)**
   - 説明: **Microsoft 365 Apps for the Research dept at Contoso**
5. **アプリ スイートの構成** タブで **Office アプリの選択** ドロップダウンを展開し、次のアプリだけが選択されていることを確認します。
   - Excel
   - Outlook
   - PowerPoint
   - Word
6. **アプリ スイート情報** セクションで、次のオプションを構成します。
   - アーキテクチャ: **64-bit**
   - 既定のファイル形式: **Office Open XML Format**
   - 更新チャネル: **Monthly Enterprise Channel**
7. **プロパティ** セクションで次のオプションを構成し、**次へ** を選択します。
   - ユーザーに代わって Microsoft ソフトウェア ライセンス条項に同意する: **はい**
8. **割り当て** タブの **必須** セクションで、**グループの追加** を選択します。
9. **グループの選択** ブレードで **Research** を選択し、**選択** を選択します。
10. **次へ** を選択します。**確認と作成** タブで、**作成** を選択します。
11. **Microsoft 365 Apps (Research)** ページで、**プロパティ** を選択します。
12. 詳細ペインの **割り当て** セクションで、**必須** の下に **Research** が表示されていることを確認します。

### タスク 3: Intune コンソールからポリシー同期を要求する

1. **Microsoft Intune 管理センター**で **デバイス** を選択し、**すべてのデバイス** を選択します。
2. 詳細ペインで **SEA-WS1** を選択します。
3. **SEA-WS1** ブレードで **同期** を選択し、求められたら **はい** を選択します。

   > Intune はデバイスへ接続し、すべてのポリシーを同期するよう指示します。これには最長15分かかる場合があります。**SEA-WS1** から同期することもできます。

### タスク 4: Microsoft 365 Apps がインストールされたことを確認する

1. **SEA-WS1** に切り替え、Microsoft 365 Suite がデバイスにインストールされるまで約10分から15分待ちます。
2. **SEA-WS1** からサインアウトし、PIN **102938** を使用して **Aaron Nicholls** として再度サインインします。
3. **SEA-WS1** のタスク バーで **Start** を選択し、**Settings** アプリを選択します。
4. **Settings** アプリで **Apps** を選択し、**Apps & features** ページを下にスクロールして、**Microsoft 365 Apps for enterprise - en-us** が一覧に表示されていることを確認します。
5. **Settings** アプリを閉じ、**Start** ボタンを選択します。
6. All apps を選択し、W まで下にスクロールして **Word** を選択し、アプリが起動することを確認します。

   > 注: 以前のラボで、Start メニューから最近追加されたアプリを削除したことを思い出してください。

7. 開いているすべてのウィンドウを閉じます。
8. SEA-WS1 からサインアウトします。

### タスク 5: Intune でアプリのインストール状態を監視する

1. 手元の PC の **Microsoft Intune 管理センター**で、**アプリ** を選択します。
2. **アプリ | 概要** ブレードで、**監視**、**アプリのインストール状態** の順に選択します。
3. 詳細ペインで **Microsoft 365 Apps (Research)** を選択します。
4. 詳細ペインの **監視** にある **ユーザーのインストール状態** で、Installed の下に **1** と表示されていることを確認します。

   > 注: 情報が表示されるまで時間がかかる場合があります。

   > 注: これは、アプリが1台のデバイスに1人のユーザー用としてインストールされたことを示します。

5. **デバイスのインストール状態** を選択します。

   > 詳細ペインでは、アプリがインストールされているデバイスとユーザー名を確認できます。**Device Name** 列に **SEA-WS1**、**Status** 列に **Installed** と表示されていることを確認します。

6. **Microsoft Intune 管理センター**で、**デバイス** を選択します。
7. **デバイス | 概要** ブレードで **すべてのデバイス** を選択し、詳細ペインで **SEA-WS1** を選択します。
8. **SEA-WS1** ブレードで、**マネージド アプリ** を選択します。
9. **SEA-WS1 | マネージド アプリ** ブレードの詳細ペインで、**Microsoft 365 Apps (Research)** を選択します。

   > **Microsoft 365 Apps (Research) - Installation details** ウィンドウでは、アプリケーションの作成、割り当て、インストール時刻と状態、およびデバイスが最後にIntuneへチェックインした時刻を確認できます。

10. 開いているすべてのウィンドウを閉じます。

**結果**: この演習を完了すると、Microsoft 365 Apps を Intune から正常に構成して展開できます。

**ラボ終了**
