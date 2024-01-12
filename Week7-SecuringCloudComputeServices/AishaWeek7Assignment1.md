# Week7: **Assignment 1:-Manage Virtual Machines**

## Report by: **Aisha Khalifan, cs-cns04-23014**
>
<ins>**[Introduction**<ins>
>
> This report is your guide to the exciting world of Azure virtual
> machines (VMs) -- how to set them up and make them work seamlessly. We
> are going to focus on making sure they\'re super reliable, scalable,
> and check out cool things like Azure virtual machine scale sets. Plus,
> we will see how to make things even easier with the nifty Azure
> Virtual Machine Custom Script extension. We will be doing fun stuff
> like setting up zone-resilient Azure VMs, tweaking VMs with cool
> extensions, and making sure we scale up our compute and storage game
> for both VMs and scale sets.
>
> **[Lab Tasks]{.underline}**
>
> **Objectives**
>
> In this lab, you will:
>
> Task 1: Deploy zone-resilient Azure virtual machines by using the
> Azure portal and an Azure Resource Manager template\
> Task 2: Configure Azure virtual machines by using virtual machine
> extensions\
> Task 3: Scale compute and storage for Azure virtual machines\
> Task 4: Register the Microsoft.Insights and
> Microsoft.AlertsManagement resource providers Task 5: Deploy
> zone-resilient Azure virtual machine scale sets by using the Azure
> portal\
> Task 6: Configure Azure virtual machine scale sets by using virtual
> machine extensions\
> Task 7: Scale compute and storage for Azure virtual machine scale
> sets (optional)
>
> **Architecture Diagram**

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image1.png){width="6.5in"
height="2.9430544619422574in"}

Exercise 1

Task 1: Deploy zone-resilient Azure virtual machines by using the Azure
portal and an Azure Resource Manager template

In this task, you will deploy Azure virtual machines into different
availability zones by using the Azure portal and an Azure Resource
Manager template.

1\. Sign in to the

2\. In the Azure portal, search for and select **Virtual machines** and,
on the **Virtual machines** blade, click **+ Create**, click **+ Azure
virtual machine**.

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image2.png){width="6.5in"
> height="2.748611111111111in"}

3\. On the **Basics** tab of the **Create a virtual machine** blade,
specify the following settings (leave others with their default values):

+-----------------------------------+-----------------------------------+
| > Setting                         | > Value                           |
+===================================+===================================+
| > Subscription                    | > the name of the Azure           |
|                                   | > subscription you will be using  |
|                                   | > in this lab                     |
+-----------------------------------+-----------------------------------+
| > Resource group                  | > the name of a new resource      |
|                                   | > group **az104-08-rg01**         |
+-----------------------------------+-----------------------------------+
| Virtual machine name              | > **az104-08-vm0**                |
+-----------------------------------+-----------------------------------+
| > Region                          | > select one of the regions that  |
|                                   | > support availability zones and  |
|                                   | > where you can provision Azure   |
|                                   | > virtual machines                |
+-----------------------------------+-----------------------------------+
| > Availability options            | > **Availability zone**           |
+-----------------------------------+-----------------------------------+
| > Availability zone               | > **Zone 1**                      |
+-----------------------------------+-----------------------------------+
| > Image                           | > **Windows Server 2019           |
|                                   | > Datacenter - Gen1/Gen2**        |
+-----------------------------------+-----------------------------------+
| > Azure Spot instance             | > **No**                          |
+-----------------------------------+-----------------------------------+

+-----------------------------------+-----------------------------------+
| > Setting                         | > Value                           |
+===================================+===================================+
| > Size                            | > **Standard D2s v3**             |
+-----------------------------------+-----------------------------------+
| > Username                        | > **Student**                     |
+-----------------------------------+-----------------------------------+
| > Password                        | > **Provide a secure password**   |
+-----------------------------------+-----------------------------------+
| Public inbound ports              | > **None**                        |
+-----------------------------------+-----------------------------------+
| > Would you like to use an        | > **Unchecked**                   |
|                                   |                                   |
| +---------+---------+---------+   |                                   |
| | e       | Windows | >       |   |                                   |
| | xisting |         |  Server |   |                                   |
| +=========+=========+=========+   |                                   |
| +---------+---------+---------+   |                                   |
|                                   |                                   |
| > license?                        |                                   |
+-----------------------------------+-----------------------------------+

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image3.png){width="6.5in"
> height="3.136111111111111in"}
>
> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image4.png){width="6.5in"
> height="3.2638877952755907in"}

4\. Click **Next: Disks \>** and, on the **Disks** tab of the **Create a
virtual machine** blade, specify the following

> settings (leave others with their default values):

+-----------------------------------+-----------------------------------+
| > Setting                         | Value                             |
+===================================+===================================+
| > OS disk type                    | **Premium SSD**                   |
+-----------------------------------+-----------------------------------+
| > Enable Ultra Disk compatibility | **Unchecked**                     |
+-----------------------------------+-----------------------------------+

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image5.png){width="6.5in"
> height="3.213888888888889in"}

5\. Click **Next: Networking \>** and, on the **Networking** tab of the
**Create a virtual machine** blade, click

> **Create new** below the **Virtual network** textbox.
>
> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image6.png){width="6.5in"
> height="2.995833333333333in"}

6\. On the **Create virtual network** blade, specify the following
settings (leave others with their default

> values):

+-----------------------------------+-----------------------------------+
| Setting                           | > Value                           |
+===================================+===================================+
| Name                              | > **az104-08-vnet01**             |
+-----------------------------------+-----------------------------------+
| Address range                     | > **10.80.0.0/20**                |
+-----------------------------------+-----------------------------------+
| Subnet name                       | > **subnet0**                     |
+-----------------------------------+-----------------------------------+
| Subnet range                      | > **10.80.0.0/24**                |
+-----------------------------------+-----------------------------------+

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image7.png){width="6.5in"
> height="3.047222222222222in"}

7\. Click **OK** and, back on the **Networking** tab of the **Create a
virtual machine** blade, specify the

> following settings (leave others with their default values):

+-----------------------------------+-----------------------------------+
| > Setting                         | Value                             |
+===================================+===================================+
| > Subnet                          | **subnet0**                       |
+-----------------------------------+-----------------------------------+
| > Public IP                       | **default**                       |
+-----------------------------------+-----------------------------------+
| > NIC network security group      | **basic**                         |
+-----------------------------------+-----------------------------------+
| > Public inbound Ports            | **None**                          |
+-----------------------------------+-----------------------------------+
| > Accelerated networking          | **Off**                           |
+-----------------------------------+-----------------------------------+
| > Place this virtual machine      | **Unchecked**                     |
| > behind an existing load         |                                   |
| > balancing solution?             |                                   |
+-----------------------------------+-----------------------------------+

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image8.png){width="6.5in"
> height="3.0972222222222223in"}
>
> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image9.png){width="6.5in"
> height="3.219443350831146in"}

