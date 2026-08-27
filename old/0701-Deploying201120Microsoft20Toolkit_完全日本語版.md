### lab:
title: '演習ラボ 0701: Microsoft Deployment Toolkit を使用した Windows 11 の展開'
description: このラボでは、Microsoft Deployment Toolkit を使用して、Windows 11 オペレーティング システム イメージを作成し、展開します。
duration: 100 minutes
level: 200
islab: true
primarytopics:
\- Windows
\- Windows 11

## 演習ラボ 0701: Microsoft Deployment Toolkit を使用した Windows 11 の展開

### 概要

このラボでは、Microsoft Deployment Toolkit を使用して、Windows 11 オペレーティング システム イメージを作成し、展開します。

#### シナリオ

SEA-WS4 という名前の新しい Windows 11 仮想マシンを展開する必要があります。Microsoft Deployment Toolkit を使用して、Hyper-V で作成した仮想マシンへオペレーティング システムを展開することにしました。MDT で新しい Deployment Share を構成し、SEA-WS4 の展開手順を実行するタスク シーケンスを構成します。

#### タスク 1: 新しい Deployment Share の作成

1. **SEA-SVR2** で、パスワード **Pa55w.rd** を使用して **Contoso\Administrator** としてサインインします。
2. タスク バーで **File Explorer** を選択し、**E:\Labfiles\ISOs** を参照します。
3. **Win11\_21H2\_Eval.iso** を右クリックし、**Mount** を選択します。ISO が DVD Drive F としてマウントされます。
4. **File Explorer** を閉じます。
5. **Start** を選択し、**Microsoft Deployment Toolkit** を展開して、**Deployment Workbench** を選択します。
6. **Deployment Workbench** で、**Deployment Shares** を右クリックし、**New Deployment Share** を選択します。<br>**New Deployment Share Wizard** が開きます。
7. **Path** ページの **Deployment share path** で、値を **E:\DeploymentShare** に変更し、**Next** を選択します。
8. **Share** ページで **Share name** を確認します。値は変更せず、**Next** を選択します。
9. **Descriptive Name** ページで既定値をそのまま使用し、**Next** を選択します。
10. **Options** ページで次のように構成し、**Next** を選択します。
    - Ask to set the local Administrator password: **Enabled**
    - その他のすべてのチェック ボックス: **Disabled**
11. **Summary** ページで情報を確認し、**Next** を選択します。
12. **Confirmation** ページで処理が正常に完了したことを確認し、**Finish** を選択します。
13. **Deployment Shares** で、**MDT Deployment Share** フォルダーを展開します。<br>Deployment Share で構成できる各種ノードを確認します。

#### タスク 2: Deployment Share へのオペレーティング システム ファイルの追加

1. **Deployment Workbench** で、**Deployment Shares**、**MDT Deployment Share** の順に展開し、**Operating Systems** を選択します。
2. **Operating Systems** を右クリックし、**Import Operating System** を選択します。**Import Operating System Wizard** が開きます。
3. **Import Operating System Wizard** の **OS Type** ページで、**Full set of source files** を選択し、**Next** を選択します。
4. **Source** ページの **Source Directory** に **F:\** と入力し、**Next** を選択します。
5. **Destination** ページで、既定の宛先ディレクトリ名を **Windows 11 Enterprise x64** に変更し、**Next** を選択します。
6. **Summary** ページで情報を確認し、**Next** を選択します。<br>オペレーティング システムのソース ファイルが Deployment Share にコピーされます。
7. **Confirmation** ページで処理が正常に完了したことを確認し、**Finish** を選択します。
8. **Deployment Workbench** で **Operating Systems** が選択されている状態で、オペレーティング システムが表示されていることを確認します。

#### タスク 3: Deployment Share へのアプリケーションの追加

1. **Deployment Workbench** で、**Deployment Shares**、**MDT Deployment Share** の順に展開し、**Applications** を選択します。
2. **Applications** を右クリックし、**New Application** を選択します。**New Application Wizard** が開きます。
3. **New Application Wizard** の **Application Type** ページで、**Application with source files** を選択し、**Next** を選択します。
4. **Details** ページで次のように構成し、**Next** を選択します。
    - Publisher: **Microsoft**
    - Application Name: **XML Notepad**
5. **Source** ページの **Source directory** に **E:\Labfiles\Apps** と入力し、**Next** を選択します。
6. **Destination** ページで既定の宛先ディレクトリ名をそのまま使用し、**Next** を選択します。
7. **Command Details** ページの **Command line** に **XmlNotepadSetup.msi /q** と入力し、**Next** を選択します。
8. **Summary** ページで情報を確認し、**Next** を選択します。
9. **Confirmation** ページで処理が正常に完了したことを確認し、**Finish** を選択します。

