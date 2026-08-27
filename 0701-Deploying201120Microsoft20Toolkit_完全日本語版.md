### lab:
title: 'Practice Lab 0701: Microsoft Deployment Toolkit を使用した Windows 11 の展開'
description: このラボでは、Microsoft Deployment Toolkit を使用して Windows 11 オペレーティング システム イメージを作成し、展開します。
duration: 100 minutes
level: 200
islab: true
primarytopics:
- Windows
- Windows 11

## Practice Lab 0701: Microsoft Deployment Toolkit を使用した Windows 11 の展開

### 概要

このラボでは、Microsoft Deployment Toolkit を使用して Windows 11 オペレーティング システム イメージを作成し、展開します。

#### シナリオ

SEA-WS4 という名前の新しい Windows 11 仮想マシンを展開する必要があります。Microsoft Deployment Toolkit を使用して、Hyper-V で作成した仮想マシンにオペレーティング システムを展開することにしました。MDT で新しい配置共有を構成し、続いて SEA-WS4 を展開する手順を実行するタスク シーケンスを構成します。

#### タスク 1: 新しい配置共有の作成

1. **SEA-SVR2** に、**Contoso\Administrator** としてパスワード **Pa55w.rd** でサインインします。

2. タスク バーで **File Explorer** を選択し、**E:\Labfiles\ISOs** に移動します。

3. **Win11_21H2_Eval.iso** を右クリックし、**Mount** を選択します。ISO が DVD ドライブ F としてマウントされます。

4. **File Explorer** を閉じます。

5. **Start** を選択し、**Microsoft Deployment Toolkit** を展開して、**Deployment Workbench** を選択します。

6. **Deployment Workbench** で、**Deployment Shares** を右クリックし、**New Deployment Share** を選択します。

   > **New Deployment Share Wizard** が開きます。

7. **Path** ページの **Deployment share path** で、値を **E:\DeploymentShare** に変更し、**Next** を選択します。

8. **Share** ページで、**Share name** を確認します。ただし変更はしません。**Next** を選択します。

9. **Descriptive Name** ページで、既定値をそのまま使用し、**Next** を選択します。

10. **Options** ページで次のように構成し、**Next** を選択します。

    - Ask to set the local Administrator password: **Enabled**
    - その他のすべてのチェック ボックス: **Disabled**

11. **Summary** ページで情報を確認し、**Next** を選択します。

12. **Confirmation** ページで、処理が正常に完了したことを確認し、**Finish** を選択します。

13. **Deployment Shares** の下で、**MDT Deployment Share** フォルダーを展開します。

    > 配置共有に対して構成できるさまざまなノードを確認します。

#### タスク 2: 配置共有へのオペレーティング システム ファイルの追加

1. Deployment Workbench で、**Deployment Shares** を展開し、**MDT Deployment Share** を展開して、**Operating Systems** を選択します。

2. **Operating Systems** を右クリックし、**Import Operating System** を選択します。Import Operating System Wizard が開きます。

3. **Import Operating System Wizard** の **OS Type** ページで、**Full set of source files** を選択し、**Next** を選択します。

4. **Source** ページの **Source Directory** に **F:\** を入力し、**Next** を選択します。

5. **Destination** ページで、既定の宛先ディレクトリ名を **Windows 11 Enterprise x64** に変更し、**Next** を選択します。

6. **Summary** ページで情報を確認し、**Next** を選択します。

   > オペレーティング システムのソース ファイルが配置共有へコピーされます。

7. **Confirmation** ページで、処理が正常に完了したことを確認し、**Finish** を選択します。

8. **Deployment Workbench** で、**Operating Systems** を選択した状態で、オペレーティング システムが表示されることを確認します。

#### タスク 3: 配置共有へのアプリケーションの追加

1. Deployment Workbench で、**Deployment Shares** を展開し、**MDT Deployment Share** を展開して、**Applications** を選択します。

2. **Applications** を右クリックし、**New Application** を選択します。New Application Wizard が開きます。

3. **New Application Wizard** の **Application Type** ページで、**Application with source files** を選択し、**Next** を選択します。

4. **Details** ページで次のように構成し、**Next** を選択します。

    - Publisher: **Microsoft**
    - Application Name: **XML Notepad**

5. **Source** ページの **Source directory** に **E:\Labfiles\Apps** を入力し、**Next** を選択します。

6. **Destination** ページで、既定の宛先ディレクトリ名をそのまま使用し、**Next** を選択します。

7. **Command Details** ページの **Command line** に **XmlNotepadSetup.msi /q** を入力し、**Next** を選択します。