8\. Click **Next: Management \>** and, on the **Management** tab of the
**Create a virtual machine** blade, specify the following settings
(leave others with their default values):

+-----------------------------------+-----------------------------------+
| > Setting                         | Value                             |
+===================================+===================================+
| > Patch orchestration options     | **Manual updates**                |
+-----------------------------------+-----------------------------------+

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image10.png){width="6.5in"
> height="3.238888888888889in"}
>
> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image11.png){width="6.5in"
> height="3.2222222222222223in"}

9\. Click **Next: Monitoring \>** and, on the **Monitoring** tab of the
**Create a virtual machine** blade, specify the following settings
(leave others with their default values):

+-----------------------------------+-----------------------------------+
| > Setting                         | > Value                           |
+===================================+===================================+
| > Boot diagnostics                | > **Enable with custom storage    |
|                                   | > account**                       |
+-----------------------------------+-----------------------------------+
| > Diagnostics storage account     | > **accept the default value**    |
+-----------------------------------+-----------------------------------+

**Note**: If necessary, select an existing storage account in the
dropdown list or create a new storage account. Record the name of the
storage account. You will use it in the next task.

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image12.png){width="6.5in"
height="3.0875in"}

10.Click **Next: Advanced \>**, on the **Advanced** tab of the **Create
a virtual machine** blade, review the available settings without
modifying any of them, and click **Review + Create**.

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image13.png){width="6.5in"
> height="3.1805555555555554in"}

11.On the **Review + Create** blade, click **Create**.

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image14.png){width="6.5in"
> height="3.179165573053368in"}
>
> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image15.png){width="6.5in"
> height="3.029166666666667in"}

12.On the deployment blade, click **Template**.

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image16.png){width="6.5in"
> height="2.904166666666667in"}
>
> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image17.png){width="6.5in"
> height="3.1138877952755903in"}

13.Review the template representing the deployment in progress and click
**Deploy**.

> **Note**: You will use this option to deploy the second virtual
> machine with matching configuration except for the availability zone.

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image18.png){width="6.5in"
height="2.941666666666667in"}

14.On the **Custom deployment** blade, specify the following settings
(leave others with their default values):

+-----------------------------------+-----------------------------------+
| > Setting                         | Value                             |
+===================================+===================================+
| > Resource Group                  | **az104-08-rg01**                 |
+-----------------------------------+-----------------------------------+
| > Network Interface Name          | **az104-08-vm1-nic1**             |
+-----------------------------------+-----------------------------------+
| > Public IP Address Name          | **az104-08-vm1-ip**               |
+-----------------------------------+-----------------------------------+
| > Virtual Machine Name, Virtual   | **az104-08-vm1**                  |
| > Machine Name1, Virtual Machine  |                                   |
| > Computer Name                   |                                   |
+-----------------------------------+-----------------------------------+
| > Virtual Machine RG              | **az104-08-rg01**                 |
+-----------------------------------+-----------------------------------+
| > Admin Username                  | **Student**                       |
+-----------------------------------+-----------------------------------+
| > Admin Password                  | +---------+---------+---------+   |
|                                   | | **Pr    | **a**   | > **s   |   |
|                                   | | ovide** |         | ecure** |   |
|                                   | +=========+=========+=========+   |
|                                   | +---------+---------+---------+   |
|                                   |                                   |
|                                   | **password**                      |
+-----------------------------------+-----------------------------------+
| > Enable Hotpatching              | **false**                         |
+-----------------------------------+-----------------------------------+
| > Zone                            | **2**                             |
+-----------------------------------+-----------------------------------+

**Note**: You need to modify parameters corresponding to the properties
of the distinct resources you are deploying by using the template,
including the virtual machine and its network interface.

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image19.png){width="6.5in"
height="2.9930555555555554in"}

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image20.png){width="6.5in"
height="3.0694444444444446in"}

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image21.png){width="6.5in"
height="3.1in"}

15.Click **Review + Create**, on the **Review + Create** blade, click
**Create**.

**Note**: Wait for both deployments to complete before you proceed to
the next task. This might take about 5 minutes.

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image22.png){width="6.5in"
height="3.0208333333333335in"}

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image23.png){width="6.5in"
height="3.2152777777777777in"}

Task 2: Configure Azure virtual machines by using virtual machine
extensions

In this task, you will install Windows Server Web Server role on the two
Azure virtual machines

you deployed in the previous task by using the Custom Script virtual
machine extension.

1\. In the Azure portal, search for and select **Storage accounts** and,
on the **Storage accounts** blade, click

> the entry representing the diagnostics storage account you created in
> the previous task.
>
> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image24.png){width="6.5in"
> height="3.236111111111111in"}
>
> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image25.png){width="6.5in"
> height="3.2194444444444446in"}

2\. On the storage account blade, in the **Data Storage** section, click
**Containers** and then click **+**

> **Container**.
>
> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image26.png){width="6.5in"
> height="3.2125in"}

3\. On the **New container** blade, specify the following settings
(leave others with their default values)

> and click **Create**:

+-----------------------------------+-----------------------------------+
| Setting                           | > Value                           |
+===================================+===================================+
| Name                              | > **scripts**                     |
+-----------------------------------+-----------------------------------+
| Public access level               | > **Private (no anonymous         |
|                                   | > access**)                       |
+-----------------------------------+-----------------------------------+

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image27.png){width="6.5in"
height="3.1666666666666665in"}

4\. Back on the storage account blade displaying the list of containers,
click **scripts**.

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image28.png){width="6.5in"
> height="3.1555555555555554in"}

5\. On the **scripts** blade, click **Upload**.

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image29.png){width="6.5in"
> height="3.2125in"}

6\. On the **Upload blob** blade, click the folder icon, in the **Open**
dialog box, navigate to the **\\Allfiles\\Labs\\08** folder, select
**az104-08-install_IIS.ps1**, click **Open**, and back on the **Upload
blob** blade, click **Upload**.

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image30.png){width="6.5in"
> height="3.220832239720035in"}
>
> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image31.png){width="6.5in"
> height="3.201388888888889in"}
>
> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image32.png){width="6.5in"
> height="3.184721128608924in"}

