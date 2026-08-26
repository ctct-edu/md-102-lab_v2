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

  > 注: Entra ID への Windows Hello サインイン認証を保護するために使用するテキスト メッセージを受信できる携帯電話も必要です。

## 演習 1: Microsoft Store アプリを Intune に追加する

### シナリオ

Microsoft Intune を使用して、Contoso Corporation のデスクトップとアプリを管理しています。Research 部門から、必要に応じてメンバーが Windows App をインストールできるようにする依頼を受けました。ユーザーが Company Portal Web サイトからアクセスできるように、Windows App を Intune へ追加します。Aaron Nicholls が、アプリ公開後のインストール処理をテストします。

### タスク 1: Windows App を Intune に追加する

1. 必要に応じて、パスワード **Pa55w.rd** を使用して **Contoso\\Administrator** として **SEA-SVR1** にサインインし、**Server Manager** を閉じます。

2. タスク バーで **Microsoft Edge** を選択します。

3. Microsoft Edge のアドレス バーに **https://intune.microsoft.com** と入力し、**Enter** キーを押します。

4. テナント管理者のパスワードを使用して、**`admin@yourtenant.onmicrosoft.com`** としてサインインします。

5. **Microsoft Intune 管理センター**ページで、**アプリ**を選択します。

6. **アプリ**ページのナビゲーション ペインで、**すべてのアプリ**を選択します。

7. 詳細ペインで、**作成**を選択します。

8. **アプリの種類の選択**ページでドロップダウン メニューを選択し、**Microsoft store app (new)** を選択して、**選択**を選択します。

9. **アプリの追加**ページで **Search the Microsoft Store app (new)** を選択し、**Windows App** を検索して選択した後、**選択**を選択します。

10. **App information** ページで、 verify the following information 続いて **次へ**:
    - Name: **Windows App**
    - Publisher: **Microsoft Corp.**
    - Category: **Business**
    - Show this as a featured app: **はい**

11. **次へ**を2回選択し、**作成**を選択します。

12. Windows App のページが開きます。

    > **プロパティ**、**デバイスのインストール状態**、**ユーザーのインストール状態**の各ノードを確認します。

### タスク 2: アプリにグループを割り当てる

1. **Windows App** ページの **管理**で、**プロパティ**を選択します。

2. details ペインで、 scroll down to the **割り当て** section 続いて **Edit**.

3. **割り当て**ページの **登録済みデバイスで使用可能**で、**グループの追加**を選択します。

4. **グループの選択**ページで **Research** グループを検索して選択し、**選択**を選択します。

5. **確認と保存**を選択し、**保存**を選択します。

### タスク 3: Intune コンソールからポリシー同期を強制する

1. **Microsoft Intune 管理センター**で、**デバイス**、**すべてのデバイス**の順に選択します。

2. details ペインで、 **SEA-WS1**.

3. **SEA-WS1** blade, **同期** and when prompted **はい**.

   > Intune はデバイスへ接続し、すべてのポリシーを同期するよう指示します。これには最長5分かかる場合があります。


### タスク 4: Company Portal Web サイトからアプリをインストールする

1. **SEA-WS1** に切り替えます。

2. Sign in as **Aaron Nicholls** with the PIN **102938**.

3. タスク バーで **Microsoft Edge** を選択します。

4. 必要に応じて、**Welcome to Microsoft Edge** ページで **Confirm and continue** を選択し、Welcome ページを閉じます。

5. アドレス バーに **https://portal.manage.microsoft.com** と入力し、**Enter** キーを押します。

6. Sign in as **Aaron Nicholls**.

7. Contoso Web ポータルで **View Devices** を選択します。

8. Devices ページで **Tap here to tell us which device you're using or add a new device** を選択します。

9. **Which device are you using** ダイアログで **SEA-WS1** の横にあるオプションを選択し、**Select** を選択します。

   > メッセージが Apps will be installed onto: SEA-WS1 に変わることを確認します。

10. 左上隅のナビゲーション ボタンを選択し、**Apps** を選択します。

   > Apps ページに Windows App が表示されていることを確認します。表示されるまで数分かかる場合があります。

11. **Windows App** を選択します。

12. Windows App ページで **Install** を選択します。

13. 求められた場合は、**Install Windows App** ダイアログで **Always allow portal.manage.microsoft.com to open links of this type in the associated app** をオンにし、**Open** を選択します。

   >It may take a few minutes for the app to install.

14. アプリのインストール後、開いているすべてのウィンドウを閉じます。

15. **Start** を選択し、Start メニューに **Windows App** が表示されていることを確認します。

**結果**: この演習を完了すると、Microsoft Store アプリを Intune に追加し、正常にインストールできます。

## 演習 2: Intune から Microsoft 365 Apps を構成して展開する

### シナリオ

Contoso の Research 部門のすべてのユーザーには Microsoft 365 Apps が必要です。64ビット版の Microsoft Excel、Outlook、PowerPoint、Word を Windows デバイスへ展開し、更新チャネルを Current Channel に構成します。

### タスク 1: SEA-WS1 にインストールされたアプリを確認する

