---
lab:
  title: 'Practice Lab 0701: Deploying Windows 11 using Microsoft Deployment Toolkit'
  description: In this lab, you will use the Microsoft Deployment Toolkit to create and deploy a Windows 11 operating system image.
  duration: 100 minutes
  level: 200
  islab: true
  primarytopics:
    - Windows
    - Windows 11
---

# 演習ラボ 0701: Microsoft Deployment Toolkit を使用した Windows 11 の展開

## 概要

In this lab, you will use the Microsoft Deployment Toolkit to create and deploy a Windows 11 operating system image. 

### シナリオ

SEA-WS4 という名前の新しい Windows 11 仮想マシンを展開する必要があります。Microsoft Deployment Toolkit を使用して、Hyper-V で作成した仮想マシンへオペレーティング システムを展開することにしました。MDT で新しい展開共有を構成し、SEA-WS4 の展開手順を実行するタスク シーケンスを構成します。

### タスク 1: 新しい展開共有の作成

1. 対象: **SEA-SVR2**, としてサインインし **Contoso\\Administrator** パスワード **Pa55w.rd**.

2. タスク バーで **File Explorer** 続いて 参照します: **E:\\Labfiles\\ISOs**.

3. 右クリックし **Win11_21H2_Eval.iso** を選択してから **Mount**. ISO mounts as DVD Drive F.

4. 閉じます **File Explorer**.

5. 選択します **Start**, 展開し **Microsoft Deployment Toolkit**, を選択してから **Deployment Workbench**.

6. 対象: **Deployment Workbench**, 右クリックし **Deployment Shares** を選択してから **New Deployment Share**. 。

   > The **New Deployment Share Wizard** opens.

7. 対象: **Path** ページ, で **Deployment share path**, change value to **E:\DeploymentShare** を選択してから **Next**.

8. 対象: **Share** ページ, 確認します **Share name**, ただし 変更しないでください. 選択します **Next**.

9. 対象: **Descriptive Name** ページ, 既定値をそのまま使用し を選択し **Next**.

10. 対象: **Options** ページ, configure 次の項目, を選択してから **Next**:

       - Ask to set the local Administrator password: **Enabled**

       - All other check boxes: **Disabled**

11. 対象: **Summary** ページ, 確認し information を選択してから **Next**. 。

12. 対象: **Confirmation** ページ, 確認し process 正常に完了したこと を選択してから **Finish**.

13. Under **Deployment Shares**, 展開し **MDT Deployment Share** folder. 。

    > Take note of the various nodes that can be configured for the deployment share.

### タスク 2: 展開共有へのオペレーティング システム ファイルの追加

1. 対象: Deployment Workbench, 展開し **Deployment Shares**, 展開し **MDT Deployment Share**, を選択してから **Operating Systems**.

2. 右クリックし **Operating Systems** を選択してから **Import Operating System**. Import Operating System Wizard が開きます.

3. 対象: **Import Operating System Wizard**, on **OS Type** ページ, 選択します **Full set of source files** を選択してから **Next**.

4. 対象: **Source** ページ, で **Source Directory**, 入力します **F:\\** を選択してから **Next**.

5. 対象: **Destination** ページ, change default destination directory name to **Windows 11 入力しますprise x64** を選択してから **Next**.

6. 対象: **Summary** ページ, 確認し information を選択してから **Next**. 。

   > The operating system source files are copied into the deployment share.

7. 対象: **Confirmation** ページ, 確認し process 正常に完了したこと を選択してから **Finish**.

8. 対象: **Deployment Workbench**, を使用して **Operating Systems** 選択しますed, 確認し operating system が表示されます.

### タスク 3: 展開共有へのアプリケーションの追加

1. 対象: Deployment Workbench, 展開し **Deployment Shares**, 展開し **MDT Deployment Share**, を選択してから **Applications**.

2. 右クリックし **Applications** を選択してから **New Application**. New Application Wizard が開きます.

3. 対象: **New Application Wizard**, on **Application Type** ページ, 選択します **Application を使用して source files** を選択してから **Next**.

4. 対象: **Details** ページ, configure 次の項目, を選択してから **Next**:
    - Publisher: **Microsoft**
    - Application Name: **XML Notepad**

5. 対象: **Source** ページ, で **Source directory**, 入力します **E:\\Labfiles\\Apps** を選択してから **Next**.

6. 対象: **Destination** ページ, accept default destination directory name を選択してから **Next**.

7. 対象: **Commおよび Details** ページ, で **Commおよび line** 入力します **XmlNotepadSetup.msi /q** を選択してから **Next**.

8. 対象: **Summary** ページ, 確認し information を選択してから **Next**. 。

