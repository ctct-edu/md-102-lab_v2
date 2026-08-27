### lab:
title: '演習ラボ 0102: Microsoft Entra Connect を使用した ID の同期'
description: このラボでは、Active Directory Domain Services から Entra ID への同期を構成します。
duration: 20 minutes
level: 200
islab: true
primarytopics:
- Microsoft Entra
- Active Directory

## 演習ラボ 0102: Microsoft Entra Connect を使用した ID の同期

### 概要
このラボでは、Active Directory Domain Services から Entra ID への同期を構成します。

#### シナリオ
Contoso Corporation では現在、AD DS と Entra ID のユーザーを別々に管理しています。Microsoft Entra Connect 同期ツールを使用して両方のディレクトリを接続します。

##### タスク 1: Microsoft Entra Connect を使用したディレクトリ同期の構成
1. SEA-SVR1 に Contoso\Administrator / Pa55w.rd でサインインし、Server Manager を閉じます。

2. Microsoft Edge で https://entra.microsoft.com を開きます。

3. Entra ID > Entra Connect を選択し、Manage タブから Download Connect Sync Agent をダウンロードします。

4. AzureAdConnect.msi を実行し、Microsoft Entra Connect Sync ウィザードを開始します。

5. I agree to the license terms and privacy notice を選択し、Continue を選択します。

6. Customize を選択し、Install required components ページで Install を選択します。

7. Password Hash Synchronization を確認して Next を選択します。

8. admin@yourtenant.onmicrosoft.com を使用して Microsoft Entra ID に接続します。

9. Contoso.com フォレストを追加し、Contoso\Administrator と Pa55w.rd を使用して AD フォレスト アカウントを構成します。

10. IT、Managers、Marketing、Research、Sales OU のみを同期対象として選択します。

11. Ready to configure ページで Start the synchronization process when configuration completes を有効にし、Install を選択します。

12. 構成完了後、Exit を選択してすべてのウィンドウを閉じます。

##### タスク 2: Entra ID で同期を確認する
1. Microsoft Entra 管理センターで ユーザー を開きます。

2. オンプレミスの同期が有効 列が はい になっていることを確認します。

3. グループ > すべてのグループ を開きます。

4. Source 列に Windows Server AD と表示されるグループを確認します。

5. Managers グループを開き、メンバーが表示されることを確認します。

6. Microsoft Edge を閉じます。

**結果**: この演習の完了後、Azure AD Connect を使用して Active Directory Domain Services と Entra ID の間で ID 同期を正常に構成できています。

ラボ終了