#### タスク 4: MDT タスク シーケンスの作成

1. **Deployment Workbench** で、**Deployment Shares**、**MDT Deployment Share** の順に展開し、**Task Sequences** を選択します。
2. **Task Sequences** を右クリックし、**New Task Sequence** を選択します。**New Task Sequence Wizard** が開きます。
3. **General Settings** ページで次のように構成し、**Next** を選択します。
    - Task sequence ID: **001**
    - Task sequence name: **Deploy Windows 11 Enterprise**
4. **Select Template** ページで **Standard Client Task Sequence** を選択し、**Next** を選択します。
5. **Select OS** ページで **Windows 10 Enterprise Evaluation** を選択し、**Next** を選択します。
6. **Specify Product Key** ページで **Do not specify a product key at this time** を選択し、**Next** を選択します。
7. **OS Settings** ページで次のように構成し、**Next** を選択します。
    - Full Name: **User**
    - Organization: **Contoso Corporation**
    - Internet Explorer Home Page: **about:blank**
8. **Admin Password** ページで **Use the specified local Administrator password** を選択し、両方のテキスト ボックスに **Pa55w.rd** と入力します。**Next** を選択します。
9. **Summary** ページで情報を確認し、**Next** を選択します。
10. **Confirmation** ページで処理が正常に完了したことを確認し、**Finish** を選択します。
11. **Deployment Workbench** で **Task Sequences** が選択されている状態で、**Deploy Windows 11 Enterprise** タスク シーケンスが表示されていることを確認します。
12. **Deploy Windows 11 Enterprise** タスク シーケンスを右クリックし、**Properties** を選択します。
13. **Task Sequence** タブを選択します。
14. **Validation** ノードを展開し、**Validate** を選択します。
15. **Properties** ページで、**Ensure minimum memory** と **Ensure minimum processor speed** の横にあるチェックを外します。<br>ほかの設定は変更しないでください。
16. **Deploy Windows 11 Enterprise Properties** ウィンドウで **OK** を選択します。

#### タスク 5: Deployment Share のプロパティと Windows PE 設定の構成

1. **Deployment Workbench** で **Deployment Shares** を展開し、**MDT Deployment Share** を選択します。
2. **MDT Deployment Share** を右クリックし、**Properties** を選択します。
3. **MDT Deployment Share Properties** ウィンドウの **General** タブで、Deployment Share の作成時に指定した情報を確認します。
4. **Rules** タブを選択します。<br>**Rules** タブには、CustomSettings.ini ファイルの内容が表示されます。これらの値も、Deployment Share の作成時に指定したものです。
5. **Windows PE** タブを選択します。<br>**Windows PE** タブには、Windows PE ブート ディスクを作成するためのオプションが表示されます。
6. **Windows PE** タブで、**Platform** の横から **x64** を選択します。
7. **Windows PE Customizations** セクションで、**Scratch space size** の横から **64** を選択します。
8. **Features** タブを選択し、次の Feature Packs の横にあるチェック ボックスをオンにします。
    - DISM Cmdlets
    - Windows PowerShell
    - Microsoft Data Access Components (MDAC/ADO) support
9. **Monitoring** タブを選択します。
10. **Monitoring** タブで、**Enable monitoring for this deployment share** の横にあるチェック ボックスをオンにします。
11. **MDT Deployment Share Properties** ウィンドウで **OK** を選択します。
12. **MDT Deployment Share** を右クリックし、**Update Deployment Share** を選択します。**Update Deployment Share Wizard** が開きます。
13. **Options** ページで **Optimize the boot image updating process** を選択し、**Next** を選択します。
14. **Summary** ページで **Next** を選択します。<br>Deployment Share の更新と Windows PE ファイルの作成が開始されます。完了まで数分かかります。
15. **Confirmation** ページで処理が正常に完了したことを確認し、**Finish** を選択します。

#### タスク 6: MDT を使用した Windows 11 の展開

