---
lab:
    title: '演習ラボ 0301: 構成ポリシーの作成と展開'
    description: この演習では、Microsoft Intune を使用して、Windows 11 デバイス用の構成ポリシーを作成して適用します。
    duration: 100 minutes
    level: 200
    islab: true
    primarytopics:
        - Microsoft Intune
        - Windows
---

## 演習ラボ 0301: 構成ポリシーの作成と展開

### 概要

この演習では、Microsoft Intune を使用して、Windows 11 デバイス用の構成ポリシーを作成して適用します。

#### 前提条件

このラボを実施する前に、次のラボを完了しておく必要があります。
- 0101-Managing Identities in Entra ID
- 0102-Synchronizing identities by using Entra Connect
- 0203-Manage Device Enrollment into Intune
- 0204-Enrolling devices into Intune<br>注: Entra ID への Windows Hello サインイン認証を保護するために使用するテキスト メッセージを受信できる携帯電話も必要になります。

### 演習 1: 構成ポリシーの作成と適用

#### シナリオ

Entra と Intune を使用して、Contoso の Developers 部門のメンバーを管理する必要があります。ユーザーが Windows 11 デバイス上で効果的かつ安全に作業できるようにするソリューションを評価するよう依頼されています。Aaron Nicholls が、ソリューションのテストと評価、およびフィードバックの提供を申し出てくれました。彼はまた、開発者の Windows デバイスに含めて適用する必要がある、いくつかの初期要件を提示しています。
- Settings の Gaming セクションが表示されないようにする。
- Settings の Privacy セクションを可能な限り制限する。
- C:\DevProjects フォルダーを Windows Defender の対象から除外する。
- プロセス devbuild.exe を Windows Defender の対象から除外する。
- 最もよく使うアプリと最近追加されたアプリが Start メニューに表示されないようにする。

#### タスク 1: デバイスの設定を確認する
- **SEA-WS1** に **Aaron Nicholls** として PIN **102938** でサインインします。
- タスク バーで **Start** を選択し、続いて **Settings** を選択します。
- **Settings** のナビゲーション一覧で、**Gaming** 設定が表示されていることを確認します。
- **Personalization** 設定を選択し、続いて Personalization ページで **Start** を選択します。**Show recently added apps** と **Show most used apps** の両方が **On** に設定されていることを確認します。
- **Settings** アプリで、**Privacy & security** を選択します。
- **Privacy & security** ページで、**Security** セクション、**Windows permissions** セクション、**App permissions** セクションで利用できるオプションを確認します。
- **Privacy & security** ページで **Windows Security** を選択し、続いて **Open Windows Security** を選択します。
- **Windows Security** ページで、**Virus & threat protection** を選択します。
- **Virus & threat protection** ページの **Virus & threat protection settings** で、**Manage settings** を選択します。
- **Exclusions** まで下にスクロールし、**Add or remove exclusions** を選択します。**User Account Control** が表示されたら、**Yes** を選択します。
- **Exclusions** ページで、除外が構成されていないことを確認します。
- **Windows Security** ウィンドウを閉じます。
- **Settings** ウィンドウを閉じます。

