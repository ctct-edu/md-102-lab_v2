---
lab:
  title: 'Practice Lab: Refreshing Windows with Autopilot Reset and Self-Deploying mode'
  description: SEA-WS4 has been deployed by using Windows Autopilot. You need to test out another provisioning scenario that involves Autopilot Reset. You will create a new deployment profile configured with the Windows Autopilot Self-Deploying mode.
  duration: 45 minutes
  level: 200
  islab: true
  primarytopics:
    - Windows
---

# 演習ラボ: Autopilot Reset と自己展開モードを使用した Windows の更新

## 概要

このラボでは、リモートで Autopilot Reset を実行する方法を学習します。

### 前提条件

このラボを開始する前に、次のラボを完了しておく必要があります。

- 0101-Managing Identities in Azure AD

- 0102-Synchronizing identities by using Entra Connect

- 0701-Deploying Windows 11 using Microsoft Deployment Toolkit

- 0801-Deploying Windows 11 with Autopilot


### シナリオ

SEA-WS4 は Windows Autopilot を使用して展開されています。Autopilot Reset を使用する別のプロビジョニング シナリオをテストする必要があります。Windows Autopilot の自己展開モードを使用する新しい展開プロファイルを作成します。

### タスク 1: 自己展開モードの Windows Autopilot 展開プロファイルの構成

1. 切り替え先: **SEA-SVR1**.

2. 対象: **Microsoft Edge**, open a new タブ および 移動します: **https://intune.microsoft.com**. 求められた場合は、 your **`Admin@yourtenant.onmicrosoft.com`**.

3. 対象: **Microsoft Intune 管理センター**, 選択します **デバイス**.

4. 対象: **デバイスのオンボード** section, 選択します **登録**. 。

5. 対象: Windows enrollment タブ, 下へスクロールして **Windows Autopilot** in 詳細ペイン, を選択してから **展開プロファイル**.

6. 対象: **Windows Autopilot 展開プロファイル** ブレード, 選択します **Contoso Profile 1** を選択してから **プロパティ**.

7. Scroll down to **割り当て** を選択してから **編集**.

8. Next to **IT Devices**, 選択します **削除**.

9. 選択します **確認と保存** を選択してから **保存**.

10. 閉じます **Contoso Profile 1|Properties** ページ.

11. 対象: **Windows Autopilot 展開プロファイル** ブレード, 選択します **プロファイルの作成** を選択してから **Windows PC**.

12. 対象: **基本** タブ, in **名前** テキスト ボックス, 入力します **Contoso profile 2**.

13. For **対象となるすべてのデバイスを Autopilot に変換する** 選択します **いいえ**, を選択してから **次へ**.

14. 対象: **Out-of-box experience (OOBE)** タブ, 確認し **展開モード** が次に設定されていることを確認します: **自己展開**.

15. 確認し 次の項目 options を設定します:

   - Language (Region): **Operating system default**
   - Automatically configure keyboard: **Yes**
   - Apply device name template: **Yes**
   - Enter a name: **Contoso-%RAND:2%**

16. 選択します **次へ**.

17. 対象: **割り当て** タブ, で **包含されたグループ** 選択します **グループの追加**.

18. 選択します **IT Devices** group および 選択します **選択**. 選択します **次へ**.

19. 対象: **確認と作成** ブレード, 確認し information を選択してから **作成**.

### タスク 2: Autopilot Reset の実行

1. 対象: **Microsoft Intune 管理センター**, 選択します **デバイス** を選択してから **すべてのデバイス**.

2. 選択します Autopilot PC (Begins を使用して name DESKTOP).

3. 対象: メニュー バー, 選択します ellipsis を選択してから **Autopilot Reset**.

5. 対象: message prompt, 選択します **はい**.

6. 切り替え先: **SEA-WS3**.

   > Note: SEA-WS3 should still be running from the previous lab.

7. Restart **SEA-WS3**.

   > Note: This process can take 30-45 minutes and will reboot several times during the process. 

### タスク 3: Autopilot 展開の確認

1. 対象: sign-in ページ, 入力します **`Aaron@yourtenant.onmicrosoft.com`** を使用して Password of **Pa55w.rd1234!**.

2. 対象: **Use Windows Hello を使用して your account**, 選択します **OK**.

3. 対象: **Verify your identity** ページ, 選択します Text verification method.

4. 対象: **入力します code** ページ, 入力します code that has been texted to your mobile device を選択してから **Verify**.

5. 対象: **Setup up a PIN** ダイアログ ボックス, in **New PIN** および **Confirm PIN** fields, 入力します **102938**, を選択してから **OK**.

6. 対象: **All set!** ページ, 選択します **OK**.

7. 選択します **Start** を選択し **Settings**. 。

8. 選択します **Accounts**, を選択してから **Access work or school**. Verify device is connected to Contoso's Azure AD.

9. 選択します **Connected to Contoso's Azure AD** を選択し **Info**.

10. 対象: **Managed by Contoso** ページ, scroll down を選択してから **Sync**.

11. 対象: **SEA-WS3**, 閉じます **Settings** ウィンドウ.

    **Results**: After completing this exercise, you will have provisioned a Windows device with Autopilot Reset using Self-Deploying mode.

**ラボ終了**
