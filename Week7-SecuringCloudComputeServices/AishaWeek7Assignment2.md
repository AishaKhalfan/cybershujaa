Week7: **Assignment 2:-Configuring and Securing ACR and AKS**

Report by: **Aisha Khalifan, cs-cns04-23014**

> **Introduction**
>
> You have been asked to deploy a proof of concept with Azure Container
> Registry and Azure Kubernetes Service. Specifically, the proof of
> concept should demonstrate:

+-----------------------------------+-----------------------------------+
| > •\                              | > Using Dockerfile to build an    |
| > •\                              | > image.                          |
| > •\                              | >                                 |
| > •                               | > Using Azure Container Registry  |
|                                   | > to store images.                |
|                                   | >                                 |
|                                   | > Configuring an Azure Kubernetes |
|                                   | > Service.                        |
|                                   | >                                 |
|                                   | > Securing and accessing          |
|                                   | > container applications both     |
|                                   | > internally and                  |
|                                   | > externally.Configuring and      |
|                                   | > Securing ACR and AKS diagram    |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

> **Configuring and Securing ACR and AKS diagram**
>
> ![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image1.png){width="2.7763877952755904in"
> height="2.7625in"}
>
> **Intructions**
>
> **Lab files:**\
> • **\\Allfiles\\Labs\\09\\nginxexternal.yaml**\
> • **\\Allfiles\\Labs\\09\\nginxinternal.yaml**
>
> **Exercise 1: Configuring and Securing ACR and AKS**
>
> **Estimated timing: 45 minutes**\
> For all the resources in this lab, we are using the **East (US)**
> region.
>
> In this exercise, you will complete the following tasks:

+-----------------------------------+-----------------------------------+
| •\                                | > Task 1: Create an Azure         |
| •                                 | > Container Registry\             |
|                                   | > Task 2: Create a Dockerfile,    |
|                                   | > build a container and push it   |
|                                   | > to Azure Container Registry     |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

+-----------------------------------+-----------------------------------+
| > •\                              | > Task 3: Create an Azure         |
| > •\                              | > Kubernetes Service cluster\     |
| > •\                              | > Task 4: Grant the AKS cluster   |
| > •\                              | > permissions to access the ACR   |
| > •\                              | > Task 5: Deploy an external      |
| > •                               | > service to AKS\                 |
|                                   | > Task 6: Verify the you can      |
|                                   | > access an external AKS-hosted   |
|                                   | > service Task 7: Deploy an       |
|                                   | > internal service to AKS\        |
|                                   | > Task 8: Verify the you can      |
|                                   | > access an internal AKS-hosted   |
|                                   | > service                         |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

**Task 1: Create an Azure Container Registry**\
In this task, you will create a resource group for the lab an Azure
Container Registry.

1\. Sign-in to the Azure portal **https://portal.azure.com/**.

> **Note**: Sign in to the Azure portal using an account that has the
> Owner or Contributor role in the Azure subscription you are using for
> this lab and the Global Administrator role in the Microsoft Entra
> tenant associated with that subscription.

![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image2.png){width="6.5in"
height="3.1625in"}

+-----------------------------------+-----------------------------------+
| 2\. 3.                            | > In the Azure portal, open the   |
|                                   | > Cloud Shell by clicking the     |
|                                   | > first icon in the top right of  |
|                                   | > the Azure Portal. If prompted,  |
|                                   | > click **Bash** and **Create     |
|                                   | > storage**.                      |
|                                   |                                   |
|                                   | Ensure **Bash** is selected in    |
|                                   | the drop-down menu in the         |
|                                   | upper-left corner of the Cloud    |
|                                   | Shell pane.                       |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

> ![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image3.png){width="6.5in"
> height="3.1680555555555556in"}

+-----------------------------------+-----------------------------------+
| 4\.                               | > In the Bash session within the  |
|                                   | > Cloud Shell pane, run the       |
|                                   | > following to create a new       |
|                                   | > resource group for this lab:    |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

> ***az group create \--name AZ500LAB09 \--location eastus***
>
> ![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image4.png){width="6.5in"
> height="3.091666666666667in"}

+-----------------------------------+-----------------------------------+
| 5\.                               | > In the Bash session within the  |
|                                   | > Cloud Shell pane, run the       |
|                                   | > following to verify the         |
|                                   | > resource group was created:     |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