7\. In the Azure portal, search for and select **Virtual machines** and,
on the **Virtual machines** blade, click **az104-08-vm0**.

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image33.png){width="6.5in"
> height="3.0749989063867016in"}

8\. On the **az104-08-vm0** virtual machine blade, in the **Settings**
section, click **Extensions + applications**, and the click **+ Add**.

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image34.png){width="6.5in"
> height="3.1416666666666666in"}
>
> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image35.png){width="6.5in"
> height="3.1555555555555554in"}

9\. On the **Install an Extension** blade, click **Custom Script
Extension** and then click **Next**.

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image36.png){width="6.5in"
> height="3.1861100174978128in"}
>
> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image37.png){width="6.5in"
> height="3.0625in"}

10.From the **Configure Custom Script Extension Extension** blade, click
**Browse**.

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image38.png){width="6.5in"
> height="3.158332239720035in"}

11.On the **Storage accounts** blade, click the name of the storage
account into which you uploaded the **az104-08-install_IIS.ps1** script,
on the **Containers** blade, click **scripts**, on the **scripts**
blade, click **az104-08-install_IIS.ps1**, and then click **Select**.

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image39.png){width="6.5in"
> height="3.1958333333333333in"}
>
> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image40.png){width="6.5in"
> height="3.1236100174978128in"}

12.Back on the **Install extension** blade, click **Review + create**
and, on the **Review + create** blade click **Create**.

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image41.png){width="6.5in"
> height="3.0805555555555557in"}
>
> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image42.png){width="6.5in"
> height="3.1805555555555554in"}

13.In the Azure portal, search for and select **Virtual machines** and,
on the **Virtual machines** blade, click **az104-08-vm1**.

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image43.png){width="6.5in"
> height="3.0069444444444446in"}

14.On the **az104-08-vm1** blade, in the **Automation** section, click
**Export template**.

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image44.png){width="6.5in"
> height="3.2055555555555557in"}

15.On the **az104-08-vm1 - Export template** blade, click **Deploy**.

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image45.png){width="6.5in"
> height="3.1861100174978128in"}

16.On the **Custom deployment** blade, click **Edit template**.

**Note**: Disregard the message stating **The resource group is in a
location that is not supported by one or more resources in the template.
Please choose a different resource group**. This is expected and can be
ignored in this case.

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image46.png){width="6.5in"
height="3.202777777777778in"}

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image47.png){width="6.5in"
height="3.1819444444444445in"}

17.On the **Edit template** blade, in the section displaying the content
of the template, insert the

> following code starting with line **20** (directly underneath the
> *\"resources\": \[* line):
>
> **Note**: If you are using a tool that pastes the code in line by line
> intellisense may add
>
> extra brackets causing validation errors. You may want to paste the
> code into
>
> notepad first and then paste it into line 20.
>
> {
>
> \"type\": \"Microsoft.Compute/virtualMachines/extensions\",
>
> \"name\": \"az104-08-vm1/customScriptExtension\",
>
> \"apiVersion\": \"2018-06-01\",
>
> \"location\": \"\[resourceGroup().location\]\",
>
> \"dependsOn\": \[

\"az104-08-vm1\"

> \],
>
> \"properties\": {
>
> \"publisher\": \"Microsoft.Compute\",
>
> \"type\": \"CustomScriptExtension\",
>
> \"typeHandlerVersion\": \"1.7\",
>
> \"autoUpgradeMinorVersion\": **true**,
>
> \"settings\": {

\"commandToExecute\":\"powershell.exe Install-Wind

> owsFeature -name Web-Server -IncludeManagementTools && powershell
>
> .exe remove-item \'C:\\\\inetpub\\\\wwwroot\\\\iisstart.htm\' &&
> powershe
>
> ll.exe Add-Content -Path \'C:\\\\inetpub\\\\wwwroot\\\\iisstart.htm\'
> -Va

+---------+---------+---------+---------+---------+---------+---------+
| lue     | \$(     | World   | from    | \'      | \+      | >       |
|         | \'Hello |         |         |         |         | \$env:c |
|         |         |         |         |         |         | omputer |
|         |         |         |         |         |         | name)\" |
+=========+=========+=========+=========+=========+=========+=========+
+---------+---------+---------+---------+---------+---------+---------+

> }
>
> }\
> }**,**
>
> **Note**: This section of the template defines the same Azure virtual
> machine custom script extension that you deployed earlier to the first
> virtual machine via Azure PowerShell.

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image48.png){width="6.5in"
height="3.202777777777778in"}

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image49.png){width="6.5in"
height="3.2124989063867018in"}

18.Click **Save** and, back on the **Custom template** blade, click
**Review + Create** and, on the **Review +** **Create** blade, click
**Create**

> **Note**: Wait for the template deployment to complete. You can
> monitor its progress from the **Extensions** blade of the
> **az104-08-vm0** and **az104-08-vm1** virtual machines. This should
> take no more than 3 minutes.

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image50.png){width="6.5in"
height="3.165277777777778in"}

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image51.png){width="6.5in"
height="3.1625in"}

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image52.png){width="6.5in"
height="3.1999989063867016in"}

19.To verify that the Custom Script extension-based configuration was
successful, navigate back on the **az104-08-vm1** blade, in the
**Operations** section, click **Run command**, and, in the list of
commands, click **RunPowerShellScript**.

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image53.png){width="6.5in"
> height="3.151388888888889in"}

20.On the **Run Command Script** blade, type the following and click
**Run** to access the web site hosted on **az104-08-vm1**:

> Invoke-WebRequest-URI http://10.80.0.4-UseBasicParsing
>
> **Note**: The **-UseBasicParsing** parameter is necessary to eliminate
> dependency on Internet Explorer to complete execution of the cmdlet

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image54.png){width="6.5in"
height="3.172221128608924in"}

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image55.png){width="6.5in"
height="3.216666666666667in"}

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image56.png){width="6.5in"
height="3.1819444444444445in"}

**Note**: The **-URI** parameter is the **Private IP address** of the
VM. Navigate to the **az104-08-vm1** blade, in the **Networking**
section, and click **Network settings**

**Note**: You can also connect to **az104-08-vm0** and run
*Invoke-WebRequest -URI http://10.80.0.5 -UseBasicParsing* to access the
web site hosted on **az104-08-vm1**.

Task 3: Scale compute and storage for Azure virtual machines

In this task you will scale compute for Azure virtual machines by
changing their size and scale their storage by attaching and configuring
their data disks.

1\. In the Azure portal, search for and select **Virtual machines** and,
on the **Virtual machines** blade, click **az104-08-vm0**.

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image57.png){width="6.5in"
> height="3.236111111111111in"}

