### lab:
title: '演習ラボ 0304: グループ ポリシー分析を使用した Intune の GPO サポートの検証'
description: このラボでは、グループ ポリシー分析を使用して Active Directory のグループ ポリシー オブジェクト (GPO) をインポートし、同等の Microsoft Intune MDM ポリシーをサポートする設定を特定します。
duration: 30 minutes
level: 200
islab: true
primarytopics:
\- Microsoft Intune
\- Active Directory

## 演習ラボ 0304: グループ ポリシー分析を使用した Intune の GPO サポートの検証

### 概要

このラボでは、グループ ポリシー分析を使用して Active Directory のグループ ポリシー オブジェクト (GPO) をインポートし、同等の Microsoft Intune MDM ポリシーをサポートする設定を特定します。

#### シナリオ

Contoso では従来、Active Directory の GPO を使用して、ドメイン全体にコンピューターおよびユーザーのポリシー設定を展開してきました。サポートされているすべての GPO 設定を Microsoft Intune の構成ポリシーへ移行する予定です。**Windows Client Policy** という名前の GPO があります。グループ ポリシー分析を使用して Windows Client Policy GPO の設定を検証し、Intune に正常に移行できる設定を特定する必要があります。

#### タスク 1: Windows Client Policy GPO を XML ファイルにエクスポートする
1. **SEA-SVR1** に切り替え、必要に応じて **Contoso\Administrator** として、パスワード **Pa55w.rd** を使用してサインインします。

2. 必要に応じて、**Server Manager**を開きます。

3. Server Manager で、**Tools**、**Group Policy Management**の順に選択します。

4. Group Policy Management コンソールで、**Forest:Contoso.com**、**Domains**、**Contoso.com**の順に展開し、**Group Policy Objects**を選択します。<br>複数のグループ ポリシー オブジェクトが一覧に表示されていることを確認します。

5. 詳細ペインで、**Windows Client Policy** GPO を選択します。

6. **Windows Client Policy**を右クリックし、**Save Report**を選択します。

7. Save GPO Report ダイアログ ボックスで **Documents**を選択し、**Save as type**を **XML file**に変更して、**Save**を選択します。

8. Group Policy Management コンソールを閉じます。

9. Server Manager を閉じます。

#### タスク 2: グループ ポリシー分析を使用して Windows Client GPO を分析する
1. **SEA-SVR1** のタスク バーで、**Microsoft Edge**を選択します。

2. Microsoft Edge のアドレス バーに [**https://intune.microsoft.com**](https://intune.microsoft.com) と入力し、**Enter**キーを押します。

3. テナント管理者のパスワードを使用して、**admin@yourtenant.onmicrosoft.com** としてサインインします。

4. Microsoft Intune 管理センターのナビゲーション ペインで、**デバイス**を選択します。

5. **デバイス | 概要**ページの**デバイスの管理**セクションで、**グループ ポリシー分析**を選択します。

6. **デバイス | グループ ポリシー分析**ブレードで、**インポート**を選択します。

7. **GPO ファイルのインポート**ページで、**ファイルの選択**ボタンを選択します。

8. **Open**ダイアログ ボックスで **Documents**を選択し、**Windows Client Policy.xml**を選択して、**Open**を選択します。<br>Windows Client Policy GPO が直ちにインポートされ、分析されます。

9. **次へ**を 2 回選択し、**作成**を選択します。<br>Windows Client Policy GPO がインポートされ、分析されます。完了まで数分かかる場合があります。

10. **GPO ファイルのインポート**ページを閉じます。

11. **デバイス | グループ ポリシー分析**ブレードで、**Windows Client Policy** の横に表示される情報を確認します。<br>設定の 86% が MDM でサポートされていることを確認します。

12. **MDM サポート**で、**89%**を選択します。<br>サポートされている各設定の**設定名**、**MDM サポート**、**CSP 名**、**CSP マッピング**を確認します。同等の CSP マッピングがない設定を記録します。

#### タスク 3: グループ ポリシー分析の概要レポートを確認する
1. Microsoft Intune 管理センターのナビゲーション ペインで、**レポート**を選択します。

2. **レポート**ページの**デバイス管理**セクションで、**グループ ポリシー分析**を選択します。

3. 詳細ペインの**概要**で、**更新**を選択します。<br>概要レポートの更新と作成には数分かかる場合があります。数回更新する必要がある場合があります。

4. **グループ ポリシー移行の準備状況**の情報を確認します。<br>移行可能なポリシーと、サポートされていないポリシーの件数が表示されます。

5. **レポート | グループ ポリシー分析**ブレードで、**レポート**タブ、**グループ ポリシー移行の準備状況**の順に選択します。<br>グループ ポリシー移行の準備状況レポートには、各設定と、サポートされるプロファイルの種類に関する情報が表示されます。

6. **再生成**を選択します。

7. グループ ポリシー移行の準備状況レポートに、各設定と、サポートされるプロファイルの種類に関する情報が表示されることを確認します。

8. **グループ ポリシー移行の準備状況**ウィンドウを閉じます。

9. Microsoft Edge を閉じます。

**結果**: この演習では、GPO をエクスポートし、グループ ポリシー分析を使用して Intune の同等のポリシー設定を検証しました。  
**ラボ終了**
