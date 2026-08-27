lab:
title: '演習ラボ 0301: 構成ポリシーの作成と展開'
description: このラボでは、Microsoft Intune を使用して Windows 11 デバイス向けの構成ポリシーを作成し、適用します。
duration: 100 minutes
level: 200
islab: true
primarytopics:
\- Microsoft Intune
\- Windows

## 演習ラボ 0301: 構成ポリシーの作成と展開

### 概要

このラボでは、Microsoft Intune を使用して Windows 11 デバイス向けの構成ポリシーを作成し、適用します。

#### 前提条件

このラボの前に、次のラボを完了しておく必要があります。
- 0101-Managing Identities in Entra ID
- 0102-Synchronizing identities by using Entra Connect
- 0203-Manage Device Enrollment into Intune
- 0204-Enrolling devices into Intune<br>注: Entra ID に対する Windows Hello サインイン認証をセキュリティで保護するため、テキスト メッセージを受信できる携帯電話も必要です。

### 演習 1: 構成ポリシーの作成と適用

#### シナリオ

Entra と Intune を使用して、Contoso の Developers 部門のメンバーを管理します。Windows 11 デバイス上でユーザーが効率的かつ安全に作業できるソリューションを評価するよう依頼されています。Aaron Nicholls が、ソリューションのテストと評価、およびフィードバックの提供に協力します。また、開発者の Windows デバイスに適用する次の初期要件が提示されています。
- Settings の Gaming セクションを表示しない。
- Settings の Privacy セクションを可能な限り制限する。
- C:\DevProjects フォルダーを Windows Defender の対象から除外する。
- devbuild.exe プロセスを Windows Defender の対象から除外する。
- Start メニューに、よく使うアプリと最近追加したアプリを表示しない。

#### タスク 1: デバイス設定を確認する

1. PIN **102938** を使用して、**SEA-WS1** に **Aaron Nicholls** としてサインインします。

2. タスク バーで **Start**、**Settings** の順に選択します。

3. **Settings** のナビゲーション リストに **Gaming** 設定が表示されていることを確認します。

4. **Personalization** 設定を選択し、**Personalization** ページで **Start** を選択します。**Show recently added apps** と **Show most used apps** がどちらも **On** に設定されていることを確認します。

5. **Settings** アプリで **Privacy & security** を選択します。

6. **Privacy & security** ページで、**Security**、**Windows permissions**、**App permissions** の各セクションにあるオプションを確認します。

7. **Privacy & security** ページで **Windows Security**、**Open Windows Security** の順に選択します。

8. **Windows Security** ページで **Virus & threat protection** を選択します。

9. **Virus & threat protection** ページの **Virus & threat protection settings** で **Manage settings** を選択します。

10. **Exclusions** まで下にスクロールし、**Add or remove exclusions** を選択します。**User Account Control** で **Yes** を選択します。

11. **Exclusions** ページで、除外が構成されていないことを確認します。

12. **Windows Security** ウィンドウを閉じます。

13. **Settings** ウィンドウを閉じます。

#### タスク 2: シナリオの要件に基づく構成ポリシーを作成する