8. **Summary** ページで情報を確認し、**Next** を選択します。

9. **Confirmation** ページで、処理が正常に完了したことを確認し、**Finish** を選択します。

#### タスク 4: MDT タスク シーケンスの作成

1. Deployment Workbench で、**Deployment Shares** を展開し、**MDT Deployment Share** を展開して、**Task Sequences** を選択します。

2. **Task Sequences** を右クリックし、**New Task Sequence** を選択します。**New Task Sequence Wizard** が開きます。

3. **General Settings** ページで次のように構成し、**Next** を選択します。

    - Task sequence ID: **001**
    - Task sequence name: **Deploy Windows 11 Enterprise**

4. **Select Template** ページで、**Standard Client Task Sequence** を選択し、**Next** を選択します。

5. **Select OS** ページで、**Windows 10 Enterprise Evaluation** を選択し、**Next** を選択します。

6. **Specify Product Key** ページで、**Do not specify a product key at this time** を選択し、**Next** を選択します。

7. **OS Settings** ページで次のように構成し、**Next** を選択します。

    - Full Name: **User**
    - Organization: **Contoso Corporation**
    - Internet Explorer Home Page: **about:blank**

8. **Admin Password** ページで、**Use the specified local Administrator password** を選択し、両方のテキスト ボックスに **Pa55w.rd** を入力します。**Next** を選択します。

9. **Summary** ページで情報を確認し、**Next** を選択します。

10. **Confirmation** ページで、処理が正常に完了したことを確認し、**Finish** を選択します。

11. **Deployment Workbench** で、**Task Sequences** を選択した状態で、**Deploy Windows 11 Enterprise** タスク シーケンスが表示されることを確認します。

12. **Deploy Windows 11 Enterprise** タスク シーケンスを右クリックし、**Properties** を選択します。

13. **Task Sequence** タブを選択します。

14. **Validation** ノードを展開し、**Validate** を選択します。

15. **Properties** ページで、**Ensure minimum memory** と **Ensure minimum processor speed** の横のチェック マークを外します。

    > その他の変更は行いません。

16. **Deploy Windows 11 Enterprise Properties** ウィンドウで、**OK** を選択します。

#### タスク 5: 配置共有のプロパティと Windows PE 設定の構成

1. Deployment Workbench で、**Deployment Shares** を展開し、**MDT Deployment Share** を選択します。

2. **MDT Deployment Share** を右クリックし、**Properties** を選択します。

3. **MDT Deployment Share Properties** ウィンドウの **General** タブで、配置共有の作成時に指定された情報を確認します。

4. **Rules** タブを選択します。

   > Rules タブには CustomSettings.ini ファイルの内容が表示されます。これらの値も、配置共有の作成時に指定されたものです。

5. **Windows PE** タブを選択します。

   > Windows PE タブには、Windows PE ブート ディスクを作成するためのオプションが表示されます。

6. **Windows PE** タブで、**Platform** の横の **x64** を選択します。

7. **Windows PE Customizations** セクションで、**Scratch space size** の横の **64** を選択します。

8. **Features** タブを選択し、次の Feature Packs の横のチェック ボックスをオンにします。

    - DISM Cmdlets
    - Windows PowerShell
    - Microsoft Data Access Components (MDAC/ADO) support

9. **Monitoring** タブを選択します。

10. **Monitoring** タブで、**Enable monitoring for this deployment share** の横のチェック ボックスをオンにします。

11. **MDT Deployment Share Properties** ウィンドウで、**OK** を選択します。

12. **MDT Deployment Share** を右クリックし、**Update Deployment Share** を選択します。Update Deployment Share Wizard が開きます。

13. **Options** ページで、**Optimize the boot image updating process** を選択し、**Next** を選択します。

14. **Summary** ページで、**Next** を選択します。

    > 配置共有の更新が開始され、Windows PE ファイルが作成されます。完了までに数分かかります。

15. **Confirmation** ページで、処理が正常に完了したことを確認し、**Finish** を選択します。

#### タスク 6: MDT を使用した Windows 11 の展開

1. SEA-SVR2 のタスク バーで、**Hyper-V Manager** を選択します。

2. Hyper-V Manager で、**Virtual Switch Manager** を選択します。

3. **New virtual network switch** を選択し、詳細ペインで **External** を選択します。**Create Virtual Switch** を選択します。

4. **Virtual Switch Properties** ページの **Name** に **External network** を入力し、**OK** を選択して、続いて **Yes** を選択します。

