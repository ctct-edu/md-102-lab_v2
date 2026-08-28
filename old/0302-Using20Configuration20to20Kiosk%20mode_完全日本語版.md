---
lab:
    title: '演習ラボ 0302: 構成ポリシーを使用したキオスク モードの構成'
    description: このラボでは、Microsoft Intune を使用して、Windows 11 デバイスで単一アプリのキオスク モードを実行するための構成ポリシーを作成して適用します。
    duration: 30 minutes
    level: 200
    islab: true
    primarytopics:
    - Microsoft Intune
    - Windows
    - Windows 11
---

## 演習ラボ 0302: 構成ポリシーを使用したキオスク モードの構成

### 概要

このラボでは、Microsoft Intune を使用して、Windows 11 デバイスで単一アプリのキオスク モードを実行するための構成ポリシーを作成して適用します。

#### 前提条件

このラボの前に、次のラボを完了しておく必要があります。

- 0203-Manage Device Enrollment into Intune

注: また、Entra ID への Windows Hello サインイン認証を保護するために使用されるテキスト メッセージを受信できる携帯電話も必要です。

### 演習 1: 構成ポリシーの作成と適用

#### シナリオ

Contoso の訪問者がインターネットを閲覧できるように、**SEA-WS2** を Windows 11 のキオスクとして構成するよう依頼されました。キオスクが次のように構成されていることを確認する必要があります。