2\. On the **az104-08-vm0** virtual machine blade, click **Size** and
set the virtual machine size to **Standard** **DS1_v2** and click
**Resize**

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image58.png){width="6.5in"
> height="3.0805555555555557in"}
>
> **Note**: Choose another size if **Standard DS1_v2** is not available.

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image59.png){width="6.5in"
height="2.9944444444444445in"}

3\. On the **az104-08-vm0** virtual machine blade, click **Disks**,
Under **Data disks** click **+ Create and attach** **a new disk**.

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image60.png){width="6.5in"
> height="3.05in"}

4\. Create a managed disk with the following settings (leave others with
their default values):

+-----------------------------------+-----------------------------------+
| Setting                           | > Value                           |
+===================================+===================================+
| Disk name                         | > **az104-08-vm0-datadisk-0**     |
+-----------------------------------+-----------------------------------+
| Storage type                      | > **Premium SSD**                 |
+-----------------------------------+-----------------------------------+
| Size (GiB                         | > **1024**                        |
+-----------------------------------+-----------------------------------+

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image61.png){width="6.5in"
> height="3.1513877952755904in"}

5\. Back on the **az104-08-vm0 - Disks** blade, Under **Data disks**
click **+ Create and attach a new disk**.

6\. Create a managed disk with the following settings (leave others with
their default values) and Save

> changes:

+-----------------------------------+-----------------------------------+
| Setting                           | > Value                           |
+===================================+===================================+
| Disk name                         | > **az104-08-vm0-datadisk-1**     |
+-----------------------------------+-----------------------------------+
| Storage type                      | > **Premium SSD**                 |
+-----------------------------------+-----------------------------------+
| Size (GiB)                        | > **1024 GiB**                    |
+-----------------------------------+-----------------------------------+

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image62.png){width="6.5in"
> height="3.158332239720035in"}

7\. Back on the **az104-08-vm0 - Disks** blade, click **Save**.

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image63.png){width="6.5in"
> height="3.029166666666667in"}

8\. On the **az104-08-vm0** blade, in the **Operations** section, click
**Run command**, and, in the list of commands, click
**RunPowerShellScript**.

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image64.png){width="6.5in"
> height="2.9986100174978128in"}
>
> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image65.png){width="6.5in"
> height="3.2083333333333335in"}

9\. On the **Run Command Script** blade, type the following and click
**Run** to create a drive Z: consisting of the two newly attached disks
with the simple layout and fixed provisioning:

> New-StoragePool -FriendlyName storagepool1 -StorageSubsystemFrien
> dlyName \"Windows Storage\*\"-PhysicalDisks (Get-PhysicalDisk -CanP
> ool \$true)
>
> New-VirtualDisk -StoragePoolFriendlyName storagepool1 -FriendlyNa me
> virtualdisk1 -Size 64GB -ResiliencySettingName Simple -Provisi
> oningType Fixed
>
> Initialize-Disk -VirtualDisk (Get-VirtualDisk -FriendlyName virtu
> aldisk1)
>
> New-Partition -DiskNumber 4 -UseMaximumSize -DriveLetter
>
> **Note**: Wait for the confirmation that the commands completed
> successfully.

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image66.png){width="6.5in"
height="3.1930544619422574in"}

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image67.png){width="6.5in"
height="3.1847222222222222in"}

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image68.png){width="6.5in"
height="3.1458333333333335in"}

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image69.png){width="6.5in"
height="3.1625in"}

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image70.png){width="6.5in"
height="3.1333333333333333in"}

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image71.png){width="6.5in"
height="3.1652766841644793in"}

10.In the Azure portal, search for and select **Virtual machines** and,
on the **Virtual machines** blade, click **az104-08-vm1**.

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image72.png){width="6.5in"
> height="3.2069433508311462in"}

11.On the **az104-08-vm1** blade, in the **Automation** section, click
**Export template**.

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image73.png){width="6.5in"
> height="3.183333333333333in"}

12.On the **az104-08-vm1 - Export template** blade, click **Deploy**.

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image74.png){width="6.5in"
> height="3.1416666666666666in"}

13.On the **Custom deployment** blade, click **Edit template**.

> **Note**: Disregard the message stating **The resource group is in a
> location that is not supported by one or more resources in the
> template. Please choose a different resource group**. This is expected
> and can be ignored in this case.

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image75.png){width="6.5in"
height="3.175in"}

14.On the **Edit template** blade, in the section displaying the content
of the template, replace the line **30***\"vmSize\":
\"Standard_D2s_v3\"* with the following line):

**\"vmSize\":\"Standard_DS1_v2\"**

> **Note**: This section of the template defines the same Azure virtual
> machine size as the one you specified for the first virtual machine
> via the Azure portal.

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image76.png){width="6.5in"
height="3.172221128608924in"}

15.On the **Edit template** blade, in the section displaying the content
of the template, replace line **51**

> (*\"dataDisks\": \[ \],*) with the following code :
>
> **\"dataDisks\":** \[

{

> \"lun\": 0,
>
> \"name\": \"az104-08-vm1-datadisk0\",
>
> \"diskSizeGB\": \"1024\",
>
> \"caching\": \"ReadOnly\",
>
> \"createOption\": \"Empty\"

},

{

> \"lun\": 1,
>
> \"name\": \"az104-08-vm1-datadisk1\",
>
> \"diskSizeGB\": \"1024\",
>
> \"caching\": \"ReadOnly\",
>
> \"createOption\": \"Empty\"

}

\]**,**

**Note**: If you are using a tool that pastes the code in line by line
intellisense may add extra

brackets causing validation errors. You may want to paste the code into
notepad first and

then paste it into line 49.

**Note**: This section of the template creates two managed disks and
attaches them to **az104-**

**08-vm1**, similarly to the storage configuration of the first virtual
machine via the Azure

portal.

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image77.png){width="6.5in"
height="3.136111111111111in"}

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image78.png){width="6.5in"
height="3.1013877952755906in"}

16.Click **Save** and, back on the **Custom deployment** blade, click
**Review + Create** and, on the **Review +** **Create** blade, click
**Create**.

> **Note**: Wait for the template deployment to complete. You can
> monitor its progress from the **Disks** blade of the **az104-08-vm1**
> virtual machine. This should take no more than 3 minutes.

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image79.png){width="6.5in"
height="3.0902777777777777in"}

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image80.png){width="6.5in"
height="3.2263877952755906in"}

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image81.png){width="6.5in"
height="3.2472222222222222in"}

17.Back on the **az104-08-vm1** blade, in the **Operations** section,
click **Run command**, and, in the list of commands, click
**RunPowerShellScript**.

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image82.png){width="6.5in"
> height="3.0319444444444446in"}