1. 受講者の手元 PC で日本語版 **Microsoft Edge** を開き、[**https://intune.microsoft.com**](https://intune.microsoft.com) にアクセスします。

2. テナントの Admin パスワードを使用して **admin@yourtenant.onmicrosoft.com** としてサインインします。

3. Microsoft Intune 管理センターのナビゲーション バーで **デバイス**を選択します。

4. **デバイス**ページの**デバイスの管理**セクションで **構成**を選択します。

5. **デバイス | 構成**ブレードの詳細ペインで **作成**、**新しいポリシー**の順に選択します。

6. **プロファイルの作成**ブレードで次のオプションを選択し、**作成**を選択します。
   - プラットフォーム: **Windows 10 以降**
   - プロファイルの種類: **テンプレート**
   - テンプレート名: **デバイスの制限**

7. **基本**タブで次の情報を入力し、**次へ**を選択します。
   - 名前: **Contoso Developer - standard**
   - 説明: **Basic restrictions and configuration for Contoso Developers.**

8. **構成設定**タブで、**コントロール パネルと設定**セクションを展開します。

9. **ゲーム**と**プライバシー**の横で**ブロック**を選択します。

10. 同じページで **Start** セクションを展開します。

11. 下にスクロールし、**よく使うアプリ**、**最近追加したアプリ**、**ジャンプ リストで最近開いた項目**の横で**ブロック**を選択します。

12. 同じページを下にスクロールし、**Microsoft Defender ウイルス対策**セクションを展開します。

13. **Microsoft Defender ウイルス対策**で下にスクロールし、**Microsoft Defender ウイルス対策の除外**を展開します。

14. **Microsoft Defender ウイルス対策の除外**の**ファイルとフォルダー**ボックスに、**C:\DevProjects** と入力します。

15. **プロセス**ボックスに **DevBuild.exe** と入力します。

16. **確認と作成**ブレードに到達するまで **次へ**を 3 回選択し、**作成**を選択します。

#### タスク 3: Contoso Developer デバイス グループを作成する

1. Microsoft Intune 管理センターのナビゲーション ペインで **グループ**を選択します。

2. **グループ | すべてのグループ**ブレードで **新しいグループ**を選択します。

3. **新しいグループ**ブレードに次の情報を入力します。
   - グループの種類: **セキュリティ**
   - グループ名: **Contoso Developer devices**
   - グループの説明: **All Windows devices in Contoso Developer department**
   - メンバーシップの種類: **割り当て済み**

4. **メンバー**で **メンバーが選択されていません**を選択します。

5. **メンバーの追加**ブレードの**検索**ボックスに **Sea** と入力します。**SEA-WS1**、**選択**の順に選択します。

6. **新しいグループ**ブレードで **作成**を選択します。

7. **グループ | すべてのグループ**ブレードに **Contoso developer devices** グループが表示されていることを確認します。

#### タスク 4: 動的 Entra ID デバイス グループを作成する

1. **グループ | すべてのグループ**ブレードの詳細ペインで **新しいグループ**を選択します。

2. **グループ**ブレードに次の値を指定します。
   - グループの種類: **セキュリティ**
   - グループ名: **Windows Devices**
   - メンバーシップの種類: **動的デバイス**

3. **動的デバイス メンバー**セクションで **動的クエリの追加**を選択します。

4. **動的メンバーシップ ルール**ブレードの**ルール構文**セクションで **編集**を選択します。

5. **ルール構文の編集**テキスト ボックスに次のメンバーシップ規則を追加し、**OK** を選択します: `(device.deviceOSType -contains "Windows")`

6. **動的メンバーシップ ルール**ブレードで **保存**を選択します。

7. **新しいグループ**ページで **作成**を選択します。

#### タスク 5: Windows デバイスに構成ポリシーを割り当てる

1. Microsoft Intune 管理センターのナビゲーション ペインで **デバイス**を選択します。

2. **デバイス**ブレードの**デバイスの管理**セクションで **構成**を選択します。

3. **デバイス | 構成**ブレードの詳細ペインで **Contoso Developer – standard** プロファイルを選択します。

4. **Contoso Developer – standard** ブレードで**割り当て**セクションまで下にスクロールし、**編集**を選択します。

5. 割り当てページの**包含されたグループ**で **グループの追加**を選択します。

6. **含めるグループの選択**ブレードの**検索**ボックスで **Contoso Developer devices** を選択し、**選択**を選択します。

7. **デバイスの制限**ブレードに戻り、**確認と保存**、**保存**の順に選択します。

8. Microsoft Intune 管理センターの階層リンクで **デバイス**を選択します。

#### タスク 6: 構成ポリシーが適用されたことを確認する

1. **SEA-WS1** に切り替えます。

2. **SEA-WS1** のタスク バーで **Start**、**Settings** の順に選択します。

3. **Settings** で **Accounts**、**Access work or school** の順に選択します。

4. **Access work or school** セクションで **Connected to Contoso's Azure AD** リンクを選択し、**Info** を選択します。

5. **Managed by Contoso** ページで下にスクロールし、**Device sync status** の **Sync** を選択します。同期が完了するまで待ちます。

6. 同期が完了したら **Settings** アプリを閉じます。

7. **SEA-WS1** で **Start**、**Settings** の順に選択し、**Gaming** 設定が削除されていることを確認します。

8. **Privacy & security** を選択し、多くのプライバシー設定が非表示になっていることを確認します。

9. **Personalization**、**Start** の順に選択し、**Show recently added apps** と **Show most used apps** が **Off** に設定されていることを確認します。

10. **Settings** アプリで **Privacy and Security** を選択します。

11. **Privacy & Security** ページで **Windows Security**、**Open Windows Security** の順に選択します。

12. **Windows Security** ページで **Virus & threat protection** を選択します。

13. **Virus & threat protection** ページの **Virus & threat protection settings** で **Manage settings** を選択します。

14. **Exclusions** まで下にスクロールし、**Add or remove exclusions** を選択します。**User Account Control** メッセージで **Yes** を選択します。

15. **Exclusions** ページに **C:\DevProjects** と **DevBuild.exe** が表示されていることを確認します。

16. **Windows Security** ページを閉じ、**Settings** アプリを閉じます。

**結果**: この演習では、Windows 11 デバイス向けの構成ポリシーを作成して割り当てました。

### 演習 2: 割り当て済み構成ポリシーの変更

#### シナリオ

Developers 部門のメンバーについては、そのデバイスの Settings で Privacy オプションをブロックしないという例外が Contoso のポリシーに追加されました。この変更を実装してテストします。

#### タスク 1: 割り当て済み構成ポリシーの設定を変更する

1. 受講者の手元 PC の Microsoft Intune 管理センターで **デバイス**を選択し、**デバイスの管理**セクションの **構成**を選択します。

2. **デバイス | 構成**ブレードの詳細ペインで **Contoso Developer -  standard** を選択します。

3. **Contoso Developer - standard** ブレードで**構成設定**セクションまで下にスクロールし、**編集**を選択します。

4. **デバイスの制限**ページで**コントロール パネルと設定**を展開します。

5. **プライバシー**の横で**構成されていません**を選択します。

6. **確認と保存**、**保存**の順に選択します。

#### タスク 2: Intune 管理センターからデバイスの同期を強制する

1. 手元 PC の Microsoft Intune 管理センターで、ナビゲーション ペインの **デバイス**、**すべてのデバイス**の順に選択します。

2. 詳細ペインで **SEA-WS1** を選択します。

3. **SEA-WS1** ブレードで **同期**を選択し、確認を求められたら**はい**を選択します。<br>_注: Intune がデバイスに接続し、すべてのポリシーを同期するよう指示します。完了まで最大 5 分かかる場合があります。_

4. Microsoft Edge を閉じます。

#### タスク 3: SEA-WS1 で変更を確認する

1. **SEA-WS1** に切り替えます。

2. **SEA-WS1** のタスク バーで **Start**、**Settings** アプリの順に選択します。

3. **Settings** アプリで **Privacy & security** を選択し、すべてのカスタマイズ オプションが再び表示されていることを確認します。

4. 開いているすべてのウィンドウを閉じ、**SEA-WS1** からサインアウトします。

**結果**: この演習では、割り当て済み構成ポリシーを変更し、その変更を確認しました。

**ラボ終了**