#### タスク 2: シナリオの要件に基づいて構成ポリシーを作成する
- 手元 PC で、日本語版 Microsoft Edge を起動します。
- アドレス バーに [**https://intune.microsoft.com**](https://intune.microsoft.com) と入力し、**Enter** キーを押します。
- **admin@yourtenant.onmicrosoft.com** としてテナントの管理者パスワードでサインインします。
- Microsoft Intune 管理センターのナビゲーション バーで、**デバイス** を選択します。
- **デバイス** ページの **デバイスの管理** セクションで、**構成** を選択します。
- **デバイス | 構成** ブレードの詳細ペインで、**+ 作成** を選択し、続いて **+ 新しいポリシー** を選択します。
- **プロファイルの作成** ブレードで、次のオプションを選択し、続いて **作成** を選択します。
- プラットフォーム: **Windows 10 以降**
- プロファイルの種類: **テンプレート**
- テンプレート名: **デバイスの制限**
- **基本** タブで、次の情報を入力し、続いて **次へ** を選択します。
- 名前: **Contoso Developer - standard**
- 説明: **Basic restrictions and configuration for Contoso Developers.**
- **構成設定** タブで、**コントロール パネルと設定** セクションを展開します。
- **Gaming** オプションと **Privacy** オプションの横にある **ブロック** を選択します。
- 同じページで、**スタート** セクションを展開します。
- 下にスクロールし、**最もよく使うアプリ**、**最近追加されたアプリ**、**ジャンプ リストの最近開いた項目** の横にある **ブロック** を選択します。
- 同じページで下にスクロールし、**Microsoft Defender ウイルス対策** セクションを展開します。
- **Microsoft Defender ウイルス対策** で下にスクロールし、**Microsoft Defender ウイルス対策の除外** を展開します。
- **Microsoft Defender ウイルス対策の除外** の **ファイルとフォルダー** ボックスに、次のように入力します。<br>**C:\DevProjects**
- **プロセス** ボックスに、次のように入力します。<br>**DevBuild.exe**
- **確認と作成** ブレードに到達するまで **次へ** を 3 回選択します。**作成** を選択します。

#### タスク 3: Contoso Developer デバイス グループを作成する
- Microsoft Intune 管理センターのナビゲーション ペインで、**グループ** を選択します。
- **グループ | すべてのグループ** ブレードで、**新しいグループ** を選択します。
- **新しいグループ** ブレードで、次の情報を入力します。
- グループの種類: **セキュリティ**
- グループ名: **Contoso Developer devices**
- グループの説明: **All Windows devices in Contoso Developer department**
- メンバーシップの種類: **割り当て済み**
- **メンバー** で、**メンバーが選択されていません** を選択します。
- **メンバーの追加** ブレードの **検索** ボックスに **Sea** と入力します。**SEA-WS1** を選択し、続いて **選択** を選びます。
- **新しいグループ** ブレードで、**作成** を選択します。
- **グループ | すべてのグループ** ブレードで、**Contoso developer devices** グループが表示されていることを確認します。

#### タスク 4: 動的な Entra ID デバイス グループを作成する
- **グループ | すべてのグループ** ブレードの詳細ペインで、**新しいグループ** を選択します。
- **グループ** ブレードで、次の値を指定します。
- グループの種類: **セキュリティ**
- グループ名: **Windows Devices**
- メンバーシップの種類: **動的デバイス**
- **動的デバイス メンバー** セクションで、**動的クエリの追加** を選択します。
- **動的メンバーシップ ルール** ブレードの **ルール構文** セクションで、**編集** を選択します。
- **ルール構文の編集** テキスト ボックスに、次のシンプルなメンバーシップ ルールを追加し、**OK** を選択します。

```
(device.deviceOSType -contains "Windows")
```
- **動的メンバーシップ ルール** ブレードで、**保存** を選択します。
- **新しいグループ** ページで、**作成** を選択します。

#### タスク 5: Windows デバイスに構成ポリシーを割り当てる
- Microsoft Intune 管理センターのナビゲーション ペインで、**デバイス** を選択します。
- **デバイス** ブレードの **デバイスの管理** セクションで、**構成** を選択します。
- **デバイス | 構成** ブレードの詳細ペインで、**Contoso Developer – standard** プロファイルを選択します。
- **Contoso Developer – standard** ブレードで、**割り当て** セクションまで下にスクロールし、**編集** を選択します。
- 割り当てページの **包含されたグループ** で、**グループの追加** を選択します。
- **含めるグループの選択** ブレードの **検索** ボックスで、**Contoso Developer devices** を選択し、続いて **選択** を選びます。
- **デバイスの制限** ブレードに戻り、**確認と保存** を選択し、続いて **保存** を選択します。
- Microsoft Intune 管理センターのパンくずナビゲーション メニューで、**デバイス** を選択します。

#### タスク 6: 構成ポリシーが適用されていることを確認する
- **SEA-WS1** に切り替えます。
- **SEA-WS1** のタスク バーで **Start** を選択し、続いて **Settings** を選択します。
- **Settings** で **Accounts** を選択し、続いて **Access work or school** を選択します。
- **Access work or school** セクションで、**Connected to Contoso's Azure AD** リンクを選択し、続いて **Info** を選択します。
- **Managed by Contoso** ページで下にスクロールし、Device sync status で **Sync** を選択します。同期が完了するまで待ちます。
- 同期が完了したら、**Settings** アプリを閉じます。
- **SEA-WS1** で **Start** を選択し、続いて **Settings** を選択します。**Gaming** 設定が削除されていることを確認します。
- **Privacy & security** を選択し、プライバシー設定の多くが非表示になっていることに注目します。
- **Personalization** 設定を選択し、続いて **Start** を選択します。**Show recently added apps** と **Show most used apps** が **Off** に設定されていることを確認します。
- **Settings** アプリで、**Privacy and Security** を選択します。
- **Privacy & Security** ページで **Windows Security** を選択し、続いて **Open Windows Security** を選択します。
- **Windows Security** ページで、**Virus & threat protection** を選択します。
- **Virus & threat protection** ページの **Virus & threat protection settings** で、**Manage settings** を選択します。
- **Exclusions** まで下にスクロールし、**Add or remove exclusions** を選択します。**User Account Control** メッセージで **Yes** を選択します。
- **Exclusions** ページで、**C:\DevProjects** と **DevBuild.exe** が表示されていることを確認します。
- **Windows Security** ページを閉じ、続いて **Settings** アプリを閉じます。  
**結果**: この演習を完了すると、Windows 11 デバイス用の構成ポリシーを作成して割り当てることに成功したことになります。

### 演習 2: 割り当てた構成ポリシーの変更

#### シナリオ

Contoso のポリシーには例外があり、Developer 部門のメンバーについては、デバイス上の Settings で Privacy オプションをブロックしないよう定められています。この変更を実装してテストする必要があります。

#### タスク 1: 割り当てた構成ポリシーの設定を変更する
- 手元 PC の日本語版 Microsoft Edge に切り替えます。
- Microsoft Intune 管理センターで **デバイス** を選択し、**デバイスの管理** セクションで **構成** を選択します。
- **デバイス | 構成** ブレードの詳細ペインで、**Contoso Developer - standard** を選択します。
- **Contoso Developer - standard** ブレードで、**構成設定** セクションまで下にスクロールし、続いて **編集** を選択します。
- **デバイスの制限** ページで、**コントロール パネルと設定** を展開します。
- **Privacy** の横にある **構成されていません** を選択します。
- **確認と保存** を選択し、続いて **保存** を選択します。

#### タスク 2: Intune 管理センターからデバイスの同期を強制する
- 手元 PC の Microsoft Intune 管理センターで、ナビゲーション ペインの **デバイス** を選択し、続いて **すべてのデバイス** を選択します。
- 詳細ペインで、**SEA-WS1** を選択します。
- **SEA-WS1** ブレードで **同期** を選択し、確認を求められたら **はい** を選択します。<br>_注: Intune はデバイスに接続し、すべてのポリシーを同期するよう指示します。これには最大 5 分かかる場合があります。_
- Microsoft Edge を閉じます。

#### タスク 3: SEA-WS1 で変更を確認する
- **SEA-WS1** に切り替えます。
- **SEA-WS1** のタスク バーで **Start** を選択し、続いて **Settings** アプリを選択します。
- **Settings** アプリで **Privacy & security** を選択し、すべてのカスタマイズ オプションが元に戻っていることを確認します。
- 開いているすべてのウィンドウを閉じ、**SEA-WS1** からサインアウトします。  
**結果**: この演習を完了すると、割り当てた構成ポリシーの変更に成功し、その変更を確認できたことになります。  
**ラボの終了**
