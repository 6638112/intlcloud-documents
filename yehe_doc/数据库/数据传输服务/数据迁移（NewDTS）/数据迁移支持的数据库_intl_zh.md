
腾讯云 DTS 支持自建数据库、腾讯云数据库和第三方云厂商数据库的迁移，具体的网络接入方式如下。
- 公网：源数据库可以通过公网 IP 访问。

- 云主机自建：源数据库部署在 [腾讯云服务器 CVM](https://intl.cloud.tencent.com/document/product/213) 上。

- 专线接入：源数据库可以通过 [专线接入](https://intl.cloud.tencent.com/document/product/216) 方式与腾讯云私有网络打通。 

- VPN 接入：源数据库可以通过 [VPN 连接](https://intl.cloud.tencent.com/document/product/1037) 方式与腾讯云私有网络打通。 

- 云数据库：源数据库属于腾讯云数据库实例。

- 云联网：源数据库可以通过 [云联网](https://intl.cloud.tencent.com/document/product/1003) 与腾讯云私有网络打通。

对于第三方云厂商数据库，一般可以选择公网方式，也可以选择 VPN 接入，专线或者云联网的方式，需要根据实际的网络情况选择。

支持迁移的数据库详情如下表所示。

| **数据流向**   | **迁移方向** | **源数据库类型及版本**   | **目标数据库类型及版本** |   **迁移类型** | **跨版本迁移** |
| ------------- | -----------  | -------------------- | ---------------------- | -------------- | -------------- |
| [MySQL > MySQL](https://intl.cloud.tencent.com/document/product/571/42645) | 入云         | <li>自建 MySQL 5.5、5.6、5.7、8.0<li>云数据库 MySQL 5.5、5.6、5.7、8.0<li>第三方云厂商（阿里云、AWS）MySQL 5.6、5.7、8.0 | 云数据库 MySQL 5.5、5.6、5.7、8.0 | <li>结构迁移<li>全量迁移<li>全量 + 增量迁移 | 支持 |
| [MariaDB > MySQL](https://intl.cloud.tencent.com/document/product/571/42644) | 入云 | <li>自建 MariaDB 5.5、10.0、10.1、10.2、10.3、10.4、10.5、10.6<li>云数据库 MariaDB 5.5、10.0、10.1、10.2、10.3、10.4、10.5、10.6 | 云数据库 MySQL 5.5、5.6、5.7、8.0 | <li>结构迁移<li>全量迁移<li>全量 + 增量迁移 | 支持 |
| [MariaDB（Percona）> MySQL](https://intl.cloud.tencent.com/document/product/571/42644) | 入云 | <li>自建 Percona 5.5、5.6、5.7、8.0<li>云数据库 MariaDB（Percona） 5.5、5.6、5.7、8.0 | 云数据库 MySQL 5.5、5.6、5.7、8.0 | <li>结构迁移<li>全量迁移<li>全量 + 增量迁移 | 支持 |
| [MySQL > TDSQL-C](https://intl.cloud.tencent.com/document/product/571/42643) | 入云 | <li>自建 MySQL 5.5、5.6、5.7<li>第三方云厂商（阿里云、AWS）MySQL 5.6、5.7 | 云原生数据库 TDSQL-C 5.6、5.7 | <li>结构迁移<li>全量迁移<li>全量 + 增量迁移 | - |
| [MySQL > TDSQL MySQL版](https://intl.cloud.tencent.com/document/product/571/42642) | 入云 | <li>自建 MySQL 5.6、5.7<li>云数据库 MySQL 5.6、5.7 | TDSQL MySQL版 5.7 | <li>结构迁移<li>全量迁移<li>全量 + 增量迁移 | - |
| [MySQL > MariaDB（Percona）](https://intl.cloud.tencent.com/document/product/571/42641) | 入云 | <li>自建 MySQL 5.6、5.7<li>云数据库 MySQL 5.6、5.7 | 云数据库 MariaDB（Percona） 5.7 | <li>结构迁移<li>全量迁移<li>全量 + 增量迁移 | - |
| [MariaDB > MariaDB](https://intl.cloud.tencent.com/document/product/571/42641) | 入云 | <li>自建 MariaDB 10.0.1、10.1.9<li>云数据库 MariaDB 10.1.9 | 云数据库 MariaDB 10.1.9 | <li>结构迁移<li>全量迁移<li>全量 + 增量迁移 | - |
| [MariaDB（Percona）> MariaDB（Percona）](https://intl.cloud.tencent.com/document/product/571/42641) | 入云 | <li>自建 MariaDB（Percona） 5.7<li>云数据库 MariaDB（Percona） 5.7 | 云数据库  MariaDB（Percona）5.7 | <li>结构迁移<li>全量迁移<li>全量 + 增量迁移 | - |
| [PostgreSQL > PostgreSQL](https://intl.cloud.tencent.com/document/product/571/42640) | 入云 | <li>自建 PostgreSQL 9.3、9.5、9.6、10、11、12<li>云数据库 PostgreSQL 9.3、9.5、9.6、10、11、12<li>第三方云厂商（All）PostgreSQL 9.3、9.5、9.6、10、11、12 | 云数据库 PostgreSQL 9.3、9.5、9.6、10、11、12 | <li>全量迁移<li>结构迁移 | 支持，同时支持13降版本迁移至12 |
| [PostgreSQL > PostgreSQL](https://intl.cloud.tencent.com/document/product/571/42640) | 入云 | PostgreSQL 10、11、12 | 云数据库 PostgreSQL 10，11，12 | 全量 + 增量迁移 | 不支持 |
| [MongoDB > MongoDB](https://intl.cloud.tencent.com/document/product/571/42639) | 入云    | <li>自建 MongoDB 3.0、3.2、3.4、3.6、4.0、4.2<li>云数据库 MongoDB 3.0、3.2、3.4、3.6、4.0、4.2<li>第三方云厂商（阿里云）MongoDB 3.0、3.2、3.4、3.6、4.0、4.2 | 云数据库 MongoDB 3.0、3.2、3.4、3.6、4.0、4.2 | <li>结构迁移<li>全量迁移<li>全量 + 增量迁移 | 支持 |
| [SQL Server > SQL Server](https://intl.cloud.tencent.com/document/product/571/42638) | 入云 | <li>自建 SQL Server 2008R2、2012、2014、2016、2017、2019<li>云数据库 SQL Server 2008R2、2012、2014、2016、2017、2019<li>第三方云厂商（阿里云、AWS）SQL Server 2008R2、2012、2014、2016、2017、2019 | 云数据库 SQL Server 2008R2、2012、2014、2016、2017、2019 | <li>全量迁移<li>全量 + 增量迁移 | 支持 |

> ?
> - 入云指目标数据库为腾讯云数据库产品的场景。
>- MySQL/TDSQL MySQL/MariaDB：目标数据库版本必须大于或等于源数据库版本， 版本以大版本号区分，如5.6.x支持迁移到5.6.x、5.7.x及以后版本。
> - PostgreSQL：仅全量迁移时，目标数据库实例版本必须大于源库实例版本；增量迁移时，支持10.x以上的版本互相迁移。 
>- MongoDB：不同版本均可互相迁移。
>- SQL Server：仅支持基础版迁移到高可用版本（包括双机高可用和集群版），且目标数据库的版本号需要大于源数据库的版本号。 
