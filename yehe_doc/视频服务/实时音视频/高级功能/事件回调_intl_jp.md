イベントコールバックサービスは、HTTP/HTTPSリクエストという形でサーバーへのTRTC業務でのイベントの通知をサポートします。イベントコールバックサービスは、ルームイベントグループ（Room Event）とメディアイベントグループ（Media Event）のいくつかのイベントを統合しています。お客様はTencent Cloudに対して、関連の構成情報を提供することができます。

[](id:deploy)
## 設定情報
TRTCコンソールは、セルフサービスのコールバック設定情報をサポートしており、設定が完了した後、イベントコールバック通知を受信できます。詳細な操作ガイドについては、[コールバック設定](https://intl.cloud.tencent.com/document/product/647/39559)をご参照ください。


>!事前に次の情報を準備する必要があります。
>- **必須項目**：コールバック通知を受信するためのHTTP/HTTPSサーバーアドレス。
>- **オプション項目**：署名を計算するためのキーで、大文字・小文字と数字で構成される最大32文字のキーをカスタマイズできます。

## タイムアウト・リトライ
イベントコールバックサーバーがメッセージ通知を送信してから5秒以内にお客様のサーバーから応答を受信しない場合、通知は失敗とみなされます。最初の通知が失敗すると、直ちにリトライが行われます。その後の失敗は、1分を超えるまで、** 10秒**の間隔でリトライし続けた後、リトライを停止します。

[](id:format)
## イベントコールバックメッセージ形式

イベントコールバックメッセージは、HTTP/HTTPS POSTリクエストとしてサーバーに送信されます。以下がその詳細となります。

- **文字エンコード形式**：UTF-8。
- **リクエスト**：bodyの形式はJSONです。
- **応答**：HTTP STATUS CODE = 200、サーバーは応答パケットの具体的な内容を無視します。プロトコルとの親和性のため、クライアントの応答内容に、JSON：`{"code":0}`を付けることをお勧めします。
- **パケット例**：以下の内容は「ルームイベントグループ-入室」”イベントのパケット例です。
<dx-codeblock>
::: JSON JSON
{
	"EventGroupId": 1,        #ルームイベントグループ
	「EventType」: 103、       #入室イベント
	「CallbackTs」: 1615554923704、        #コールバック時間。単位はミリ秒単位
	"EventInfo": {
		"RoomId": 12345,        #数字のルーム番号
		「EventTs」: 1608441737、        #イベント発生時間。単位は秒
		「UserId」: 「test」、        #ユーザーID
		「UniqueId」: 1615554922656、      #固有識別子
		"Role": 20,        #ユーザーロール、キャスター
		「Reason」: 1        #退室の原因、正常な入室
		}
}
:::
</dx-codeblock>



## パラメータの説明
[](id:message)
### コールバックメッセージのパラメータ

- イベントコールバックメッセージのheaderには、次のフィールドが含まれています。
<table id="header">
<tr><th>フィールド名</th><th>値</th></tr></thead><tr>
<td>Content-Type</td><td>application/json</td>
</tr><tr>
<td>Sign</td><td>署名値</td>
</tr><tr>
<td>SdkAppId</td><td>sdk application id</td>
</tr></table>
- イベントコールバックメッセージのbodyには、次のフィールドが含まれています。
<table id="body">
<tr><th>フィールド名</th><th>タイプ</th><th>意味</th>
</tr><tr>
<td>EventGroupId</td><td>Number</td>
<td><a href="#eventId">イベントグループID</a></td>
</tr><tr>
<td>EventType</td>
<td>Number</td>
<td><a href="#event_type">コールバック通知のイベントタイプ</a></td>
</tr><tr>
<td>CallbackTs</td>
<td>Number</td>
<td>イベントコールバックサーバーからお客様のサーバーに送信されるコールバックリクエストのUnixタイムスタンプ。単位はミリ秒</td>
</tr><tr>
<td>EventInfo</td>
<td>JSON Object</td>
<td><a href="#event_infor">イベント情報</a></td>
</tr>
</tbody></table>

[](id:eventId)
### イベントグループID

| フィールド名            | 値   | 意味       |
| ----------------- | ---- | ---------- |
| EVENT_GROUP_ROOM  | 1    | ルームイベントグループ |
| EVENT_GROUP_MEDIA | 2    | メディアイベントグループ |

[](id:event_type)
### イベントタイプ

| フィールド名                  | 値   | 意味             |
| ----------------------- | ---- | ---------------- |
| EVENT_TYPE_CREATE_ROOM  | 101  | ルームの作成         |
| EVENT_TYPE_DISMISS_ROOM | 102  | ルームの解散         |
| EVENT_TYPE_ENTER_ROOM   | 103  | ルームに参加         |
| EVENT_TYPE_EXIT_ROOM    | 104  | ルームを退出         |
|  EVENT_TYPE_CHANGE_ROLE   | 105  |    ロールの切り替え      |
| EVENT_TYPE_START_VIDEO  | 201  | ビデオデータのプッシュを開始 |
| EVENT_TYPE_STOP_VIDEO   | 202  | ビデオデータのプッシュを停止 |
| EVENT_TYPE_START_AUDIO  | 203  |オーディオデータのプッシュを開始 |
| EVENT_TYPE_STOP_AUDIO   | 204  | オーディオデータのプッシュを停止 |
| EVENT_TYPE_START_ASSIT  | 205  | サブストリームデータのプッシュを開始 |
| EVENT_TYPE_STOP_ASSIT   | 206  | サブストリームデータのプッシュを停止 |

[](id:event_infor)
### イベント情報

| フィールド名  | タイプ   | 意味                              |
| ------- | ------ | --------------------------------- |
RoomId      |     String/Number       |     ルーム名（タイプはクライアントのルーム番号タイプと同様）    |
| EventTs | Number | 時間で発生するUnixタイムスタンプ。単位は秒   |
| UserId  | String | ユーザーID                            |
| UniqueId  | Number | [固有識別子](#UniqueId)（option：ルームイベントグループ付与）                            |
| Role    | Number | [ロールタイプ](#role_type)（option：入退室時に付帯）  |
| Reason  | Number | [具体的な原因](#reason) （option：入退室時に付帯） |

>?[](id:UniqueId) **固有識別子の定義：**クライアントでネットワークの切り替え、異常退出および再入室プロセスなどの特殊な行為が発生すると、お客様のコールバックサーバーが同じユーザーの複数回の入室および退室コールバックを受信する可能性があり、UniqueIdを使用してユーザーの同一回の入退室を識別することができます。

[](id:role_type)
### ロールタイプ

| フィールド名            | 値   | 意味 |
| ------------------ | ---- | ---- |
| MEMBER_TRTC_ANCHOR | 20   | キャスター |
| MEMBER_TRTC_VIEWER | 21   | 視聴者 |

[](id:reason)
### 具体的な原因

| フィールド名    | 意味                              |
| -------  | --------------------------------- |
|入室   |<li/>1：正常な入室<li/>2：ネットワークの切り替え<li/>3：タイムアウト・リトライ<li/>4：ルーム間のマイク接続・入室 |
|退室 | <li/>1：正常な退室<li/>2：タイムアウトによる退室<li/>3：ルームのユーザーが削除される<li/>4：マイク接続のキャンセル・退室<li/>5：強制終了|



### 署名計算
署名はHMAC SHA256暗号化アルゴリズムによって算出されます。イベントコールバック受信サーバーがコールバックメッセージを受信した後、同じメソッドで署名が算出されます。同様に、Tencent CloudのTRTCのイベントコールバックであり、偽造されていないことを意味します。署名の計算は次のとおりです。
```
//署名Signの計算式のkeyは、署名Signの計算に用いられる暗号化鍵です。
Sign = base64(hmacsha256(key, body))
```