1. **SEA-WS1** のタスク バーで **Start**、**Settings** の順に選択します。

2. **Settings** アプリで **Apps**、**Apps & features** の順に選択します。

   > **Microsoft 365 Apps for enterprise - en-us** が一覧にないことを確認します。

3. 開いているすべてのウィンドウを閉じます。

### タスク 2: Microsoft 365 Apps を Intune に追加する

1. 手元の PC の **Microsoft Intune 管理センター**で **アプリ**を選択します。

2. **Apps | Overview** blade, **All Apps**. details ペインで、 **作成**.

3. **アプリの種類の選択**ブレードの **Microsoft 365 Apps** で **Windows 10 以降**を選択し、**選択**を選択します。

4. **Add Microsoft 365 Apps** blade, configure the following options and **次へ**:

    - Suite Name: **Microsoft 365 Apps (Research)**

    - Description: **Microsoft 365 Apps for the Research dept at Contoso**

5. **アプリ スイートの構成**タブで **Office アプリの選択**ドロップダウンを展開し、次のアプリだけが選択されていることを確認します。

    - Excel

    - Outlook

    - PowerPoint

    - Word

6. **App suite information** section, configure the following options:

     - Architecture: **64-bit**

     - Default file format: **Office Open XML Format**

     - Update channel: **Monthly Enterprise Channel**

7. **Properties** section, configure the following options and **次へ**:

     - Accept the Microsoft Software License Terms on behalf of users: **はい**
     
8. **割り当て**タブの **必須**セクションで、**グループの追加**を選択します。

9. **グループの選択**ブレードで **Research** を選択し、**選択**を選択します。

10. **次へ**を選択し、**確認と作成**タブで **作成**を選択します。

11. **Microsoft 365 Apps (Research)** ページで、 **Properties**.

12. 詳細ペインの **割り当て**セクションで、**必須**の下に **Research** が表示されていることを確認します。

### タスク 3: Intune コンソールからポリシー同期を要求する

1. **Microsoft Intune 管理センター**で、**デバイス**、**すべてのデバイス**の順に選択します。

2. details ペインで、 **SEA-WS1**.

3. **SEA-WS1** blade, **同期** and when prompted **はい**.

   > Intune はデバイスへ接続し、すべてのポリシーを同期するよう指示します。これには最長15分かかる場合があります。**SEA-WS1** から同期することもできます。

### タスク 4: Microsoft 365 Apps がインストールされたことを確認する

1. **SEA-WS1** に切り替え、Microsoft 365 Suite がデバイスにインストールされるまで約10分から15分待ちます。

2. **SEA-WS1** からサインアウトし、PIN **102938** を使用して **Aaron Nicholls** として再度サインインします。

3. **SEA-WS1** のタスク バーで **Start**、**Settings** の順に選択します。

4. **Settings** アプリで **Apps** を選択し、**Apps & features** ページを下にスクロールして、**Microsoft 365 Apps for enterprise - en-us** が一覧に表示されていることを確認します。

5. **Settings** アプリを閉じ、**Start** ボタンを選択します。

6. All apps を選択し、W まで下にスクロールして **Word** を選択し、アプリが起動することを確認します。

   > _Note: Recall in a previous lab, you removed recently added apps from the Start Menu._

7. 開いているすべてのウィンドウを閉じます。

8. Sign out of SEA-WS1.

### タスク 5: Intune でアプリのインストール状態を監視する

1. Switch to **SEA-SVR1**.

2. **Microsoft Intune admin center**, **Apps**.

3. **Apps | Overview** blade, **Monitor** 続いて **App install status**.

4. details ペインで、 **Microsoft 365 Apps \(Research\)**.

5. 詳細ペインの **監視**にある **ユーザーのインストール状態**で、Installed の下に **1** と表示されていることを確認します。

   _Note: It may take some time for the information to display._
   
   _注: これは、アプリが1台のデバイスに1人のユーザー用としてインストールされたことを示します。_

6. **デバイスのインストール状態**を選択します。

   > 詳細ペインでは、アプリがインストールされているデバイスとユーザー名を確認できます。**Device Name** 列に **SEA-WS1**、**Status** 列に **Installed** と表示されていることを確認します。これは、アプリが SEA-WS1 にインストールされていることを示します。

7. **Microsoft Intune admin center**, **デバイス**.

8. **デバイス | 概要**ブレードで **すべてのデバイス**を選択し、詳細ペインで **SEA-WS1** を選択します。

9. **SEA-WS1** blade, **Managed Apps**.

10. **SEA-WS1 | マネージド アプリ**ブレードの詳細ペインで、**Microsoft 365 Apps (Research)** を選択します。

   > **Microsoft 365 Apps (Research) - Installation details** window, you can see the entire lifecycle of the application, that is - when it was created, assigned, installation time and status and the last time the device checked in (synced with Intune).

11. 開いているすべてのウィンドウを閉じます。

**結果**: この演習を完了すると、Microsoft 365 Apps を Intune から正常に構成して展開できます。

**ラボ終了**