> ***az group list \--query \"\[?name==\'AZ500LAB09\'\]\" -o table***
>
> ![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image5.png){width="6.5in"
> height="3.1555555555555554in"}

+-----------------------------------+-----------------------------------+
| 6\.                               | > In the Bash session within the  |
|                                   | > Cloud Shell pane, run the       |
|                                   | > following to create a new Azure |
|                                   | > Container Registry (ACR)        |
|                                   | > instance (The name of the ACR   |
|                                   | > must be globally unique):       |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

***az acr create \--resource-group AZ500LAB09 \--name
az500\$RANDOM\$RANDOM \--sku Basic***

> ![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image6.png){width="6.5in"
> height="3.111111111111111in"}
>
> ![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image7.png){width="6.5in"
> height="3.1819444444444445in"}
>
> ![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image8.png){width="6.5in"
> height="3.170832239720035in"}

+-----------------------------------+-----------------------------------+
| 7\.                               | > In the Bash session within the  |
|                                   | > Cloud Shell pane, run the       |
|                                   | > following to confirm that the   |
|                                   | > new ACR was created:            |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

***az acr list \--resource-group AZ500LAB09***\
**Note**: Record the name of the ACR. You will need it in the next task.

![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image9.png){width="6.5in"
height="3.1680555555555556in"}

![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image10.png){width="6.5in"
height="3.1638888888888888in"}

![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image11.png){width="6.5in"
height="3.0444444444444443in"}

***Task 2: Create a Dockerfile, build a container and push it to Azure
Container Registry***

In this task, you will create a Dockerfile, build an image from the
Dockerfile, and deploy the

image to the ACR.

+-----------------------------------+-----------------------------------+
| 1\.                               | > In the Bash session within the  |
|                                   | > Cloud Shell pane, run the       |
|                                   | > following to create a           |
|                                   | > Dockerfile to create an         |
|                                   | > Nginx-based image:              |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

> ***echo FROM nginx \> Dockerfile***
>
> ![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image12.png){width="6.5in"
> height="0.5694444444444444in"}

+-----------------------------------+-----------------------------------+
| 2\.                               | > In the Bash session within the  |
|                                   | > Cloud Shell pane, run the       |
|                                   | > following to build an image     |
|                                   | > from the Dockerfile and push    |
|                                   | > the image to the new ACR.       |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

**Note**: The trailing period at the end of the command line is
required. It designates the

current directory as the location of Dockerfile.

