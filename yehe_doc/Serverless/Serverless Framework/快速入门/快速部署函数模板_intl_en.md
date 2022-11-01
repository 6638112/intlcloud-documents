>! Due to the domain name's ICP filing update, you currently cannot log in by scanning the QR code during CLI deployment. You can log in by configuring a permanent key locally or visiting the URL as prompted on the command line. For more information, see [Account and Permission Configuration](https://intl.cloud.tencent.com/document/product/1040/36793).
## Overview
This document describes how to quickly create, configure, and deploy an SCF application in Tencent Cloud through Serverless Cloud Framework.

## Prerequisites
- [Serverless Cloud Framework 1.67.2 or above](https://intl.cloud.tencent.com/document/product/1040/37034) has been installed.
```
npm install -g serverless-cloud-framework
```
- You have [registered a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/10495).

>?If your account is a **Tencent Cloud sub-account**, please get the authorization from the root account first as instructed in [Account and Permission Configuration](https://intl.cloud.tencent.com/document/product/1040/36793).

## Directions
### Quick deployment

In an **empty folder** directory, run the following command:

```sh
serverless-cloud-framework
```

Next, follow the interactive prompts to initialize the project. Please select the `scf-starter` template for the application and select the runtime you want to use (Node.js is used as an example here):
```sh
serverless-cloud-framework: No serverless project is detected. Do you want to create one? Yes
serverless-cloud-framework: Please select the Serverless application you want to create: scf-starter - quickly deploys an SCF function

  react-starter - quickly deploys a React.js application 
  restful-api - quickly deploys a RESTful API to use Python + API Gateway 
❯ scf-starter - quickly deploys an SCF function 
  vue-starter - quickly deploys a basic Vue.js application 
  website-starter - quickly deploys a static website 
  eggjs-starter - quickly deploys a basic Egg.js application 
  express-starter - quickly deploys a basic Express.js application 
  
serverless-cloud-framework: Please select the runtime of the application: scf-nodejs - quickly deploys an SCF function in Node.js

  scf-golang - quickly deploys an SCF function in Go 
❯ scf-nodejs - quickly deploys an SCF function in Node.js 
  scf-php - quickly deploys an SCF function in PHP 
  scf-python - quickly deploys an SCF function in Python  
  
serverless-cloud-framework: Please enter the project name: demo
serverless-cloud-framework: Installing the scf-nodejs application...

scf-nodejs › Created


The demo project has been successfully created!
```

Select **Deploy Now** to quickly deploy the initialized project to the SCF console:

```sh
serverless-cloud-framework: Do you want to deploy the project in the cloud now? Yes

xxxxxxxx
x  QR  x
x CODE x
xxxxxxxx
Please scan the QR code above with WeChat or click the link below to log in
https://scflogin.qcloud.com/XKYUcbaK
Logged in successfully!

serverless-cloud-framework
Action: "deploy" - Stage: "dev" - App: "scfApp" - Instance: "scfdemo"

functionName: helloworld
description:  helloworld blank template function
namespace:    default
runtime:      Nodejs10.15
handler:      index.main_handler
memorySize:   128
lastVersion:  $LATEST
traffic:      1
triggers: 
  apigw: 
    - http://service-xxxxxxx.gz.apigw.tencentcs.com/release/

27s › scfdemo › Success
```

After deployment, complete the remote invocation of the function by running the following command:
```sh
scf invoke --inputs function=helloworld
```
>?`scf` is short for the `serverless-cloud-framework` command.

### Viewing deployment information

If you want to check the deployment status and resources of the application again, you can go to the folder where the project is successfully deployed and run the following command to view the corresponding information:

```
cd demo # Enter the project directory. Please change to your actual project's directory name here
scf info
```

### Viewing directory structure
In the directory of the initialized project, you can see the most basic structure of a serverless function project:

```
.
├── serverless.yml  # Configuration file
├—— index.js    # Entry function
└── .env # Environment variable file
```

- The `serverless.yml` configuration file implements the quick configuration of the basic function information. All the configuration items supported by the SCF console can be configured in the `.yml` file (for more information, please see [SCF Configuration Information](https://github.com/serverless-components/tencent-scf/blob/master/docs/configure.md)).
- `index.js` is the entry function of the project, which is the `helloworld` template here.
- The `.env` file stores user login authentication information. You can also configure other environment variables in it.

### Redeployment
In the local project directory, you can modify the function template and configuration file and then redeploy the project by running the following command:
```
scf deploy
```
>?If you want to view the details during the removal process, you can add the `--debug` parameter.

### Continuous development
After the deployment is completed, Serverless Cloud Framework supports running different commands to help you implement continuous development, deployment, and grayscale release for the project. You can also use this component in conjunction with other components to manage the deployment of multi-component applications.

For more information, please see [Application Management](https://intl.cloud.tencent.com/document/product/1040/38288) and [List of Supported Commands](https://intl.cloud.tencent.com/document/product/1040/36861).

## FAQs

#### the wizard does not pop up by default when `serverless-cloud-framework` is entered.
  Solution: add the `SERVERLESS_PLATFORM_VENDOR=tencent` configuration item to the `.env` file.
	
#### after `scf deploy` is entered in a network environment outside the Chinese mainland, the deployment is very slow.
  Solution: add the `GLOBAL_ACCELERATOR_NA=true` configuration item to the `.env` file to enable acceleration outside the Chinese mainland. 
	
#### after `sls deploy` is entered, the deployment reports a network error.
  Solution: add the following proxy configuration to the `.env` file.
  ```
  HTTP_PROXY=http://127.0.0.1:12345 # Replace "12345" with your proxy port
  HTTPS_PROXY=http://127.0.0.1:12345 # Replace "12345" with your proxy port
  ```

  