18.On the **Run Command Script** blade, type the following and click
**Run** to create a drive Z: consisting of the two newly attached disks
with the simple layout and fixed provisioning:

> New-StoragePool -FriendlyName storagepool1 -StorageSubsystemFrien
> dlyName \"Windows Storage\*\"-PhysicalDisks (Get-PhysicalDisk -CanP
> ool \$true)
>
> New-VirtualDisk -StoragePoolFriendlyName storagepool1 -FriendlyNa
>
> me virtualdisk1 -Size 2046GB -ResiliencySettingName Simple -Provi
> sioningType Fixed
>
> Initialize-Disk -VirtualDisk (Get-VirtualDisk -FriendlyName virtu
> aldisk1)
>
> New-Partition -DiskNumber 4 -UseMaximumSize -DriveLetter Z
>
> **Note**: Wait for the confirmation that the commands completed
> successfully.

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image83.png){width="6.5in"
height="3.1458333333333335in"}

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image84.png){width="6.5in"
height="3.263888888888889in"}

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image85.png){width="6.5in"
height="3.2194444444444446in"}

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image86.png){width="6.5in"
height="3.1319444444444446in"}

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image87.png){width="6.5in"
height="3.1944444444444446in"}

Task 4: Register the Microsoft.Insights and Microsoft.AlertsManagement
resource

providers

1\. In the Azure portal, open the **Azure Cloud Shell** by clicking on
the icon in the top right of the Azure

> Portal.
>
> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image88.png){width="6.5in"
> height="3.1555544619422573in"}

2\. If prompted to select either **Bash** or **PowerShell**, select
**PowerShell**.

> **Note**: If this is the first time you are starting **Cloud Shell**
> and you are presented with
>
> the **You have no storage mounted** message, select the subscription
> you are using in
>
> this lab, and click **Create storage**.

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image89.png){width="6.5in"
height="3.1805555555555554in"}

3\. From the Cloud Shell pane, run the following to register the
Microsoft.Insights and Microsoft.AlertsManagement resource providers.

Register-AzResourceProvider -ProviderNamespace Microsoft.Insights

> Register-AzResourceProvider -ProviderNamespace Microsoft.AlertsMa
> nagement
>
> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image90.png){width="6.5in"
> height="3.1305544619422574in"}

Task 5: Deploy zone-resilient Azure virtual machine scale sets by using
the Azure portal

In this task, you will deploy Azure virtual machine scale set across
availability zones by using the Azure portal.

1\. In the Azure portal, search for and select **Virtual machine scale
sets** and, on the **Virtual machine** **scale sets** blade, click **+
Add** (or **+ Create**).

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image91.png){width="6.5in"
> height="3.0611100174978128in"}
>
> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image92.png){width="6.5in"
> height="3.0638877952755905in"}

2\. On the **Basics** tab of the **Create a virtual machine scale set**
blade, specify the following settings (leave others with their default
values) and click **Next : Disks \>**:

+-----------------------------------+-----------------------------------+
| Setting                           | > Value                           |
+===================================+===================================+
| Subscription                      | > the name of the Azure           |
|                                   | > subscription you are using in   |
|                                   | > this lab                        |
+-----------------------------------+-----------------------------------+
| Resource group                    | the name of a new resource group  |
|                                   | **az104-08-rg02**                 |
+-----------------------------------+-----------------------------------+
| > Virtual machine                 | > **az10408vmss0**                |
|                                   |                                   |
| scale set name                    |                                   |
+-----------------------------------+-----------------------------------+
| Region                            | > select one of the regions that  |
|                                   | > support availability zones and  |
|                                   | > where you can provision Azure   |
|                                   | > virtual machines different from |
|                                   | > the one you used to deploy      |
|                                   | > virtual machines earlier in     |
|                                   | > this lab                        |
+-----------------------------------+-----------------------------------+
| Availability zone                 | > **Zones 1, 2, 3**               |
+-----------------------------------+-----------------------------------+
| Orchestration mode                | > **Uniform**                     |
+-----------------------------------+-----------------------------------+
| Image                             | > **Windows Server 2019           |
|                                   | > Datacenter - Gen2**             |
+-----------------------------------+-----------------------------------+
| > Run with Azure Spot discount    | > **No**                          |
+-----------------------------------+-----------------------------------+
| Size                              | > **Standard D2s_v3**             |
+-----------------------------------+-----------------------------------+
| Username                          | > **Student**                     |
+-----------------------------------+-----------------------------------+
| Password                          | > **Provide a secure password**   |
+-----------------------------------+-----------------------------------+
| > Already have a                  | > **Unchecked**                   |
| >                                 |                                   |
| > Windows Server                  |                                   |
|                                   |                                   |
| license?                          |                                   |
+-----------------------------------+-----------------------------------+

**Note**: For the list of Azure regions which support deployment of
Windows virtual machines to availability zones, refer to

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image93.png){width="6.5in"
height="3.0680555555555555in"}

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image94.png){width="6.5in"
height="2.85in"}

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image95.png){width="6.5in"
height="3.138888888888889in"}

3\. On the **Disks** tab of the **Create a virtual machine scale set**
blade, accept the default values and click **Next : Networking \>**.

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image96.png){width="6.5in"
> height="3.15in"}

4\. On the **Networking** tab of the **Create a virtual machine scale
set** blade, click the **Create virtual** **network** link below the
**Virtual network** textbox and create a new virtual network with the
following settings (leave others with their default values).

  -----------------------------------------------------------------------
  Setting                             Value
  ----------------------------------- -----------------------------------
  Name                                **az104-08-rg02-vnet**

  Address range                       **10.82.0.0/20**

  Subnet name                         **subnet0**

  Subnet range                        **10.82.0.0/24**
  -----------------------------------------------------------------------

**Note**: Once you create a new virtual network and return to the
**Networking** tab of the **Create a virtual machine scale set** blade,
the **Virtual network** value will be automatically set to
**az104-08-rg02-vnet**.

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image97.png){width="6.5in"
height="3.2291666666666665in"}

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image98.png){width="6.5in"
height="3.1680555555555556in"}

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image99.png){width="6.5in"
height="2.995833333333333in"}

5\. Back on the **Networking** tab of the **Create a virtual machine
scale set** blade, click the **Edit network** **interface** icon to the
right of the network interface entry.

6\. On the **Edit network interface** blade, in the **NIC network
security group** section, click **Advanced** and click **Create new**
under the **Configure network security group** drop-down list.

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image100.png){width="6.5in"
> height="3.165277777777778in"}

