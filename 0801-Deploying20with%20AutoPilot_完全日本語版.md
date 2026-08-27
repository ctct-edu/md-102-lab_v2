### lab:
title: 'Practice Lab 0801: Autopilot を使用した Windows の展開'
description: このラボでは、ユーザー ドリブン モードを使用して、Autopilot で Windows 11 デバイスをプロビジョニングする方法を学びます。
duration: 30 minutes
level: 200
islab: true
primarytopics:
- Windows
- Windows 11

## Practice Lab 0801: Autopilot を使用した Windows の展開

### 概要

このラボでは、ユーザー ドリブンの展開プロファイルを使用して、Autopilot で Windows 11 デバイスをプロビジョニングする方法を学びます。

#### 前提条件

このラボの前に、次のラボを完了しておく必要があります。

- 0101-Managing Identities in Entra ID
- 0102-Synchronizing identities by using Entra Connect

#### シナリオ

Contoso IT では、Autopilot を使用して新しい Windows 11 デバイスの展開を実施することを計画しています。これらのデバイスには Windows 11 が既定でインストールされています。ユーザーは、デバイスを接続して電源を入れ、OOBE 中に最小限の質問に答えるだけで、自分の Entra ID 資格情報を使用してサインインできる必要があります。このプロセスによって、デバイスは自動的に Entra ID に参加し、Intune に登録されます。あなたは、このエクスペリエンスを構成してテストするよう依頼されました。

#### タスク 1: Entra ID でのグループの作成

1. **SEA-SVR1** に、**Contoso\Administrator** としてパスワード **Pa55w.rd** でサインインし、**Server Manager** を閉じます。

2. タスク バーで、**Microsoft Edge** を選択します。