5. Hyper-V Manager で、**SEA-SVR2** を選択し、Actions ペインで **New** を選択して、続いて **Virtual Machine** を選択します。

6. **Before you Begin** ページで、**Next** を選択します。

7. **Specify Name and Location** ページの **Name** ボックスに **SEA-WS4** を入力します。

8. **Store the virtual machine in a different location** の横のチェック ボックスをオンにし、**Location** の横に **E:\Labfiles\VirtualMachines** を入力します。**Next** を選択します。

9. **Specify Generation** ページで、**Generation 2** が選択されていることを確認し、**Next** を選択します。

10. **Assign Memory** ページの **Startup memory** の横に **8192** を入力し、**Next** を選択します。

11. **Configure Networking** ページの **Connection** の横で、**External Network** を選択し、**Next** を選択します。

12. **Connect Virtual Hard Disk** ページで、**Create a virtual hard disk** を選択し、次を入力して、**Next** をクリックします。

    - Name: **SEA-WS4.vhdx**
    - Location: **E:\Labfiles\VirtualMachines**
    - Size: **60 GB**

13. **Installation Options** ページで、**Install an operating system from a bootable image file** を選択し、次のように構成します。

    - Image file (.iso): **E:\DeploymentShare\Boot\LiteTouchPE_x64.iso**

14. **Next** を選択し、続いて **Finish** を選択します。

15. Hyper-V Manager で、**SEA-WS4** を右クリックし、**Settings** を選択します。

16. **Security** を選択し、**Enable Trusted Platform Module** の横のチェック ボックスをオンにします。

17. **Processor** を選択し、仮想プロセッサの数を **2** に変更します。

18. **OK** を選択して Settings ダイアログ ボックスを閉じます。

19. Hyper-V Manager で、**SEA-WS4** を選択し、**Connect** を選択して、続いて **Start** を選択します。

20. コンピューターの起動時に、キーボードの任意のキーを押して MDT Deployment Wizard を呼び出します。必要に応じてウィンドウを最大化します。

21. **Welcome** ページで、**Run the Deployment Wizard to install a new Operating System** を選択します。

22. **Specify credentials for connecting to network shares** ウィンドウで、次を入力し、**OK** を選択します。

    - User Name: **Administrator**
    - Password: **Pa55w.rd**
    - Domain: **Contoso**

23. **Task Sequence** ページで、**Deploy Windows 11 Enterprise** を選択し、**Next** を選択します。

24. **Computer Details** ページの **Computer name** の横に **SEA-WS4** を入力し、**Next** を選択します。

25. **Move Data and Settings** ページで、**Next** を選択します。

26. **User Data (Restore)** ページで、**Next** を選択します。

27. **Locale and Time** ページで、**Next** を選択します。

28. **Applications** ページで、**Next** を選択します。

29. **Administrator Password** ページで、両方のテキスト ボックスに **Pa55w.rd** を入力し、**Next** を選択します。

30. **Ready** ページで、**Begin** を選択します。

    > インストールが開始されます。完了までに 15～20 分かかり、インストール中に必要に応じて SEA-WS4 が再起動されます。

31. **Deployment Workbench** に切り替えます。

32. Deployment Workbench で、**Deployment Shares** を展開し、**MDT Deployment Share** を展開します。

33. **Monitoring** を選択し、詳細ペインで **SEA-WS4** をダブルクリックします。

    > 展開中の監視状態を確認します。

34. **SEA-WS4** に切り替えます。

35. インストールが完了すると、デスクトップが開いて展開が最終処理されます。展開の概要で、**Finish** を選択します。

36. **SEA-WS4** をシャットダウンし、Virtual Machine Connection ウィンドウを閉じます。

37. Hyper-V Manager で、**SEA-WS4** を右クリックし、**Settings** を選択します。

38. **Settings for SEA-WS4** で、**SCSI Controller** を展開し、**DVD Drive** を選択します。

39. 詳細ペインの **Media** の下で、**None** を選択し、**OK** を選択します。

40. **SEA-WS4** を右クリックし、**Checkpoint** を選択して、SEA-WS4 の現在の状態のチェックポイントを作成します。

41. SEA-SVR2 で、**Hyper-V Manager** を閉じ、**Deployment Workbench** を閉じます。

42. **File Explorer** を開き、**DVD Drive F** を右クリックして、**Eject** を選択します。

43. **File Explorer** を閉じ、**SEA-SVR2** からサインアウトします。

**結果**: この演習を完了すると、Microsoft Deployment Toolkit を使用して Windows 11 ワークステーションを正常に作成し、展開できています。

**ラボ終了**