7\. On the **Create network security group** blade, specify the
following settings (leave others with their default values):

  -----------------------------------------------------------------------
  Setting                             Value
  ----------------------------------- -----------------------------------
  Name                                **az10408vmss0-nsg**

  -----------------------------------------------------------------------

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image101.png){width="6.5in"
> height="3.2152777777777777in"}

8\. Click **Add an inbound rule** and add an inbound security rule with
the following settings (leave others with their default values):

  -----------------------------------------------------------------------
  Setting                             Value
  ----------------------------------- -----------------------------------
  Source                              **Any**

  Source port ranges                  **\***

  Destination                         **Any**

  Destination port ranges             **80**

  Protocol                            **TCP**

  Action                              **Allow**

  Priority                            **1010**

  Name                                **custom-allow-http**
  -----------------------------------------------------------------------

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image102.png){width="6.5in"
> height="3.1319444444444446in"}
>
> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image103.png){width="6.5in"
> height="3.1486111111111112in"}

9\. Click **Add** and, back on the **Create network security group**
blade, click **OK**.

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image104.png){width="6.5in"
> height="3.0in"}
>
> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image105.png){width="6.5in"
> height="3.1694444444444443in"}

10.Back on the **Edit network interface** blade, in the **Public IP
address** section, click **Enabled** and click **OK**.

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image106.png){width="6.5in"
> height="3.0708333333333333in"}

11.Back on the **Networking** tab of the **Create a virtual machine
scale set** blade, under the **Load** **balancing** section, specify the
following (leave others with their default values).

  -----------------------------------------------------------------------
  Setting                             Value
  ----------------------------------- -----------------------------------
  Load balancing options              **Azure load balancer**

  Select a load balancer              **Create a load balancer**
  -----------------------------------------------------------------------

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image107.png){width="6.5in"
> height="3.1527777777777777in"}

12.On the **Create a load balancer** page, specify the load balancer
name and take the defaults. Click **Create** when you are done then
**Next : Scaling \>**.

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image108.png){width="6.5in"
> height="3.179165573053368in"}

  -----------------------------------------------------------------------
  Setting                             Value
  ----------------------------------- -----------------------------------
  Load balancer name                  **az10408vmss0-lb**

  -----------------------------------------------------------------------

13.On the **Scaling** tab of the **Create a virtual machine scale set**
blade, specify the following settings (leave others with their default
values) and click **Next : Management \>**:

  -----------------------------------------------------------------------
  Setting                             Value
  ----------------------------------- -----------------------------------
  Initial instance count              **2**

  Scaling policy                      **Manual**
  -----------------------------------------------------------------------

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image109.png){width="6.5in"
height="3.0680544619422574in"}

14.On the **Management** tab of the **Create a virtual machine scale
set** blade, specify the following settings (leave others with their
default values):

+-----------------------------------+-----------------------------------+
| > Setting                         | > Value                           |
+===================================+===================================+
| > Boot diagnostics                | > **Enable with custom storage    |
|                                   | > account**                       |
+-----------------------------------+-----------------------------------+
| > Diagnostics storage account     | > accept the default value        |
+-----------------------------------+-----------------------------------+

> **Note**: You will need the name of this storage account in the next
> task.
>
> Click **Next : Health \>**:

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image110.png){width="6.5in"
height="3.0805555555555557in"}

15.On the **Health** tab of the **Create a virtual machine scale set**
blade, review the default settings without making any changes and click
**Next : Advanced \>**.

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image111.png){width="6.5in"
> height="3.183333333333333in"}

16.On the **Advanced** tab of the **Create a virtual machine scale set**
blade, specify the following settings (leave others with their default
values) and click **Review + create**.

+-----------------------------------+-----------------------------------+
| Setting                           | > Value                           |
+===================================+===================================+
| Spreading algorithm               | > **Fixed spreading (not          |
|                                   | > recommended with zones)**       |
+-----------------------------------+-----------------------------------+

> **Note**: The **Max spreading** setting is currently not functional.

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image112.png){width="6.5in"
height="3.125in"}

17.On the **Review + create** tab of the **Create a virtual machine
scale set** blade, ensure that the validation passed and click
**Create**.

**Note**: Wait for the virtual machine scale set deployment to complete.
This should take about 5 minutes.

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image113.png){width="5.916666666666667in"
height="2.245832239720035in"}

**I got this validation error because my azure students account only
allowed 3 Public IP addresses. To solve I had to disable the Public IP
on the new NIC created**

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image114.png){width="6.5in"
height="2.9305555555555554in"}

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image115.png){width="6.5in"
height="3.0666655730533683in"}

Task 6: Configure Azure virtual machine scale sets by using virtual
machine extensions

In this task, you will install Windows Server Web Server role on the
instances of the Azure virtual machine scale set you deployed in the
previous task by using the Custom Script virtual machine extension.

1\. In the Azure portal, search for and select **Storage accounts** and,
on the **Storage accounts** blade, click the entry representing the
diagnostics storage account you created in the previous task.

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image116.png){width="6.5in"
> height="1.9972222222222222in"}

2\. On the storage account blade, in the **Data Storage** section, click
**Containers** and then click **+**

> **Container**.
>
> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image117.png){width="6.5in"
> height="2.988888888888889in"}

3\. On the **New container** blade, specify the following settings
(leave others with their default values)

> and click **Create**:

+-----------------------------------+-----------------------------------+
| Setting                           | > Value                           |
+===================================+===================================+
| Name                              | > **scripts**                     |
+-----------------------------------+-----------------------------------+
| Public access level               | > **Private (no anonymous         |
|                                   | > access**)                       |
+-----------------------------------+-----------------------------------+

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image118.png){width="6.5in"
> height="2.975in"}

4\. Back on the storage account blade displaying the list of containers,
click **scripts**.

5\. On the **scripts** blade, click **Upload**.

6\. On the **Upload blob** blade, click the folder icon, in the **Open**
dialog box, navigate to the

**\\Allfiles\\Labs\\08** folder, select **az104-08-install_IIS.ps1**,
click **Open**, and back on the **Upload blob**

> blade, click **Upload**.

7\. In the Azure portal, navigate back to the **Virtual machine scale
sets** blade and click **az10408vmss0**.

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image119.png){width="6.5in"
> height="2.058332239720035in"}

8\. On the **az10408vmss0** blade, in the **Settings** section, click
**Extensions and applications**, and the click

> **+ Add**.
>
> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image120.png){width="6.5in"
> height="3.1041666666666665in"}
>
> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image121.png){width="6.5in"
> height="3.095832239720035in"}