9. 対象: **Confirmation** ページ, 確認し process 正常に完了したこと を選択してから **Finish**.

### タスク 4: MDT タスク シーケンスの作成

1. 対象: Deployment Workbench, 展開し **Deployment Shares**, 展開し **MDT Deployment Share**, を選択してから **Task Sequences**.

2. 右クリックし **Task Sequences** を選択してから **New Task Sequence**. **New Task Sequence Wizard** が開きます.

3. 対象: **General Settings** ページ, configure 次の項目 を選択してから **Next**:
   - Task sequence ID: **001**
   - Task sequence name: **Deploy Windows 11 Enterprise**

4. 対象: **選択します Template** ページ, 選択します **Stおよびard Client Task Sequence**, を選択してから **Next**.

5. 対象: **選択します OS** ページ, 選択します **Windows 10 入力しますprise Evaluation** を選択してから **Next**.

6. 対象: **Specify Product Key** ページ, 選択します **Do not specify a product key at this time**, を選択してから **Next**.

7. 対象: **OS Settings** ページ, configure 次の項目 を選択してから **Next**:
   - Full Name: **User**
   - Organization: **Contoso Corporation**
   - Internet Explorer Home Page: **about:blank**

8. 対象: **Admin Password** ページ, 選択します **Use specified local Administrator password**, 続いて 入力します **Pa55w.rd** in both テキスト ボックスes. 選択します **Next**.

9. 対象: **Summary** ページ, 確認し information を選択してから **Next**. 。

10. 対象: **Confirmation** ページ, 確認し process 正常に完了したこと を選択してから **Finish**.

11. 対象: **Deployment Workbench**, を使用して **Task Sequences** 選択しますed 確認し **Deploy Windows 11 入力しますprise** task sequence が表示されます.

12. 右クリックし **Deploy Windows 11 入力しますprise** task sequence, を選択してから **Properties**. 。

13. 選択します **Task Sequence** タブ. 。

14. Expおよび **Validation** node を選択してから **Validate**.

15. 対象: **Properties** ページ, remove check marks の横で **Ensure minimum memory** および **Ensure minimum processor speed**. 。

    > Do not make any other changes.

16. 対象: **Deploy Windows 11 入力しますprise Properties** ウィンドウ, 選択します **OK**.

### タスク 5: 展開共有のプロパティと Windows PE 設定の構成

1. 対象: Deployment Workbench, 展開し **Deployment Shares**, を選択し **MDT Deployment Share**.

2. 右クリックし **MDT Deployment Share** を選択してから **Properties**.

3. 対象: **MDT Deployment Share Properties** ウィンドウ, on **General** タブ, 確認します information that was provided when deployment share was created.

4. 選択します **Rules** タブ. 。

   > The Rules tab displays the content of the CustomSettings.ini file. These values were also provided during the creation of the deployment share.

5. 選択します **Windows PE** タブ. 。

   > The Windows PE tab provides options for creating a Windows PE boot disk.

6. 対象: **Windows PE** タブ, の横で **Platform**, 選択します **x64**.

7. 対象: **Windows PE Customizations** section, の横で **Scratch space size**, 選択します **64**.

8. 選択します **Features** タブ を選択してから チェック ボックス の横で 次の項目 Feature Packs:
   - DISM Cmdlets
   - Windows PowerShell
   - Microsoft Data Access Components (MDAC/ADO) support

9. 選択します **Monitoring** タブ.

10. 対象: **Monitoring** タブ, 選択します チェック ボックス の横で **Enable monitoring for this deployment share**.

11. 対象: **MDT Deployment Share Properties** ウィンドウ, 選択します **OK**.

12. 右クリックし **MDT Deployment Share** を選択してから **Update Deployment Share**. Update Deployment Share Wizard が開きます.

13. 対象: **Options** ページ, 選択します **Optimize boot image updating process** を選択してから **Next**.

14. 対象: **Summary** ページ, 選択します **Next**. 。

    > The Deployment Share starts to update and create the Windows PE files. This will take a few minutes to complete.

15. 対象: **Confirmation** ページ, 確認し process 正常に完了したこと を選択してから **Finish**.

### タスク 6: MDT を使用した Windows 11 の展開

1. 対象: SEA-SVR2, on taskbar, 選択します **Hyper-V Manager**.

2. 対象: Hyper-V Manager, 選択します **Virtual Switch Manager**.

3. 選択します **New virtual network switch** 続いて in 詳細ペイン, 選択します **External**. 選択します **Create Virtual Switch**.

4. 対象: **Virtual Switch Properties** ページ, で **Name**, 入力します **External network**, 選択します **OK**, を選択してから **Yes**.

5. 対象: Hyper-V Manager, 選択します **SEA-SVR2** 続いて in Actions pane, 選択します **New** を選択してから **Virtual Machine**.

