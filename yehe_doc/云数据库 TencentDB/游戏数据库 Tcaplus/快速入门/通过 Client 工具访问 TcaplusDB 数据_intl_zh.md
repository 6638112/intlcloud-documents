���Ľ������ͨ���ͻ��˹���tcaplus_client�������ݡ�
�������ݲ����������where������where�����б�����������ֶΣ�������������������ʹ��and����������ֶ�����������

## ͨ�� client ���߷��� TcaplusDB ����
tcaplus_client ��һ�� TcaplusDB ����ʵĿͻ��˹��ߣ���ͨ���±��е��������ӽ������ء�

Linux x86_64 ƽ̨�� TcaplusServiceAPI ����������64λ Linux �汾�� tcaplus_client ���ߣ�

| �汾 | ����ϵͳ|���ذ��� | 
|---------|---------|---------|
| 3.36.0.192960 | Linux |[TcaplusPbApi3.36.0.192960.x86_64](https://tcaplusdb-sdk-1301716906.cos.ap-shanghai.myqcloud.com/3.36.0.192960/TcaplusPbApi3.36.0.192960.x86_64_release_20200115.tar.gz) |

>?��ز�����Ҫ���û���Ѷ���˺��������ͬ VPC ���磬ͬ�������Ʒ����� CVM �н��С�

### ��װ�ͻ���
������� TcaplusServiceApi ��װ���󣬽��� [ͨ���ϴ�����](https://intl.cloud.tencent.com/document/product/213/34821) �ϴ����� TcaplusDB ��ȺͬһVPC��ͬһ�������Ʒ������С�
1. �ϴ���ɺ�ִ�����������ѹ��װ����
```
tar -xf TcaplusServiceApi3.32.0.191008.x86_64_release_20190409.tar.gz -C tcaplus
```
2. ��ѹ��ɺ󣬽����� tcaplus �� bin Ŀ¼�У��������ִ��Ȩ�ޣ�
```
cd tcaplus/release/x86_64/bin
chmod +x tcaplus_client
```
3. ֱ��ִ��`./tcaplus_client`�������ʾ�������ݿ�����Ĳ�����Ϣ���û����Ը����Լ��ļ�Ⱥ��Ϣ������д��
>!����ʾ���У�app_id ����Ⱥ���� ID��App ����Ⱥ��zone �������顣
>

```
# ./tcaplus_client
--------------------------------------------------------------------------------
 invalid parameters, please start the client as following:
    ./tcaplus_client -a app_id -z zone_id -s signature -d dir_server_url [-t table_name] [-l log_file.xml] [-T tdr_file.tdr] [-e execute_command]
    the params in [] are optional, and theire order is not important.
    -a(--ap_id)    App ID
    -z(--zone_id)    ZONE ID
	-s(--signature)    PASSWORD
    -d(--dir)    dir server addr
    -t(--table)    table to add
    -l(--log)    log file name that must be client_log.xml, and log class name be client
    -T(--tdr)    tdr filename 
    -e(--execute)    content following should be with qoutes.
    e.g. ./tcaplus_client -a 2 -z 3 -s "test@Password1" -d 172.xx.xx.181:9999 -T table_test.tdr 
--------------------------------------------------------------------------------
```

### ���� TcaplusDB
ʹ���������� TcaplusDB������ʾ���У����ʵ���Ϣ���£������ڱ���� ID Ϊ1�ı�����д����˱� tb_online��
- ��Ⱥ����ID��2
- �������룺test@Password1
- ������ַ:�����˿ڣ�10.125.32.21:9999
- �����ID��1

```
./tcaplus_client -a 2 -z 1 -s "test@Password1" -d 10.125.32.21:9999
+------------------------------------------------------------------------------+
|    tcaplus_client x86_64  build at Wed Jan 18 22:08:38 CST 2017              |
|                                                                              |
|    Welcome!                                                                  |
+------------------------------------------------------------------------------+

tcaplus>
```

����ʾ��֮������ help���ɿ�����һ���İ�����Ϣ��ͨ�� `> help ��������` ���Բ鿴����ʹ�÷�����
```
tcaplus>help
--------------------------------------------------------------------------------
    show                 get server status related information. executing help show for details.
    dir                  add dir server url. if no dir_server_url added ,
                         commands will fail when executing.
    desc                 output current table struction description
    count                output table row count
    select               query data
    update               update record. if record does not exist then add it or update it if exists.
    insert               insert a new record (not implemented)
    delete               delete record(s)
    bson                 execute bson query
    dump                 dump records from tcaplus to file with csv format
    load                 load records from csv file and import the records to tcplus
    clean                clean table
    quit                 exit the client
    help                 follow a command to get details.
                         e.g. help show, help dir etc.
    note: tdr mode means starting client with -T, and none tdr mode starting client without -T
--------------------------------------------------------------------------------
```


���ķֱ���ʾ��������ִ�з��������á�

#### desc ����
�鿴��Ķ�����Ϣ��Ƕ���ֶ�ֻ�ܿ���������ΪǶ�����ͣ������޷��鿴Ƕ�׽ṹ��Ķ��塣
ʹ���﷨Ϊ��`desc ����;`
```
tcaplus>desc game_players;
TableName:game_players
TableType:PROTOBUF
-------------------------------------------------------------------------
| Field                         Type                          Key       |
-------------------------------------------------------------------------
| player_id                     int64                         key       |
| player_email                  string                        key       |
| player_name                   string                                  |
| game_server_id                int32                                   |
| login_timestamp               string                                  |
| logout_timestamp              string                                  |
| is_online                     int8                                    |
| pay                           message                                 |
-------------------------------------------------------------------------
```

#### count ����
�鿴���¼������ʹ���﷨Ϊ��`count ����;`
```
tcaplus>count t1;
-------------------------------------------
| TableName                     COUNT(*)  |
-------------------------------------------
| t1                            15        |
-------------------------------------------
```

#### ��������
ʹ�� dump �����ָ�������еļ�¼�������ļ��� json ��ʽ��
ʹ���﷨��`dump * from ���� into �ļ���;`
```
tcaplus>dump * from player into player.txt;
--------------------------------------------------------------------------------
      dump from table("player") success. total record number is 4
--------------------------------------------------------------------------------
```

#### ��������
ʹ�� load ����� csv �ļ��е���ָ����ļ�¼���޷�ֱ�ӵ��� dump �������ļ���
ʹ���﷨��`load ���� from �ļ�;`
```
tcaplus>load hehe from test1;
--------------------------------------------------------------------------------
      1 records loaded successfully.
--------------------------------------------------------------------------------
```

#### ��ձ�����
��Ϊ��ȫԭ�򣬵�ǰ�ͻ��˹��߲�֧��ֱ����������ݡ�����������ű����ݣ���ͨ������̨ [�����](https://console.cloud.tencent.com/tcaplusdb/table) ���ܽ��С�


### ��������
insert��䵱ǰ�޷�ʹ�ã���ʹ��update��������¼��

### �޸�����
ʹ�� update ����д���¼����where�����е������ֶ�ֵ�޿�ƥ������Ϊ������¼��
�﷨Ϊ��update �� set �ֶ�=ֵ[,�ֶ�2=ֵ2��] where �����ֶ�=ֵ [and �����ֶ�2=ֵ2��]��

```
tcaplus>update tb_online set gamesvrid=4099, logintime=101 where uin=1024 and name="tcaplus_user" and region=10;
--------------------------------------------------------------------------------
        success. 
--------------------------------------------------------------------------------
update time: 5593 us
```

### ��ȡ����
**ʹ�� select �����ȡ�����ֶ����ݡ�**
�﷨Ϊ��select �ֶ�[,�ֶ�2��] from �� where �����ֶ�=ֵ [and �����ֶ�2=ֵ]��
�����������recDataVersion ��ָ�ĵ�ǰ��¼�İ汾�š�
```
tcaplus>select gamesvrid, logintime from tb_online where uin=1024 and name="tcaplus_user" and region=10;
+------+--------------+--------+------------------+--------------+-----------+
| uin  | name         | region | recDataVersion   | gamesvrid    | logintime |
+------+--------------+--------+------------------+--------------+-----------+
| 1024 | tcaplus_user | 10     | 2                | 4099         | 101       |
+------+--------------+--------+------------------+--------------+-----------+
totally 1 record(s) responded.
query time 8686 us
```
֧��select * from �� where �����ֶ�=ֵ��������ʾ��
```
tcaplus>select * from test where id=1 and name=1;
+----+------+------------------+----+
| id | name | recDataVersion   | em |
+----+------+------------------+----+
| 1  | 1    | 1                | 1  |
+----+------+------------------+----+
totally 1 record(s) responded.
query time 7537 us
```
֧�� \G�Լ�\P��ʽ�����,\G��������ֶκ�������\P���ǰ��ձ������ķ�ʽ���,Ĭ�ϲ�����ʽ������ֶ����Ǹ���\Pģʽ�����
```
tcaplus>select * from hehe where id=1 and name=1 \G;
----------------------------------------1.row----------------------------------------
id: 1
name: 1
recDataVersion: 1
em: 1
responding record total:1
query time 3285 us
```
select ���֧�ֵ����������ļ���
�﷨Ϊ��select * into [outfile] �ļ��� from ���� where ����=ֵ [and ����2=ֵ];
```
tcaplus>select * into outfile test2.xml from hehe where id=1 and name=1;
+----+------+------------------+----+
| id | name | recDataVersion   | em |
+----+------+------------------+----+
| 1  | 1    | 1                | 1  |
+----+------+------------------+----+
totally 1 record(s) responded.
query time 5399 us
```
### ɾ������
ʹ��delete����ɾ��д��ļ�¼��
�﷨Ϊ��delete from ���� where ����=ֵ [and ����2=ֵ];
```
tcaplus>delete from hehe where id=4 and name=4;
--------------------------------------------------------------------------------
        success
--------------------------------------------------------------------------------
delete time 4280 us
```