1. **SEA-SVR2** のタスク バーで **Hyper-V Manager** を選択します。
2. **Hyper-V Manager** で **Virtual Switch Manager** を選択します。
3. **New virtual network switch** を選択し、詳細ペインで **External** を選択します。**Create Virtual Switch** を選択します。
4. **Virtual Switch Properties** ページの **Name** に **External network** と入力し、**OK**、**Yes** の順に選択します。
5. **Hyper-V Manager** で **SEA-SVR2** を選択し、**Actions** ペインで **New**、**Virtual Machine** の順に選択します。
6. **Before you Begin** ページで **Next** を選択します。
7. **Specify Name and Location** ページの **Name** ボックスに **SEA-WS4** と入力します。
8. **Store the virtual machine in a different location** の横にあるチェック ボックスをオンにし、**Location** の横に **E:\Labfiles\VirtualMachines** と入力します。**Next** を選択します。
9. **Specify Generation** ページで **Generation 2** が選択されていることを確認し、**Next** を選択します。
10. **Assign Memory** ページの **Startup memory** の横に **8192** と入力し、**Next** を選択します。
11. **Configure Networking** ページの **Connection** の横から **External Network** を選択し、**Next** を選択します。
12. **Connect Virtual Hard Disk** ページで **Create a virtual hard disk** を選択し、次の値を入力して **Next** を選択します。
    - Name: **SEA-WS4.vhdx**
    - Location: **E:\Labfiles\VirtualMachines**
    - Size: **60 GB**
13. **Installation Options** ページで **Install an operating system from a bootable image file** を選択し、次のように構成します。
    - Image file (.iso): **E:\DeploymentShare\Boot\LiteTouchPE\_x64.iso**
14. **Next**、**Finish** の順に選択します。
15. **Hyper-V Manager** で **SEA-WS4** を右クリックし、**Settings** を選択します。
16. **Security** を選択し、**Enable Trusted Platform Module** の横にあるチェック ボックスをオンにします。
17. **Processor** を選択し、仮想プロセッサの数を **2** に変更します。
18. **OK** を選択して **Settings** ダイアログ ボックスを閉じます。
19. **Hyper-V Manager** で **SEA-WS4** を選択し、**Connect**、**Start** の順に選択します。
20. コンピューターの起動時にキーボードの任意のキーを押して、MDT Deployment Wizard を起動します。必要に応じてウィンドウを最大化します。
21. **Welcome** ページで **Run the Deployment Wizard to install a new Operating System** を選択します。
22. **Specify credentials for connecting to network shares** ウィンドウで次の値を入力し、**OK** を選択します。
    - User Name: **Administrator**
    - Password: **Pa55w.rd**
    - Domain: **Contoso**
23. **Task Sequence** ページで **Deploy Windows 11 Enterprise** を選択し、**Next** を選択します。
24. **Computer Details** ページの **Computer name** の横に **SEA-WS4** と入力し、**Next** を選択します。
25. **Move Data and Settings** ページで **Next** を選択します。
26. **User Data (Restore)** ページで **Next** を選択します。
27. **Locale and Time** ページで **Next** を選択します。
28. **Applications** ページで **Next** を選択します。
29. **Administrator Password** ページで、両方のテキスト ボックスに **Pa55w.rd** と入力し、**Next** を選択します。
30. **Ready** ページで **Begin** を選択します。<br>インストールが開始されます。完了まで 15～20 分かかり、必要に応じてインストール中に SEA-WS4 が再起動します。
31. **Deployment Workbench** に切り替えます。
32. **Deployment Workbench** で、**Deployment Shares**、**MDT Deployment Share** の順に展開します。
33. **Monitoring** を選択し、詳細ペインで **SEA-WS4** をダブルクリックします。<br>展開中の監視状態を確認します。
34. **SEA-WS4** に切り替えます。
35. インストールが完了すると、デスクトップが開き、展開が完了します。展開の概要で **Finish** を選択します。
36. **SEA-WS4** をシャットダウンし、Virtual Machine Connection ウィンドウを閉じます。
37. **Hyper-V Manager** で **SEA-WS4** を右クリックし、**Settings** を選択します。
38. **Settings for SEA-WS4** で **SCSI Controller** を展開し、**DVD Drive** を選択します。
39. 詳細ペインの **Media** で **None** を選択し、**OK** を選択します。
40. **SEA-WS4** を右クリックし、**Checkpoint** を選択して、SEA-WS4 の現在の状態のチェックポイントを作成します。
41. **SEA-SVR2** で **Hyper-V Manager** と **Deployment Workbench** を閉じます。
42. **File Explorer** を開き、**DVD Drive F** を右クリックして、**Eject** を選択します。
43. **File Explorer** を閉じ、**SEA-SVR2** からサインアウトします。

**結果**: この演習を完了すると、Microsoft Deployment Toolkit を使用して Windows 11 ワークステーションを正常に作成し、展開できます。

**ラボ終了**
