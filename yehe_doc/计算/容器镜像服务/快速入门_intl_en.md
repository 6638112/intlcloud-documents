This document describes how to purchase a Tencent Container Registry (TCR) Enterprise Edition instance, configure a network access policy, and push and pull container images.  
To use the TCR Personal Edition, please see [Image Registry User Guide](https://intl.cloud.tencent.com/document/product/457/9117).
> The TCR Enterprise Edition is currently in the beta phase. If you do not have the qualifications to use TCR Enterprise Edition beta, submit an application.  
>

## Step 1: Signing up for a Tencent Cloud Account
If you already have a Tencent Cloud account, ignore this step.  
Otherwise, go to the [Tencent Cloud Account Registration](https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fintl.cloud.tencent.com%2Fzh%2F%3Flang%3Dzh%26pg%3D) page and sign up for an account.

## Step 2: Purchasing an Enterprise Edition Instance<span id="domain"></span>
> If your enterprise is qualified for TCR Enterprise Edition beta but has not activated the TCR service, activate TCR and authorize TCR to access your COS and VPC resources. To activate TCR, use a root account or a sub-account with admin permissions. If you are using a sub-account, grant the sub-account corresponding permissions first. For more information, see Examples of Enterprise Edition Authorization Schemes.
>
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and go to the "Instance List" page.
2. Click **Create**. In the "Create Instance" window, configure your exclusive Enterprise Edition instance by referring to the information shown in the figure below.

 - **Instance Name**: enter a custom instance name. The name must be globally unique and cannot be identical with an existing instance name of your own or other users. This name is used to access the domain name of this TCR instance. **The name cannot be modified after creation.** We recommend that you use an abbreviation that combines the company name and instance region or project as the instance name.
 - **Instance Region**: select a region where you want to deploy the instance. **The region cannot be changed after the instance is created**. Select the region based on the location of the container cluster resources.
 - **Instance Specification**: select the instance specifications you wish to purchase. Different instance specifications have different instance performance and quotas. You can only purchase a **Standard** edition instance in the beta phase.
 - **Instance Domain Name**: the instance domain name that is automatically generated. Its prefix is the same as that of the instance name. **The instance domain name cannot be modified after the instance is created.** This domain name is used when you run the `docker login` command to log in to the instance.
3. After completing the configuration, click **OK** to start creating an Enterprise Edition instance.
You can check the instance creation progress on the "Instance List" page. This process takes about 1 minute.
4. When the instance status changes to **Running**, the instance was successfully created and is running properly. You can perform the following procedure to configure the access control policy of the instance and log in to the instance to push or pull images.


## Step 3: Configuring the Network Access Policy<span id="network"></span>
> To protect your data, all Internet and private network access is denied by default after the instance is created. Before you log in to the instance and push and pull images, configure the network access policy.
>
Click **Access Control** in the left sidebar of the console, select **Public network** or **Private network** as needed, and configure the network access policy by referring to the following procedure.

### Internet access
1. In the upper part of the "Public network" page, select the created instance.
2. Click **Open Internet Access Entry** in the upper right corner. The button status changes to **Opening**. See the figure below.
After Internet access is enabled, the Docker client can access the image repositories through the Internet.

3. When the button status changes from **Opening** to **Close Internet Access Entry**, Internet access has been successfully enabled. Then, click **Add a Public IP Whitelist** in the upper left of the list to add the public IP addresses that are allowed to access the image repositories.
4. In the "Create Public Network Access Whitelist" window, add the public IP addresses or IP ranges that are allowed to access the image repositories and add remarks for this rule (optional). See the figure below.
We do not recommend that you add `0.0.0.0/0` to allow all Internet access. Alternatively, delete this rule before formally activating the instance.


### Private network access
1. In the upper part of the "Private network" page, select the created instance.
2. Click **Create**. In the "Create Private Network Access Whitelist" window, configure the VPC and subnet information. See the figure below.
Select the VPC where your container cluster that needs to access the image repositories is located and select any subnet in this VPC that has usable VPC IP addresses.


## Step 4: Creating an Image Repository
1. Select **Namespace** in the left sidebar. On the "Namespace" page displayed, click "Create".
> Namespaces are used to manage image repositories in the instance. They do not directly store container images, but can map to teams, product projects, or other custom layers in an enterprise.
>
2. In the "Create a Namespace" window, configure the namespace information and click **OK**. See the figure below.

 - **Name**: we recommend that you set this parameter to the name of an enterprise team or product project. Namespace names must be unique in an instance.
 - **Access Level**: you can select either **Private** or **Public**. Image repositories and Helm chart repositories in the namespace will inherit this attribute. You can modify this attribute after creating the namespace.
3. Click **Image Repository** in the left sidebar to go to the "Image Repository" list page.
4. Click **Create**. In the "Create an Image Repository" window, configure the image repository information and click **OK**. See the figure below.
In the "Namespace" drop-down list, you can select a created namespace. "Name" can be a multi-level path, and "Detailed Description" supports the Markdown syntax.


## Step 5: Pushing and Pulling an Image
After completing the preceding steps, you have created an instance and image repository. Next, you can perform the following operations to push an image to or pull an image from the image repository.
> In this step, you need to use a CVM or CPM with Docker installed and ensure that the target client is in the Internet or private network access whitelist defined in [Configure the Network Access Policy](#network).  

### Logging in to the TCR instance
1. Select **Instance List** in the left sidebar and click the instance name to go to the instance management page.
2. Select the **Access Credential** tab to obtain the username of the instance from "Credential Information" and click **Re-generate Password** to re-generate a temporary password for login.
3. In the command line tool, run the following command to log in to the instance.
You can modify the access domain name based on the instance created in [Purchase an Enterprise Edition Instance](#domain).
```
docker login demo-tcr.tencentcloudcr.com
```
4. Enter the username and temporary password as prompted. The password is not displayed by default.
If `Login Succeeded` is displayed in the command line tool, you have logged in to the instance successfully.



### Pushing a container image
You can create a container image on the local server or obtain a public image from DockerHub for testing.
This document uses the official and latest Nginx image on Docker Hub as an example. In the command line tool, run the following commands sequentially to push this image. Note that you need to replace `demo-tcr`, `project-a`, and `nginx` with the actual instance, namespace, and image repository names you have created.
```
docker tag nginx:latest demo-tcr.tencentcloudcr.com/project-a/nginx:latest
```
```
docker push demo-tcr.tencentcloudcr.com/project-a/nginx:latest
```

### Pulling a container image
This document uses successfully pushed Nginx image as an example. In the command line tool, run the following command to pull this image:
```
docker pull demo-tcr.tencentcloudcr.com/project-a/nginx:latest
```

## What If a Problem Occurs?
If you encounter a problem while using TCR, locate and solve the problem by referring to FAQ. Alternatively, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category), and we will solve the problem for you as soon as possible.