9\. On the **New resource** blade, click **Custom Script Extension** and
then click **Next**.

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image122.png){width="6.5in"
> height="3.033332239720035in"}

10.From the **Install extension** blade, **Browse** to and **Select**
the **az104-08-install_IIS.ps1** script that was uploaded to the
**scripts** container in the storage account earlier in this task, and
then click **Create**.

> **Note**: Wait for the installation of the extension to complete
> before proceeding to the next step.

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image123.png){width="6.5in"
height="3.044443350831146in"}

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image124.png){width="6.5in"
height="3.0069444444444446in"}

11.In the **Settings** section of the **az10408vmss0** blade, click
**Instances**, select the checkboxes next to the two instances of the
virtual machine scale set, click **Upgrade**, and then, when prompted
for confirmation, click **Yes**.

> **Note**: Wait for the upgrade to complete before proceeding to the
> next step.

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image125.png){width="6.5in"
height="2.826388888888889in"}

12.In the Azure portal, search for and select **Load balancers** and, in
the list of load balancers, click **az10408vmss0-lb**.

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image126.png){width="6.5in"
> height="3.0680544619422574in"}

13.On the **az10408vmss0-lb** blade, note the value of the **Public IP
address** assigned to the frontend of the load balancer, open an new
browser tab, and navigate to that IP address.

> **Note**: Verify that the browser page displays the name of one of the
> instances of the Azure virtual machine scale set **az10408vmss0**.

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image127.png){width="6.5in"
height="2.9624989063867018in"}

Task 7: Scale compute and storage for Azure virtual machine scale sets

In this task, you will change the size of virtual machine scale set
instances, configure their autoscaling settings, and attach disks to
them.

1\. In the Azure portal, search for and select **Virtual machine scale
sets** and select the **az10408vmss0** scale set

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image128.png){width="6.5in"
> height="3.183333333333333in"}

2\. In the **az10408vmss0** blade, in the **Settings** section, click
**Size**.

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image129.png){width="6.5in"
> height="3.1875in"}

3\. In the list of available sizes, select **Standard DS1_v2** and click
**Resize**.

> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image130.png){width="6.5in"
> height="3.209722222222222in"}
>
> ![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image131.png){width="6.5in"
> height="3.054165573053368in"}

4\. In the **Settings** section, click **Instances**, select the
checkboxes next to the two instances of the virtual machine scale set,
click **Upgrade**, and then, when prompted for confirmation, click
**Yes**.

5\. In the list of instances, click the entry representing the first
instance and, on the scale set instance blade, note its **Location** (it
should be one of the zones in the target Azure region into which you
deployed the Azure virtual machine scale set).

6\. Return to the **az10408vmss0 - Instances** blade, click the entry
representing the second instance and, on the scale set instance blade,
note its **Location** (it should be one of the other two zones in the
target Azure region into which you deployed the Azure virtual machine
scale set).

7\. Return to the **az10408vmss0 - Instances** blade, and in the
**Settings** section, click **Scaling**.

8\. On the **az10408vmss0 - Scaling** blade, select the **Custom
autoscale** option and configure autoscale with the following settings
(leave others with their default values):

  -----------------------------------------------------------------------
  Setting                             Value
  ----------------------------------- -----------------------------------
  Scale mode                          **Scale based on a metric**

  -----------------------------------------------------------------------

+-----------------------------------+-----------------------------------+
| 9\.                               | > Click the **+ Add a rule** link |
|                                   | > and, on the **Scale rule**      |
|                                   | > blade, specify the following    |
|                                   | > settings (leave others          |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

> with their default values):

+-----------------------------------+-----------------------------------+
| > Setting                         | > Value                           |
+===================================+===================================+
| > Metric source                   | > **Current resource              |
|                                   | > (az10480vmss0)**                |
+-----------------------------------+-----------------------------------+
| > Time aggregation                | > **Average**                     |
+-----------------------------------+-----------------------------------+
| > Metric namespace                | > **Virtual Machine Host**        |
+-----------------------------------+-----------------------------------+
| > Metric name                     | > **Network In Total**            |
+-----------------------------------+-----------------------------------+
| > Operator                        | > **Greater than**                |
+-----------------------------------+-----------------------------------+
| > Metric threshold to trigger     | > **10**                          |
| > scale action                    |                                   |
+-----------------------------------+-----------------------------------+
| > Duration (in minutes)           | > **1**                           |
+-----------------------------------+-----------------------------------+
| > Time grain statistic            | > **Average**                     |
+-----------------------------------+-----------------------------------+
| > Operation                       | > **Increase count by**           |
+-----------------------------------+-----------------------------------+
| > Instance count                  | > **1**                           |
+-----------------------------------+-----------------------------------+
| > Cool down (minutes)             | > **5**                           |
+-----------------------------------+-----------------------------------+

> **Note**: Obviously these values do not represent a realistic
> configuration, since their purpose is to trigger autoscaling as soon
> as possible, without extended wait period.

10.Click **Add** and, back on the **az10408vmss0 - Scaling** blade,
specify the following settings (leave others with their default values):

+-----------------------------------+-----------------------------------+
| > Setting                         | Value                             |
+===================================+===================================+
| > Instance limits Minimum         | **1**                             |
+-----------------------------------+-----------------------------------+
| > Instance limits Maximum         | **3**                             |
+-----------------------------------+-----------------------------------+
| > Instance limits Default         | **1**                             |
+-----------------------------------+-----------------------------------+

11.Click **Save**.

12.In the Azure portal, open the **Azure Cloud Shell** by clicking on
the icon in the top right of the Azure Portal.

13.If prompted to select either **Bash** or **PowerShell**, select
**PowerShell**.

14.From the Cloud Shell pane, run the following to identify the public
IP address of the load balancer in front of the Azure virtual machine
scale set **az10408vmss0**.

+-----------------------+-----------------------+-----------------------+
| > \$rgName            | =                     | \'az104-08-rg02\'     |
+=======================+=======================+=======================+
+-----------------------+-----------------------+-----------------------+

+-----------------------+-----------------------+-----------------------+
| > \$lbpipName         | =                     | > \'az104             |
|                       |                       | 08vmss0-lb-publicip\' |
+=======================+=======================+=======================+
+-----------------------+-----------------------+-----------------------+

> \$pip=(Get-AzPublicIpAddress -ResourceGroupName \$rgName-Name \$l
> bpipName).IpAddress

15.From the Cloud Shell pane, run the following to start an infinite
loop that sends the HTTP requests to the web sites hosted on the
instances of Azure virtual machine scale set **az10408vmss0**.