3. Microsoft Edge のアドレス バーに [**https://entra.microsoft.com**](https://entra.microsoft.com) を入力し、**Enter** キーを押します。プロンプトが表示されたら、**Admin@yourtenant.onmicrosoft.com** と既定のテナント パスワードでサインインします。

4. ナビゲーション ペインで、**Entra ID** を展開します。

5. **グループ** を選択し、続いて **すべてのグループ** を選択します。

6. **グループ | すべてのグループ** ブレードで、**新しいグループ** を選択します。

7. **新しいグループ** ブレードの **グループの種類** の一覧で、**セキュリティ** を選択します。

8. **グループ名** ボックスに **IT Devices** を入力します。

9. **グループの説明** ボックスに **IT Department Devices** を入力します。

10. **メンバーシップの種類** の一覧で、**動的デバイス** を選択します。

11. **動的クエリの追加** を選択します。

12. **動的メンバーシップ ルール** ブレードで、**ルール構文** ボックスの上にある **編集** を選択します。

13. ルール構文の編集テキスト ボックスに、次のシンプルなメンバーシップ ルールを追加し、**OK** を選択します。

    ```
    (device.devicePhysicalIDs -any (_ -contains "[ZTDId]"))
    ```

14. **保存** を選択して **動的メンバーシップ ルール** を閉じ、続いて **作成** を選択してグループを作成します。

#### タスク 2: デバイス固有のコンマ区切り値 (CSV) ファイルの生成

1. **SEA-WS3** に切り替え、**Admin** としてパスワード **Pa55w.rd** でサインインします。

2. **Start** を右クリックし、**Windows Terminal (Admin)** を選択して、**User Account Control** のプロンプトで **Yes** を選択します。

3. Windows PowerShell のコマンド ライン プロンプトで、次のコマンドレットを入力し、**Enter** キーを押します。

    ```powershell
    Install-Script -Name Get-WindowsAutoPilotInfo
    ```

4. 3 回のプロンプトが表示されます。そのつど **Y** を入力し、**Enter** キーを押します。

5. Windows PowerShell のコマンド ライン プロンプトで、次のコマンドレットを入力し、**Enter** キーを押します。

    ```powershell
    Set-ExecutionPolicy -ExecutionPolicy RemoteSigned
    ```

6. Windows PowerShell のコマンド ライン プロンプトで、次のコマンドレットを入力し、**Enter** キーを押します。

    ```powershell
    Get-WindowsAutoPilotInfo.ps1 -OutputFile C:\Computer.csv
    ```

7. Windows PowerShell のコマンド ライン プロンプトで、次のコマンドを入力し、**Enter** キーを押してから、ファイルの内容を確認します。

    ```powershell
    type C:\Computer.csv
    ```

8. **Windows Terminal** を閉じます。

#### タスク 3: Windows Autopilot 展開プロファイルの操作

1. **SEA-WS3** の Windows タスク バーで、**Microsoft Edge** を選択します。

2. **Microsoft Edge** で、[**https://intune.microsoft.com**](https://intune.microsoft.com) に移動します。**Admin@yourtenant.onmicrosoft.com** アカウントでサインインします。

    > **注:** MFA の登録を求められる場合があります。このコースで以前使用したのと同じ手順に従って、電話番号を追加してください。

3. **Microsoft Intune 管理センター** で、**デバイス** を選択します。

4. **デバイスのオンボード** セクションで、**登録** を選択します。

5. **Windows** タブで、**Windows Autopilot** までスクロールし、**デバイス** を選択します。

6. **Windows Autopilot デバイス** ブレードのメニュー バーで、**インポート** を選択し、**フォルダー アイコン** を選択して、**C:\** を参照します。**Computer.csv** を選択し、**Open** を選択して、続いて **インポート** を選択します。

    > _注: インポート処理には最大 15 分かかることがありますが、通常は約 5 分です。_
    >
    > _**重要**: 処理が完了しても、デバイスが自動的に表示されない場合があります。その場合は、**更新** ボタンを選択してください。それでもデバイスが表示されない場合は、**同期** ボタンを選択し、数分待ってから **更新** を選択してください。_

7. **X** を選択して **Windows Autopilot デバイス** ブレードを閉じます。

8. Windows の登録ブレードの詳細ペインで、**展開プロファイル** を選択します。

9. **Windows AutoPilot 展開プロファイル** ブレードで、**プロファイルの作成** を選択し、続いて **Windows PC** を選択します。

10. **基本** タブの **名前** テキスト ボックスに **Contoso profile1** を入力します。

11. **対象のすべてのデバイスを Autopilot に変換** では **いいえ** を選択し、続いて **次へ** を選択します。

12. **初回起動時のエクスペリエンス (OOBE)** タブで、**展開モード** が **ユーザー ドリブン** に設定されていることを確認します。

13. **Entra ID への参加方法** が **Microsoft Entra 参加済み** に設定されていることを確認します。

14. 次のオプションが設定されていることを確認します。

    - Microsoft ソフトウェア ライセンス条項: **非表示**
    - プライバシー設定: **非表示**
    - アカウント変更オプションの非表示: **非表示**
    - ユーザー アカウントの種類: **管理者**
    - 事前プロビジョニングされた展開を許可: **いいえ**
    - 言語 (地域): **オペレーティング システムの既定**
    - キーボードを自動的に構成する: **はい**
    - デバイス名テンプレートの適用: **いいえ**

15. **次へ** を選択します。

16. **割り当て** タブの **包含されたグループ** で、**グループの追加** を選択します。

17. **IT Devices** グループを選択し、**選択** をクリックします。**次へ** を選択します。

18. **確認と作成** タブで情報を確認し、**作成** を選択します。

19. **Microsoft Edge** を閉じます。

#### タスク 4: PC のリセット

1. **SEA-WS3** で、**Start** を選択し、**reset** と入力して、**Reset this PC** を選択します。

2. **System > Recovery** ページで、**Reset PC** を選択します。

3. **Remove everything** を選択し、続いて **Local reinstall** を選択します。

4. **Next** を選択し、続いて **Reset** を選択します。

    > **注:** 通常、この手順は物理デバイスの新規展開では不要です。デバイスの Autopilot 情報は製造元から提供されるか、OOBE の前にデバイスから取得できます。このラボの目的上、新しいデバイスの OOBE をシミュレートするためにリセットを開始する必要があります。
    >
    > **注:** このプロセスには 30～45 分かかることがあり、その間にデバイスは数回再起動します。

#### タスク 5: Autopilot 展開の確認

1. **Let's set things up for your work or school** ページで、**Aaron@yourtenant.onmicrosoft.com** を入力し、**Next** を選択します。

2. Password ページで、**Pa55w.rd1234!** を入力し、**Sign in** を選択します。

3. **Use Windows Hello with your account** で、**OK** を選択します。

4. **Verify your identity** ページで、Text の確認方法を選択します。

5. **Enter code** ページで、モバイル デバイスに送信されたコードを入力し、**Verify** を選択します。

6. **Setup up a PIN** ダイアログ ボックスの **New PIN** および **Confirm PIN** フィールドに **102938** を入力し、**OK** を選択します。

7. **All set!** ページで、**OK** を選択します。

8. **Start** を選択し、**Settings** を選択します。

9. **Accounts** を選択し、続いて **Access work or school** を選択します。デバイスが Contoso の Azure AD に接続されていることを確認します。

10. **Connected to Contoso's Azure AD** を選択し、**Info** を選択します。

11. **Managed by Contoso** ページで、下にスクロールし、続いて **Sync** を選択します。

12. **SEA-WS3** で、**Settings** ウィンドウを閉じます。

13. **SEA-SVR1** に切り替えます。

14. Microsoft Entra 管理センターで、**Entra ID** を展開し、**デバイス** を展開して、続いて **すべてのデバイス** を選択します。

    > 新しいデバイスが、Autopilot デバイスであることを示すアイコンとともに表示されることに注目してください。また、参加の種類が **Microsoft Entra 参加済み** で、所有者が Aaron Nicholls になっていることにも注目してください。

15. Autopilot デバイスを選択し、続いて **管理** を選択します。

16. デバイスに対して、廃止 (Retire)、ワイプ (Wipe)、同期 (Sync)、再起動 (Restart) を実行できることを確認します。

17. メニュー バーの末尾にある省略記号を選択し、追加の管理機能に注目します。

    > 追加の機能には、新規スタート (Fresh Start)、Autopilot リセット (Autopilot Reset)、クイック スキャン (Quick scan)、フル スキャン (Full scan) などがあります。

18. Microsoft Edge を閉じます。

**結果**: この演習を完了すると、ユーザー ドリブン モードを使用して、Autopilot で Windows デバイスをプロビジョニングできています。

**ラボ終了**
