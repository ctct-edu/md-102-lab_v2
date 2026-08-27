### lab:
title: '演習ラボ 0602: Intune を使用したディスク暗号化の構成'
description: このラボでは、Intune を使用して BitLocker ディスク暗号化を構成します。
duration: 90 minutes
level: 200
islab: true

## 演習ラボ 0602: Intune を使用したディスク暗号化の構成

### 概要

このラボでは、Intune を使用して BitLocker ディスク暗号化を構成します。

#### 前提条件

このラボを開始する前に、次のラボを完了しておく必要があります。
- 0203-Intune へのデバイス登録の管理
- 0204-Intune へのデバイスの登録
- 0301-構成プロファイルの作成と展開

> **注:** Entra ID に対する Windows Hello サインイン認証の保護に使用するテキスト メッセージを受信できる携帯電話も必要です。

#### シナリオ

SEA-WS1 上のすべての情報を暗号化する必要があると判断されました。SEA-WS1 でディスク全体の暗号化を構成し、起動時に追加の PIN 認証を要求するよう依頼されました。

#### タスク 1: Intune でデバイス構成ポリシーを構成する

1. 手元の PC で日本語版 Microsoft Edge を起動し、[**https://intune.microsoft.com**](https://intune.microsoft.com) にアクセスします。

2. **admin@yourtenant.onmicrosoft.com** と既定のテナント パスワードを使用してサインインします。

3. Microsoft Intune 管理センターのナビゲーション バーで、**エンドポイント セキュリティ**を選択します。

4. **エンドポイント セキュリティ | 概要**ページで、**ディスク暗号化**を選択します。

5. **エンドポイント セキュリティ | ディスク暗号化**ブレードの詳細ペインで、**ポリシーの作成**を選択します。

6. **プロファイルの作成**ページで次のオプションを選択し、**作成**を選択します。
   - プラットフォーム: **Windows**
   - プロファイル: **BitLocker**

7. **基本**ページで次の情報を入力し、**次へ**を選択します。
   - 名前: **Contoso BitLocker**
   - 説明: **Enable BitLocker for all devices**

8. **構成設定**タブで **BitLocker**を展開し、次のオプションを構成します。
   - デバイスの暗号化を要求: **有効**

    > **注:** 次の手順に進む前に、**BitLocker**セクションを展開してオプションを有効にしたことを確認してください。このオプションを構成しないと、ポリシーは有効になりません。

9. **構成設定**タブで **オペレーティング システム ドライブ**まで下へスクロールし、ほかのオプションは既定値のまま、次のオプションを構成します。
   - オペレーティング システム ドライブのドライブ暗号化の種類を適用: **有効**
   - 起動時に追加の認証を要求: **有効**
   - 起動時の PIN の最小長を構成: **有効**
   - BitLocker で保護されたオペレーティング システム ドライブの回復方法を選択: **有効**
   - オペレーティング システム ドライブの回復情報が AD DS に保存されるまで BitLocker を有効にしない: **True**
   - BitLocker セットアップ ウィザードから回復オプションを省略: **True**
   - オペレーティング システム ドライブの BitLocker 回復情報を AD DS に保存: **True**

10. **構成設定**ページで、**次へ**を選択します。

11. **スコープ タグ**ページで、**次へ**を選択します。

12. **割り当て**タブで **Contoso**を検索し、**Contoso Developer devices**を選択して、**次へ**を選択します。

13. **確認と作成**ページで、**保存**を選択します。

14. 手元の PC で開いている Microsoft Intune 管理センターのウィンドウを閉じます。

#### タスク 2: BitLocker 設定を検証して有効にする

1. **SEA-WS1** で、PIN **102938** を使用して **Aaron Nicholls** としてサインインします。

2. タスク バーで **Start**を選択し、**Settings**アプリを選択します。

3. **Settings**アプリで **Accounts**、**Access work or school**の順に選択します。

4. **Access work or school**セクションで **Connected to Contoso's Azure AD**リンクを選択し、**Info**を選択して、**Sync**を選択します。

5. **Encryption needed**通知を選択します。

    > **注:** 通知が表示されるまで時間がかかる場合があります。また、Windows Focus Assist によって通知が表示されない場合があります。その場合は、通知を手動で確認できます。

6. **Are you ready to start encryption?**ダイアログで、**I don't have any other disk encryption software installed, encrypt all my disks**の横にあるチェック ボックスをオンにし、**Yes**を選択します。

7. **Choose how to unlock your drive at startup?**ページで、**Enter a PIN**を選択します。

8. **Enter a PIN**ページの **PIN**ボックスと **Reenter PIN**ボックスに **123456** と入力し、**Set PIN**を選択します。

9. **Choose how much of your drive to encrypt**ページで **Encrypt used disk space only**を選択し、**Next**を選択します。

10. **Choose which encryption mode to use**ページで **New encryption mode (best for fixed drives on this device)**が選択されていることを確認し、**Next**を選択します。

11. **Are you ready to encrypt this drive**ページで **Continue**を選択し、暗号化が完了するまで待ちます。

12. **Encryption of C: is complete**というメッセージが表示されたら **Close**を選択し、**SEA-WS1**を再起動します。

13. **SEA-WS1**が再起動したら、ドライブのロックを解除するために **123456** と入力し、**Enter**キーを押します。

#### タスク 3: BitLocker 保護を検証する

1. **SEA-WS1** で、PIN **102938** を使用して **Aaron Nicholls** としてサインインします。

2. タスク バーで **File Explorer**を選択し、**This PC**を選択します。

3. ナビゲーション ペインで **Local Disk (C:)**を右クリックし、**Show more options**、**Manage BitLocker**の順に選択します。

4. **BitLocker Drive Encryption**ウィンドウで、状態が **C: BitLocker on**と表示されていることを確認します。これは、ドライブが暗号化されていることを示します。

5. 開いているすべてのウィンドウを閉じ、**SEA-WS1**からサインアウトします。

**結果:** この演習では、Intune を使用してディスク暗号化を正常に構成しました。

**ラボ終了**
