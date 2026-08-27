---
lab:
  title: '演習ラボ 0701: Microsoft Deployment Toolkit を使用した Windows 11 の展開'
  description: このラボでは、Microsoft Deployment Toolkit を使用して Windows 11 オペレーティング システム イメージを作成し、展開します。
  duration: 100 minutes
  level: 200
  islab: true
  primarytopics:
    - Windows
    - Windows 11
---

# 演習ラボ 0701: Microsoft Deployment Toolkit を使用した Windows 11 の展開

## 概要

このラボでは、Microsoft Deployment Toolkit を使用して Windows 11 オペレーティング システム イメージを作成し、展開します。 

### シナリオ

You need to deploy a new Windows 11 virtual machine named SEA-WS4. You decide to use Microsoft Deployment Toolkit to deploy オペレーティング システム to a virtual machine created in Hyper-V. You will configure a new Deployment Share in MDT 、続いて configure the task sequence that will perform the steps to deploy SEA-WS4.

### タスク 1: 新しい Deployment Share の作成

1. On **SEA-SVR2**, としてサインインします **Contoso\\Administrator** パスワード **Pa55w.rd**.

2. タスク バーで, **File Explorer** 、続いて browse to **E:\\Labfiles\\ISOs**.

3. 右クリックします **Win11_21H2_Eval.iso** 、続いて **Mount**. The ISO mounts as DVD Drive F.

4. 閉じます **File Explorer**.

5. **Start**, 展開します **Microsoft Deployment Toolkit**, 、続いて **Deployment Workbench**.

6. の **Deployment Workbench**, 右クリックします **Deployment Shares** 、続いて **New Deployment Share**. 

   > The **New Deployment Share Wizard** opens.

7. の **Path** ページ, で **Deployment share path**, change the value to **E:\DeploymentShare** 、続いて **Next**.

8. の **Share** ページ, 確認します: the **Share name**, but do not change it. **Next**.

9. の **Descriptive Name** ページ, accept the default value and **Next**.

10. の **Options** ページ, configure the following, 、続いて **Next**:

       - Ask to set the local Administrator password: **Enabled**

       - All other check boxes: **Disabled**

11. の **概要** ページ, 情報を確認し 、続いて **Next**. 

12. の **Confirmation** ページ, 処理が正常に完了したことを確認し 、続いて **Finish**.

13. で **Deployment Shares**, 展開します the **MDT Deployment Share** folder. 

    > 確認します: the various nodes that can be configured for the deployment share.

### タスク 2: Deployment Share へのオペレーティング システム ファイルの追加

1. の Deployment Workbench, 展開します **Deployment Shares**, 展開します **MDT Deployment Share**, 、続いて **Operating Systems**.

2. 右クリックします **Operating Systems** 、続いて **Import Operating System**. The Import Operating System Wizard opens.

3. の **Import Operating System Wizard**, の **OS 入力します** ページ, **Full set of source files** 、続いて **Next**.

4. の **Source** ページ, で **Source Directory**, **F:\\** 、続いて **Next**.

5. の **Destination** ページ, change the default destination directory name to **Windows 11 Enterprise x64** 、続いて **Next**.

6. の **概要** ページ, 情報を確認し 、続いて **Next**. 

   > オペレーティング システム source files are copied into the deployment share.

7. の **Confirmation** ページ, 処理が正常に完了したことを確認し 、続いて **Finish**.

8. の **Deployment Workbench**, with **Operating Systems** selected, 次のことを確認します: オペレーティング システム displays.

### タスク 3: Deployment Share へのアプリケーションの追加

1. の Deployment Workbench, 展開します **Deployment Shares**, 展開します **MDT Deployment Share**, 、続いて **Applications**.

2. 右クリックします **Applications** 、続いて **New Application**. The New Application Wizard opens.

3. の **New Application Wizard**, の **Application 入力します** ページ, **Application with source files** 、続いて **Next**.

4. の **Details** ページ, configure the following, 、続いて **Next**:
    - Publisher: **Microsoft**
    - Application Name: **XML Notepad**

5. の **Source** ページ, で **Source directory**, **E:\\Labfiles\\Apps** 、続いて **Next**.

6. の **Destination** ページ, accept the default destination directory name 、続いて **Next**.

7. の **Command Details** ページ, で **Command line** **XmlNotepadSetup.msi /q** 、続いて **Next**.

