### lab:
title: '演習ラボ 0302: 構成ポリシーを使用したキオスク モードの構成'
description: このラボでは、Microsoft Intune を使用して構成ポリシーを作成して適用し、Windows 11 デバイスを単一アプリのキオスク モードで実行します。
duration: 30 minutes
level: 200
islab: true
primarytopics:
\- Microsoft Intune
\- Windows
\- Windows 11

## 演習ラボ 0302: 構成ポリシーを使用したキオスク モードの構成

### 概要

このラボでは、Microsoft Intune を使用して構成ポリシーを作成して適用し、Windows 11 デバイスを単一アプリのキオスク モードで実行します。

#### 前提条件

このラボを開始する前に、次のラボを完了しておく必要があります。
- 0203-Manage Device Enrollment into Intune  
注: Microsoft Entra ID への Windows Hello サインイン認証を保護するために使用するテキスト メッセージを受信できる携帯電話も必要です。

### 演習 1: 構成ポリシーの作成と適用

#### シナリオ

Contoso の訪問者がインターネットを閲覧できるように、SEA-WS2 を Windows 11 キオスクとして構成するよう依頼されました。キオスクが次のように構成されていることを確認する必要があります。
- 単一アプリの全画面キオスク
- 自動ログオン
- Public Browsing (InPrivate) モードに構成した Microsoft Edge ブラウザーへのアクセスを提供し、ホーム ページを [https://bing.com](https://bing.com) に設定

#### タスク 1: SEA-WS2 を Microsoft Intune に登録する
1. **SEA-WS2** に **Admin** として、パスワード **Pa55w.rd** を使用してサインインします。

2. **Start**を選択し、**Settings**を選択します。

3. **Settings**で、**Accounts**を選択します。

4. **Accounts**ページで、**Access work or school**を選択します。

5. **Access work or school**ページで、**Connect**を選択します。

6. **Microsoft account**ウィンドウで、**Join this device to Microsoft Entra ID**を選択します。

7. **Sign in**ページで、**AllanD@yourtenant.onmicrosoft.com** と入力し、**Next**を選択します。

8. **Enter password**ページでユーザーのパスワードを入力し、**Sign in**を選択します。

9. **Make sure this is your organization**ダイアログ ボックスで、**Join**を選択します。

10. **You're all set\!**ページの情報を読み、**Done**を選択します。

11. **Access work or school**セクションに **Connected to Contoso's Azure AD** と表示されていることを確認します。

12. **Connected to Contoso's Azure AD**を選択し、**Info**を選択します。

13. 下へスクロールして **Sync**を選択し、Intune とのデバイス同期を強制的に実行します。

14. **Settings**ウィンドウを閉じます。

#### タスク 2: Contoso Kiosk デバイス グループを作成する
1. 手元 PC で Microsoft Edge を開き、[**https://intune.microsoft.com**](https://intune.microsoft.com) にアクセスします。

2. テナント管理者のパスワードを使用して、**admin@yourtenant.onmicrosoft.com** としてサインインします。

3. Microsoft Intune 管理センターのナビゲーション ペインで、**グループ**を選択します。

4. **グループ | すべてのグループ**ブレードで、**新しいグループ**を選択します。

5. **新しいグループ**ブレードで、次の情報を入力します。

   - グループの種類: **セキュリティ**
   - グループ名: **Contoso Kiosk Devices**
   - グループの説明: **All Windows devices configured as a Kiosk**
   - メンバーシップの種類: **割り当て済み**

6. **メンバー**で、**メンバーが選択されていません**を選択します。

7. **メンバーの追加**ブレードの**検索**ボックスに **Sea** と入力します。**SEA-WS2**を選択し、**選択**を選択します。

8. **新しいグループ**ブレードで、**作成**を選択します。

9. **グループ | すべてのグループ**ブレードに **Contoso Kiosk Devices** グループが表示されていることを確認します。新しいグループを表示するには、**更新**ボタンの選択が必要な場合があります。

#### タスク 3: シナリオの要件に基づいて構成ポリシーを作成する
1. Microsoft Intune 管理センターのナビゲーション バーで、**デバイス**を選択します。

2. **デバイス**ページの**デバイスの管理**セクションで、**構成**を選択します。

3. **デバイス | 構成**ブレードの詳細ペインで、**作成**、**新しいポリシー**の順に選択します。

4. **プロファイルの作成**ブレードで次のオプションを選択し、**作成**を選択します。

   - プラットフォーム: **Windows 10 以降**
   - プロファイルの種類: **テンプレート**
   - テンプレート名: **キオスク**

5. **基本**ブレードで次の情報を入力し、**次へ**を選択します。

   - 名前: **Contoso Kiosk Policy**
   - 説明: **Basic settings for Contoso Kiosk Devices.**

6. **構成設定**ブレードの**キオスク モードを選択**の横で、**単一アプリの全画面キオスク**を選択します。<br>選択したモードに応じて追加のオプションが表示されます。

7. **構成設定**ブレードで次のオプションを選択し、キオスク URL を必ず上書きしてから、**次へ**を選択します。

   - ユーザー ログオンの種類: **自動ログオン (Windows 10 バージョン 1803 以降、または Windows 11)**
   - アプリケーションの種類: **Microsoft Edge ブラウザーの追加**
   - Edge キオスク URL: [**https://bing.com**](https://bing.com)
   - Microsoft Edge キオスク モードの種類: **パブリック ブラウズ (InPrivate)**
   - アイドル時間後にブラウザーを更新する: **5**
   - アプリの再起動のメンテナンス期間を指定する: **構成されていません**

8. **割り当て**ブレードの**包含されたグループ**で、**グループの追加**を選択します。

9. **含めるグループの選択**ウィンドウで、**Contoso Kiosk Devices**を選択し、**選択**を選択します。

10. **確認と作成**ブレードが表示されるまで **次へ**を 2 回選択し、**作成**を選択します。

11. Microsoft Edge を閉じます。

#### タスク 4: 構成ポリシーが適用されていることを確認する
1. **SEA-WS2** に切り替えます。

2. **SEA-WS2** のタスク バーで、**Start**、**Settings**の順に選択します。

3. **Settings**で、**Accounts**、**Access work or school**の順に選択します。

4. **Access work or school**セクションで、**Connected to Contoso's Azure AD**リンクを選択し、**Info**を選択します。

5. **Managed by Contoso**ページを下へスクロールし、Device sync status で **Sync**を選択します。同期が完了するまで待ちます。<br>**注**: キオスク ポリシーが同期可能になるまで 5～10 分かかることがあります。**Sync**を選択する前に 5～10 分待つことをお勧めします。

6. **Settings**アプリを閉じます。

7. **SEA-WS2**を再起動します。<br>SEA-WS2 が自動的にサインインし、ユーザー プロファイルが作成されることを確認します。サインインが完了すると、InPrivate ブラウズが構成された Microsoft Edge が表示されます。SEA-WS2 が自動的にサインインしない場合は、手順 1～7 を繰り返して、デバイス上でポリシーが更新されたことを確認します。

**結果**: この演習では、Windows 11 デバイスを単一アプリ キオスクとして構成するための構成ポリシーを作成し、割り当てました。  
**ラボ終了**