- 単一アプリのフルスクリーン キオスク。
- 自動ログオン。
- Public Browsing (InPrivate) モードで構成する Microsoft Edge ブラウザーへのアクセスを提供します。ホーム ページは [https://bing.com](https://bing.com) に構成する必要があります。

#### タスク 1: SEA-WS2 を Microsoft Intune に登録する

1. **SEA-WS2** に、**Admin** としてパスワード **Pa55w.rd** でサインインします。

2. **Start** を選択し、続いて **Settings** を選択します。

3. **Settings** で、**Accounts** を選択します。

4. **Accounts** ページで、**Access work or school** を選択します。

5. **Access work or school** ページで、**Connect** を選択します。

6. **Microsoft account** ウィンドウで、**Join this device to Microsoft Entra ID** を選択します。

7. **Sign in** ページで、**AllanD@yourtenant.onmicrosoft.com** と入力し、**Next** を選択します。

8. **Enter password** ページで、ユーザーのパスワードを入力し、**Sign in** を選択します。

9. **Make sure this is your organization** ダイアログ ボックスで、**Join** を選択します。

10. **You're all set!** ページで、情報を読んで **Done** を選択します。

11. **Access work or school** セクションで、**Connected to Contoso's Azure AD** が表示されることを確認します。

12. **Connected to Contoso's Azure AD** を選択し、続いて **Info** を選択します。

13. 下にスクロールし、**Sync** を選択します。これにより、Intune とのデバイス同期が強制されます。

14. **Settings** ウィンドウを閉じます。

#### タスク 2: Contoso Kiosk デバイス グループの作成

1. **SEA-SVR1** に切り替え、**Contoso\Administrator** としてパスワード **Pa55w.rd** でサインインします。**Server Manager** を閉じます。

2. **SEA-SVR1** のタスク バーで、**Microsoft Edge** を選択します。

3. **Microsoft Edge** のアドレス バーに [**https://intune.microsoft.com**](https://intune.microsoft.com) と入力し、**Enter** キーを押します。

4. **admin@yourtenant.onmicrosoft.com** として、テナントの Admin パスワードでサインインします。

5. Microsoft Intune 管理センターのナビゲーション ペインで、**グループ** を選択します。

6. **グループ | すべてのグループ** ブレードで、**新しいグループ** を選択します。

7. **新しいグループ** ブレードで、次の情報を入力します。

   - グループの種類: **セキュリティ**
   - グループ名: **Contoso Kiosk Devices**
   - グループの説明: **All Windows devices configured as a Kiosk**
   - メンバーシップの種類: **割り当て済み**

8. **メンバー** の下で、**メンバーが選択されていません** を選択します。

9. **メンバーの追加** ブレードの **検索** ボックスに **Sea** と入力します。**SEA-WS2** を選択し、続いて **選択** を選びます。

10. **新しいグループ** ブレードで、**作成** を選択します。

11. **グループ | すべてのグループ** ブレードで、**Contoso Kiosk Devices** グループが表示されていることを確認します。新しいグループが表示されるようにするには、**更新** ボタンを選択する必要がある場合があります。

#### タスク 3: シナリオ要件に基づく構成ポリシーの作成

1. Microsoft Intune 管理センターで、ナビゲーション バーから **デバイス** を選択します。

2. **デバイス** ページで、**デバイスの管理** セクションの **構成** を選択します。

3. **デバイス | 構成** ブレードの詳細ペインで、**+ 作成** を選択し、続いて **+ 新しいポリシー** を選択します。

4. **プロファイルの作成** ブレードで、次のオプションを選択し、**作成** を選択します。

   - プラットフォーム: **Windows 10 以降**
   - プロファイルの種類: **テンプレート**
   - テンプレート名: **Kiosk**

5. **基本** ブレードで、次の情報を入力し、**次へ** を選択します。

   - 名前: **Contoso Kiosk Policy**
   - 説明: **Basic settings for Contoso Kiosk Devices.**

6. **構成設定** ブレードで、**キオスク モードの選択** の横で、**単一アプリ、フルスクリーン キオスク** を選択します。

   > 選択したモードに基づいて、追加のオプションが表示されます。

7. **構成設定** ブレードで、次のオプションを選択し (キオスク URL を必ず上書きしてください)、**次へ** を選択します。

   - ユーザー ログオンの種類: **自動ログオン (Windows 10 バージョン 1803 以降、または Windows 11)**
   - アプリケーションの種類: **Microsoft Edge ブラウザーの追加**
   - Edge キオスク URL: [**https://bing.com**](https://bing.com)
   - Microsoft Edge キオスク モードの種類: **パブリック ブラウジング (InPrivate)**
   - アイドル時間後にブラウザーを更新: **5**
   - アプリ再起動のメンテナンス期間の指定: **構成されていません**

8. **割り当て** ブレードで、**包含されたグループ** の下の **グループの追加** を選択します。

9. **含めるグループの選択** ウィンドウで、**Contoso Kiosk Devices** を選択し、**選択** をクリックします。

10. **確認と作成** ブレードに到達するまで、**次へ** を 2 回選択します。**作成** を選択します。

11. **Microsoft Edge** を閉じます。

#### タスク 4: 構成ポリシーが適用されていることの確認

1. **SEA-WS2** に切り替えます。

2. **SEA-WS2** のタスク バーで、**Start** を選択し、続いて **Settings** を選択します。

3. **Settings** で、**Accounts** を選択し、続いて **Access work or school** を選択します。

4. **Access work or school** セクションで、**Connected to Contoso's Azure AD** リンクを選択し、続いて **Info** を選択します。

5. **Managed by Contoso** ページで下にスクロールし、**Device sync status** の下の **Sync** を選択します。同期が完了するまで待ちます。

   > **注**: キオスク ポリシーが同期で利用可能になるまでに 5～10 分かかる場合があります。**Sync** を選択する前に、5～10 分待つとよいでしょう。

6. **Settings** アプリを閉じます。

7. **SEA-WS2** を再起動します。

   > SEA-WS2 が自動的にサインインし、ユーザー プロファイルを作成することに注意してください。サインインが完了すると、InPrivate ブラウジングで構成された Microsoft Edge が表示されます。SEA-WS2 が自動的にサインインしない場合は、手順 1 ～ 7 を繰り返して、ポリシーがデバイスで更新されていることを確認します。

**結果**: この演習を完了すると、Windows 11 デバイスを単一アプリのキオスクとして構成するための構成ポリシーを正常に作成して割り当てられています。

**ラボ終了**
