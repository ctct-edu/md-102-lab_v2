---
lab:
  title: '演習ラボ: Autopilot Reset と Self-Deploying モードを使用した Windows の更新'
  description: SEA-WS4 は Windows Autopilot を使用して展開されています。Autopilot Reset を使用する別のプロビジョニング シナリオをテストします。Windows Autopilot の Self-Deploying モードを構成した新しい展開プロファイルを作成します。
  duration: 45 minutes
  level: 200
  islab: true
  primarytopics:
    - Windows
---

# 演習ラボ: Autopilot Reset と Self-Deploying モードを使用した Windows の更新

## 概要

このラボでは、リモートで Autopilot Reset を実行する方法を学習します。

### 前提条件

このラボを開始する前に、次のラボを完了しておく必要があります。

- 0101-Managing Identities in Azure AD

- 0102-Synchronizing identities by using Entra Connect

- 0701-Microsoft Deployment Toolkit を使用した Windows 11 の展開

- 0801-Deploying Windows 11 with Autopilot


### シナリオ

SEA-WS4 は Windows Autopilot を使用して展開されています。Autopilot Reset を使用する別のプロビジョニング シナリオをテストします。Windows Autopilot の Self-Deploying モードを構成した新しい展開プロファイルを作成します。

### タスク 1: Self-Deploying Windows Autopilot 展開プロファイルの構成

1. に切り替えます **SEA-SVR1**.

2. In **Microsoft Edge**, 開きます a new タブ and navigate to **https://intune.microsoft.com**. If prompted, sign in with your **`Admin@yourtenant.onmicrosoft.com`**.

3. の **Microsoft Intune admin center**, **Devices**.

4. の **Device onboarding** section, **Enrollment**. 

5. の Windows enrollment タブ, scroll down to **Windows Autopilot** 詳細ペインで, 、続いて **Deployment Profiles**.

6. の **Windows AutoPilot deployment profiles** ブレード, **Contoso Profile 1** 、続いて **Properties**.

7. Scroll down to **Assignments** 、続いて **Edit**.

8. の横で **IT Devices**, **Remove**.

9. **Review and save** 、続いて **Save**.

10. 閉じます the **Contoso Profile 1|Properties** ページ.

11. の **Windows AutoPilot deployment profiles** ブレード, **Create profile** 、続いて **Windows PC**.

12. の **Basics** タブ, の **Name** テキスト ボックス, **Contoso profile 2**.

13. For **Convert all targeted devices to Autopilot** **No**, 、続いて **Next**.

14. の **Out-of-box experience (OOBE)** タブ, ensure that the **Deployment mode** is set to **Self-Deploying**.

15. Ensure that the following options are set:

   - Language (Region): **Operating system default**
   - Automatically configure keyboard: **Yes**
   - Apply device name template: **Yes**
   - 入力します a name: **Contoso-%RAND:2%**

16. **Next**.

17. の **Assignments** タブ, で **Included groups** **Add groups**.

18. 選択します the **IT Devices** group and click **選択します**. **Next**.

19. の **Review + create** ブレード, 情報を確認し 、続いて **Create**.

### タスク 2: Autopilot Reset の実行

1. の **Microsoft Intune admin center**, **Devices** 、続いて **All devices**.

2. 選択します the Autopilot PC (Begins with the name DESKTOP).

3. の メニュー バー, 選択します the ellipsis 、続いて **Autopilot Reset**.

5. At the message prompt, **Yes**.

6. に切り替えます **SEA-WS3**.

   > Note: SEA-WS3 should still be running from the previous lab.

7. Restart **SEA-WS3**.

   > Note: この処理には 30-45 分かかる場合があり、処理中に数回再起動します. 

### タスク 3: Autopilot 展開の確認

1. At the sign-in ページ, **`Aaron@yourtenant.onmicrosoft.com`** パスワード of **Pa55w.rd1234!**.

2. At the **Use Windows Hello with your account**, **OK**.

3. At the **Verify your identity** ページ, 選択します the Text verification method.

4. At the **入力します code** ページ, 入力します the code that has been texted to your mobile device 、続いて **Verify**.

5. の **Setup up a PIN** dialog box, の **New PIN** and **Confirm PIN** fields, **102938**, 、続いて **OK**.

6. の **All set!** ページ, **OK**.

7. **Start** and **Settings**. 

8. **Accounts**, 、続いて **Access work or school**. Verify デバイス is connected to Contoso's Azure AD.

9. **Connected to Contoso's Azure AD** and **Info**.

10. の **Managed by Contoso** ページ, scroll down 、続いて **Sync**.

11. On **SEA-WS3**, 閉じます the **Settings** ウィンドウ.

    **結果**: この演習を完了すると、 provisioned a Windows device with Autopilot Reset using Self-Deploying mode.

**ラボ終了**
