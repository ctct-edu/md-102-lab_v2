---
lab:
  title: '演習ラボ 0602: Intune を使用したディスク暗号化の構成'
  description: このラボでは、Intuneを使用してBitLockerディスク暗号化を構成します。
  duration: 90 minutes
  level: 200
  islab: true
---

# 演習ラボ 0602: Intune を使用したディスク暗号化の構成

## 概要

このラボでは、Intuneを使用してBitLockerディスク暗号化を構成します。

### 前提条件

このラボを開始する前に、次のラボを完了しておく必要があります。

- 0203-Manage Device Enrollment into Intune

- 0204-Enrolling devices into Intune

- 0301-Creating and Deploying Configuration Profiles

  Note: You will also need a mobile phone that can receive text messages used to secure Windows Hello sign in authentication to Entra ID.

### シナリオ

SEA-WS1上のすべての情報を暗号化する必要があります。SEA-WS1でディスク全体の暗号化を構成し、起動時に追加のPIN認証を要求するよう依頼されました。

### タスク 1: Intune でデバイス構成ポリシーを構成する

1. 手元の PC で Microsoft Edge を起動します。

2. アドレス バーに **https://intune.microsoft.com** と入力し、**Enter** キーを押します。

3. 次のアカウントとしてサインインします: **`admin@yourtenant.onmicrosoft.com`** 既定のテナントパスワードを使用します.

3. In the Microsoft Intune 管理センター, select **エンドポイント セキュリティ** from the navigation bar.

3. On the **エンドポイント セキュリティ | Overview** page, select **ディスク暗号化**.

3. On the **エンドポイント セキュリティ | ディスク暗号化** blade, in the details pane, select **+ Create Policy**.

3. In the **プロファイルの作成** page, select the following options, and then select **Create**:

    -   プラットフォーム: **Windows**
    -   Profile: **BitLocker**

3. On the **基本** page, enter the following information, and then select **Next**:

    -   Name: **Contoso BitLocker**
    -   Description: **Enable BitLocker for all devices**

3. On the **構成設定** tab, expand **BitLocker** and then configure the following option:

     - Require Device Encryption: **Enabled**

  >**Note**: Please ensure you have expanded the **BitLocker** section and enabled the option before moving on to the next step. Your policy will be ineffective unless this option is configured.

3. On the **構成設定** tab, scroll down to **Operating System Drives** and then configure the following options, leaving all other options to their defaults:

     - Enforce drive encryption type on operating system drives: **Enabled**
     - Require additional authentication at startup: **Enabled**
     - Configure minimum PIN length for startup: **Enabled**
     - Choose how Bitlocker-protected operating system drives can be recovered: **Enabled**
     - Do not enable Bitlocker until recovery information is stored to AD DS for operating system drives: **True**
     - Omit recovery options from the BitLocker setup wizard: **True**
     - Save Bitlocker recovery information to AD DS for operating system drives: **True**

3. On the **構成設定** page, select **Next**.

3. On the **スコープ タグ** page, select **Next**.

3. On the **割り当て** tab, search for **Contoso** and then select **Contoso Developer devices**, and then select **Next**.

3. On the **確認と作成** page, select **Save**.

3. Close all open windows on **SEA-SVR1**.

### タスク 2: BitLocker 設定を確認して有効にする

1. On **SEA-WS1**, sign in as **Aaron Nicholls** with the PIN **102938**.
    
2. On the taskbar, select **Start** and then select the **Settings** app.

3. In the **Settings** app, select **Accounts** and then select **Access work or school**.

4. In the **Access work or school** section, select the **Connected to Contoso's Azure AD** link and then select **Info**. Select **Sync**.

5. Select the **Encryption needed** notification.

   _Note: It may take some time until the notification shows up. Windows Focus Assist may also prevent the notification from appearing. You can check notifications manually._

6. On the **Are you ready to start encryption?** dialog, select the checkbox next to **I don't have any other disk encryption software installed, encrypt all my disks**, and select **Yes**.

7. On the **Choose how to unlock your drive at startup?** page, select **Enter a PIN**

8. On the **Enter a PIN** page, in the **PIN** and **Reenter PIN** boxes, enter **123456**, and then select **Set PIN**.

9. On the **Choose how much of your drive to encrypt** page, select **Encrypt used disk space only** and select **Next**.
   
11. On the **Choose which encryption mode to use** page, ensure that **New encryption mode (best for fixed drives on this device)** is selected, and then select **Next**.
    
12. On the **Are you ready to encrypt this drive** page, select **Continue**. Wait for the encryption to complete.

13. At the **Encryption of C: is complete** message, select **Close**, and then restart **SEA-WS1**.

14. When **SEA-WS1** restarts, type **123456** and press **Enter** to unlock the drive.

### タスク 3: BitLocker 保護を確認する

1. Sign in to **SEA-WS1** as **Aaron Nicholls** with the PIN **102938**.

2. On the taskbar, select **File Explorer** and then select **This PC**.

3. In the navigation pane, right-click **Local Disk (C:)**, select **Show more options**, and then select **Manage BitLocker**.

4. In the **BitLocker Drive Encryption** window, ensure that you see **C: BitLocker on** status. This means that drive is encrypted. 

5. 開いているすべてのウィンドウを閉じ、次のデバイスからサインアウトします: **SEA-WS1**.

**結果**: After completing this exercise, you will have successfully configured disk encryption by using Intune.

**ラボ終了**
