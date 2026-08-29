---
lab:
    title: 'ラボ 05: 自動化と運用'
    description: 'このラボでは、Microsoft Graph PowerShell を使用したデバイス管理、プロアクティブな修復の展開、スコープ タグを使用したロールベースのアクセス制御の構成、監査ログの確認、Intune の組み込みレポートの利用を行います。'
    duration: 100 minutes
    level: 200
    islab: true
    primarytopics:
    - Microsoft Intune
    - Microsoft Graph
    - Microsoft Entra ID
    - Windows
---

## ラボ 05: 自動化と運用

### ラボのシナリオ

あなたは、Contoso Healthcare のモダン エンドポイント管理者である **Jordan Chen** です。Intune 環境の展開が完了し (デバイスの登録、アプリの展開、セキュリティ ポリシーの構成が済んだ状態)、ここからは自動化と運用の卓越性に関するプラクティスを実装する必要があります。スクリプトによるデバイス管理には Microsoft Graph PowerShell を使用し、プロアクティブな修復を展開し、委任管理のためにスコープ タグを使用したロールベースのアクセス制御 (RBAC) を実装し、監査ログを構成し、運用上の分析情報を得るために組み込みのレポート機能を活用します。

このラボの終了時までに、次のことを完了しています。

- 無人の Graph API 自動化のために Microsoft Entra ID にアプリを登録した
- Microsoft Graph PowerShell SDK で認証した
- Graph API を使用して管理対象デバイスとポリシーをクエリした (Pharmacy スコープ タグによるフィルター処理を含む)
- **パイロット優先**の展開パターンを使用して、プロアクティブな修復スクリプト パッケージを展開した
- **Pharmacy Helpdesk** カスタム ロール (**ラボ 01 演習 2 タスク 6** で作成) を委任管理者 (**Lee Gu**) に割り当て、ラボ 02 ～ 04 で作成したすべての Pharmacy スコープ オブジェクトにわたってスコープの動作をエンドツーエンドで検証した
- 条件付きアクセス ポリシーの編集、コンプライアンス ポリシーの変更、スコープ タグの操作を含む、管理アクティビティの追跡のために監査ログを確認した
- 組み込みレポートを使用して、デバイスとコンプライアンスのデータをエクスポートした
- テナントの正常性とサービスの状態を監視した

### ラボの所要時間

**推定所要時間:** 100 分

### 手順

#### 開始する前に

このラボには、次が必要です。

- **ラボ 01** の完了 (デバイスの登録、グループの構成)
- **ラボ 02** の完了 (更新リング、機能更新プログラム、コンプライアンス ポリシーの展開)
- Contoso の Microsoft 365 テナント (\<TenantPrefix\>.onmicrosoft.com) へのアクセス
- グローバル管理者の資格情報
- **SEA-DEV1** (登録済みデバイス。Megan Bowen でサインイン済み)
- SEA-DEV1 にインストールされた Microsoft Graph PowerShell SDK

### 演習 1: Microsoft Graph PowerShell による自動化

#### シナリオ

Microsoft Graph は、Intune を含む Microsoft 365 サービスへのプログラムによるアクセスを提供する REST API です。無人自動化のために Microsoft Entra ID でアプリケーションを登録し、Graph PowerShell SDK で認証し、PowerShell を使用して一般的な管理タスクを実行します。

#### タスク 1: Microsoft Graph PowerShell SDK のインストール

1. **SEA-DEV1** で、**Terminal (Admin)** を開きます (**Start** を右クリックし、**Terminal (Admin)** を選択します。**Windows Terminal** は既定で PowerShell タブを開きます)。

2. **Do you want to allow this app to make changes to your device?** というプロンプトで、**Yes** を選択します。

3. Microsoft Graph PowerShell SDK をインストールします。

   ```powershell
   Install-Module Microsoft.Graph -Scope AllUsers -Force
   ```

   > [!NOTE]
   > Microsoft.Graph モジュールは、すべての Graph PowerShell モジュールをインストールするメタパッケージです。信頼されていないリポジトリからのインストールを求められた場合は、**Y** を入力して Enter キーを押します。

4. インストールを確認します。

   ```powershell
   Get-Module -Name Microsoft.Graph.* -ListAvailable
   ```

   出力には、複数の Microsoft.Graph.* モジュール (例: Microsoft.Graph.Authentication、Microsoft.Graph.Intune、Microsoft.Graph.Users) が表示されるはずです。

**Microsoft Graph PowerShell SDK が正常にインストールされました。**

#### タスク 2: 無人自動化のためのアプリケーションの登録

対話型の自動化では、委任されたアクセス許可 (ユーザーがサインインする) を使用できます。無人自動化 (例: スケジュールされたスクリプト) では、アプリケーションのアクセス許可とクライアント シークレットまたは証明書が必要です。

