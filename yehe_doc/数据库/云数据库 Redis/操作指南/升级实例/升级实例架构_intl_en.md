
TencentDB for Redis supports standard architecture and cluster architecture. To help you process ever-growing business data, it allows you to upgrade from standard architecture to cluster architecture if the performance and capacity of standard architecture are insufficient.

## Upgrade Description
- For Redis 4.0 or later, a standard architecture instance can be upgraded to a cluster architecture instance on the same version; for example, you can upgrade from Redis 4.0 Standard Architecture to Redis 4.0 Cluster Architecture.
- Cross-version architecture upgrade is not supported; for example, you cannot upgrade from Redis 4.0 Standard Architecture to Redis 5.0 Cluster Architecture.
- The architecture of Redis 2.8 cannot be upgraded.
- Cluster architecture cannot be downgraded to standard architecture.
- Cross-AZ architecture upgrade is not supported.
- Cluster architecture upgrade is not supported for pay-as-you-go instances.
- After standard architecture is upgraded to cluster architecture, fees will be charged based on cluster architecture and thus get increased. For more information, see [Pricing](https://intl.cloud.tencent.com/document/product/239/9894).

## How Upgrade Works
- Redis standard architecture can be directly upgraded to cluster architecture (single shard) within three minutes with no data migration required.
- In Redis 4.0 or later, if standard architecture is upgraded to cluster architecture, only the runtime mode of the instance will change from having no slot limit to having a slot limit, but data migration will not be involved.

## Upgrade Preparations (Compatibility Check)
To avoid business failures caused by compatibility problems during migration to cluster architecture, check the compatibility before the upgrade:
- Cluster architecture stores data in a distributed manner, and its biggest difference from standard architecture lies in whether a single command supports multikey access. For the cluster architecture, commands can be categorized into supported, partially supported, and unsupported. For the complete list of compatible commands, see [Command Compatibility](https://intl.cloud.tencent.com/document/product/239/31958).
- For more information about compatibility check, see [Check on Migration from Standard Architecture to Cluster Architecture](https://intl.cloud.tencent.com/document/product/239/37594).

## Affect of Upgrading to New CLB
- Generally, upgrade can be completed in three minutes.
- During the upgrade, existing connections will be closed momentarily; therefore, your business should have a reconnection mechanism.

## Upgrade Directions
1. Log in to the [TencentDB for Redis Console](https://console.cloud.tencent.com/redis), select a region in the instance list, and click an instance ID to enter the instance details page.
2. On the instance details page, click **Upgrade Architecture**.
![](https://main.qcloudimg.com/raw/ebc4ecc50af95d99be2fa23f45d11278.png)
3. In the pop-up dialog box, select the architecture and switch time, indicate your consent to the notice about compatibility risks, and click **OK**.
Architecture upgrade supports **Switch Now** and **Switch in Maintenance Time** options. You can modify the maintenance time in **Maintenance Time** on the instance details page.
![](https://main.qcloudimg.com/raw/f584ccc7b3004feb662e72e8ddcf819a.png)
4. After the payment is completed, you will be redirected to the instance list. After the status of the instance becomes **Running**, it can be used normally.
