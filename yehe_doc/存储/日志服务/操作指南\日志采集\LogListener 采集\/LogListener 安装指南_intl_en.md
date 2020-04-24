LogListener is a log collector provided by Tencent Cloud Log Service (CLS). You can install and deploy it on a server to collect logs quickly.

## Installation Environment

LogListener supports only Linux 64-bit operating systems but not Windows for the moment. It is compatible with mainstream Linux distributions. If it is incompatible with the Linux distribution you use, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

| OS | Compatible Versions |
| ---------------- | ------------------------------------------------------------ |
| CentOS (64-bit) | CentOS_6.8_64-bit, CentOS_6.9_64-bit, CentOS_7.2_64-bit, CentOS_7.3_64-bit, CentOS_7.4_64-bit, CentOS_7.5_64-bit, CentOS_7.6_64-bit |
| Ubuntu (64-bit) | Ubuntu Server_14.04.1_LTS_64-bit, Ubuntu Server_16.04.1_LTS_64-bit, Ubuntu Server_18.04.1_LTS_64-bit |
| Debian (64-bit) | Debian_8.2_64-bit, Debian_9.0_64-bit |
| openSUSE (64-bit) | openSUSE_42.3_64-bit |





## Installation and Startup

### 1. Download and install LogListener

Download the latest version of LogListener [here](https://loglistener-1254077820.cos.ap-shanghai.myqcloud.com/loglistener-linux-x64-2.2.8.tar.gz).

Download the LogListener installation package and decompress it to the installation path (`/usr/local/` in this example). Then, go to the LogListener directory `loglistener/tools` and run the following installation command:

```shell
wget https://loglistener-1254077820.cos.ap-shanghai.myqcloud.com/loglistener-linux-x64-2.2.8.tar.gz && tar -zxvf loglistener-linux-x64-2.2.8.tar.gz -C /usr/local && cd /usr/local/loglistener-2.2.8/tools && ./loglistener.sh install
```

### 2. Initialize LogListener

In the `loglistener/tools` path, run the following command to initialize LogListener as the root user (by default, the private network is used to access the service):

```shell
./loglistener.sh init -secretid AKIDPEtPyKabfW8Z3Uspdz83xxxxxxxxxxx -secretkey whHwQfjdLnzzCE1jIf09xxxxxxxxxxxx -region ap-shanghai
```

A private domain name is used by default:


![](https://main.qcloudimg.com/raw/ea417c6d60ab21e52984d04c1364b30d.png)

If you need to access the service at a public domain name, run the following command to set the network parameter `internet` explicitly:

```shell
./loglistener.sh init -secretid AKIDPEtPyKabfW8Z3Uspdz83xxxxxxxxxxxx -secretkey whHwQfjdLnzzCE1jIf0xxxxxxxxxxxx -region ap-shanghai -network internet
```

![](https://main.qcloudimg.com/raw/653ebe0400dca5b21b3e25d01f93cb5b.png)

#### Parameter description

| Parameter Name | Description |
| --------- | ------------------------------------------------------------ |
| secretid  | Part of a [TencentCloud API key](https://console.cloud.tencent.com/cam/capi), which is used to identify the API requester. |
| secretkey | Part of a [TencentCloud API key](https://console.cloud.tencent.com/cam/capi), which is used to encrypt the strings to create a signature so that Tencent Cloud server can validate the identity of the requester. |
| region    | [Region](https://intl.cloud.tencent.com/document/product/614/18940) where CLS resides. |
| network   | Type of the network through which LogListener accesses the service domain name. Valid values : intra (private network), internet (public network). Default value: intra.|

>
> - You are recommended to use a collaborator key, and the root account should grant the read/write permission of CLS to the collaborator.
> - `region` indicates the region of your CLS service instead of the region where your business server resides.
> - If your CVM instance and logset are in the same region, you are recommended to access the service domain name over the private network.

### 3. Start LogListener

After LogListener is successfully installed, run the following command to start it:

```shell
/etc/init.d/loglistenerd start
```


![](https://main.qcloudimg.com/raw/184d6cc3308206b14288372da59a99a0.png)

## Using LogListener

> The operation command description in this document is only applicable to LogListener 2.2.4 and above.

#### Viewing LogListener version

```shell
/etc/init.d/loglistenerd -v
```

#### Starting LogListener

```shell
/etc/init.d/loglistenerd start
```

#### Restarting LogListener

```shell
/etc/init.d/loglistenerd restart
```

#### Stopping LogListener

```shell
/etc/init.d/loglistenerd stop
```

#### Initializing LogListener

Run the initialization command in the `loglistener/tools` directory as an administrator:

```shell
./loglistener.sh init -secretid AKIDPEtPyKabfW8Z3Uspdz83xxxxxxxxxxxx -secretkey whHwQfjdLnzzCE1jIf09xxxxxxxxxxxx -region ap-beijing
```

#### Uninstalling LogListener

Run the uninstallation command in the `loglistener/tools` directory as an administrator:

```shell
./loglistener.sh uninstall
```

#### Viewing LogListener process status

```shell
/etc/init.d/loglistenerd status 
```

LogListener normally runs three processes:

![](https://main.qcloudimg.com/raw/6300054d2089484f2af5399082f9b880.png)


#### Checking LogListener heartbeat and configuration

```shell
/etc/init.d/loglistenerd check
```


![](https://main.qcloudimg.com/raw/82430a9cb1aa364d2abfbc47ebae5ef5.png)


## Manually Updating LogListener

- Breakpoint file reused (logs will not be repeatedly collected)
  1. Run the stop command to stop the old version of LogListener.
  2. Back up the breakpoint file directory (loglistener/data) on the old version; for example, back up the legacy breakpoint file to the `/tmp/loglistener-backup` directory.
 ```shell
 cp -r loglistener-2.2.3/data /tmp/loglistener-backup/
 ```
 3. Run the uninstallation command to uninstall the earlier version of LogListener.
 4. Download the latest version of LogListener and install and initialize it with relevant commands.
 5. Copy the breakpoint file directory backed up in step 2 to the new LogListener directory; for example:
 ```shell
 cp -r /tmp/loglistener-backup/data loglistener-2.2.8/
 ```
 6. Run the start command to start the new version of LogListener.
- Breakpoint file not reused (logs may be repeatedly collected)
  1. Run the stop command to stop the old version of LogListener.
  2. Run the uninstallation command to uninstall the earlier version of LogListener.
  3. Download the latest version of LogListener and install and initialize it with relevant commands.
  4. Run the start command to start the new version of LogListener.
