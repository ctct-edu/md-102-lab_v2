---
lab:
  title: '演習ラボ 0602: Intune を使用したディスク暗号化の構成'
  description: このラボでは、Intune を使用して BitLocker ディスク暗号化を構成します。
  duration: 90 minutes
  level: 200
  islab: true
---

# 演習ラボ 0602: Intune を使用したディスク暗号化の構成

## 概要

このラボでは、Intune を使用して BitLocker ディスク暗号化を構成します。

### 前提条件

このラボを開始する前に、次のラボを完了しておく必要があります。

- 0203-Manage Device Enrollment into Intune

- 0204-Enrolling devices into Intune

- 0301-Creating and Deploying Configuration Profiles

  注: Entra ID への Windows Hello サインイン認証を保護するために使用するテキスト メッセージを受信できる携帯電話も必要です。

### シナリオ

SEA-WS1 上のすべての情報を暗号化する必要があります。SEA-WS1 でディスク全体の暗号化を構成し、起動時に追加の PIN 認証を要求するよう依頼されました。

### タスク 1: Intune でデバイス構成ポリシーを構成する

1. 手元の PC で Microsoft Edge を起動します。

2. アドレス バーに **https://intune.microsoft.com** と入力し、**Enter** キーを押します。

3. 既定のテナント パスワードを使用して、**`admin@yourtenant.onmicrosoft.com`** としてサインインします。

4. Microsoft Intune 管理センターで、ナビゲーション バーから **エンドポイント セキュリティ** を選択します。

5. **エンドポイント セキュリティ | 概要** ページで、**ディスク暗号化** を選択します。

6. **エンドポイント セキュリティ | ディスク暗号化** ブレードの詳細ペインで、**ポリシーの作成** を選択します。

7. **プロファイルの作成** ページで次のオプションを選択し、**作成** を選択します。

   - プラットフォーム: **Windows**
   - プロファイル: **BitLocker**

8. **基本** ページで次の情報を入力し、**次へ** を選択します。

   - 名前: **Contoso BitLocker**
   - 説明: **Enable BitLocker for all devices**

9. **構成設定** タブで **BitLocker** を展開し、次のオプションを構成します。

   - Require Device Encryption: **Enabled**

   **注**: 次の手順へ進む前に、**BitLocker** セクションを展開して、このオプションを有効にしたことを確認してください。このオプションを構成しない場合、ポリシーは有効に機能しません。

10. **構成設定** タブで **Operating System Drives** まで下にスクロールし、次のオプションを構成します。その他のオプションは既定値のままにします。

    - Enforce drive encryption type on operating system drives: **Enabled**
    - Require additional authentication at startup: **Enabled**
    - Configure minimum PIN length for startup: **Enabled**
    - Choose how Bitlocker-protected operating system drives can be recovered: **Enabled**
    - Do not enable Bitlocker until recovery information is stored to AD DS for operating system drives: **True**
    - Omit recovery options from the BitLocker setup wizard: **True**
    - Save Bitlocker recovery information to AD DS for operating system drives: **True**

11. **構成設定** ページで、**次へ** を選択します。

12. **スコープ タグ** ページで、**次へ** を選択します。

13. **割り当て** タブで **Contoso** を検索し、**Contoso Developer devices** を選択して、**次へ** を選択します。

14. **確認と作成** ページで、**保存** を選択します。

### タスク 2: BitLocker 設定を確認して有効にする

1. **SEA-WS1** で、PIN **102938** を使用して **Aaron Nicholls** としてサインインします。

2. タスク バーで **Start** を選択し、**Settings** アプリを選択します。

3. **Settings** アプリで **Accounts** を選択し、**Access work or school** を選択します。

4. **Access work or school** セクションで **Connected to Contoso's Azure AD** リンクを選択し、**Info** を選択します。続いて **Sync** を選択します。

5. **Encryption needed** 通知を選択します。

   > 注: 通知が表示されるまで時間がかかる場合があります。Windows Focus Assist によって通知が表示されない場合もあります。通知は手動で確認できます。

6. **Are you ready to start encryption?** ダイアログで、**I don't have any other disk encryption software installed, encrypt all my disks** の横にあるチェック ボックスをオンにし、**Yes** を選択します。

7. **Choose how to unlock your drive at startup?** ページで、**Enter a PIN** を選択します。

8. **Enter a PIN** ページの **PIN** ボックスと **Reenter PIN** ボックスに **123456** と入力し、**Set PIN** を選択します。

9. **Choose how much of your drive to encrypt** ページで、**Encrypt used disk space only** を選択し、**Next** を選択します。

10. **Choose which encryption mode to use** ページで、**New encryption mode (best for fixed drives on this device)** が選択されていることを確認し、**Next** を選択します。

11. **Are you ready to encrypt this drive** ページで、**Continue** を選択します。暗号化が完了するまで待ちます。

12. **Encryption of C: is complete** メッセージで **Close** を選択し、**SEA-WS1** を再起動します。

13. **SEA-WS1** が再起動したら、**123456** と入力し、**Enter** キーを押してドライブのロックを解除します。

### タスク 3: BitLocker 保護を確認する

1. PIN **102938** を使用して、**Aaron Nicholls** として **SEA-WS1** にサインインします。

2. タスク バーで **File Explorer** を選択し、**This PC** を選択します。

3. ナビゲーション ペインで **Local Disk (C:)** を右クリックし、**Show more options**、**Manage BitLocker** の順に選択します。

4. **BitLocker Drive Encryption** ウィンドウで、**C: BitLocker on** の状態が表示されていることを確認します。これは、ドライブが暗号化されていることを示します。

5. 開いているすべてのウィンドウを閉じ、**SEA-WS1** からサインアウトします。

**結果**: この演習を完了すると、Intune を使用したディスク暗号化の構成が正常に完了します。

**ラボ終了**