***ACRNAME=\$(az acr list \--resource-group AZ500LAB09 \--query
\'\[\].{Name:name}\' \--output tsv)***

***az acr build \--resource-group AZ500LAB09 \--image sample/nginx:v1
\--registry \$ACRNAME \--file Doc***

***kerfile .***

**Note**: Wait for the command to successfully complete. This might take
about 2 minutes.

![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image13.png){width="6.5in"
height="3.1944444444444446in"}

![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image14.png){width="6.5in"
height="3.1555555555555554in"}

![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image15.png){width="6.5in"
height="3.1958333333333333in"}

![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image16.png){width="6.5in"
height="3.111111111111111in"}

+-----------------------------------+-----------------------------------+
| 3\. 4.                            | > Close the Cloud Shell pane.     |
|                                   | >                                 |
|                                   | > In the Azure portal, navigate   |
|                                   | > to the **AZ500Lab09** resource  |
|                                   | > group and, in the list of       |
|                                   | > resources, click the entry      |
|                                   | > representing the Azure          |
|                                   | > Container Registry instance you |
|                                   | > provisioned in the previous     |
|                                   | > task.                           |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

> ![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image17.png){width="6.5in"
> height="3.1805555555555554in"}

5\. On the Container registry blade, in the **Services** section, click
**Repositories**.

> ![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image18.png){width="6.5in"
> height="3.0569444444444445in"}

6\. Verify that the list of repositories includes the new container
image named **sample/nginx**.

> ![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image19.png){width="6.5in"
> height="3.1305544619422574in"}

7\. Click the **sample/nginx** entry and verify presence of the **v1**
tag that identifies the image version.

> ![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image20.png){width="6.5in"
> height="3.125in"}

8\. Click the **v1** entry to view the image manifest.

> **Note**: The manifest includes the sha256 digest, manifest creation
> date, and platform entries.

![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image21.png){width="6.5in"
height="3.111111111111111in"}

![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image22.png){width="6.5in"
height="3.120832239720035in"}

![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image23.png){width="6.5in"
height="3.1041666666666665in"}

**Task 3: Create an Azure Kubernetes Service cluster**\
In this task, you will create an Azure Kubernetes service and review the
deployed resources.

+-----------------------------------+-----------------------------------+
| 1\.                               | > In the Azure portal, in the     |
|                                   | > **Search resources, services,   |
|                                   | > and docs** text box at the top  |
|                                   | > of the Azure portal page, type  |
|                                   | > **Kubernetes services** and     |
|                                   | > press the **Enter** key.        |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

> ![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image24.png){width="6.5in"
> height="3.1555555555555554in"}

+-----------------------------------+-----------------------------------+
| 2\.                               | > On the **Kubernetes services**  |
|                                   | > blade, click **+ Create** and,  |
|                                   | > in the drop-down menu, click    |
|                                   | > **+ Create a Kubernetes         |
|                                   | > cluster**                       |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

> ![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image25.png){width="6.5in"
> height="3.1222222222222222in"}

+-----------------------------------+-----------------------------------+
| 3\.                               | > On the **Basics** tab of the    |
|                                   | > **Create Kubernetes cluster**   |
|                                   | > blade, select **Cluster preset  |
|                                   | > configuration**, select         |
|                                   | > **Dev/Test (\$)**. Now specify  |
|                                   | > the following settings (leave   |
|                                   | > others with their default       |
|                                   | > values):                        |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

+-----------------------------------+-----------------------------------+
| Setting                           | > Value                           |
+===================================+===================================+
| Subscription                      | > the name of the Azure           |
|                                   | > subscription you are using in   |
|                                   | > this lab                        |
+-----------------------------------+-----------------------------------+
| Resource group                    | > **AZ500LAB09**                  |
+-----------------------------------+-----------------------------------+
| > Kubernetes cluster name         | > **MyKubernetesCluster**         |
+-----------------------------------+-----------------------------------+
| Region                            | > **(US) East US**                |
+-----------------------------------+-----------------------------------+
| Availability zones                | > **None**                        |
+-----------------------------------+-----------------------------------+
| Scale method                      | > **Manual**                      |
+-----------------------------------+-----------------------------------+
| Node count                        | > **1**                           |
+-----------------------------------+-----------------------------------+

![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image26.png){width="6.5in"
height="3.158332239720035in"}

![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image27.png){width="6.5in"
height="3.1277777777777778in"}

+-----------------------------------+-----------------------------------+
| 4\.                               | > Click **Next: Node Pools \>**   |
|                                   | > and, on the **Node Pools** tab  |
|                                   | > of the **Create Kubernetes      |
|                                   | > cluster** blade, specify the    |
|                                   | > following settings (leave       |
|                                   | > others with their default       |
|                                   | > values):                        |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

  -----------------------------------------------------------------------
  Setting                             Value
  ----------------------------------- -----------------------------------
  Enable virtual nodes                cleared checkbox

  -----------------------------------------------------------------------

> ![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image28.png){width="6.5in"
> height="2.941666666666667in"}

+-----------------------------------+-----------------------------------+
| 5\.                               | > Click **Next: Access \>**, on   |
|                                   | > the **Access** tab of the       |
|                                   | > **Create Kubernetes cluster**   |
|                                   | > blade, accept the defaults, and |
|                                   | > click **Next: Networking \>**.  |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

> ![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image29.png){width="6.5in"
> height="3.1486100174978127in"}

+-----------------------------------+-----------------------------------+
| 6\.                               | > On the **Networking** tab of    |
|                                   | > the **Create Kubernetes         |
|                                   | > cluster** blade, specify the    |
|                                   | > following settings (leave       |
|                                   | > others with their default       |
|                                   | > values):                        |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

+-----------------------------------+-----------------------------------+
| Setting                           | > Value                           |
+===================================+===================================+
| Network configuration             | > **Azure CNI**                   |
+-----------------------------------+-----------------------------------+
| DNS name prefix                   | > **Leave the default value**     |
+-----------------------------------+-----------------------------------+

> **Note**: AKS can be configured as a private cluster. This assigns a
> private IP to the API server to ensure network traffic between your
> API server anly. For more information, visit page.

![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image30.png){width="6.5in"
height="3.0402766841644793in"}

+-----------------------------------+-----------------------------------+
| 7\.                               | > Click **Next: Integrations \>** |
|                                   | > and, on the **Integrations**    |
|                                   | > tab of the **Create Kubernetes  |
|                                   | > cluster** blade, set            |
|                                   | > **Container monitoring** to     |
|                                   | > **Disabled**.                   |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

> **Note**: In production scenarios, you would want to enable
> monitoring. Monitoring is disabled in this case since it is not
> covered in the lab.

![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image31.png){width="6.5in"
height="2.934721128608924in"}

![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image32.png){width="6.5in"
height="3.1319444444444446in"}

8\. Click **Review + Create** and then click **Create**.

> **Note**: Wait for the deployment to complete. This might take about
> 10 minutes.

![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image33.png){width="6.5in"
height="3.1277777777777778in"}

![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image34.png){width="6.5in"
height="3.109721128608924in"}

+-----------------------------------+-----------------------------------+
| 9\.                               | > Once the deployment completes,  |
|                                   | > in the Azure portal, in the     |
|                                   | > **Search resources, services,   |
|                                   | > and docs** text box at the top  |
|                                   | > of the Azure portal page, type  |
|                                   | > **Resource groups** and press   |
|                                   | > the **Enter** key.              |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

> ![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image35.png){width="6.5in"
> height="3.165277777777778in"}

10.On the **Resource groups** blade, in the listing of resource groups,
note a new resource group named
**MC_AZ500LAB09_MyKubernetesCluster_eastus** that holds components of
the AKS Nodes. Review resources in this resource group.

> ![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image36.png){width="6.5in"
> height="3.0388888888888888in"}

11.Navigate back to the **Resource groups** blade and click the
**AZ500LAB09** entry.

> **Note**: In the list of resources, note the AKS Cluster and the
> corresponding virtual network.

![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image37.png){width="6.5in"
height="3.123611111111111in"}

12.In the Azure portal, open a Bash session in the Cloud Shell.

> **Note**: Ensure **Bash** is selected in the drop-down menu in the
> upper-left corner of the Cloud Shell pane.

![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image38.png){width="6.5in"
height="3.0833333333333335in"}

13.In the Bash session within the Cloud Shell pane, run the following to
connect to the Kubernetes cluster:

> ***az aks get-credentials \--resource-group AZ500LAB09 \--name
> MyKubernetesCluster***
>
> ![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image39.png){width="6.5in"
> height="3.1652766841644793in"}

14.In the Bash session within the Cloud Shell pane, run the following to
list nodes of the Kubenetes cluster:

***kubectl get nodes***

**Note**: Verify that the **Status** of the cluster node is listed as
**Ready**.

![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image40.png){width="6.5in"
height="3.0430555555555556in"}

**Task 4: Grant the AKS cluster permissions to access the ACR and manage
its virtual network**\
In this task, you will grant the AKS cluster permission to access the
ACR and manage its virtual network.

+-----------------------------------+-----------------------------------+
| 1\.                               | > In the Bash session within the  |
|                                   | > Cloud Shell pane, run the       |
|                                   | > following to configure the AKS  |
|                                   | > cluster to use the Azure        |
|                                   | > Container Registry instance you |
|                                   | > created earlier in this lab.    |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

> ***ACRNAME=\$(az acr list \--resource-group AZ500LAB09 \--query
> \'\[\].{Name:name}\' \--output tsv )***
>
> ***az aks update -n MyKubernetesCluster -g AZ500LAB09 \--attach-acr
> \$ACRNAME***

**Note**: This command grants the 'acrpull' role assignment to the ACR.
**Note**: It may take a few minutes for this command to complete.

![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image41.png){width="6.5in"
height="3.0208333333333335in"}

![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image42.png){width="6.5in"
height="3.1652766841644793in"}

![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image43.png){width="6.5in"
height="3.1486111111111112in"}

![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image44.png){width="6.5in"
height="3.1194433508311463in"}

![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image45.png){width="6.5in"
height="3.1222222222222222in"}

![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image46.png){width="6.5in"
height="3.1666666666666665in"}

![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image47.png){width="6.5in"
height="3.1347222222222224in"}

+-----------------------------------+-----------------------------------+
| 2\.                               | > In the Bash session within the  |
|                                   | > Cloud Shell pane, run the       |
|                                   | > following to grant the AKS      |
|                                   | > cluster the Contributor role to |
|                                   | > its virtual network.            |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

> *RG_AKS=AZ500LAB09*\
> *AKS_VNET_NAME=AZ500LAB09-vnet*\
> *AKS_CLUSTER_NAME=MyKubernetesCluster*\
> *AKS_VNET_ID=\$(az network vnet show \--name \$AKS_VNET_NAME
> \--resource-group \$RG_AK S \--query id -o tsv)*\
> *AKS_MANAGED_ID=\$(az aks show \--name \$AKS_CLUSTER_NAME
> \--resource-group \$RG_A KS \--query identity.principalId -o tsv)*\
> *az role assignment create \--assignee \$AKS_MANAGED_ID \--role
> \"Contributor\" \--scope \$AKS_V NET_ID*
>
> ![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image48.png){width="6.5in"
> height="3.05in"}
>
> ![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image49.png){width="6.5in"
> height="3.1819444444444445in"}
>
> ![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image50.png){width="6.5in"
> height="2.322221128608924in"}

**Task 5: Deploy an external service to AKS**\
In this task, you will download the Manifest files, edit the YAML file,
and apply your changes to the cluster.

+-----------------------------------+-----------------------------------+
| 1\.                               | > In the Bash session within the  |
|                                   | > Cloud Shell pane, click the     |
|                                   | > **Upload/Download files** icon, |
|                                   | > in the drop-down menu, click    |
|                                   | > **Upload**, in the **Open**     |
|                                   | > dialog box, naviate to the      |
|                                   | > location where you downloaded   |
|                                   | > the lab files, select           |
|                                   | > **\\Allfile                     |
|                                   | s\\Labs\\09\\nginxexternal.yaml** |
|                                   | > click **Open**. Next, select\   |
|                                   | > **\\Allfiles                    |
|                                   | \\Labs\\09\\nginxinternal.yaml**, |
|                                   | > and click **Open**.             |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

> ![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image51.png){width="6.5in"
> height="3.051388888888889in"}
>
> ![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image52.png){width="6.5in"
> height="2.988888888888889in"}

+-----------------------------------+-----------------------------------+
| 2\.                               | > In the Bash session within the  |
|                                   | > Cloud Shell pane, run the       |
|                                   | > following to identify the name  |
|                                   | > of the Azure Container Registry |
|                                   | > instance:                       |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

> ***echo \$ACRNAME***
>
> **Note**: Record the Azure Container Registry instance name. You will
> need it later in this task.

![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image53.png){width="6.5in"
height="3.058333333333333in"}

+-----------------------------------+-----------------------------------+
| 3\.                               | > In the Bash session within the  |
|                                   | > Cloud Shell pane, run the       |
|                                   | > following to open the           |
|                                   | > nginxexternal.yaml file, so you |
|                                   | > can edit its content.           |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

> ***code ./nginxexternal.yaml***
>
> **Note**: This is the *external* yaml file.

![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image53.png){width="6.5in"
height="3.058333333333333in"}

+-----------------------------------+-----------------------------------+
| 4\.                               | > In the editor pane, scroll down |
|                                   | > to **line 24** and replace the  |
|                                   | > **\<ACRUniquename\>**           |
|                                   | > placeholder with the ACR name.  |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

> ![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image54.png){width="6.5in"
> height="3.1347222222222224in"}

+-----------------------------------+-----------------------------------+
| 5\. 6.                            | > In the editor pane, in the      |
|                                   | > upper right corner, click the   |
|                                   | > **ellipses** icon, click        |
|                                   | > **Save** and then click **Close |
|                                   | > editor**.                       |
|                                   | >                                 |
|                                   | > In the Bash session within the  |
|                                   | > Cloud Shell pane, run the       |
|                                   | > following to apply the change   |
|                                   | > to the cluster:                 |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

> ***kubectl apply -f nginxexternal.yaml***
>
> ![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image55.png){width="6.5in"
> height="0.5916655730533683in"}

+-----------------------------------+-----------------------------------+
| 7\.                               | > In the Bash session within the  |
|                                   | > Cloud Shell pane, review the    |
|                                   | > output of the command you run   |
|                                   | > in the previous task to verify  |
|                                   | > that the deployment and the     |
|                                   | > corresponding service have been |
|                                   | > created.                        |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

> ***deployment.apps/nginxexternal created***\
> ***service/nginxexternal created***
>
> ![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image55.png){width="6.5in"
> height="0.5916666666666667in"}

**Task 6: Verify the you can access an external AKS-hosted service**\
In this task, verify the container can be accessed externally using the
public IP address.

+-----------------------------------+-----------------------------------+
| 1\.                               | > In the Bash session within the  |
|                                   | > Cloud Shell pane, run the       |
|                                   | > following to retrieve           |
|                                   | > information about the           |
|                                   | > nginxexternal service including |
|                                   | > name, type, IP addresses, and   |
|                                   | > ports.                          |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

> ***kubectl get service nginxexternal***

![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image56.png){width="6.5in"
height="1.5166655730533682in"}

+-----------------------------------+-----------------------------------+
| 2\.                               | > In the Bash session within the  |
|                                   | > Cloud Shell pane, review the    |
|                                   | > output and record the value in  |
|                                   | > the External-IP column. You     |
|                                   | > will need it in the next step.  |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

> **EXTERNAL IP = 4.157.130.38**

3\. Open a new browser tab and browse to the IP address you identified
in the previous step.

> ![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image57.png){width="6.5in"
> height="0.5069444444444444in"}

4\. Ensure the **Welcome to nginx!** page displays.

> ![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image58.png){width="6.5in"
> height="3.683333333333333in"}

**Task 7: Deploy an internal service to AKS**

In this task, you will deploy the internal facing service on the AKS.

+-----------------------------------+-----------------------------------+
| 1\.                               | > In the Bash session within the  |
|                                   | > Cloud Shell pane, run the       |
|                                   | > following to open the           |
|                                   | > nginxintenal.yaml file, so you  |
|                                   | > can edit its content.           |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

> ***code ./nginxinternal.yaml***
>
> **Note**: This is the *internal* yaml file.

![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image59.png){width="6.5in"
height="3.2875in"}

+-----------------------------------+-----------------------------------+
| 2\.                               | > In the editor pane, scroll down |
|                                   | > to the line containing the      |
|                                   | > reference to the container      |
|                                   | > image and replace the           |
|                                   | > **\<ACRUniquename\>**           |
|                                   | > placeholder with the ACR name.  |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

> ![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image60.png){width="6.5in"
> height="3.2222222222222223in"}
>
> ![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image61.png){width="6.5in"
> height="3.1430555555555557in"}

+-----------------------------------+-----------------------------------+
| 3\.                               | > In the editor pane, in the      |
|                                   | > upper right corner, click the   |
|                                   | > **ellipses** icon, click        |
|                                   | > **Save** and then click **Close |
|                                   | > editor**.                       |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

> ![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image62.png){width="6.5in"
> height="3.1305555555555555in"}

4\. In the Bash session within the Cloud Shell pane, run the following
to apply the change to the cluster:

> ***kubectl apply -f nginxinternal.yaml***
>
> ![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image63.png){width="6.5in"
> height="3.3180544619422574in"}

+-----------------------------------+-----------------------------------+
| 5\.                               | > In the Bash session within the  |
|                                   | > Cloud Shell pane, review the    |
|                                   | > output to verify your           |
|                                   | > deployment and the service have |
|                                   | > been created:                   |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

> ***deployment.apps/nginxinternal created***\
> ***service/nginxinternal created***

+-----------------------------------+-----------------------------------+
| 6\.                               | > In the Bash session within the  |
|                                   | > Cloud Shell pane, run the       |
|                                   | > following to retrieve           |
|                                   | > information about the           |
|                                   | > nginxinternal service including |
|                                   | > name, type, IP addresses, and   |
|                                   | > ports.                          |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

> ***kubectl get service nginxinternal***
>
> ![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image64.png){width="6.5in"
> height="2.015277777777778in"}

+-----------------------------------+-----------------------------------+
| 7\.                               | > In the Bash session within the  |
|                                   | > Cloud Shell pane, review the    |
|                                   | > output. The External-IP is, in  |
|                                   | > this case, a private IP         |
|                                   | > address. If it is in a          |
|                                   | > **Pending** state then run the  |
|                                   | > previous command again.         |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

> **Note**: Record this IP address. You will need it in the next task.
>
> **Note**: To access the internal service endpoint, you will connect
> interactively to one of the pods running in the cluster.

**Note**: Alternatively you could use the CLUSTER-IP address.

![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image65.png){width="6.5in"
height="2.1277766841644796in"}

**Task 8: Verify the you can access an internal AKS-hosted service**

In this task, you will use one of the pods running on the AKS cluster to
access the internal service.

+-----------------------------------+-----------------------------------+
| 1\.                               | > In the Bash session within the  |
|                                   | > Cloud Shell pane, run the       |
|                                   | > following to list the pods in   |
|                                   | > the default namespace on the    |
|                                   | > AKS cluster:                    |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

***kubectl get pods***

![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image66.png){width="6.5in"
height="1.6416666666666666in"}

2\. In the listing of the pods, copy the first entry in the **NAME**
column.

**Note**: This is the pod you will use in the subsequent steps.

**nginxexternal-7c4d7d9f77-djf42**

+-----------------------------------+-----------------------------------+
| 3\.                               | > In the Bash session within the  |
|                                   | > Cloud Shell pane, run the       |
|                                   | > following to connect            |
|                                   | > interactively to the first pod  |
|                                   | > (replace the \<pod_name\>       |
|                                   | > placeholder with the name you   |
|                                   | > copied in the previous step):   |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

> ***kubectl exec -it \<pod_name\> \-- /bin/bash***

+-----------------------------------+-----------------------------------+
| 4\.                               | > In the Bash session within the  |
|                                   | > Cloud Shell pane, run the       |
|                                   | > following to verify that the    |
|                                   | > nginx web site is available via |
|                                   | > the private IP address of the   |
|                                   | > service (replace the            |
|                                   | > \<internal_IP\> placeholder     |
|                                   | > with the IP address you         |
|                                   | > recorded in the previous task): |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

> ***curl http://\<internal_IP\>***
>
> **This was my Internal IP = 4.157.130.38/**
>
> ![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image67.png){width="6.5in"
> height="3.1055555555555556in"}

5\. Close the Cloud Shell pane.

> Result: You have configured and secured ACR and AKS.

**Clean up resources**\
Remember to remove any newly created Azure resources that you no longer
use.

> Removing unused resources ensures you will not incur unexpected costs.

+-----------------------------------+-----------------------------------+
| 1\. 2. 3.                         | > In the Azure portal, open the   |
|                                   | > Cloud Shell by clicking the     |
|                                   | > first icon in the top right of  |
|                                   | > the Azure Portal.               |
|                                   | >                                 |
|                                   | > In the upper-left drop-down     |
|                                   | > menu of the Cloud Shell pane,   |
|                                   | > select **PowerShell** and, when |
|                                   | > prompted, click **Confirm**.    |
|                                   | >                                 |
|                                   | > In the PowerShell session       |
|                                   | > within the Cloud Shell pane,    |
|                                   | > run the following to remove the |
|                                   | > resource groups you created in  |
|                                   | > this lab:                       |
+===================================+===================================+
+-----------------------------------+-----------------------------------+

> ***Remove-AzResourceGroup -Name \"AZ500LAB09\" -Force --AsJob***
>
> ![](vertopal_be450274848f4fba90bb5ebb70f91455/media/image68.png){width="6.5in"
> height="2.6944444444444446in"}

4\. Close the **Cloud Shell** pane.

[Conclusion]{.underline}

In the lab, I had a hands-on journey with Azure tech. Learned to make
apps work in containers using Doc ker. Azure Container Registry helped
keep the app stuff safe and organized. Then, we jumped into Azure
Kubernetes Service, setting up a smart system for our apps that can grow
easily. Made sure apps were saf e to use, whether we were working
together or letting others see them. This all happened in the East US p
art of Azure, giving me a cool experience with putting apps on the
cloud.