> **while**(\$true){Invoke-WebRequest-Uri \"http://\$pip\"}

16.Minimize the Cloud Shell pane but do not close it, switch back to the
**az10408vmss0 - Instances** blade and monitor the number of instances.

> **Note**: You might need to wait a couple of minutes and click
> **Refresh**.

17.Once the third instance is provisioned, navigate to its blade to
determine its **Location** (it should be different than the first two
zones you identified earlier in this task.

18.Close Cloud Shell pane.

19.On the **az10408vmss0** blade, in the **Settings** section, click
**Disks**, click **+ Create and attach a new disk**, and attach a new
managed disk with the following settings (leave others with their
default values):

  -----------------------------------------------------------------------
  Setting                             Value
  ----------------------------------- -----------------------------------
  LUN                                 **0**

  Storage type                        **Standard HDD**

  Size (GiB)                          **32**
  -----------------------------------------------------------------------

20.Save the change, in the **Settings** section of the **az10408vmss0**
blade, click **Instances**, select the checkboxes next to the instances
of the virtual machine scale set, click **Upgrade**, and then, when
prompted for confirmation, click **Yes**.

> **Note**: The disk attached in the previous step is a raw disk. Before
> it can be used, it is necessary to create a partition, create a
> filesystem, and mount it. To accomplish this, you will use Azure
> virtual machine Custom Script extension. First, you will need to
> remove the existing Custom Script Extension.

21.In the **Settings** section of the **az10408vmss0** blade, click
**Extensions and applications**, click **CustomScriptExtension**, and
then click **Uninstall**.

> **Note**: Wait for uninstallation to complete.

22.In the Azure portal, open the **Azure Cloud Shell** by clicking on
the icon in the top right of the Azure Portal.

23.If prompted to select either **Bash** or **PowerShell**, select
**PowerShell**.

24.In the toolbar of the Cloud Shell pane, click the **Upload/Download
files** icon, in the drop-down menu, click **Upload** and upload the
file **\\Allfiles\\Labs\\08\\az104-08-configure_VMSS_disks.ps1** into
the Cloud Shell home directory.

25.From the Cloud Shell pane, run the following to display the content
of the script:

+-----------------------+-----------------------+-----------------------+
| > Set-Location        | -Path                 | \$HOME                |
+=======================+=======================+=======================+
+-----------------------+-----------------------+-----------------------+

> Get-Content-Path ./az104-08-configure_VMSS_disks.ps1
>
> **Note**: The script installs a custom script extension that
> configures the attached disk.

26.From the Cloud Shell pane, run the following to execute the script
and configure disks of Azure virtual machine scale set:

> ./az104-08-configure_VMSS_disks.ps1

27.Close the Cloud Shell pane.

28.In the **Settings** section of the **az10408vmss0** blade, click
**Instances**, select the checkboxes next to the instances of the
virtual machine scale set, click **Upgrade**, and then, when prompted
for confirmation, click **Yes**.

Clean up resources

> **Note**: Remember to remove any newly created Azure resources that
> you no longer use. Removing unused resources ensures you will not see
> unexpected charges.
>
> **Note**: Don't worry if the lab resources cannot be immediately
> removed. Sometimes resources have dependencies and take a longer time
> to delete. It is a common Administrator task to monitor resource
> usage, so just periodically review your resources in the Portal to see
> how the cleanup is going. 1. In the Azure portal, open the
> **PowerShell** session within the **Cloud Shell** pane.

1\. Remove az104-08-configure_VMSS_disks.ps1 by running the following
command:

> rm\~\\az104-08\*

2\. List all resource groups created throughout the labs of this module
by running the following command:

> Get-AzResourceGroup -Name \'az104-08\*\'

3\. Delete all resource groups you created throughout the labs of this
module by running the following command:

> Get-AzResourceGroup -Name \'az104-08\*\' \| Remove-AzResourceGroup -F
> orce -AsJob
>
> **Note**: The command executes asynchronously (as determined by the
> -AsJob parameter), so while you will be able to run another PowerShell
> command immediately afterwards within the same PowerShell session, it
> will take a few minutes before the resource groups are actually
> removed.
>
> Review
>
> In this lab, you have:
>
> • Deployed zone-resilient Azure virtual machines by using the Azure
> portal and an Azure
>
> Resource Manager template
>
> • Configured Azure virtual machines by using virtual machine
> extensions
>
> • Scaled compute and storage for Azure virtual machines
>
> • Deployed zone-reslient Azure virtual machine scale sets by using the
> Azure portal
>
> • Configured Azure virtual machine scale sets by using virtual machine
> extensions
>
> • Scaled compute and storage for Azure virtual machine scale sets
>
> **[Conclusion]{.underline}**
>
> **Failed to update resource \'az10408vmss0\'**

There was an error updating instance count for resource
\'az10408vmss0\'. Detail message \'{ \"error\": {

\"details\": \[\], \"code\": \"PublicIPCountLimitExceededByVMScaleSet\",
\"message\": \"The requested number of

+---------+---------+---------+---------+---------+---------+---------+
| > pub   | 2       | for     | VM      | Scale   | Set     | > /sub  |
| licIPAd |         |         |         |         |         | scripti |
| dresses |         |         |         |         |         | ons/3db |
|         |         |         |         |         |         | bb8d5-1 |
|         |         |         |         |         |         | 829-48d |
|         |         |         |         |         |         | 8-a51d- |
+=========+=========+=========+=========+=========+=========+=========+
+---------+---------+---------+---------+---------+---------+---------+

> c7f11b061059/resourceGroups/AZ104-08-

RG02/providers/Microsoft.Compute/virtualMachineScaleSets/az10408vmss0
will exceed the maximum

number of publicIPAddresses allowed 3 for subscription
3dbbb8d5-1829-48d8-a51d-c7f11b061059.\" } }\',

Please try again in a few moments.This error really prevented me from
tackling fully task 7. This is due to

> my free student subscription which only allows a maximum number of 3
> public IP addresses.

![](vertopal_7e545625c4ee41eeb45f45cf83692f56/media/image132.png){width="6.5in"
height="2.9555555555555557in"}

This report highlights the deployment and management of zone-resilient
Azure virtual machines and scale

sets. Using the Azure portal and Resource Manager templates, we achieved
fault tolerance across multiple

availability zones. Virtual machine extensions were employed for
efficient configuration, ensuring a

customized and easily maintainable environment. The report also
emphasizes the scalability of compute

and storage resources, enabling dynamic adaptation to varying workloads.
Overall, these implementations align with best practices, establishing a
resilient, high-performance cloud infrastructure
