---
lab:
  title: '演習ラボ 0801: Autopilotを使用したWindowsの展開'
  description: このラボでは、ユーザー主導モードのAutopilotを使用してWindows 11デバイスをプロビジョニングする方法を学習します。
  duration: 30 minutes
  level: 200
  islab: true
  primarytopics:
    - Windows
    - Windows 11
---

# 演習ラボ 0801: Autopilotを使用したWindowsの展開

## 概要

このラボでは、ユーザー主導の展開プロファイルを使用して、AutopilotでWindows 11デバイスをプロビジョニングする方法を学習します。

### 前提条件

このラボを開始する前に、0101と0102の各ラボを完了しておく必要があります。

### シナリオ

Contoso ITでは、Autopilotを使用して新しいWindows 11デバイスを展開します。ユーザーはデバイスを接続して電源を入れ、OOBEで最小限の質問に回答し、Entra ID資格情報でサインインします。デバイスは自動的にEntra IDへ参加し、Intuneへ登録されます。このエクスペリエンスを構成してテストします。

### タスク 1: Entra IDにグループを作成する

1. 手元のPCでMicrosoft Edgeを起動し、**https://entra.microsoft.com**を開いてテナント管理者でサインインします。
2. ナビゲーション ペインで**Entra ID**を展開します。
3. **グループ**、**すべてのグループ**の順に選択します。
4. **グループ | すべてのグループ**ブレードで、**新しいグループ**を選択します。
5. **新しいグループ**ブレードの**グループの種類**で、**セキュリティ**を選択します。
6. **グループ名**に**IT Devices**と入力します。
7. **グループの説明**に**IT Department Devices**と入力します。
8. **メンバーシップの種類**で、**動的デバイス**を選択します。
9. **動的クエリの追加**を選択します。
10. **動的メンバーシップ ルール**ブレードで、**ルール構文**ボックスの上にある**編集**を選択します。
11. ルール構文の編集テキスト ボックスに次のメンバーシップ規則を追加し、**OK**を選択します。

    ```cmd
    (device.devicePhysicalIDs -any (_ -contains "[ZTDId]"))
    ```

12. **保存**を選択して**動的メンバーシップ ルール**を閉じ、**作成**を選択してグループを作成します。

### タスク 2: デバイス固有のCSVファイルを生成する

1. **SEA-WS3**に切り替え、パスワード**Pa55w.rd**を使用して**Admin**としてサインインします。
2. **Start**を右クリックし、**Windows Terminal (Admin)**を選択して、**User Account Control**で**Yes**を選択します。
3. Windows PowerShellのコマンドラインで次のコマンドレットを入力し、**Enter**キーを押します。

    ```powershell
    Install-Script -Name Get-WindowsAutoPilotInfo
    ```

4. 3回表示される各プロンプトで**Y**と入力し、**Enter**キーを押します。
5. 次のコマンドレットを入力し、**Enter**キーを押します。

    ```powershell
    Set-ExecutionPolicy -ExecutionPolicy RemoteSigned
    ```

6. 次のコマンドレットを入力し、**Enter**キーを押します。

    ```powershell
    Get-WindowsAutoPilotInfo.ps1 -OutputFile C:\Computer.csv
    ```

7. 次のコマンドを入力して**Enter**キーを押し、ファイルの内容を確認します。

    ```cmd
    type C:\Computer.csv
    ```

8. **Windows Terminal**を閉じます。

### タスク 3: Windows Autopilot展開プロファイルを操作する

1. **SEA-WS3**のタスク バーで、**Microsoft Edge**を選択します。
2. **https://intune.microsoft.com**へ移動し、**`Admin@yourtenant.onmicrosoft.com`**アカウントでサインインします。
   > 注: MFAの登録を求められた場合は、以前と同じ手順で携帯電話番号を追加します。
3. **Microsoft Intune管理センター**で、**デバイス**を選択します。
4. **デバイスのオンボード**セクションで、**登録**を選択します。
5. **Windows**タブを**Windows Autopilot**まで下へスクロールし、**デバイス**を選択します。
6. **Windows Autopilotデバイス**ブレードのメニュー バーで**インポート**を選択します。フォルダー アイコンを選択して**C:\\**へ移動し、**Computer.csv**、**開く**、**インポート**の順に選択します。
   _注: インポートには最大15分かかる場合がありますが、通常は約5分です。_
   _**重要**: 完了後にデバイスが表示されない場合は、**更新**を選択します。それでも表示されない場合は、**同期**を選択して数分待ち、再度**更新**を選択します。_