8. の **概要** ページ, 情報を確認し 、続いて **Next**. 

9. の **Confirmation** ページ, 処理が正常に完了したことを確認し 、続いて **Finish**.

### タスク 4: Create an MDT タスク Sequence

1. の Deployment Workbench, 展開します **Deployment Shares**, 展開します **MDT Deployment Share**, 、続いて **タスク Sequences**.

2. 右クリックします **タスク Sequences** 、続いて **New タスク Sequence**. The **New タスク Sequence Wizard** opens.

3. の **General Settings** ページ, configure the following 、続いて **Next**:
   - タスク sequence ID: **001**
   - タスク sequence name: **Deploy Windows 11 Enterprise**

4. の **選択します Template** ページ, **Standard Client タスク Sequence**, 、続いて **Next**.

5. の **選択します OS** ページ, **Windows 10 Enterprise Evaluation** 、続いて **Next**.

6. の **Specify Product Key** ページ, **Do not specify a product key at this time**, 、続いて **Next**.

7. の **OS Settings** ページ, configure the following 、続いて **Next**:
   - Full Name: **User**
   - Organization: **Contoso Corporation**
   - Internet Explorer Home ページ: **about:blank**

8. の **Admin Password** ページ, **Use the specified local Administrator password**, 、続いて **Pa55w.rd** in both text boxes. **Next**.

9. の **概要** ページ, 情報を確認し 、続いて **Next**. 

10. の **Confirmation** ページ, 処理が正常に完了したことを確認し 、続いて **Finish**.

11. の **Deployment Workbench**, with **タスク Sequences** selected 次のことを確認します: the **Deploy Windows 11 Enterprise** task sequence displays.

12. 右クリックします the **Deploy Windows 11 Enterprise** task sequence, 、続いて **Properties**. 

13. 選択します the **タスク Sequence** タブ. 

14. 展開します the **Validation** node 、続いて **Validate**.

15. の **Properties** ページ, remove the check marks の横で **Ensure minimum memory** and **Ensure minimum processor speed**. 

    > Do not make any other changes.

16. の **Deploy Windows 11 Enterprise Properties** ウィンドウ, **OK**.

### タスク 5: Deployment Share のプロパティと Windows PE 設定の構成

1. の Deployment Workbench, 展開します **Deployment Shares**, and **MDT Deployment Share**.

2. 右クリックします **MDT Deployment Share** 、続いて **Properties**.

3. の **MDT Deployment Share Properties** ウィンドウ, の **General** タブ, 確認します: 情報 that was provided when the deployment share was created.

4. 選択します the **Rules** タブ. 

   > The Rules タブ displays the content of the CustomSettings.ini file. These values were also provided during the creation of the deployment share.

5. 選択します the **Windows PE** タブ. 

   > The Windows PE タブ provides options for creating a Windows PE boot disk.

6. の **Windows PE** タブ, の横で **Platform**, **x64**.

7. の **Windows PE Customizations** section, の横で **Scratch space size**, **64**.

8. 選択します the **Features** タブ 、続いて の横にあるチェック ボックスを選択し the following Feature Packs:
   - DISM Cmdlets
   - Windows PowerShell
   - Microsoft Data Access Components (MDAC/ADO) support

9. 選択します the **Monitoring** タブ.

10. の **Monitoring** タブ, の横にあるチェック ボックスを選択し **Enable monitoring for this deployment share**.

11. の **MDT Deployment Share Properties** ウィンドウ, **OK**.

12. 右クリックします **MDT Deployment Share** 、続いて **Update Deployment Share**. The Update Deployment Share Wizard opens.

13. の **Options** ページ, **Optimize the boot image updating process** 、続いて **Next**.

14. の **概要** ページ, **Next**. 

    > The Deployment Share starts to update and create the Windows PE files. This will take a few minutes to complete.

15. の **Confirmation** ページ, 処理が正常に完了したことを確認し 、続いて **Finish**.

### タスク 6: MDT を使用した Windows 11 の展開

1. On SEA-SVR2, タスク バーで, **Hyper-V Manager**.

2. In Hyper-V Manager, **Virtual Switch Manager**.

3. **New virtual network switch** 、続いて 詳細ペインで, **External**. **Create Virtual Switch**.

4. の **Virtual Switch Properties** ページ, で **Name**, **External network**, **OK**, 、続いて **Yes**.

