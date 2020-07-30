���ĵ�Ϊ Tcaplus RESTful API v1.0 �û��ֲ�

## ����
Tcaplus RESTful API Ϊ�������ṩ��һ��ͨ�� HTTP ������ Tcaplus ���ݿ�Զ�̽����ķ�ʽ������ͨ�� RESTful API �� Json Я�����ݷ��� HTTP ����������յ���Ӧ�� Json ��ʽ����Ӧ���������߿���ͨ���κ����Ի򹤾߷��� RESTful API ��������ݽ�������ɾ���ġ��������

## ׼������

ȷ�����Ѿ��� [��Ѷ��TcaplusDB](https://console.cloud.tencent.com/tcaplusdb/app) �����˼�Ⱥ�������Ѿ���ȡ��Ӧ�ļ�Ⱥ��Ϣ������AppId(��Ⱥ����ID)��ZoneId(�����ID)��AppKey����Ⱥ�������룩������ǰ Tcaplus RESTful API ֻ֧��ͨ�� protobuf ����ı�

## ��ǰ�汾

��ǰ������ Tcaplus RESTful API ������Ĭ�϶�ʹ�� ver1.0 �汾��

## ����

���е� API ����������ͨ�� HTTP�����е����ݶ�ͨ�� JSON ��ʽ���ݡ������ǵ��͵�������� URI ��ʽ��

```
http://{Tcaplus_REST_URL}/{Version}/apps/{AppId}/zones/{ZoneId}/tables/{TableName}/records
```
* Tcaplus_REST_URL��Tcaplus RESTful URL �����
* Version��Tcaplus RESTful API �汾�ţ�Ĭ��"ver1.0"
* AppId����Ⱥ��**����ID**
* ZoneId�������**ID**
* TableName������

ʾ����
```
http://10.123.9.70/ver1.0/apps/2/zones/1/tables/tb_rest_test/records
```

### HTTP ͷ

ͨ������ HTTP ͷ���������û� HTTP �ͻ���ͨ������ͻذ�����һЩ�������Ϣ��

#### ��Ȩ

`x-tcaplus-pwd-md5`
���ֶ���д�û� app key �� MD5 ���������ڿͻ���Ȩ����֤��
��ͨ������ bash ��������ַ����� MD5 ֵ��
```
# echo -n "c3eda5f013f92c81dda7afcdc273cf82" | md5sum
879423b88d153cace7b31773a7f46039  -
```

#### ����У�� 

- `x-tcaplus-target`ָ�� Tcaplus RESTful API �������������������²������ͣ�
 * Tcaplus.GetRecord ��ȡ��¼
 * Tcaplus.AddRecord �����¼
 * Tcaplus.SetRecord ���ü�¼
 * Tcaplus.DeleteRecord ɾ����¼
 * Tcaplus.FieldGetRecord �����ֶζ�
 * Tcaplus.FieldSetRecord �����ֶ�����
 * Tcaplus.FieldIncRecord �����ֶ�����
 * Tcaplus.PartkeyGetRecord ����������
- `x-tcaplus-idl-type` ָ�� Tcaplus �����ͣ�Ŀǰֻ֧�� protobuf��pb�����͡�


####  ���ñ�� 

- `x-tcaplus-data-version-check` Specifies Tcaplus data version check policy use with `x-tcaplus-data-version`. It can be set as:
ָ�� Tcaplus ���ݰ汾��У����ԣ�ʵ���ֹ������ܣ���`x-tcaplus-data-version`������ʹ�ã���ѡֵ���£�

 * `1`��������Ϊ1���ͻ��˵����ݰ汾�ű�����洢�����ݰ汾��һ�²���д�����������������ݰ汾��+1��
 * `2`��������Ϊ2���Ͳ����ͻ��˰汾�������˰汾��֮��Ĺ�ϵ��ǿ�ƽ��ͻ��˴���İ汾�����õ��洢�㡣
 * `3`��������Ϊ3���Ͳ����ͻ��˰汾�������˰汾��֮��Ĺ�ϵ��д�����Ὣ�洢�����ݰ汾��+1��

 �˱�ǽ��� Tcaplus.AddRecord �� Tcaplus.SetRecord �����塣

- `x-tcaplus-data-version` �� `x-tcaplus-data-version-check` �������ϣ����ÿͻ��˵����ݰ汾�š���ѡֵ���£�
 * version <= 0 ���԰汾�����ԡ�
 * version > 0 ָ���ͻ������ݼ�¼�汾�š�
- `x-tcaplus-result-flag` ����Ӧ�����Ƿ�����������ݵĲ��ԣ����ܵ�ȡֵ�У�
 * `0` ����Ϊ0��Ӧ���н���������ɹ���ʧ�ܡ�
 * `1` ����Ϊ1��Ӧ���а���������һ�µ�ֵ��
 * `2` ����Ϊ2��Ӧ���а������޸ĵ����ݵ������ֶ�����ֵ��
 * `3` ����Ϊ3��Ӧ���а�����¼���޸�ǰ��ֵ��


### ���� JSON ���� 

```
Request Data:
{
 "ReturnValues": "...", // �û����õı������ݣ������󵽴�tcaplus����Ӧ��ԭ������
 "Record": {
     ... // ���ݼ�¼����ϸ��ʽ��μ���API����ʾ����һ��
 }
}
```

## Ӧ��

### Ӧ���е� JSON ����

GetRecord��SetRecord��AddRecord��DeleteRecord��FieldGetRecord��FieldSetRecord �� FieldIncRecord �����Ľ�����᷵�ص������ݣ�Ӧ�� JSON ���ݸ�ʽ���£�

```
Response Data
{
 "ErrorCode": 0, // ������
 "ErrorMsg": "Succeed", // ������Ϣ
 "RecordVersion": 1, // ���ݰ汾��
 "ReturnValues": "...", // �û����õı������ݣ������󵽴�tcaplus����Ӧ��ԭ������
 "Record": { // ���ݼ�¼����ϸ��ʽ��μ���API����ʾ����һ��
     ...
 }
}
```

PartkeyGetRecord �����Ľ���п��ܴ��ض������ݣ�Ӧ��� JSON ���ݸ�ʽ���£�

```
Response Data
{
 "ErrorCode": 0, // ������
 "ErrorMsg": "Succeed", // ������Ϣ
 "MultiRecords": [ //�������ݹ��ɵ�����
  {"RecordVersion": 1,  //ÿ�����ݵİ汾��
   "Record": {...}  // ���ݼ�¼����ϸ��ʽ��μ���API����ʾ����һ��
  },
  ...
  ],
 "RemainNum": 0, //��δ���ʵ�����������
 "TotalNum": 5   //��������������������
}
```

###  ������ 

|HTTP ״̬��       |������    |������Ϣ |
| -----------------|-------------- | ------------ |
|200 |0|�ɹ� |
|400  |-2579|���ݷ����л����� |
|401 |-279|��Ȩ���� |
|400  |-11539|�Ƿ����� <br>��ϸԭ����ο�������Ϣ�ֶ�|
|400  |-2067|�������Ͳ�ƥ�� |
|400  |-1811|�Ƿ����� |
|400  |-5395|û�����������ֶ� |
|400  |-2323|�������л����� |
|400  |-7949|�Ƿ����ݰ汾�� <br>һ�㷢����д������Ӧ�����ݰ汾������ʱ|
|400  |-1293|��¼�Ѿ����� |
|404  |261|��¼������ |
|404  |-34565|���������� |
|500  |-|ϵͳ�ڲ�����<br>��ο�������Ϣ�ֶ�|

## API ����ʾ�� 

###   Tcaplus.GetRecord 
```
GET /ver1.0/apps/{APP_ID}/zones/{ZONE_ID}/tables/{TABLE_NAME}/records?keys={JSONKeysObj}&select={JSONSelectObj}
```
��һ�� Tcaplus pb ����ͨ��ָ��һ����¼�� key ��Ϣ��ѯ�˼�¼��������������������¼ȡ���������������� select ������select ������ָ������Ҫ��Ӧ���з��ص��ֶΣ���� select ������ָ����������ʾ�����ֶ���Ϣ��������ݼ�¼�����ڣ����᷵�ش���

������ URI ��ָ��`keys`�������� select �������ǿ�ѡ�keys ָ����������ֵ��select ָ��Ҫ��ʾ�� value �ֶε����ơ�����������ͨ�����·���ķ�ʽָ��Ƕ�׽ṹ�е��ֶΣ����磺��pay.total_money����

>!  ����ı�������ͨ�� UrlEncode ���룬�뽫url�еĿո����Ϊ"%20"������"+"��

|����             |����             |ȡֵ |
| -----------------|-------------- | ------------ |
|x-tcaplus-target  |String|Tcaplus.GetRecord |
|x-tcaplus-version  |String|Tcaplus3.32.0 |
|x-tcaplus-pwd-md5  |String|MD5 of AppKey(Password) |
|x-tcaplus-idl-type  |String|protobuf |


#### ʾ����

##### URL:
- URL δ UrlEncode �����
```
http://10.123.9.70:31002/ver1.0/apps/2/zones/1/tables/tb_example/records?keys={'region': 101, 'name': 'calvinshao', 'uin': 100}
```
- URL UrlEncode �����
```
http://10.123.9.70:31002/ver1.0/apps/2/zones/1/tables/tb_example/records?keys=%7B%22region%22%3A%20101%2C%20%22name%22%3A%20%22calvinshao%22%2C%20%22uin%22%3A%20100%7D
```

##### ���� HTTP ͷ��
```
[
 "x-tcaplus-target:Tcaplus.GetRecord",
 "x-tcaplus-version:Tcaplus3.32.0",
 "x-tcaplus-pwd-md5:c3eda5f013f92c81dda7afcdc273cf82",
 "x-tcaplus-idl-type:protobuf"
]
```

##### Ӧ�����ݣ�

```
{
 "ErrorCode": 0,
 "ErrorMsg": "Succeed",
 "RecordVersion": 1,
 "Record": {
  "name": "calvinshao",
  "lockid": [
   50,
   60,
   70
  ],
  "pay": {
   "pay_times": 2,
   "total_money": 10000,
   "pay_id": 5,
   "auth": {
    "pay_keys": "adqwacsasafasda",
    "update_time": 1528018372
   }
  },
  "region": 101,
  "uin": 100,
  "is_available": true,
  "gamesvrid": 4099,
  "logintime": 404
 }
}
```

### Tcaplus.SetRecord 
```
PUT /ver1.0/apps/{APP_ID}/zones/{ZONE_ID}/tables/{TABLE_NAME}/records
```

ͨ��ָ��һ����¼�� key ��Ϣ���ô˼�¼�������¼����ִ�и��ǲ���������ִ�в��������

SetRecord����֧��resultflag��������ȡֵ��

* `0` ����Ϊ0��Ӧ���н���������ɹ���ʧ��
* `1` ����Ϊ1��Ӧ���а���������һ�µ�ֵ
* `2` ����Ϊ2��Ӧ���а������޸ĵ����ݵ������ֶ�����ֵ
* `3` ����Ϊ3��Ӧ���а�����¼���޸�ǰ��ֵ

|����             |����             |ȡֵ |
| -----------------|-------------- | ------------ |
|x-tcaplus-target  |String|Tcaplus.SetRecord |
|x-tcaplus-version  |String|Tcaplus3.32.0 |
|x-tcaplus-pwd-md5  |String|MD5 of AppKey(Password) |
|x-tcaplus-result-flag  |Int|2 |
|x-tcaplus-data-version-check  |Int|2 |
|x-tcaplus-data-version  |Int|-1 |
|x-tcaplus-idl-type  |String|protobuf |


#### ʾ����
##### URL:
```
http://10.123.9.70/ver1.0/apps/2/zones/1/tables/tb_example/records
```

##### ���� HTTP ͷ��
```
[
 "x-tcaplus-target:Tcaplus.SetRecord",
 "x-tcaplus-version:Tcaplus3.32.0",
 "x-tcaplus-pwd-md5:c3eda5f013f92c81dda7afcdc273cf82",
 "x-tcaplus-result-flag:2",
 "x-tcaplus-data-version-check:2",
 "x-tcaplus-data-version:-1",
 "x-tcaplus-idl-type:Protobuf"
]
```
##### ���� JSON ���ݣ�
```
{
 "ReturnValues": "Send to tcaplus by calvinshao",
 "Record": {
  "name": "calvinshao",
  "lockid": [
   50,
   60,
   70,
   80,
   90,
   100
  ],
  "pay": {
   "pay_times": 3,
   "total_money": 12000,
   "pay_id": 5,
   "auth": {
    "pay_keys": "adqwacsasafasda",
    "update_time": 1528018372
   }
  },
  "region": 101,
  "uin": 100,
  "is_available": false,
  "gamesvrid": 4099,
  "logintime": 404
 }
}
```

##### Ӧ�� JSON ����
```
{
 "ErrorCode": 0,
 "ErrorMsg": "Succeed",
 "RecordVersion": 1,
 "ReturnValues": "Send to tcaplus by calvinshao",
 "Record": {
  "name": "calvinshao",
  "lockid": [
   50,
   60,
   70,
   80,
   90,
   100
  ],
  "pay": {
   "pay_times": 3,
   "total_money": 12000,
   "pay_id": 5,
   "auth": {
    "pay_keys": "adqwacsasafasda",
    "update_time": 1528018372
   }
  },
  "region": 101,
  "uin": 100,
  "is_available": false,
  "gamesvrid": 4099,
  "logintime": 404
 }
}
```

###  Tcaplus.AddRecord 
```
POST /ver1.0/apps/{APP_ID}/zones/{ZONE_ID}/tables/{TABLE_NAME}/records
```
ͨ��ָ��һ����¼�� key ��Ϣ����һ����¼�������¼���ڷ��ش���

AddRecord����֧��resultflag��������ȡֵ��

* `0` ����Ϊ0��Ӧ���н���������ɹ���ʧ��
* `1` ����Ϊ1��Ӧ���а���������һ�µ�ֵ
* `2` ����Ϊ2��Ӧ���а������޸ĵ����ݵ������ֶ�����ֵ
* `3` ����Ϊ3��Ӧ���а�����¼���޸�ǰ��ֵ

|����            |����           |ȡֵ |
| -----------------|-------------- | ------------ |
|x-tcaplus-target  |String|Tcaplus.SetRecord |
|x-tcaplus-version  |String|Tcaplus3.32.0 |
|x-tcaplus-pwd-md5  |String|MD5 of AppKey(Password) |
|x-tcaplus-result-flag  |Int|1 |
|x-tcaplus-idl-type  |String|protobuf |


#### ʾ����

##### URL��
```
 http://10.123.9.70/ver1.0/apps/2/zones/1/tables/tb_example/records
```
##### ���� HTTP ͷ��

```
[
 "x-tcaplus-target:Tcaplus.AddRecord",
 "x-tcaplus-version:Tcaplus3.32.0",
 "x-tcaplus-pwd-md5:c3eda5f013f92c81dda7afcdc273cf82",
 "x-tcaplus-result-flag:1",
 "x-tcaplus-idl-type:protobuf"
]
```

##### ���� JSON ���ݣ�

```
{
 "ReturnValues": "Send to tcaplus by calvinshao",
 "Record": {
  "name": "calvinshao",
  "lockid": [
   50,
   60,
   70
  ],
  "pay": {
   "pay_times": 2,
   "total_money": 10000,
   "pay_id": 5,
   "auth": {
    "pay_keys": "adqwacsasafasda",
    "update_time": 1528018372
   }
  },
  "region": 101,
  "uin": 100,
  "is_available": true,
  "gamesvrid": 4099,
  "logintime": 404
 }
}
```

##### Ӧ�� JSON ���ݣ�

```
{
 "ErrorCode": 0,
 "ErrorMsg": "Succeed",
 "RecordVersion": 1,
 "ReturnValues": "Send to tcaplus by calvinshao",
 "Record": {
  "name": "calvinshao",
  "lockid": [
   50,
   60,
   70
  ],
  "pay": {
   "pay_times": 2,
   "total_money": 10000,
   "pay_id": 5,
   "auth": {
    "pay_keys": "adqwacsasafasda",
    "update_time": 1528018372
   }
  },
  "region": 101,
  "uin": 100,
  "is_available": true,
  "gamesvrid": 4099,
  "logintime": 404
 }
}
```



###  Tcaplus.DeleteRecord 

```
DELETE /ver1.0/apps/{APP_ID}/zones/{ZONE_ID}/tables/{TABLE_NAME}/records

```

ͨ��ָ��һ����¼�� key ��Ϣɾ���˼�¼��������ݲ������򷵻ش���

DeleteRecord����֧��resultflag��������ȡֵ��

* `0` ����Ϊ0��Ӧ���н���������ɹ���ʧ��
* `1` ����Ϊ1��Ӧ���а���������һ�µ�ֵ
* `2` ����Ϊ2��Ӧ���а������޸ĵ����ݵ������ֶ�����ֵ
* `3` ����Ϊ3��Ӧ���а�����¼���޸�ǰ��ֵ

|����             |����             |ȡֵ |
| -----------------|-------------- | ------------ |
|x-tcaplus-target  |String|Tcaplus.SetRecord |
|x-tcaplus-version  |String|Tcaplus3.32.0 |
|x-tcaplus-pwd-md5  |String|MD5 of AppKey(Password) |
|x-tcaplus-result-flag  |Int|1 |
|x-tcaplus-idl-type  |String|protobuf |


#### ʾ����

##### URI��
```
http://10.123.9.70/ver1.0/apps/2/zones/1/tables/tb_example/records
```

##### ���� HTTP ͷ��

```
[
 "x-tcaplus-target:Tcaplus.DeleteRecord",
 "x-tcaplus-version:Tcaplus3.32.0",
 "x-tcaplus-pwd-md5:c3eda5f013f92c81dda7afcdc273cf82",
 "x-tcaplus-result-flag:1",
 "x-tcaplus-idl-type:protobuf"
]
```

##### ���� JSON ���ݣ�

```
{
 "ReturnValues": "Send to tcaplus by calvinshao",
 "Record": {
  "region": 101,
  "name": "calvinshao",
  "uin": 100
 }
}
```

##### Ӧ�� JSON ���ݣ�
```
{
 "ErrorCode": 0,
 "Record": {},
 "RecordVersion": -1,
 "ReturnValues": "Send to tcaplus by calvinshao"
}
```



###  Tcaplus.FieldGetRecord 
```
GET /ver1.0/apps/{APP_ID}/zones/{ZONE_ID}/tables/{TABLE_NAME}/records?keys={JSONKeysObj}&select={JSONSelectObj}
```

��һ�� Tcaplus pb ����ͨ��ָ��һ����¼�� key ��Ϣ��ѯ�˼�¼��������ֻ��ѯ�ʹ����û�ͨ�� select ����ָ�����ֶε�ֵ���⽫�������紫�������������� GetRecord �������Ĳ�֮ͬ����������ݼ�¼�����ڣ����᷵�ش���
������ URI ��ָ��`keys`��`select`������keys ָ������������ֵ��select ָ����Ҫ��ʾ�� value �ֶε����ơ������û�����ͨ�����·���ķ�ʽָ��Ƕ�׽ṹ�е��ֶΣ����磺��pay.total_money����

>! ����ı�������ͨ�� urlencode ���룬�뽫url�еĿո����Ϊ"%20"������"+"��

|����             |����            |ȡֵ |
| -----------------|-------------- | ------------ |
|x-tcaplus-target  |String|Tcaplus.FieldGetRecord |
|x-tcaplus-version  |String|Tcaplus3.32.0 |
|x-tcaplus-pwd-md5  |String|MD5 of AppKey(Password) |
|x-tcaplus-idl-type  |String|protobuf |

#### ʾ����

##### URL δ UrlEncode ���:

```
http://10.123.9.70/ver1.0/apps/2/zones/1/tables/tb_example/records?keys={'region': 101, 'name': 'calvinshao', 'uin': 100}&select=['gamesvrid', 'lockid', 'pay.auth.pay_keys', 'pay.total_money']
```

##### URL UrlEncode �����

```
http://10.123.9.70/ver1.0/apps/2/zones/1/tables/tb_example/records?keys=%7B%22region%22%3A%20101%2C%20%22name%22%3A%20%22calvinshao%22%2C%20%22uin%22%3A%20100%7D&select=%5B%22gamesvrid%22%2C%20%22lockid%22%2C%20%22pay.auth.pay_keys%22%2C%20%22pay.total_money%22%5D
```

##### ���� HTTP ͷ��

```
[
 "x-tcaplus-target:Tcaplus.FieldGetRecord",
 "x-tcaplus-version:Tcaplus3.32.0",
 "x-tcaplus-pwd-md5:c3eda5f013f92c81dda7afcdc273cf82",
 "x-tcaplus-idl-type:protobuf"
]
```

##### Ӧ�� JSON ���ݣ�

```
{
 "ErrorCode": 0,
 "ErrorMsg": "Succeed",
 "RecordVersion": 1,
 "Record": {
  "name": "calvinshao",
  "lockid": [
   50,
   60,
   70
  ],
  "pay": {
   "total_money": 10000,
   "auth": {
    "pay_keys": "adqwacsasafasda"
   }
  },
  "region": 101,
  "uin": 100,
  "gamesvrid": 4099
 }
}
```

###  Tcaplus.FieldSetRecord  

```
PUT /ver1.0/apps/{APP_ID}/zones/{ZONE_ID}/tables/{TABLE_NAME}/records
```


ͨ��ָ��һ����¼�� key ��Ϣ�޸Ĵ˼�¼���� SetRecord ������ͬ���Ǵ˲���ֻ���䲢����ָ���ֶε�ֵ���������������ֶΡ��⽫��������������������ݼ�¼���ڣ���ִ�и��²��������򽫻᷵�ش���

FieldSetRecord����֧��resultflag��������ȡֵ��

* `0` ����Ϊ0��Ӧ���н���������ɹ���ʧ��
* `1` ����Ϊ1��Ӧ���а���������һ�µ�ֵ


|����            |����             |ȡֵ |
| -----------------|-------------- | ------------ |
|x-tcaplus-target  |String|Tcaplus.SetRecord |
|x-tcaplus-version  |String|Tcaplus3.32.0 |
|x-tcaplus-pwd-md5  |String|MD5 of AppKey(Password) |
|x-tcaplus-result-flag  |Int|2 |
|x-tcaplus-data-version-check  |Int|2 |
|x-tcaplus-data-version  |Int|-1 |
|x-tcaplus-idl-type  |String|protobuf |


#### ʾ����

##### URL��

```
http://10.123.9.70/ver1.0/apps/2/zones/1/tables/tb_example/records

```

##### ���� HTTP ͷ��

```
[
 "x-tcaplus-target:Tcaplus.FieldSetRecord",
 "x-tcaplus-version:Tcaplus3.32.0",
 "x-tcaplus-pwd-md5:c3eda5f013f92c81dda7afcdc273cf82",
 "x-tcaplus-result-flag:1",
 "x-tcaplus-data-version-check:1",
 "x-tcaplus-data-version:-1",
 "x-tcaplus-idl-type:Protobuf"
]

```
##### ���� JSON ���ݣ�

```
{
 "ReturnValues": "aaaaaaaaaa",
 "FieldPath": [ // ��ʽָ����Ҫ���µ��ֶ�·��
    "gamesvrid",
    "logintime",
    "pay.total_money",
    "pay.auth.pay_keys"
 ],
 "Record": { // ������Ҫ���µ��ֶ���ֵ
  "name": "calvinshao",
  "pay": {
   "total_money": 17190,
   "auth": {
    "pay_keys": "bingo"
   }
  },
  "region": 101,
  "uin": 100,
  "gamesvrid": 1719,
  "logintime": 1719
 }
}
```

##### Ӧ�� JSON ���ݣ�

```
{
 "ErrorCode": 0,
 "ErrorMsg": "Succeed",
 "RecordVersion": 3,
 "ReturnValues": "aaaaaaaaaa",
 "Record": {
  "name": "calvinshao",
  "pay": {
   "total_money": 17190,
   "auth": {
    "pay_keys": "bingo"
   }
  },
  "region": 101,
  "uin": 100,
  "gamesvrid": 1719,
  "logintime": 1719
 }
}
```


### Tcaplus.FieldIncRecord 

```
PUT /ver1.0/apps/{APP_ID}/zones/{ZONE_ID}/tables/{TABLE_NAME}/records
```


ͨ��ָ��һ����¼�� key ��Ϣ��ָ�����ֶν��������������������ֽ�֧�� `int32`�� `int64`�� `uint32` �� `uint64`�����ֶΡ������� FieldSetRecord ���ơ�

SetRecord����֧��resultflag��������ȡֵ��

* `0` ����Ϊ0��Ӧ���н���������ɹ���ʧ��
* `1` ����Ϊ1��Ӧ���а���ָ���ֶ��޸ĺ��ֵ


|����            |����             |ȡֵ |
| -----------------|-------------- | ------------ |
|x-tcaplus-target  |String|Tcaplus.SetRecord |
|x-tcaplus-version  |String|Tcaplus3.32.0 |
|x-tcaplus-pwd-md5  |String|MD5 of AppKey(Password) |
|x-tcaplus-result-flag  |Int|2 |
|x-tcaplus-data-version-check  |Int|2 |
|x-tcaplus-data-version  |Int|-1 |
|x-tcaplus-idl-type  |String|protobuf |


#### ʾ����

##### URL��

```
http://10.123.9.70/ver1.0/apps/2/zones/1/tables/tb_example/records
```

##### ���� HTTP ͷ��

```
[
 "x-tcaplus-target:Tcaplus.FieldIncRecord",
 "x-tcaplus-version:Tcaplus3.32.0",
 "x-tcaplus-pwd-md5:c3eda5f013f92c81dda7afcdc273cf82",
 "x-tcaplus-result-flag:1",
 "x-tcaplus-data-version-check:1",
 "x-tcaplus-data-version:-1",
 "x-tcaplus-idl-type:Protobuf"
]
```

##### ���� JSON ���ݣ�

```
{
 "ReturnValues": "aaaaaaaaaa",
 "Record": {
  "name": "calvinshao",
  "pay": {
   "total_money": -1, 
   "auth": {
    "update_time": -1
   }
  },
  "region": 101,
  "uin": 100,
  "gamesvrid": 2,
  "logintime": -2
 }
}
```

##### Ӧ�� JSON ���ݣ�

```
{
 "ErrorCode": 0,
 "ErrorMsg": "Succeed",
 "RecordVersion": 9,
 "ReturnValues": "aaaaaaaaaa",
 "Record": {
  "name": "calvinshao",
  "pay": {
   "total_money": 11999,
   "auth": {
    "update_time": 921
   }
  },
  "region": 101,
  "uin": 100,
  "gamesvrid": 4101,
  "logintime": 98
 }
}
```


###  Tcaplus.PartkeyGetRecord 
```
GET /ver1.0/apps/{APP_ID}/zones/{ZONE_ID}/tables/{TABLE_NAME}/records?keys={JSONKeysObj}&select={JSONSelectObj}
```

ͨ��ָ������������ֵ��ѯ������¼��������������ض������ݣ�����ͨ�� select ����ָ�����ֶ�����ʾ���˲�����ǰ����ָ�����������ϱ����ڽ����ʱ�򴴽�������������᷵�ش���

������ URI ��ָ��`keys`�������� select �������ǿ�ѡ�keys ָ������������ֵ��select ָ����Ҫ��ʾ�� value �ֶε����ơ������û�����ͨ�����·���ķ�ʽָ��Ƕ�׽ṹ�е��ֶΣ����磺��pay.total_money����

limit��offset�����ڼ�¼���ַ��ؿ��ƵĲ�����

>! ����ı�������ͨ�� urlencode ���룬�뽫 url �еĿո����Ϊ��%20�������ǡ�+�������� HEADER�� ͨ��`x-tcaplus-index-name`ָ����Ҫ���ʵ����������������ڱ����ļ��п����ҵ���

|����            |����             |ȡֵ |
| -----------------|-------------- | ------------ |
|x-tcaplus-target  |String|Tcaplus.GetRecord |
|x-tcaplus-version  |String|Tcaplus3.32.0 |
|x-tcaplus-pwd-md5  |String|MD5 of AppKey(Password) |
|x-tcaplus-idl-type  |String|protobuf |
|x-tcaplus-index-name  |String| {index_name}|


#### ʾ����

##### URL δ UrlEncode �����

```
http://10.123.9.70/ver1.0/apps/2/zones/1/tables/tb_example/records?keys={'name': 'calvinshao', 'uin': 100}&select=['gamesvrid', 'lockid', 'pay.total_money', 'pay.auth.pay_keys']
```

##### URL UrlEncode �����
```
http://10.123.9.70/ver1.0/apps/2/zones/1/tables/tb_example/records?keys=%7B%22name%22%3A%20%22calvinshao%22%2C%20%22uin%22%3A%20100%7D&select=%5B%22gamesvrid%22%2C%20%22lockid%22%2C%20%22pay.total_money%22%2C%20%22pay.auth.pay_keys%22%5D
```

##### ���� HTTP ͷ��
```
[
"x-tcaplus-target:Tcaplus.PartkeyGetRecord",
"x-tcaplus-version:Tcaplus3.32.0",
"x-tcaplus-pwd-md5:c3eda5f013f92c81dda7afcdc273cf82",
"x-tcaplus-idl-type:protobuf"
"x-tcaplus-index-name:index_name"
]
```



##### Ӧ�����ݣ�

```
{
 "ErrorCode": 0,
 "ErrorMsg": "Succeed",
 "MultiRecords": [
  {
   "RecordVersion": 9,
   "Record": {
    "name": "calvinshao",
    "lockid": [
     50,
     60,
     70,
     80,
     90,
     100
    ],
    "pay": {
     "total_money": 11999,
     "auth": {
      "pay_keys": "adqwacsasafasda"
     }
    },
    "region": 101,
    "uin": 100,
    "gamesvrid": 4101
   }
  },
  {
   "RecordVersion": 1,
   "Record": {
    "name": "calvinshao",
    "lockid": [
     50,
     60,
     70,
     80
    ],
    "pay": {
     "total_money": 10000,
     "auth": {
      "pay_keys": "adqwacsasafasda"
     }
    },
    "region": 102,
    "uin": 100,
    "gamesvrid": 4100
   }
  },
  {
   "RecordVersion": 1,
   "Record": {
    "name": "calvinshao",
    "lockid": [
     60,
     70,
     80,
     90
    ],
    "pay": {
     "total_money": 10000,
     "auth": {
      "pay_keys": "adqwacsasafasda"
     }
    },
    "region": 103,
    "uin": 100,
    "gamesvrid": 4101
   }
  }
 ],
 "RemainNum": 0,
 "TotalNum": 3
}
```