7. **X**を選択して**Windows Autopilotデバイス**ブレードを閉じます。
8. Windows登録ブレードの詳細ペインで、**展開プロファイル**を選択します。
9. **Windows Autopilot展開プロファイル**ブレードで、**プロファイルの作成**、**Windows PC**の順に選択します。
10. **基本**タブの**名前**に**Contoso profile1**と入力します。
11. **対象となるすべてのデバイスをAutopilotに変換する**で**いいえ**を選択し、**次へ**を選択します。
12. **Out-of-box experience (OOBE)**タブで、**展開モード**が**ユーザー主導**になっていることを確認します。
13. **Entra IDへの参加方法**が**Microsoft Entra joined**になっていることを確認します。
14. 次のオプションを設定します。
   - Microsoftソフトウェア ライセンス条項: **非表示**
   - プライバシー設定: **非表示**
   - アカウント変更オプションを非表示にする: **非表示**
   - ユーザー アカウントの種類: **管理者**
   - 事前プロビジョニングされた展開を許可する: **いいえ**
   - 言語（地域）: **オペレーティング システムの既定値**
   - キーボードを自動的に構成する: **はい**
   - デバイス名テンプレートを適用する: **いいえ**
15. **次へ**を選択します。
16. **割り当て**タブの**含まれるグループ**で、**グループの追加**を選択します。
17. **IT Devices**グループを選択し、**選択**、**次へ**の順に選択します。
18. **確認と作成**タブで情報を確認し、**作成**を選択します。
19. Microsoft Edgeを閉じます。

### タスク 4: PCをリセットする

1. **SEA-WS3**で**Start**を選択して**reset**と入力し、**Reset this PC**を選択します。
2. **System > Recovery**ページで、**Reset PC**を選択します。
3. **Remove everything**、**Local reinstall**の順に選択します。
4. **Next**、**Reset**の順に選択します。
   > 注: 新しい物理デバイスの通常の展開では、このタスクは不要です。このラボでは、新しいデバイスのOOBEをシミュレートするためにリセットを実行します。
   > 注: この処理には30分から45分かかる場合があり、処理中に複数回再起動します。

### タスク 5: Autopilot展開を確認する

1. **Let's set things up for your work or school**ページで、**`Aaron@yourtenant.onmicrosoft.com`**と入力し、**Next**を選択します。
2. パスワード ページで**Pa55w.rd1234!**と入力し、**Sign in**を選択します。
3. **Use Windows Hello with your account**で、**OK**を選択します。
4. **Verify your identity**ページで、テキストによる確認方法を選択します。
5. **Enter code**ページで、携帯電話へ送信されたコードを入力し、**Verify**を選択します。
6. **Setup up a PIN**ダイアログの**New PIN**と**Confirm PIN**に**102938**と入力し、**OK**を選択します。
7. **All set!**ページで、**OK**を選択します。
8. **Start**、**Settings**の順に選択します。
9. **Accounts**、**Access work or school**の順に選択し、デバイスがContosoのAzure ADへ接続されていることを確認します。
10. **Connected to Contoso's Azure AD**、**Info**の順に選択します。
11. **Managed by Contoso**ページを下へスクロールし、**Sync**を選択します。
12. **SEA-WS3**で**Settings**ウィンドウを閉じます。
13. 手元のPCのMicrosoft Entra管理センターに切り替えます。
14. **Entra ID**、**デバイス**を展開し、**すべてのデバイス**を選択します。
    > 新しいデバイスにAutopilotデバイスを示すアイコンが表示され、**参加の種類**が**Microsoft Entra joined**、所有者がAaron Nichollsであることを確認します。
15. Autopilotデバイスを選択し、**管理**を選択します。
16. デバイスに対して、使用停止、ワイプ、同期、再起動を実行できることを確認します。
17. メニュー バーの末尾にある省略記号を選択し、追加の管理機能を確認します。
    > 追加機能には、Fresh Start、Autopilot Reset、クイック スキャン、フル スキャンなどがあります。
18. Microsoft Edgeを閉じます。

**結果**: この演習を完了すると、ユーザー主導モードのAutopilotを使用したWindowsデバイスのプロビジョニングが完了します。

**ラボ終了**
