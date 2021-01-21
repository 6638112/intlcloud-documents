## Overview

This document describes how to create an asset package, which will be uploaded to and deployed in GSE for game hosting.

## Prerequisites

You have completed the [GSE Application Form](https://intl.cloud.tencent.com/apply/p/k0b6pvbhs6) and your application has been approved.

## Directions

1. Log in to the [GSE console](https://console.cloud.tencent.com/gse/asset) and click **Asset** on the left sidebar.
2. Select the service region in the top-left corner and click **Create**.
3. To create an asset package, you can upload one through the console page or CLI.

### Page upload
Enter the basic package information, the package name, the package version, and the OS, select the submission mode, upload the code, and click **OK**.
   - Asset Package Name: descriptive name of the asset package to be created, which does not need to be unique and can be modified and updated.
   - Asset Package Version: detailed information of asset package version, which is used to distinguish between different asset package versions.
   - OS: the operating system on which the game server asset package runs. It cannot be modified after the asset package is created. The default OS is CentOS 7.16.
   - Submission Mode: currently, only local zip packages can be uploaded.
   - Upload Codes: the asset package requires [integrating the gRPC framework](https://intl.cloud.tencent.com/document/product/1055/37418). The asset package directory must contain all the components necessary for running your game server, including executable files, dependency packages, and installation scripts of the game server. All are compressed into a zip package.
     - Server executable: a file required for running the game server. The asset package can contain multiple server executables, provided that they are built for the same platform.
     - Dependency: any file required for running the server executable.
     - Installation script: script used to execute the tasks for installing the asset package on the GSE-hosted server. This file must be placed in the root directory of the asset package and will run once during fleet creation.
![](https://main.qcloudimg.com/raw/776e5e422d9ce4afb68de44356e4a303.png)

### CLI upload

#### Step 1: download the script
Click [here](https://uploadasset-1301007756.cos.ap-guangzhou.myqcloud.com/uploadasset.zip?_ga=1.169449890.2037398510.1594263380) to download the `uploadasset.py` script.

#### Step 2: install the script dependency packages
Running the script requires the following two dependency packages.
-  **tencentcloud-sdk-python**
 - Installation command: `pip install tencentcloud-sdk-python`
 - Supported version: TencentCloud API SDK Python V2.7-V3.6. For more information, see [Python](https://intl.cloud.tencent.com/zh/document/product/494/7244).
- **cos-python-sdk-v5**
 - Installation command: `pip install -U cos-python-sdk-v5`
 - Supported version: for more information, see [Getting Started](https://intl.cloud.tencent.com/document/product/436/12269).

#### Step 3: run the script
**1. Modify the configuration**
Configure your authentication in the script. Replace `secret_id` and `secret_key` with your actual values.

**2. Run the command**
Run the following command to run the script:
```
python uploadasset.py  --local_path ./game_folder/
```
You will see `help` after running the command code. Click `help` to view more parameter information.
