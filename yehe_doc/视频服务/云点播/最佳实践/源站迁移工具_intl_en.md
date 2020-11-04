## Overview

VOD Migrate Tool is an all-in-one tool that integrates data migration features. By writing a simple configuration file, you can quickly migrate media files at the source address to VOD.

## Supported Data Sources
* [x] Local folder
* [x] URL list
* [x] Tencent Cloud COS
* [x] AWS S3
* [x] Alibaba Cloud OSS
* [x] Qiniu Kodo

## Prerequisites

#### OS

Windows, Linux, and macOS.

#### Software dependency

- Python 2.7/3.4+.
- Latest version of pip.
  
## Installation

### Installing through pip (recommended)
You can install the SDK into your project through pip. If you haven't installed pip in your project environment yet, install it first as instructed at pip's official website.

```
pip install vodmigrate
```


### Installing through source package
Click [here](https://github.com/tencentyun/vod-migrate.git) to download the source code.
Download the latest code and decompress:

```shell
git clone https://github.com/tencentyun/vod-migrate.git
cd vod-migrate
python setup.py install
```

## Use Cases
Run the following command:
```
vodmigrate config.toml
```
> ?After the migration is completed, the result will be output to the directory corresponding to the configuration item `migrateResultOutputPath`, and the filename will be `vod_migrate_result.txt`.

## Configuration File Description
The configuration file is in TOML format (for more information, please see [config_template.toml](https://github.com/tencentyun/vod-migrate/blob/master/test/config_template.toml). Make sure that the file is encoded in UTF-8). The file content can be divided into the following parts:

### 1. Configure the migration type

`type` indicates the migration type, which should be filled in based on your migration needs. For example, to migrate local data to VOD, you need to configure `type=migrateLocal` for `[migrateType]`.
```
[migrateType]
type="migrateLocal"
```
Currently, the following migration types are supported:

| migrateType | Description |
| :----------- | :----------------------: |
| migrateLocal | From local system to VOD |
| migrateUrl | From download URL to VOD |
| migrateCos | From Tencent Cloud COS to VOD |
| migrateAws | From AWS S3 to VOD |
| migrateAli | From Alibaba Cloud OSS to VOD |
| migrateQiniu | From Qiniu Kodo to VOD |

### 2. Configure the migration task

You can configure a migration task based on your actual needs, including information configuration for VOD and task configuration.

``` 
# Common configuration for the migration tool
[common]
secretId = "SECRETID"
secretKey = "SECRETKEY"
region = 'REGION'
subAppId = 0
concurrency = 5
supportMediaClassification = [ 'video', 'audio', 'image' ]
excludeMediaType = [  ]
migrateDbStoragePath = ''
migrateResultOutputPath = ''
```
| Name | Description |
| :------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
| secretId | `SecretId` of your key. Replace `SECRETID` with your real key information, which can be obtained on the TencentCloud API key page in the [CAM Console](https://console.cloud.tencent.com/cam/capi) |
| secretKey | `SecretKey` of your key. Replace `SECRETKEY` with your real key information, which can be obtained on the TencentCloud API key page in the [CAM Console](https://console.cloud.tencent.com/cam/capi) |
| region | Access point region, i.e., the region where to request a VOD server. This is different from the storage region. For more information, please see [the list of supported regions](https://intl.cloud.tencent.com/document/product/266/34113) |
| subAppId                   |                VOD [Subapplication](https://intl.cloud.tencent.com/document/product/266/33987) ID. If you need to migrate files in a subapplication, enter the subapplication ID in this field; otherwise, leave it empty.             |
| concurrency | Number of concurrently migrated files. Maximum value: 50 |
| supportMediaClassification | List of media types supported for migration. Valid values: video, audio, image |
| excludeMediaType | List of file types to be excluded |
| migrateDbStoragePath | Save path of the migrated `db`. If this parameter is empty, it means the current directory |
| migrateResultOutputPath | Save path of the migration result (one migration record corresponds to one line of JSON string). If this parameter is empty, it means the current directory |

File type description:
- Video: MP4, TS, FLV, WMV, ASF, RM, RMVB, MPG, MPEG, 3GP, MOV, WEBM, MKV, AVI. **HLS and DASH are not supported**
- Audio: MP3, M4A, FLAC, OGG, WAV
- Image: JPG, JPEG, PNG, GIF, BMP, TIFF, AI, CDR, EPS

### 3. Configure the data source
Configure the applicable section according to the migration type described in `[migrateType]`. For example, if the configuration item of `[migrateType]` is `type=migrateLocal`, you only need to configure the `[migrateLocal]` section.

#### 3.1. Configure a local data source (migrateLocal)

If you migrate data from a local system to VOD, configure this section. The specific configuration items and descriptions are as follows:

``` 
# Configuration section for migration from a local system to VOD
[migrateLocal]
localPath = ''
excludes = [ ]
```
| Configuration Item | Description |
| :-------- | :-------------------------------------------------------------------: |
| localPath | Local path, which should be an absolute path |
| excludes | Absolute path of the directory to be excluded, which means that some files in the directory at `localPath` are not to be migrated |

#### 3.2. Configure a URL list data source (migrateUrl)
If you migrate data from a specified URL list to VOD, configure this section. The specific configuration items and descriptions are as follows:
```
# Configuration section for migration from a URL list download to VOD
[migrateUrl]
urllistPath = 'D:\folder\urllist.txt'
```
| Configuration Item | Description |
| :---------- | :------------------------------------------------------------------------: |
| urllistPath | Absolute path of the file storing the URL list. The file content is URL text containing one original URL address per line |

#### 3.3. Configure a COS data source (migrateCos)

If you migrate data from Tencent Cloud COS to VOD, configure this section. The specific configuration items and descriptions are as follows:
``` 
# Configuration section for migration from Tencent Cloud COS to VOD
[migrateCos]
region = 'ap-shanghai'
bucket = 'examplebucket-1250000000'
secretId = 'COS_SECRETID'
secretKey = 'COS_SECRETKEY'
prefix = ''
```

| Configuration Item | Description |
| :-------- | :---------------------------------------------------------------------------------------------------------: |
| region | Bucket region. For more information, please see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) |
| bucket | Bucket name in the format of `<BucketName-APPID>`. The bucket name must include the `APPID`, such as `examplebucket-1250000000` |
| secretId | `secretId` of the key of the account owning the bucket, which can be viewed in [TencentCloud API Key](https://console.cloud.tencent.com/cam/capi) |
| secretKey | `secretKey` of the key of the account owning the bucket, which can be viewed in [TencentCloud API Key](https://console.cloud.tencent.com/cam/capi) |
| prefix | Prefix of the path to be migrated. If all data in the bucket needs to be migrated, leave the prefix empty |

#### 3.4. Configure an AWS S3 data source (migrateAws)
If you migrate data from AWS S3 to VOD, configure this section. The specific configuration items and descriptions are as follows:
```
# Configuration section for migration from AWS S3 to VOD
[migrateAws]
region = 'ap-northeast-2'
bucket = 'bucket-aws'
accessKeyId = 'AccessKeyId'
accessKeySecret = 'AccessKeySecret'
prefix = ''
```
| Configuration Item | Description |
| :-------------- | :----------------------------------------------------------------: |
| region | AWS S3 region |
| bucket | AWS S3 bucket name |
| accessKeyId | Replace `AccessKeyId` with your real key information |
| accessKeySecret | Replace `AccessKeySecret` with your real key information |
| prefix | Prefix of the path to be migrated. If all data in the bucket needs to be migrated, leave the prefix empty |

#### 3.5. Configure an Alibaba Cloud OSS data source (migrateAli)
If you migrate data from Alibaba Cloud OSS to VOD, configure this section. The specific configuration items and descriptions are as follows:

```
# Configuration section for migration from Alibaba Cloud OSS to VOD
[migrateAli]
bucket = 'bucket-aliyun'
accessKeyId = 'yourAccessKeyId'
accessKeySecret = 'yourAccessKeySecret'
endPoint = 'oss-cn-hangzhou.aliyuncs.com'
prefix = ''
```

| Configuration Item | Description |
| :-------------- | :----------------------------------------------------------------: |
| bucket | Alibaba Cloud OSS bucket name |
| accessKeyId | Replace `yourAccessKeyId` with your real key information |
| accessKeySecret | Replace `yourAccessKeySecret` with your real key information |
| endPoint | Alibaba Cloud endpoint address |
| prefix | Prefix of the path to be migrated. If all data in the bucket needs to be migrated, leave the prefix empty |

#### 3.6. Configure a Qiniu Kodo data source (migrateQiniu)
If you migrate data from Qiniu Kodo to VOD, configure this section. The specific configuration items and descriptions are as follows:
```
# Configuration section for migration from Qiniu Kodo to VOD
[migrateQiniu]
bucket = 'bucket-qiniu'
accessKeyId = 'AccessKey'
accessKeySecret = 'SecretKey'
endPoint = 'www.bkt.clouddn.com'
prefix = ''
```
| Configuration Item | Description |
| :-------------- | :----------------------------------------------------------------: |
| bucket | Qiniu Kodo bucket name |
| accessKeyId | Replace `AccessKey` with your real key information |
| accessKeySecret | Replace `SecretKey` with your real key information |
| endPoint | Download address of Qiniu Kodo, which corresponds to `downloadDomain` |
| prefix | Prefix of the path to be migrated. If all data in the bucket needs to be migrated, leave the prefix empty |

## Use Limits
- The tool is designed as a one-time migration tool. The migration is divided into three stages: **origin server file scanning**, **migrating**, and **migration completed**. After the file scan is completed, if the configuration needs to be changed, the `db` file must be cleared (i.e., deleting `migrate.db` or modifying the `db` storage path) to avoid errors with configuration file MD5 verification.
- The migrated files must be displayed with the file extension.
- HLS/DASH files cannot be migrated currently.
- After the migration, the directory relationship between the original videos cannot be maintained, and each video has an independent `FileId`, all of which are not related to each other.

## Migration Process Overview
1. The configuration file is read, the corresponding configuration section is read according to the migration type, and parameters are checked.
2. The origin server is scanned according to the migration type, and migration tasks are generated.
3. After the scan is completed, the migration is performed, and the results of each task and the overall progress are printed.
4. After the migration is completed, the details are output to the result file.
![](https://main.qcloudimg.com/raw/132acd323d0aa947f319f113182b83c1.png)
