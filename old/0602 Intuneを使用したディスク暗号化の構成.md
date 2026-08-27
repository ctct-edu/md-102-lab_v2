---
lab:
  title: '演習ラボ 0602: Intuneを使用したディスク暗号化の構成'
  description: このラボでは、Intuneを使用してBitLockerディスク暗号化を構成します。
  duration: 90 minutes
  level: 200
  islab: true
---

# 演習ラボ 0602: Intuneを使用したディスク暗号化の構成

## 概要

このラボでは、Intuneを使用してBitLockerディスク暗号化を構成します。

### 前提条件

このラボを開始する前に、0203、0204、0301の各ラボを完了しておく必要があります。

> 注: Entra IDへのWindows Helloサインイン認証に使用するテキスト メッセージを受信できる携帯電話も必要です。

### シナリオ

SEA-WS1上のすべての情報を暗号化します。SEA-WS1でディスク全体の暗号化を構成し、起動時に追加のPIN認証を要求します。

### タスク 1: Intuneでデバイス構成ポリシーを構成する

1. 手元のPCでMicrosoft Edgeを起動し、**https://intune.microsoft.com**を開いてテナント管理者でサインインします。
2. Microsoft Intune管理センターのナビゲーション バーで、**エンドポイント セキュリティ**を選択します。
3. **エンドポイント セキュリティ | 概要**ページで、**ディスク暗号化**を選択します。
4. **エンドポイント セキュリティ | ディスク暗号化**ブレードの詳細ペインで、**ポリシーの作成**を選択します。
5. **プロファイルの作成**ページで次のオプションを選択し、**作成**を選択します。
   - プラットフォーム: **Windows**
   - プロファイル: **BitLocker**
6. **基本**ページで次の情報を入力し、**次へ**を選択します。
   - 名前: **Contoso BitLocker**
   - 説明: **Enable BitLocker for all devices**
7. **構成設定**タブで**BitLocker**を展開し、次のオプションを構成します。
   - デバイスの暗号化を必須にする: **有効**
   > **注**: 次の手順へ進む前に、**BitLocker**セクションを展開してこのオプションを有効にしてください。この設定がないとポリシーは機能しません。
8. **構成設定**タブを**オペレーティング システム ドライブ**まで下へスクロールし、ほかの設定は既定値のまま、次のオプションを構成します。
   - オペレーティング システム ドライブの暗号化の種類を適用する: **有効**
   - 起動時に追加の認証を要求する: **有効**
   - 起動時のPINの最小長を構成する: **有効**
   - BitLockerで保護されたオペレーティング システム ドライブの回復方法を選択する: **有効**
   - 回復情報がAD DSに保存されるまでBitLockerを有効にしない: **True**
   - BitLockerセットアップ ウィザードに回復オプションを表示しない: **True**
   - オペレーティング システム ドライブのBitLocker回復情報をAD DSへ保存する: **True**
9. **構成設定**ページで、**次へ**を選択します。
10. **スコープ タグ**ページで、**次へ**を選択します。
11. **割り当て**タブで**Contoso**を検索し、**Contoso Developer devices**を選択して、**次へ**を選択します。
13. **確認と作成**ページで、**保存**を選択します。
14. **SEA-SVR1**で開いているすべてのウィンドウを閉じます。

### タスク 2: BitLocker設定を確認して有効にする

1. **SEA-WS1**で、PIN **102938**を使用して**Aaron Nicholls**としてサインインします。
2. タスク バーで**Start**、**Settings**の順に選択します。
3. **Settings**で**Accounts**、**Access work or school**の順に選択します。
4. **Connected to Contoso's Azure AD**リンク、**Info**、**Sync**の順に選択します。
5. **Encryption needed**通知を選択します。
   _注: 通知が表示されるまで時間がかかる場合があります。Windows Focus Assistによって通知が表示されない場合は、通知を手動で確認できます。_
6. **Are you ready to start encryption?**ダイアログで、**I don't have any other disk encryption software installed, encrypt all my disks**をオンにし、**Yes**を選択します。
7. **Choose how to unlock your drive at startup?**ページで、**Enter a PIN**を選択します。
8. **Enter a PIN**ページの**PIN**と**Reenter PIN**に**123456**と入力し、**Set PIN**を選択します。
9. **Choose how much of your drive to encrypt**ページで、**Encrypt used disk space only**、**Next**の順に選択します。
11. **Choose which encryption mode to use**ページで、**New encryption mode (best for fixed drives on this device)**が選択されていることを確認し、**Next**を選択します。
12. **Are you ready to encrypt this drive**ページで、**Continue**を選択します。暗号化が完了するまで待ちます。
13. **Encryption of C: is complete**メッセージで**Close**を選択し、**SEA-WS1**を再起動します。
14. **SEA-WS1**が再起動したら、**123456**と入力して**Enter**キーを押し、ドライブのロックを解除します。

### タスク 3: BitLocker保護を確認する

1. PIN **102938**を使用して、**Aaron Nicholls**として**SEA-WS1**にサインインします。
2. タスク バーで**File Explorer**、**This PC**の順に選択します。
3. ナビゲーション ペインで**Local Disk (C:)**を右クリックし、**Show more options**、**Manage BitLocker**の順に選択します。
4. **BitLocker Drive Encryption**ウィンドウに**C: BitLocker on**と表示されていることを確認します。これはドライブが暗号化されていることを示します。
5. 開いているすべてのウィンドウを閉じ、**SEA-WS1**からサインアウトします。

**結果**: この演習を完了すると、Intuneを使用したディスク暗号化の構成が完了します。

**ラボ終了**