5. In Hyper-V Manager, **SEA-SVR2** 、続いて の Actions ペイン, **New** 、続いて **Virtual Machine**.

6. の **Before you Begin** ページ, **Next**.

7. の **Specify Name and Location** ページ, の **Name** box **SEA-WS4**. 

8. の横にあるチェック ボックスを選択し **Store the virtual machine in a different location** 、続いて の横で **Location** **E:\\Labfiles\\VirtualMachines**. **Next**.

9. の **Specify Generation** ページ, ensure that **Generation 2** is selected 、続いて **Next**.

10. の **Assign Memory** ページ, の横で **Startup memory** **8192** 、続いて **Next**.

11. の **Configure Networking** ページ, の横で **Connection**, **External Network** 、続いて **Next**.

12. の **Connect Virtual Hard Disk** ページ, **Create a virtual hard disk** and 入力します the following 、続いて click **Next**:

    - Name: **SEA-WS4.vhdx**
    - Location: **E:\\Labfiles\\VirtualMachines**
    - Size: **60 GB**

13. の **Installation Options** ページ, **Install an operating system from a bootable image file** and configure the following:

    - Image file (.iso): **E:\\DeploymentShare\\Boot\\LiteTouchPE_x64.iso**

14. **Next** 、続いて **Finish**.

15. In Hyper-V Manager, 右クリックします **SEA-WS4**, 、続いて **Settings**.

16. **Security**, 、続いて の横にあるチェック ボックスを選択し **Enable Trusted Platform Module**.

17. **Processor**, 、続いて change the number of virtual processors to **2**. 

18. **OK** to 閉じます the Settings dialog box.

19. In Hyper-V Manager, **SEA-WS4**, **Connect**,  、続いて **Start**. 

20. As the computer starts press any key の keyboard to invoke the MDT Deployment Wizard. Maximize the ウィンドウ as needed.

21. の **Welcome** ページ, **Run the Deployment Wizard to install a new Operating System**.

22. の **Specify credentials for connecting to network shares** ウィンドウ, 入力します the following 、続いて **OK**:
    - User Name: **Administrator**
    - Password: **Pa55w.rd**
    - Domain: **Contoso**

23. の **タスク Sequence** ページ, **Deploy Windows 11 Enterprise** 、続いて **Next**.

24. の **Computer Details** ページ, の横で **Computer name** **SEA-WS4** 、続いて **Next**.

25. の **Move Data and Settings** ページ, **Next**.

26. の **User Data (Restore)** ページ, **Next**.

27. の **Locale and Time** ページ, **Next**.

28. の **Applications** ページ, **Next**.

29. の **Administrator Password** ページ, **Pa55w.rd** in both text boxes 、続いて **Next**.

30. の **Ready** ページ, **Begin**. 

    > The installation begins. It will take 15-20 minutes to complete and will reboot SEA-WS4 during the installation as needed.

31. に切り替えます the **Deployment Workbench**.

32. の Deployment Workbench, 展開します **Deployment Shares**, and 展開します **MDT Deployment Share**.

33. **Monitoring** 、続いて 詳細ペインで, double-click **SEA-WS4**.

    > Review the monitoring status during the deployment.

34. に切り替えます **SEA-WS4**.

35. After the installation is complete, the desktop will 開きます and finalize the deployment. At the deployment summary, **Finish**.

36. Shut down **SEA-WS4** and 閉じます the Virtual Machine Connection ウィンドウ.

37. In Hyper-V Manager, 右クリックします **SEA-WS4** 、続いて **Settings**.

38. の **Settings for SEA-WS4**, 展開します **SCSI Controller** 、続いて **DVD Drive**.

39. 詳細ペインで, で **Media**, **None**, 、続いて **OK**.

40. 右クリックします **SEA-WS4** 、続いて **Checkpoint** to create a checkpoint of the current state of SEA-WS4.

41. On SEA-SVR2, 閉じます **Hyper-V Manager** and 閉じます the **Deployment Workbench**.

42. 開きます **File Explorer**, 右クリックします **DVD Drive F** 、続いて **Eject**.

43. 閉じます **File Explorer** and sign out of **SEA-SVR2**.

**結果**: この演習を完了すると、 successfully used the Microsoft Deployment Toolkit to create and deploy a Windows 11 workstation.

**ラボ終了**