6. 対象: **Before you Begin** ページ, 選択します **Next**.

7. 対象: **Specify Name および Location** ページ, in **Name** box 入力します **SEA-WS4**. 。

8. 選択します チェック ボックス の横で **Store virtual machine in a different location** 続いて の横で **Location** 入力します **E:\\Labfiles\\VirtualMachines**. 選択します **Next**.

9. 対象: **Specify Generation** ページ, 確認し **Generation 2** is 選択しますed を選択してから **Next**.

10. 対象: **Assign Memory** ページ, の横で **Startup memory** 入力します **8192** を選択してから **Next**.

11. 対象: **Configure Networking** ページ, の横で **Connection**, 選択します **External Network** を選択してから **Next**.

12. 対象: **Connect Virtual Hard Disk** ページ, 選択します **Create a virtual hard disk** および 入力します 次の項目 続いて 選択します **Next**:

    - Name: **SEA-WS4.vhdx**
    - Location: **E:\\Labfiles\\VirtualMachines**
    - Size: **60 GB**

13. 対象: **Installation Options** ページ, 選択します **Install an operating system から a booタブle image file** および configure 次の項目:

    - Image file (.iso): **E:\\DeploymentShare\\Boot\\LiteTouchPE_x64.iso**

14. 選択します **Next** 続いて **Finish**.

15. 対象: Hyper-V Manager, 右クリックし **SEA-WS4**, を選択してから **Settings**.

16. 選択します **Security**, を選択してから チェック ボックス の横で **Enable Trusted Platform Module**.

17. 選択します **Processor**, 続いて change number of virtual processors to **2**. 。

18. 選択します **OK** to 閉じます Settings ダイアログ ボックス.

19. 対象: Hyper-V Manager, 選択します **SEA-WS4**, 選択します **Connect**,  を選択してから **Start**. 。

20. As computer starts press any key on keyboard to invoke MDT Deployment Wizard. Maximize ウィンドウ as needed.

21. 対象: **Welcome** ページ, 選択します **Run Deployment Wizard to install a new Operating System**.

22. 対象: **Specify credentials for connecting to network shares** ウィンドウ, 入力します 次の項目 を選択してから **OK**:
    - User Name: **Administrator**
    - Password: **Pa55w.rd**
    - Domain: **Contoso**

23. 対象: **Task Sequence** ページ, 選択します **Deploy Windows 11 入力しますprise** を選択してから **Next**.

24. 対象: **Computer Details** ページ, の横で **Computer name** 入力します **SEA-WS4** を選択してから **Next**.

25. 対象: **Move Data および Settings** ページ, 選択します **Next**.

26. 対象: **User Data (Restore)** ページ, 選択します **Next**.

27. 対象: **Locale および Time** ページ, 選択します **Next**.

28. 対象: **Applications** ページ, 選択します **Next**.

29. 対象: **Administrator Password** ページ, 入力します **Pa55w.rd** in both テキスト ボックスes を選択してから **Next**.

30. 対象: **Ready** ページ, 選択します **Begin**. 。

    > The installation begins. It will take 15-20 minutes to complete and will reboot SEA-WS4 during the installation as needed.

31. 切り替え先: **Deployment Workbench**.

32. 対象: Deployment Workbench, 展開し **Deployment Shares**, および 展開し **MDT Deployment Share**.

33. 選択します **Monitoring** 続いて in 詳細ペイン, double-選択します **SEA-WS4**.

    > Review the monitoring status during the deployment.

34. 切り替え先: **SEA-WS4**.

35. After installation is complete, desktop will open および finalize deployment. 対象: deployment summary, 選択します **Finish**.

36. Shut down **SEA-WS4** および 閉じます Virtual Machine Connection ウィンドウ.

37. 対象: Hyper-V Manager, 右クリックし **SEA-WS4** を選択してから **Settings**.

38. 対象: **Settings for SEA-WS4**, 展開し **SCSI Controller** を選択してから **DVD Drive**.

39. 対象: 詳細ペイン, で **Media**, 選択します **None**, を選択してから **OK**.

40. 右クリックし **SEA-WS4** を選択してから **Checkpoint** to create a checkpoint of current state of SEA-WS4.

41. 対象: SEA-SVR2, 閉じます **Hyper-V Manager** および 閉じます **Deployment Workbench**.

42. Open **File Explorer**, 右クリックし **DVD Drive F** を選択してから **Eject**.

43. 閉じます **File Explorer** および sign out of **SEA-SVR2**.

**結果**: この演習を完了すると、Microsoft Deployment Toolkit を使用して Windows 11 ワークステーションを作成し、展開できるようになります。

**ラボ終了**
