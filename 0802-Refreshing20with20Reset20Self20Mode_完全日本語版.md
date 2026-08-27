### lab:
title: 'Practice Lab: Autopilot Reset とセルフ デプロイ モードによる Windows の更新'
description: SEA-WS4 は Windows Autopilot を使用して展開されています。Autopilot Reset を伴う別のプロビジョニング シナリオをテストする必要があります。Windows Autopilot のセルフ デプロイ モードで構成された新しい展開プロファイルを作成します。
duration: 45 minutes
level: 200
islab: true
primarytopics:
- Windows

## Practice Lab: Autopilot Reset とセルフ デプロイ モードによる Windows の更新

### 概要

このラボでは、リモートで Autopilot リセットを実行する方法を学びます。

#### 前提条件

このラボの前に、次のラボを完了しておく必要があります。

- 0101-Managing Identities in Azure AD
- 0102-Synchronizing identities by using Entra Connect
- 0701-Deploying Windows 11 using Microsoft Deployment Toolkit
- 0801-Deploying Windows 11 with Autopilot

#### シナリオ

SEA-WS4 は Windows Autopilot を使用して展開されています。あなたは、Autopilot Reset を伴う別のプロビジョニング シナリオをテストする必要があります。Windows Autopilot のセルフ デプロイ モードで構成された新しい展開プロファイルを作成します。

#### タスク 1: セルフ デプロイの Windows Autopilot 展開プロファイルの構成

1. **SEA-SVR1** に切り替えます。

2. **Microsoft Edge** で新しいタブを開き、[**https://intune.microsoft.com**](https://intune.microsoft.com) に移動します。プロンプトが表示されたら、**Admin@yourtenant.onmicrosoft.com** でサインインします。

3. **Microsoft Intune 管理センター** で、**デバイス** を選択します。

4. **デバイスのオンボード** セクションで、**登録** を選択します。

5. Windows の登録タブで、詳細ペインの **Windows Autopilot** までスクロールし、続いて **展開プロファイル** を選択します。

6. **Windows AutoPilot 展開プロファイル** ブレードで、**Contoso Profile 1** を選択し、続いて **プロパティ** を選択します。

7. **割り当て** までスクロールし、続いて **編集** を選択します。

8. **IT Devices** の横で、**削除** を選択します。

9. **確認と保存** を選択し、続いて **保存** を選択します。

10. **Contoso Profile 1 プロパティ** ページを閉じます。

11. **Windows AutoPilot 展開プロファイル** ブレードで、**プロファイルの作成** を選択し、続いて **Windows PC** を選択します。

12. **基本** タブの **名前** テキスト ボックスに **Contoso profile 2** を入力します。

13. **対象のすべてのデバイスを Autopilot に変換** では **いいえ** を選択し、続いて **次へ** を選択します。

14. **初回起動時のエクスペリエンス (OOBE)** タブで、**展開モード** が **セルフ デプロイ** に設定されていることを確認します。

15. 次のオプションが設定されていることを確認します。

    - 言語 (地域): **オペレーティング システムの既定**
    - キーボードを自動的に構成する: **はい**
    - デバイス名テンプレートの適用: **はい**
    - 名前を入力: **Contoso-%RAND:2%**

16. **次へ** を選択します。

17. **割り当て** タブの **包含されたグループ** で、**グループの追加** を選択します。

18. **IT Devices** グループを選択し、**選択** をクリックします。**次へ** を選択します。

19. **確認と作成** ブレードで情報を確認し、続いて **作成** を選択します。

#### タスク 2: Autopilot リセットの実行

1. **Microsoft Intune 管理センター** で、**デバイス** を選択し、続いて **すべてのデバイス** を選択します。

2. Autopilot PC (名前が DESKTOP で始まるもの) を選択します。

3. メニュー バーで、省略記号を選択し、続いて **Autopilot Reset** を選択します。

4. メッセージのプロンプトで、**はい** を選択します。

5. **SEA-WS3** に切り替えます。

    > 注: SEA-WS3 は前のラボから引き続き実行されているはずです。

6. **SEA-WS3** を再起動します。

    > 注: このプロセスには 30～45 分かかることがあり、その間に数回再起動します。

#### タスク 3: Autopilot 展開の確認

1. サインイン ページで、**Aaron@yourtenant.onmicrosoft.com** をパスワード **Pa55w.rd1234!** で入力します。

2. **Use Windows Hello with your account** で、**OK** を選択します。

3. **Verify your identity** ページで、Text の確認方法を選択します。

4. **Enter code** ページで、モバイル デバイスに送信されたコードを入力し、続いて **Verify** を選択します。

5. **Setup up a PIN** ダイアログ ボックスの **New PIN** および **Confirm PIN** フィールドに **102938** を入力し、続いて **OK** を選択します。

6. **All set!** ページで、**OK** を選択します。

7. **Start** を選択し、**Settings** を選択します。

8. **Accounts** を選択し、続いて **Access work or school** を選択します。デバイスが Contoso の Azure AD に接続されていることを確認します。

9. **Connected to Contoso's Azure AD** を選択し、**Info** を選択します。

10. **Managed by Contoso** ページで、下にスクロールし、続いて **Sync** を選択します。

11. **SEA-WS3** で、**Settings** ウィンドウを閉じます。

**結果**: この演習を完了すると、セルフ デプロイ モードを使用して Autopilot Reset で Windows デバイスをプロビジョニングできています。

**ラボ終了**