1. **SEA-DEV1** で **Microsoft Edge** を開き、[**https://entra.microsoft.com**](https://entra.microsoft.com) に移動します。

2. **admin@\<TenantPrefix\>.onmicrosoft.com** としてサインインします。

3. **Microsoft Entra 管理センター**の左側のナビゲーションで、**Entra ID** を展開し、**アプリの登録** を選択します。

   > [!NOTE]
   > 現在の Entra ポータルでは、**アプリの登録** は **Entra ID** の直下の子項目であり、"アプリケーション" の親ノードはありません。(以前の "ID → アプリケーション → アプリの登録" というパスは存在しなくなりました。)

4. **+ 新規登録** を選択します。

5. **アプリケーションの登録** ページで、次を入力します。

   - **名前:** **Intune Automation App**
   - **サポートされているアカウントの種類:** 単一テナントのみ - Contoso (既定値。これは "この組織ディレクトリ内のアカウントのみ" のモダンなラベルです)
   - **リダイレクト URI:** 空白のままにします

6. **登録** を選択します。

7. **Intune Automation App** の概要ページで、次の値をメモします。

   - **アプリケーション (クライアント) ID:** (この値をコピーします。認証に必要になります)
   - **ディレクトリ (テナント) ID:** (この値をコピーします)

**Graph API アクセス用のアプリケーションが正常に登録されました。**

#### タスク 3: アプリケーションへの API アクセス許可の付与

1. **Intune Automation App** の詳細で、左側のナビゲーションから **API のアクセス許可** を選択します。

2. **+ アクセス許可の追加** を選択します。

3. **API アクセス許可の要求** ペインで、**Microsoft Graph** を選択します。

4. **アプリケーションの許可** (委任されたアクセス許可ではなく) を選択します。

5. 次のアクセス許可を検索して選択します。

   - **DeviceManagementManagedDevices.Read.All** (デバイス情報の読み取り)
   - **DeviceManagementRBAC.Read.All** (Intune のロールベースのアクセス制御データの読み取り)
   - **DeviceManagementConfiguration.ReadWrite.All** (構成ポリシーの読み取り/書き込み)
   - **DeviceManagementApps.ReadWrite.All** (アプリケーションの読み取り/書き込み)
   - **Group.Read.All** (ディレクトリ グループの読み取り — タスク 8 の Get-MgGroup に必要)

   > [!NOTE]
   > アプリケーションのアクセス許可は、ユーザーの ID ではなく、アプリケーションの ID で実行されます。無人自動化に適していますが、管理者の同意が必要です。

6. **アクセス許可の追加** を選択します。

7. **Intune Automation App | API のアクセス許可** ページで、**Contoso に管理者の同意を与える** を選択します。

8. 確認ダイアログで、**はい** を選択します。

9. すべてのアクセス許可について、**状態** 列に緑色のチェックマーク (管理者の同意が付与されたことを示します) が表示されていることを確認します。

**アプリケーションに API アクセス許可が正常に付与されました。**

#### タスク 4: クライアント シークレットの作成

1. **Intune Automation App** の詳細で、左側のナビゲーションから **証明書とシークレット** を選択します。

2. **クライアント シークレット** で、**+ 新しいクライアント シークレット** を選択します。

3. **クライアント シークレットの追加** ペインで、次を入力します。

   - **説明:** **Automation secret for PowerShell scripts**
   - **有効期限:** 6 か月 (またはポリシーに応じて 12 か月)

4. **追加** を選択します。

5. **シークレットの値をすぐにコピーします** (**値** 列にある長い英数字の文字列)。

   > [!WARNING]
   > クライアント シークレットは 1 回だけ表示されます。紛失した場合は、新しいシークレットを生成する必要があります。

6. シークレットを安全に保存します (例: Azure Key Vault またはパスワード マネージャー)。ラボの目的では、SEA-DEV1 上のテキスト ファイル (例: C:\LabScripts\ClientSecret.txt) に保存します。

**無人認証用のクライアント シークレットが正常に作成されました。**

#### タスク 5: アプリケーション資格情報を使用した Microsoft Graph への認証

1. **SEA-DEV1** で、**Windows PowerShell** (管理者) を開きます。

2. 自動化スクリプト用のフォルダーを作成します。

   ```powershell
   New-Item -Path "C:\LabScripts" -ItemType Directory -Force
   ```

3. 認証スクリプトを作成し、C:\LabScripts\Connect-GraphApp.ps1 に保存します。まず、単一引用符で囲まれた \<Your Tenant ID\>、\<Your Application (client) ID\>、\<Your Client Secret\> を、先ほどコピーした値に置き換え、次を実行してファイルを書き込みます。

   ```powershell
   @'
   $tenantId = "<Your Tenant ID>"
   $clientId = "<Your Application (client) ID>"
   $clientSecret = "<Your Client Secret>"
   # Convert client secret to secure string
   $secureSecret = ConvertTo-SecureString $clientSecret -AsPlainText -Force
   # Create credential object
   $credential = New-Object System.Management.Automation.PSCredential ($clientId, $secureSecret)
   # Connect to Microsoft Graph
   Connect-MgGraph -TenantId $tenantId -ClientSecretCredential $credential
   # Verify connection
   Get-MgContext
   '@ | Out-File -FilePath "C:\LabScripts\Connect-GraphApp.ps1" -Encoding UTF8
   ```

   > [!NOTE]
   > 単一引用符で囲まれた here-string (@'...'@) は、$tenantId、$clientId などの変数を今すぐ展開するのではなく、**リテラルとして** ファイルに書き込みます。

4. スクリプト フォルダーに移動し、スクリプトを実行します。

   ```powershell
   cd C:\LabScripts
   .\Connect-GraphApp.ps1
   ```

5. Get-MgContext の出力を確認して、接続を検証します。

   - **TenantId:** テナント ID と一致するはずです
   - **Scopes:** 付与されたアプリケーションのアクセス許可が表示されるはずです
   - **AuthType:** "AppOnly" と表示されるはずです

**アプリケーション資格情報を使用して Microsoft Graph に正常に認証されました。**

#### タスク 6: Graph PowerShell を使用した管理対象デバイスのクエリ

1. PowerShell セッション (Graph に接続済み) で、すべての管理対象デバイスをクエリします。

   ```powershell
   Get-MgDeviceManagementManagedDevice | Select-Object DeviceName, OperatingSystem, ComplianceState, LastSyncDateTime
   ```

2. 出力を確認します。SEA-DEV1 と SEA-DEV2 が、それぞれのコンプライアンス状態とともに一覧表示されるはずです。

3. 特定のフィルターを使用してデバイスをクエリします。

   ```powershell
   # Get devices running Windows
   Get-MgDeviceManagementManagedDevice -Filter "operatingSystem eq 'Windows'" | Select-Object DeviceName, OperatingSystem
   # Get non-compliant devices
   Get-MgDeviceManagementManagedDevice -Filter "complianceState eq 'noncompliant'" | Select-Object DeviceName, ComplianceState
   ```

4. Pharmacy スコープ タグ (**ラボ 01 演習 2 タスク 6** で作成し、**ラボ 02 ～ 04** でプロファイルに適用) が付けられた構成プロファイルをクエリします。これは、委任管理者 (Pharmacy Helpdesk) に表示されるすべてのものを列挙する、Graph PowerShell の標準的な方法です。

   > [!NOTE]
   > roleScopeTags コレクションは、現時点では **beta** Graph エンドポイント経由でのみ公開されているため、このルックアップでは型指定された Get-Mg* コマンドレットではなく、Invoke-MgGraphRequest を直接使用します。

   ```powershell
   # Resolve the Pharmacy scope tag's numeric ID via the beta endpoint
   $tagsResp = Invoke-MgGraphRequest -Method GET -Uri 'https://graph.microsoft.com/beta/deviceManagement/roleScopeTags'
   $pharmacyTag = $tagsResp.value | Where-Object { $_.displayName -eq 'Pharmacy' }
   if ($pharmacyTag) {
       Write-Output "Pharmacy scope tag ID: $($pharmacyTag.id)"
   } else {
       Write-Output "Pharmacy scope tag not found - confirm it was created in Lab 01 Exercise 2 Task 6"
   }
   # List all device configuration profiles that include the Pharmacy scope tag
   Get-MgDeviceManagementDeviceConfiguration -All |
       Where-Object { $_.AdditionalProperties.roleScopeTagIds -contains $pharmacyTag.id } |
       Select-Object DisplayName, Id
   # List all compliance policies tagged Pharmacy
   Get-MgDeviceManagementDeviceCompliancePolicy -All |
       Where-Object { $_.AdditionalProperties.roleScopeTagIds -contains $pharmacyTag.id } |
       Select-Object DisplayName, Id
   ```

   > [!NOTE]
   > Graph API は、roleScopeTagIds 配列を介して、オブジェクトごとにスコープ タグのメンバーシップを公開します。これは、委任管理者に表示される内容をフィルター処理する際に Microsoft Intune 管理センターが読み取る基になるフィールドです。Graph 経由で直接クエリすることが、委任チームにスコープを絞ったコンプライアンス ダッシュボードを構築する方法であり、特定のスコープ タグがどのポリシーに適用されているかを監査する方法でもあります。

**Microsoft Graph PowerShell を使用して、管理対象デバイスと Pharmacy スコープのポリシーが正常にクエリされました。**

#### タスク 7: Graph API を使用したコンプライアンス ポリシーの作成

Microsoft Intune 管理センターの代わりに、Graph API を使用して Windows コンプライアンス ポリシーを作成します。

1. PowerShell セッションで、コンプライアンス ポリシーの JSON ペイロードを定義します。末尾の **scheduledActionsForRule** ブロックに注意してください。Graph API では、すべてのコンプライアンス ポリシーに **正確に 1 つの** ブロック アクションが必要なため、このネストされたオブジェクトは必須です。

   ```powershell
   $compliancePolicyJson = @"
   {
     "@odata.type": "#microsoft.graph.windows10CompliancePolicy",
     "displayName": "Graph API - Windows Compliance Policy",
     "description": "Compliance policy created via Microsoft Graph PowerShell",
     "passwordRequired": true,
     "passwordBlockSimple": true,
     "passwordMinimumLength": 8,
     "passwordRequiredType": "alphanumeric",
     "osMinimumVersion": "10.0.19041",
     "bitLockerEnabled": true,
     "secureBootEnabled": true,
     "codeIntegrityEnabled": true,
     "storageRequireEncryption": true,
     "scheduledActionsForRule": [
       {
         "ruleName": "PasswordRequired",
         "scheduledActionConfigurations": [
           {
             "actionType": "block",
             "gracePeriodHours": 0,
             "notificationTemplateId": "",
             "notificationMessageCCList": []
           }
         ]
       }
     ]
   }
   "@
   ```

   > [!IMPORTANT]
   > v1.0 の **windows10CompliancePolicy** で使用できるプロパティは、Windows デバイスの正常性構成証明の設定 (BitLocker、Secure Boot、Code Integrity、パスワード規則、ストレージの暗号化) に限定されています。ファイアウォール、ウイルス対策、Defender 関連のプロパティは windows10MobileCompliancePolicy に存在するか、beta のみの型が必要です。v1.0 の完全なプロパティ一覧は [Microsoft Graph → Create windows10CompliancePolicy](https://learn.microsoft.com/graph/api/intune-deviceconfig-windows10compliancepolicy-create?view=graph-rest-1.0) にあります。

2. Graph API を使用してポリシーを作成します。

   ```powershell
   Invoke-MgGraphRequest -Method POST -Uri "https://graph.microsoft.com/v1.0/deviceManagement/deviceCompliancePolicies" -Body $compliancePolicyJson -ContentType "application/json"
   ```

3. ポリシーが作成されたことを確認します。

   ```powershell
   Get-MgDeviceManagementDeviceCompliancePolicy | Where-Object { $_.DisplayName -eq "Graph API - Windows Compliance Policy" } | Select-Object DisplayName, Description, Id
   ```

**Microsoft Graph API を使用してコンプライアンス ポリシーが正常に作成されました。**

#### タスク 8: コンプライアンス ポリシーのグループへの割り当て

1. ポリシー ID を取得します。

   ```powershell
   $policy = Get-MgDeviceManagementDeviceCompliancePolicy | Where-Object { $_.DisplayName -eq "Graph API - Windows Compliance Policy" }
   $policyId = $policy.Id
   ```

2. ターゲット グループの ID を取得します (例: dyn-Windows-Devices)。

   ```powershell
   $group = Get-MgGroup -Filter "displayName eq 'dyn-Windows-Devices'"
   $groupId = $group.Id
   ```

3. 割り当ての JSON ペイロードを作成します。assignments 配列ラッパーに注意してください。/assign アクションは、単一の割り当てオブジェクトではなく、コレクションを受け入れます。

   ```powershell
   $assignmentJson = @"
   {
     "assignments": [
       {
         "target": {
           "@odata.type": "#microsoft.graph.groupAssignmentTarget",
           "groupId": "$groupId"
         }
       }
     ]
   }
   "@
   ```

4. **/assign** アクション エンドポイント (/assignments ではなく) を使用して、ポリシーをグループに割り当てます。

   ```powershell
   Invoke-MgGraphRequest -Method POST -Uri "https://graph.microsoft.com/v1.0/deviceManagement/deviceCompliancePolicies/$policyId/assign" -Body $assignmentJson -ContentType "application/json"
   ```

   > [!NOTE]
   > コンプライアンス ポリシーの割り当ては、サブコレクションへの POST (/assignments) ではなく、Graph の **アクション** (/assign) です。このアクションは割り当てセット全体を受け取り、既存の割り当てをすべて置き換えます。べき等な自動化スクリプトに役立ちます。

5. Microsoft Intune 管理センターで割り当てを確認します。

   - **デバイス** → **コンプライアンス** → **Graph API - Windows Compliance Policy** → **プロパティ** の順に移動します

**Microsoft Graph API を使用してコンプライアンス ポリシーがグループに正常に割り当てられました。**

### 演習 2: プロアクティブな修復の展開

#### シナリオ

プロアクティブな修復は、ユーザーが報告する前に、一般的なデバイスの問題を自動的に検出して修正します。新しい修復スクリプトの中上級パターンは、**パイロット優先の展開** です。まずパイロット コホートに展開し、1 ～ 2 日間、検出と修復の結果を観察してから、より広範なフリートに拡大します。ここではそのパターンに従います。ブロック モードの ESP (ラボ 01)、Pilot 更新リング (ラボ 02)、ブロック モードの ASR (ラボ 04) を受け取ったのと同じパイロット グループ (sg-Intune-Pilot-Users) が、新しい修復を最初に受け取ります。

#### タスク 1: 検出スクリプトと修復スクリプトの作成

1. **SEA-DEV1** で、修復スクリプト用のフォルダーを作成します。

   ```powershell
   New-Item -Path "C:\LabScripts\Remediations" -ItemType Directory -Force
   ```

2. 検出スクリプト (Detect-StaleWindowsUpdateCache.ps1) を作成します。

   ```powershell
   @"
   # Detection script: Check for Windows Update cache files older than 30 days
   `$updateCachePath = "C:\Windows\SoftwareDistribution\Download"
   `$oldFiles = Get-ChildItem -Path `$updateCachePath -Recurse -File -ErrorAction SilentlyContinue | Where-Object { `$_.LastWriteTime -lt (Get-Date).AddDays(-30) }
   if (`$oldFiles.Count -gt 0) {
       Write-Output "Found `$(`$oldFiles.Count) stale Windows Update cache files"
       exit 1  # Issue detected
   } else {
       Write-Output "Windows Update cache is clean"
       exit 0  # Compliant
   }
   "@ | Out-File -FilePath "C:\LabScripts\Remediations\Detect-StaleWindowsUpdateCache.ps1" -Encoding UTF8
   ```

3. 修復スクリプト (Remediate-StaleWindowsUpdateCache.ps1) を作成します。

   ```powershell
   @"
   # Remediation script: Clear stale Windows Update cache files
   `$updateCachePath = "C:\Windows\SoftwareDistribution\Download"
   try {
       Stop-Service -Name wuauserv -Force -ErrorAction SilentlyContinue
       Get-ChildItem -Path `$updateCachePath -Recurse -File -ErrorAction SilentlyContinue | Where-Object { `$_.LastWriteTime -lt (Get-Date).AddDays(-30) } | Remove-Item -Force -ErrorAction SilentlyContinue
       Start-Service -Name wuauserv -ErrorAction SilentlyContinue
       Write-Output "Stale Windows Update cache cleared"
       exit 0  # Success
   } catch {
       Write-Error "Failed to clear Windows Update cache: `$_"
       exit 1  # Failure
   }
   "@ | Out-File -FilePath "C:\LabScripts\Remediations\Remediate-StaleWindowsUpdateCache.ps1" -Encoding UTF8
   ```

**検出スクリプトと修復スクリプトが正常に作成されました。**

#### タスク 2: 修復スクリプト パッケージの Intune へのアップロード

1. **Microsoft Edge** で、[**https://intune.microsoft.com**](https://intune.microsoft.com) に移動します。

2. **admin@\<TenantPrefix\>.onmicrosoft.com** としてサインインします。

3. **テナント管理** → **コネクタとトークン** → **Windows データ** の順に移動します。

4. **Windows データ** を展開し、**プロセッサ構成で Windows 診断データを必要とする機能を有効にする** を **オン** に設定します。**Windows ライセンスの確認** を展開し、**テナントがこれらのライセンスのいずれかを所有していることを確認します** を **オン** に設定します。

5. **Microsoft Intune 管理センター**で、**デバイス** を選択し、次に **スクリプトと修復** を選択します。

6. **修復** タブを選択します。

7. **+ 作成** を選択します。

8. **基本情報** タブで、次を入力します。

   - **名前:** **Remediation - Clear Stale Windows Update Cache**
   - **説明:** **Detects and removes Windows Update cache files older than 30 days**

9. **次へ** を選択します。

10. **設定** タブで、次を構成します。

    - **検出スクリプト ファイル:** C:\LabScripts\Remediations\Detect-StaleWindowsUpdateCache.ps1 を参照して選択します
    - **修復スクリプト ファイル:** C:\LabScripts\Remediations\Remediate-StaleWindowsUpdateCache.ps1 を参照して選択します
    - **このスクリプトをログオン資格情報を使用して実行する:** いいえ (SYSTEM として実行)
    - **スクリプト署名チェックを強制する:** いいえ
    - **64 ビット PowerShell でスクリプトを実行する:** はい

11. **次へ** を選択します。

12. **スコープ タグ** タブで、**次へ** を選択します。

13. **割り当て** タブの **割り当て先** で、**+ 含めるグループの選択** を選択します。

14. **sg-Intune-Pilot-Users** (ラボ 01 のパイロット コホート。検出と修復の結果を確認した後、タスク 4 でフリートに拡大します) を検索して選択します。

15. **選択** を選択します。

16. **次へ** → **作成** の順に選択します。

**プロアクティブな修復スクリプト パッケージが正常にアップロードされ、パイロット コホートに割り当てられました。**

#### タスク 3: 修復の実行の監視

1. **Microsoft Intune 管理センター**の **修復** タブで、**Remediation - Clear Stale Windows Update Cache** を選択します。

2. 左側のナビゲーションから **デバイスの状態** を選択します。

3. 修復がデバイス上で実行されるまで、10 ～ 15 分待ちます。

   > [!NOTE]
   > 修復はスケジュールに従って実行されます (既定: 1 日に 1 回)。より迅速にテストするには、デバイスの同期を強制するか、次の同期サイクルを待ちます。

4. デバイスの状態を確認します。

   - **検出状態:** 問題が検出された (終了コード 1) か、検出されなかった (終了コード 0) かを示します
   - **修復状態:** 修復が成功した (終了コード 0) か、失敗した (終了コード 1) かを示します
   - **最終チェックイン:** スクリプトが最後に実行された日時

**プロアクティブな修復スクリプトが正常に展開され、監視されました。**

#### タスク 4: 修復のパイロットからフリートへの拡大

パイロット デバイスの状態 (タスク 3) で、検出スクリプトが問題なく実行され (誤検出なし)、修復スクリプトが成功している (スクリプト エラーなし) ことが示されたら、割り当てをより広範なフリートに拡大します。これは、あらゆる新しい修復スクリプトの標準的な _パイロット → フリート_ の展開です。

1. **Microsoft Intune 管理センター**の **修復** タブで、**Remediation - Clear Stale Windows Update Cache** を選択します。

2. 左側のナビゲーションから **プロパティ** を選択し、**割り当て** セクションで **編集** を選択します。

3. **割り当て先** → **+ 含めるグループの選択** で 2 つ目の割り当てを追加し、**dyn-Windows-Devices** を選択します。含まれるグループから **sg-Intune-Pilot-Users** グループを削除します。**除外グループ** で、**+ 除外するグループの選択** を選択し、**sg-Intune-Pilot-Users** を追加します (パイロットには既に適用されているため、二重に割り当てる必要はありません)。

4. **確認と保存** → **保存** の順に選択します。

   > [!NOTE]
   > 実際の運用環境での展開では、この手順の前にパイロットを 24 ～ 72 時間実行し、検出スクリプトの終了コード 1 の割合が実際の問題の発生率と一致していること (つまり誤検出がないこと)、および修復が実行されるたびに成功したことを確認したいところです。このラボでは、展開のフローをシミュレートしています。

**修復がパイロットからより広範なフリートに正常に拡大されました。**

### 演習 3: Pharmacy Helpdesk 委任ロールのエンドツーエンドでの割り当てと検証

#### シナリオ

**ラボ 01 演習 2 タスク 6** では、**Pharmacy Helpdesk** カスタム Intune ロールと **Pharmacy** スコープ タグを作成しました。**ラボ 02 ～ 04** では、Pharmacy スコープ タグを構成プロファイル (ラボ 02 演習 1 ～ 2)、コンプライアンス ポリシー (ラボ 02 演習 2)、パイロット更新リング (ラボ 02 演習 4)、Win32 LOB アプリ (ラボ 03 演習 2)、Defender セキュリティ ベースライン + ウイルス対策 + ASR (ラボ 04 演習 2)、BitLocker ポリシー (ラボ 04 演習 3) に適用しました。ここでは、このロールを委任管理者 (**Lee Gu**、LeeG@\<TenantPrefix\>.OnMicrosoft.com) に **割り当て**、次に **Lee Gu としてサインイン** して、委任管理者にはテナント全体ではなく、Pharmacy スコープのオブジェクトのみが表示されることをエンドツーエンドで検証します。

これは、ラボ シリーズ全体にわたる Thread A の集大成です。この演習の終了までに、Lee Gu は Pharmacy の臨床ポリシーを管理できますが、テナントの残りの部分からは見えない形で分離されます。

#### タスク 1: Pharmacy Helpdesk ロールと Pharmacy スコープ タグの確認

1. **Microsoft Intune 管理センター**で、**テナント管理** を選択し、**ロール** を選択します。

2. **すべてのロール** を選択します。**Pharmacy Helpdesk** (**ラボ 01 演習 2 タスク 6** で作成) を見つけて選択します。

3. 左側のナビゲーションから **プロパティ** を選択します。

4. **アクセス許可** の横にある **編集** を選択します。

5. **アクセス許可** タブを確認します。アクセス許可が正しく設定されていることを確認します。

   - **管理対象デバイス:** 読み取り、プライマリ ユーザーの設定、更新 = **はい**。削除とワイプ = **いいえ**
   - **リモート タスク:** デバイスの同期、今すぐ再起動、診断の収集 = **はい**
   - **組織:** 読み取り = **はい**
   - **ロール:** 読み取り = **はい**
   - **デバイス コンプライアンス ポリシー**、**デバイス構成**、**マネージド アプリ**、**モバイル アプリ**、**エンドポイント保護レポート**、**セキュリティ ベースライン:** 読み取り = **はい**。作成、更新、削除、割り当て = **いいえ**
   - **リモート ヘルプ アプリ:** 完全な制御を取得 = **はい**。画面の表示 = **はい**

   > [!NOTE]
   > これは、ラボ 01 で定義した最小特権の原則に基づくロールです。日常的にデバイスを操作するには十分ですが、ポリシーを変更する権限はありません。Pharmacy Helpdesk は、デバイスの同期、再起動の強制、診断の収集は行えますが、"BitLocker must be on" と定めるコンプライアンス ポリシーを作成または削除することはできません。

6. **Pharmacy Helpdesk | プロパティ** に戻り、**Pharmacy** スコープ タグが **スコープ タグ** の下に一覧表示されていることを確認します。

7. **テナント管理** → **ロール** → **スコープ タグ** に戻り、**Pharmacy** を選択します。**スコープ タグ Pharmacy** ページで、**基本** セクション (名前と説明) と、スコープ タグが割り当てられているグループを一覧表示する **割り当て** セクションを確認します。

**ラボ 01 で作成したロールとスコープ タグが正常に確認されました。**

#### タスク 2: ラボ シリーズ全体にわたる Pharmacy タグ付きオブジェクトのインベントリ

ロールを割り当てる前に、Lee Gu に表示されるようになるオブジェクトを確認します。これは、**演習 1 タスク 6** で実行した Graph PowerShell クエリと一致します。今回はポータル UI で行います。

1. **Microsoft Intune 管理センター**で、**デバイス** → **デバイスの管理** → **構成** の順に移動します。

2. ポリシーの一覧で、**スコープ タグ** 列を探します (表示されていない場合は列の選択ツールで追加します)。スコープ タグ列に **Pharmacy** が表示されているポリシーを、フィルター処理またはスクロールして見つけます。想定: **ラボ 02 演習 1** の設定カタログとデバイスの制限のプロファイル、および競合解決で残した場合はカメラ無効化プロファイル。

3. **デバイス** → **デバイスの管理** → **コンプライアンス** の順に移動します。Compliance - Windows Security Baseline に **Pharmacy** が表示されていることを確認します。

4. **アプリ** → **すべてのアプリ** の順に移動します。7-Zip Portable と 7-Zip Portable v2.0 (またはカスタムのポータブル アプリ) を選択し、**プロパティ** を選択します。**スコープ タグ** セクションに **Pharmacy** が表示されていることを確認します。

5. **エンドポイント セキュリティ** に移動します。**セキュリティ ベースライン**、**ウイルス対策**、**攻撃面の減少**、**ディスクの暗号化** の各オプションを個別に選択します。Security Baseline - Defender for Endpoint、Antivirus - Defender Configuration、ASR - Block (Pilot)、BitLocker - Full Disk Encryption の各ポリシーの **スコープ タグ** に、すべて **Pharmacy** が一覧表示されていることを確認します。

   > [!NOTE]
   > 想定されるオブジェクトに **Pharmacy** が表示されない場合は、そのラボの演習に戻ってスコープ タグを追加します (いつでも対応できます。スコープ タグは、ポリシーの **プロパティ** → **スコープ タグ** → **編集** から後からでも編集できます)。

**Pharmacy タグ付きオブジェクトのインベントリが正常に作成されました。**

#### タスク 3: Pharmacy Helpdesk ロールの Lee Gu への割り当て

Intune のロールの割り当てでは、**セキュリティ グループのみ** を受け入れます。**管理者グループ** タブや **スコープ (グループ)** タブで個々のユーザーを直接追加することはできません。そのため、まずセキュリティ グループを作成し、Lee Gu をメンバーとして追加してから、そのグループをロールに割り当てます。

1. **Microsoft Intune 管理センター**で、**グループ** → **すべてのグループ** の順に移動します。

2. **+ 新しいグループ** を選択し、次を入力します。

   - **グループの種類:** セキュリティ
   - **グループ名:** **sg-Pharmacy-Helpdesk-Admins**
   - **メンバーシップの種類:** 割り当て済み

3. **メンバー** で、**メンバーが選択されていません** を選択します。**Lee Gu** (LeeG@\<TenantPrefix\>.OnMicrosoft.com) を検索して選択し、**選択** を選択します。

4. **作成** を選択します。

5. **テナント管理** → **ロール** → **すべてのロール** の順に移動します。

6. **Pharmacy Helpdesk** を選択します。

7. 左側のナビゲーションから **割り当て** を選択します。

8. **+ 割り当て** を選択します。

9. **基本情報** ページで、次を入力します。

   - **割り当て名:** **Pharmacy Helpdesk - Lee Gu**
   - **説明:** **Grants Lee Gu Pharmacy-scoped helpdesk access**

10. **次へ** を選択します。

11. **管理者グループ** タブで、**グループの追加** を選択します。

    > [!NOTE]
    > 管理者グループ タブは、_誰が_ ロールを保持するかを定義します。グループのみを受け入れるため、Lee Gu を直接ではなく、(Lee Gu を含む) sg-Pharmacy-Helpdesk-Admins を割り当てます。

12. **sg-Pharmacy-Helpdesk-Admins** を検索して選択します。

13. **選択** を選択し、次に **次へ** を選択します。

14. **スコープ グループ** タブで、**グループの追加** を選択し、**dyn-Windows-Devices** (Pharmacy 操作のデバイス ターゲット) を追加します。**選択** を選択し、次に **次へ** を選択します。

15. **スコープ タグ** タブで、**+ スコープ タグの選択** を選択し、**Pharmacy** を選びます。**選択** を選択します。

    > [!IMPORTANT]
    > **スコープ (タグ) が、ロールを実際にスコープ化するものです。** 割り当てにスコープ タグがないと、Lee Gu はデバイス ターゲット グループ内のすべてのオブジェクトを表示できてしまいます。スコープ タグは、ロールのアクセス許可および割り当てのグループ ターゲットと交差して、最終的な表示範囲を生成します。つまり、dyn-Windows-Devices にも含まれる Pharmacy タグ付きオブジェクトのみが対象になります。

16. **次へ** → **作成** の順に選択します。

**Pharmacy Helpdesk ロールが Lee Gu に正常に割り当てられました。**

#### タスク 4: Lee Gu としてサインインし、スコープされた表示範囲をエンドツーエンドで検証する

これは Thread A の正念場です。Lee Gu としてサインインし、ラボ 01 ～ 04 で構築した Pharmacy スコープのチェーン全体が表示され、それ以外は何も表示されないことを確認します。

1. 新しい **InPrivate** ウィンドウまたは **Incognito** ウィンドウを開きます。

2. [**https://intune.microsoft.com**](https://intune.microsoft.com) に移動します。

3. **LeeG@\<TenantPrefix\>.OnMicrosoft.com** としてサインインします。Lee Gu のパスワード (ラボの資格情報配布資料に記載) を使用します。

   > [!NOTE]
   > Lee Gu が MFA のセットアップを完了していない場合は、登録を求められます。Authenticator のセットアップを完了します。**ラボ 02 演習 2** のレポート専用モード (または **ラボ 04 演習 6** の後に適用) の条件付きアクセス ポリシーは、Lee が sg-Intune-Pilot-Users に含まれていないため、Lee Gu をブロックしません。

4. Lee Gu として Intune 管理センターで、**デバイス** → **デバイスの管理** → **構成** の順に移動します。

5. Lee Gu には、**Pharmacy** タグが付けられた構成プロファイル **のみ** が表示されることを確認します。**Default** のみのタグが付けられた一部のプロファイル (機能更新プロファイル、優先品質更新ポリシー) は、Lee Gu のビューに表示され **ない** はずです。

6. **デバイス** → **デバイスの管理** → **コンプライアンス** の順に移動します。Compliance - Windows Security Baseline が表示され、他のコンプライアンス ポリシーは表示されないことを確認します。

7. **アプリ** → **すべてのアプリ** の順に移動します。7-Zip Portable と 7-Zip Portable v2.0 (またはカスタムのポータブル アプリ) が表示され、Microsoft 365 Apps、Microsoft To Do、Google Chrome (Default タグ付き) は表示され **ない** ことを確認します。

8. **エンドポイント セキュリティ** → **セキュリティ ベースライン** / **ウイルス対策** / **攻撃面の減少** / **ディスクの暗号化** の順に移動します。Pharmacy タグ付きのポリシーのみが表示されることを確認します。

9. Antivirus - Defender Configuration ポリシーの **編集** を試みます。

   - ポリシーを開きます
   - **プロパティ** までスクロールし、設定セクションで **編集** の選択を試みます
   - **編集** ボタンはグレーアウトされているか使用できないはずです。または選択すると承認エラーが返されます。Lee Gu のロールでは、コンプライアンス ポリシーに対する **読み取り** は許可されていますが、**作成/更新/削除** は許可されていません

   > [!NOTE]
   > **これで、Lee Gu が Pharmacy の臨床ポリシーを表示および監査し、デバイスを同期し、リモート タスクを実行できる一方で、ポリシーの編集や削除はできないことが証明されました。** これはまさに中上級の委任パターンです。スコープされた表示範囲 + 制限された書き込み権限です。Pharmacy Helpdesk は日常的なデバイス操作を処理し、中央 IT (Jordan Chen、グローバル管理者) がポリシーの作成権限を保持します。

10. **リモート ヘルプ** を試します (これは **ラボ 06 演習 2** で完全に有効化して実行します)。Lee Gu として Intune 管理センターで、**テナント管理** → **リモート ヘルプ** の順に移動します。Lee Gu には **"アクセス権がありません"** と表示されます。

11. InPrivate ウィンドウからサインアウトし、Jordan Chen の管理者セッションに戻ります。

**Pharmacy Helpdesk ロール + Pharmacy スコープ タグの委任が、ラボ シリーズ全体にわたって設計どおりに機能することが、エンドツーエンドで正常に検証されました。**

### 演習 4: 監査ログと運用の正常性の監視

#### シナリオ

監査ログは、Intune の管理アクションを追跡し、説明責任とトラブルシューティングの分析情報を提供します。監査ログを確認し、ログを Azure Monitor にルーティングするための診断設定を構成します (概念的な内容)。

#### タスク 1: 監査ログの確認

1. **Microsoft Intune 管理センター**で、**テナント管理** を選択し、次に **監査ログ** を選択します。

2. **監査ログ** ページで、最近の管理アクションの一覧を確認します。

   - **アクティビティ:** アクションの種類 (作成、更新、削除、割り当てなど)
   - **日付:** アクションのタイムスタンプ
   - **開始者 (アクター):** アクションを実行したユーザーまたはサービス プリンシパル
   - **ターゲット:** 変更されたオブジェクト (ポリシー、デバイス、アプリなど)

3. アクティビティでログをフィルター処理します。

   - **アクティビティ** ドロップダウンを使用して、アクションの種類 (例: "ポリシーの作成") でフィルター処理します
   - **日付範囲** ピッカーを使用して、期間でフィルター処理します

4. 監査ログのエントリを選択して、詳細情報を表示します。

   - **プロパティ:** 変更前後の状態を示す JSON ペイロード (更新アクションの場合)
   - **アクター:** アクションを実行したユーザーの UPN と IP アドレス

   > [!NOTE]
   > 監査ログは Intune で 30 日間保持されます。長期保持するには、ログを Azure Monitor または SIEM システムにエクスポートします。

**Intune の監査ログが正常に確認されました。**

#### タスク 2: 監査ログの CSV へのエクスポート

1. **監査ログ** ページで、上部のツールバーから **エクスポート** を選択します。

2. エクスポートが完了するまで待ち、CSV ファイルをダウンロードします (小規模なデータセットでは通常 1 ～ 2 分)。

3. CSV ファイルを **Excel** で開き、列を確認します。

   - **日付**
   - **アクティビティ**
   - **開始者**
   - **ターゲット**
   - **カテゴリ**

**レポート用に監査ログが正常にエクスポートされました。**

#### タスク 3: 診断設定の理解 (概念)

診断設定は、長期保持と高度なクエリのために、Intune のログを Azure Monitor Log Analytics にルーティングします。

1. **Microsoft Intune 管理センター**で、**テナント管理** → **診断設定** の順に移動します。

   > [!NOTE]
   > 診断設定には、Azure サブスクリプションと Log Analytics ワークスペースが必要です。ラボの目的では、構成オプションを概念的に確認します。

2. 利用可能なログ カテゴリを確認します。

   - **AuditLogs:** Intune の管理アクション

   > [!NOTE]
   > 現在の Intune ポータルは、このテナントで **AuditLogs** を公開しています。他のログ カテゴリはサービスとテナントによって異なる場合があります。**OperationalLogs** や **DeviceComplianceOrg** がすべてのポータル エクスペリエンスで表示されるとは限りません。

3. 構成のワークフローを理解します (作成はしません)。

   - Azure で Log Analytics ワークスペースを作成する
   - Intune で、ワークスペースを指す診断設定を作成する
   - ログは、KQL (Kusto クエリ言語) でクエリするために Azure Monitor にルーティングされる
   - 保持期間は、90 日、1 年、またはそれ以上に延長できる

**診断設定によって長期のログ保持と高度な分析がどのように可能になるかを理解しました。**

#### タスク 4: 以前のラボの条件付きアクセス、コンプライアンス、RBAC 操作のトレース

監査ログは、"誰が、何を、いつ、なぜ変更したか" を再構築する方法であり、インシデント後のレビューの基盤です。ラボ シリーズ全体で実行した特定の操作をトレースします。

1. **Microsoft Intune 管理センター**の **テナント管理** → **監査ログ** で、ログをフィルター処理します。

   - **日付:** **日付** フィルターで、**開始** と **終了** を過去 7 日間をカバーするように設定し、**適用** を選択します
   - **アクティビティ:** **アクティビティ** 検索ボックスに Create と入力し、関連する作成アクティビティ (例: **Create DeviceCompliancePolicy** や **Create DeviceAndAppManagementRoleAssignment**) を選択してポリシー/ロールの作成イベントを見つけ、**適用** を選択します

2. **Pharmacy Helpdesk** カスタム ロール作成 (**ラボ 01 演習 2 タスク 6**) の監査ログ エントリを見つけます。それを選択し、ロールのアクセス許可の付与を示す **プロパティ** → JSON ペイロードを確認します。

3. **Compliance - Windows Security Baseline** 作成 (**ラボ 02 演習 2 タスク 1**) の監査ログ エントリを見つけます。**開始者** フィールドにグローバル管理者アカウントが表示され、**ターゲット** に Compliance - Windows Security Baseline ポリシーが表示されることを確認します。

4. **Pharmacy Helpdesk → Lee Gu** ロールの割り当て (このラボの **演習 3 タスク 3** で作成) の監査ログ エントリを見つけます。割り当てのペイロードに **Pharmacy** スコープ タグと **dyn-Windows-Devices** グループが含まれていることを確認します。

5. **ラボ 02 演習 6 タスク 2** で競合を解決するために WIN - Camera - Enabled (Pilot) を **削除** した監査ログ エントリを見つけます。アクティビティは **Delete deviceConfiguration** です。プロパティ ペインには、削除されたオブジェクトの最後に判明していた状態が含まれており、ロールバックの判断に役立ちます。

6. [**https://entra.microsoft.com**](https://entra.microsoft.com) で **Microsoft Entra 管理センター** に切り替えます。**監視と正常性** → **監査ログ** (Intune のものとは異なる Entra の監査ログ) の順に移動します。

7. Entra の監査ログをフィルター処理します。

   - **サービス:** 条件付きアクセス
   - **日付:** 過去 7 日間

8. CA - Require compliant device (Pharmacy pilot) を **レポート専用** から **オン** に **切り替えた** エントリ (**ラボ 04 演習 6 タスク 3**) を見つけます。プロパティにポリシーの状態変更が表示されます。

   > [!NOTE]
   > **2 つの別々の監査ログ。** Intune 固有のアクション (コンプライアンス、構成、アプリ、RBAC、スコープ タグ) は、**テナント管理** の下の **Intune の監査ログ** にあります。条件付きアクセス ポリシー、Entra のロールの割り当て、ディレクトリ操作は、**ID → 監視と正常性** の下の **Entra の監査ログ** にあります。実際のインシデントを調査するときは、通常、両方が必要です。

**Intune と Entra の両方の監査ログにわたって操作が正常にトレースされました。**

### 演習 5: 組み込みレポートの使用

#### シナリオ

Intune には、デバイス、コンプライアンス、構成、アプリケーションなどの組み込みレポートが用意されています。運用上の分析情報を得るために、レポートを生成してエクスポートします。

#### タスク 1: デバイス コンプライアンス レポートの生成

1. **Microsoft Intune 管理センター**で、**レポート** → **デバイスのコンプライアンス** の順に移動します。

2. **レポート** タブを選択し、次に **非準拠のデバイスと設定** を選択します。

3. **レポートの生成** (以前に生成した場合は **レポートの実行**) を選択します。

4. レポート データを確認します。

   - **デバイス名**
   - **プライマリ ユーザーのプリンシパル名**
   - **設定のコンプライアンス状態**
   - **最終チェックイン**
   - **オペレーティング システム**

5. **フィルター** オプションを使用して、結果を絞り込みます (例: OS = Windows でフィルター処理)。

6. **エクスポート** を選択し、次に **はい** を選択して、レポートを CSV としてダウンロードします。

**デバイス コンプライアンス レポートが正常に生成され、エクスポートされました。**

#### タスク 2: デバイス構成レポートの生成

1. **Microsoft Intune 管理センター**で、**レポート** → **デバイス構成** の順に移動します。

2. **レポートの生成** を選択します。

3. **概要** タブで、**上位 5 つの構成ポリシーの状態** の概要を確認します。

   - **ポリシー名**
   - **ポリシーの種類**
   - **成功したデバイス**
   - **エラーのあるデバイス**
   - **競合のあるデバイス**

   > [!NOTE]
   > **概要** タブの **上位 5 つの構成ポリシーの状態** テーブルは読み取り専用の概要であり、ポリシーの行は選択できません。デバイスごとの状態を詳しく確認するには、**デバイス** → **デバイスの管理** → **構成** の順に移動し、ポリシーを選択して、**レポートの表示** を選択します。

**デバイス構成レポートが正常に生成されました。**

#### タスク 3: テナントの状態ダッシュボードの確認

1. **Microsoft Intune 管理センター**で、**テナント管理** → **テナントの状態** の順に移動します。

2. **テナントの状態** ダッシュボードを確認します。

   - **テナントの詳細:** 登録済みデバイスの総数、ライセンスを持つユーザー、Intune ライセンス
   - **サービス正常性とメッセージ センター:** Intune に影響する現在のインシデントまたはアドバイザリを表示します
   - **コネクタの状態:** コネクタ (Defender for Endpoint、Microsoft Tunnel など) の正常性を表示します

3. **サービス正常性** を見つけて、詳細なインシデント情報を表示します。

4. **メッセージ センター** を見つけて、今後の変更と機能の展開を表示します。

**テナントの状態ダッシュボードが正常に確認されました。**

### ラボの概要

おめでとうございます。ラボ 05: 自動化と運用 が完了しました。

このラボでは、次のことを達成しました。

**演習 1: Microsoft Graph PowerShell による自動化**

- Microsoft Graph PowerShell SDK をインストールした
- 無人自動化のためのアプリケーションを登録した
- API アクセス許可を付与し、クライアント シークレットを作成した
- アプリケーション資格情報を使用して Microsoft Graph に認証した
- Graph PowerShell を使用して管理対象デバイスをクエリした
- Graph API を使用してコンプライアンス ポリシーを作成し、割り当てた

**演習 2: プロアクティブな修復の展開**

- 検出と修復の PowerShell スクリプトを作成した
- 修復スクリプト パッケージを Intune にアップロードし、パイロット コホートに割り当てた
- パイロット デバイスでの修復の実行を監視した
- 展開をパイロットからより広範なフリートに拡大した

**演習 3: Pharmacy Helpdesk 委任ロールのエンドツーエンドでの割り当てと検証**

- **ラボ 01 演習 2 タスク 6** で作成した Pharmacy Helpdesk ロールと Pharmacy スコープ タグを確認した
- **ラボ 02 ～ 04** の Pharmacy タグ付きオブジェクト (構成、コンプライアンス、アプリ、セキュリティ ベースライン、ASR、BitLocker) のインベントリを作成した
- 割り当てに Pharmacy スコープ タグを付けて、Pharmacy Helpdesk ロールを Lee Gu に割り当てた
- Lee Gu としてサインインし、Pharmacy タグ付きオブジェクトのみが表示され、ポリシーの編集がブロックされることをエンドツーエンドで検証した

**演習 4: 監査ログと運用の正常性の監視**

- 管理アクションについて Intune の監査ログを確認した
- レポート用に監査ログを CSV にエクスポートした
- Azure Monitor での長期ログ保持のための診断設定を理解した
- ラボ 02 ～ 04 の条件付きアクセス、コンプライアンス、競合解決、RBAC の操作を、**Intune の監査ログ** と **Entra の監査ログ** の両方にわたってトレースした

**演習 5: 組み込みレポートの使用**

- デバイスのコンプライアンス レポートと構成レポートを生成した
- レポート データを CSV にエクスポートした
- サービス正常性とコネクタの状態についてテナントの状態ダッシュボードを確認した

**重要なポイント:**

- Microsoft Graph PowerShell は、一括操作、レポート作成、スコープ タグを認識するクエリのためのスクリプト化された自動化を可能にします (roleScopeTagIds が基になるプロパティです)
- アプリケーションのアクセス許可とクライアント シークレットにより、ユーザー操作なしで無人自動化が可能になります
- プロアクティブな修復は、ユーザーが問題を報告する前に一般的な問題を検出して修正します。パイロット優先の展開が標準的なパターンです
- カスタム RBAC ロール + スコープ タグ + グループ スコープ = Intune の委任管理の 3 つの次元です。ロールのアクセス許可がスコープ タグおよびグループ ターゲットと交差して、委任管理者に表示される最終的な表示範囲を生成します
- Pharmacy Helpdesk → Lee Gu は、エンドツーエンドのデモンストレーションです。初日 (ラボ 01) に作成したロールが、ラボ 02 ～ 04 で作成したすべてのポリシーにわたって表示範囲を制御し、ラボ 05 でのそれ以上の構成は不要です
- Intune と Entra にはそれぞれ独自の監査ログがあります。インシデントや変更を調査するときは、両方を参照します
- 組み込みレポートとテナントの状態ダッシュボードは、運用上の可視性を提供します

**次のステップ:** ラボ 06 では、Intune Suite (Endpoint Privilege Management、Remote Help、Advanced Analytics) を使用して Intune の機能を拡張し、クラウドでホストされるデスクトップ (Windows 365 と Azure Virtual Desktop) を探索します。

**ラボ終了**
