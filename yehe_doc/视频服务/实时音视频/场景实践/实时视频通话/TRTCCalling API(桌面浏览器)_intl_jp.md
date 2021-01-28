## TRTCCallingの概要

[TRTCCalling](https://www.npmjs.com/package/trtc-calling-js)コンポーネントは、Tencent CloudのTencent Real-Time Communication（ TRTC）とInstant Messaging （IM）サービスの組み合わせにより構成されており、1対1および複数人でのビデオ/音声通話をサポートしています。具体的な実装プロセスについては、 [リアルタイムビデオ通話（デスクトップブラウザ）]](https://intl.cloud.tencent.com/document/product/647/38927)をご参照ください。

- TRTC SDK：[TRTC SDK](https://intl.cloud.tencent.com/zh/document/product/647)を低レイテンシーのオーディオビデオ通話コンポーネントとして使用しています。
- IM SDK： [IM SDK](https://intl.cloud.tencent.com/zh/document/product/1047)をシグナリング情報の送信と処理に利用します。

## TRTCCalling API 

#### イベントサブスクリプション/サブスクリプションのキャンセルに関するインターフェース関数 

このコンポーネントはイベントのディスパッチに基づいて管理します。アプリケーション層は、コンポーネントからディスパッチされるイベントにインタラクティブに応じて変更することができます。

| API                                                                         | 説明         |
| --------------------------------------------------------------------------- | ------------ |
| [on(eventName, callback, context)](#on(eventname.2C-callback.2C-context))   | イベントをサブスクライブします     |
| [off(eventName, callback, context)](#off(eventname.2C-callback.2C-context)) | イベントのサブスクライブをキャンセルします |

#### SDK 基本関数

| API                                                         | 説明                                           |
| ----------------------------------------------------------- | ---------------------------------------------- |
| [login({userID, userSig})](#login(.7Buserid.2C-usersig.7D)) | IMインターフェースにログインします。すべての機能は、まずログインしてからでないと使用できません |
| [logout()](#logout())                                       | インターフェースからログアウトします。ログアウトした後は、ダイヤル操作ができなくなります           |

#### 通話操作に関連するインターフェース関数

| API                                                                                       | 説明         |
| ----------------------------------------------------------------------------------------- | ------------ |
| [call({userID, type, timeout}))](#call(.7Buserid.2C-type.2C-timeout.7D))                  | 個人の通話の招待 |
| [groupCall({userIDList, type, groupID})](#groupcall(.7Buseridlist.2C-type.2C-groupid.7D)) | グループチャット通話の招待 |
| [accept({inviteID, roomID, callType})](#accept(.7Binviteid.2C-roomid.2C-calltype.7D))     | 通話招待の受け入れ |
| [reject({inviteID, isBusy, callType})](#reject(.7Binviteid.2C-isbusy.2C-calltype.7D))     | 通話招待の拒否 |
| [hangup()](#hangup())                                                                     | 現在通話の終了 |

#### ビデオ制御に関連するインターフェース関数

| API                                                                                           | 説明               |
| --------------------------------------------------------------------------------------------- | ------------------ |
| [startRemoteView({userID, videoViewDomID})](#startremoteview(.7Buserid.2C-videoviewdomid.7D)) | リモート画像のレンダリングの起動   |
| [stopRemoteView({userID, videoViewDomID})](#stopremoteview(.7Buserid.2C-videoviewdomid.7D))   | リモート画像のレンダリングの停止   |
| [startLocalView({userID, videoViewDomID})](#startlocalview(.7Buserid.2C-videoviewdomid.7D))   | ローカル画像のレンダリングの起動   |
| [stopLocalView({userID, videoViewDomID})](#stoplocalview(.7Buserid.2C-videoviewdomid.7D))     | ローカル画像のレンダリングの停止   |
| [openCamera()](#opencamera())                                                                 | カメラの起動         |
| [closeCamera()](#closecamera())                                                               | カメラの終了         |
| [setMicMute(isMute)](#setmicmute(ismute))                                                     | デバイスマイクのミュートの有無 |


## TRTCCallingの詳細

### TRTCCallingコンポーネントのインスタンスの作成

まず、[Tencent Real-Time Communicationコンソール](https://console.cloud.tencent.com/trtc/app)でアプリケーションを作成し、SDKAppIDを取得する必要があります。
その後、`new TRTCCalling()`メソッドを使ってTRTCCalling コンポーネントのインスタンスを取得することができます。

```javascript javascript
let options = {
  SDKAppID: 0 // 0 // アクセスするときは、0をお客様のIMアプリケーションのSDKAppIDに置き換える必要があります
};
let trtcCalling = new TRTCCalling(options);
```

### イベントのサブスクリプション/サブスクリプションキャンセルに関するインターフェース関数 




#### on(eventName, callback, context)

コンポーネントからディスパッチされたイベントを監視するために使用します。詳細については、[イベントリスト](#event)をご参照ください。

```javascript javascript
let handleInvite = function ({inviteID, sponsor, inviteData}) {
    console.log(`inviteID: ${inviteID}, sponsor: ${sponsor}, inviteData: ${JSON.stringify(inviteData)}`);
};
trtcCalling.on('onInvited', handleInvite, this);
```




#### off(eventName, callback, context)

イベント監視をキャンセルするために使用します。

```javascript javascript
let handleInvite = function ({inviteID, sponsor, inviteData}) {
    console.log(`inviteID: ${inviteID}, sponsor: ${sponsor}, inviteData: ${JSON.stringify(inviteData)}`);
};
trtcCalling.off('onInvited', handleInvite, this);
```

### SDK 基本関数

#### login({userID, userSig})

インターフェースにログインします。

``` javascript javascript
trtcCalling.login({userID, userSig})
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味                                                                                                                    |
| ------- | ------ | ----------------------------------------------------------------------------------------------------------------------- |
| userID   | String | 現在のユーザーID、文字列タイプでは、英語のアルファベット（a-z と A-Z）、数字（0-9）、ハイフン（-）とアンダーライン（\_）のみ使用できます。 |
| userSig  | String                | Tencent Cloudによって設計されたセキュリティ保護署名。取得方法については[UserSigの計算方法 ](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。 |




#### logout()

 インターフェースからログアウトします。

```javascript javascript
trtcCalling.logout()
```

### 通話操作に関連するインターフェース関数




#### call({userID, type, timeout})

1対1通話招待、そのうちtypeは通話タイプ、1は音声通話、2はビデオ通話です。

```javascript javascript
trtcCalling.call({userID, type, timeout})
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味                     |
| ------- | ------ | ------------------------ |
| userID  | String | 被招待者のuserID          |
| type    | Number | 1：音声通話、2：ビデオ通話 |
| timeout | Number | 0はタイムアウトしていないことを意味し、単位はs （秒）  |



#### groupCall({userIDList, type, groupID})
groupID パラメータは IM SDKにおけるグループ IDです。このパラメータを設定すると、通話リクエストメッセージがグループメッセージシステムを介してブロードキャストされます。このメッセージブロードキャスト方式は簡単で信頼性の高い方法です。設定しない場合は、`TRTCCalling` コンポーネントが単発メッセージで1人1人に通知を行います。

``` javascript javascript
trtcCalling.groupCall({userIDList, type, groupID})
```

パラメータは下表に示すとおりです。

| パラメータ       | タイプ   | 意味                     |
| ---------- | ------ | ------------------------ |
| userIDList | Array  | 招待リスト                 |
| type       | Number | 1：音声通話、2：ビデオ通話 |
| groupID    | String | IMグループID（オプション）       |




#### accept({inviteID, roomID, callType})
招待を受け取った後、このインターフェースを呼び出すと、現在の招待を受け入れます。
>? 前回のinvitationの処理が未完了の場合、コンポーネントはデフォルトでビジー状態になり、その後のすべての招待はビジーを返します。

``` javascript javascript
import TrtcCalling from 'trtc-calling-js';
trtcCalling.on(TrtcCalling.EVENT.INVITED, ({inviteID, sponsor, inviteData}) => {
  // ...
  trtcCalling.accept({inviteID, roomID, callType})
})
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ   | 意味                     |
| -------- | ------ | ------------------------ |
| inviteID | String | 招待ID、1回の招待を表示    |
| roomID   | Number | 通話ルーム番号 ID            |
| callType | Number | 1：音声通話、2：ビデオ通話 |



#### reject({inviteID, isBusy, callType})
招待を受け取った後、このインターフェースを呼び出すと、現在の招待が拒否されます。

``` javascript javascript
import TrtcCalling from 'trtc-calling-js';
trtcCalling.on(TrtcCalling.EVENT.INVITED, ({inviteID, sponsor, inviteData}) => {
  // ...
  trtcCalling.reject({inviteID, isBusy, callType})
})
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ    | 意味                    |
| -------- | ------- | ------------------------ |
| inviteID | String  | 招待ID、1回の招待を表示    |
| isBusy   | Boolean | ビジー状態の有無             |
| callType | Number  | 1：音声通話、2：ビデオ通話 |


#### hangup()
1. 通話中にこの関数を呼び出せば、通話を終了することができます。
2. ダイヤルしていない状態では、通話をキャンセルするために用いることができます。

```javascript javascript
trtcCalling.hangup()
```


### ビデオ制御に関連するインターフェース関数
#### startRemoteView({userID, videoViewDomID})
リモートユーザーのカメラデータを指定されたDOM IDノードにレンダリングします。

```javascript javascript
trtcCalling.startRemoteView({userID, videoViewDomID})
```

パラメータは下表に示すとおりです。

| パラメータ           | タイプ   | 意味                                                      |
| -------------- | ------ | --------------------------------------------------------- |
| userID         | String | ユーザーID                                                   |
| videoViewDomID | String | konoユーザーデータは、このDOM IDノードにレンダリングされたvideoタグを介して再生されます |

#### stopRemoteView({userID, videoViewDomID})
リモートユーザーのカメラデータによってレンダリングされたDOMノードを削除します。

```javascript javascript
trtcCalling.stopRemoteView({userID, videoViewDomID})
```

パラメータは下表に示すとおりです。

| パラメータ           | タイプ   | 意味                                              |
| -------------- | ------ | ------------------------------------------------- |
| userID         | String | ユーザーID                                           |
| videoViewDomID | String | このDOM ID ノードのvideoタグを削除し、ビデオの再生を停止します |

#### startLocalView({userID, videoViewDomID})
ローカルユーザーのカメラデータを指定されたDOM IDノードにレンダリングします。

```javascript javascript
trtcCalling.startLocalView({userID, videoViewDomID})
```

パラメータは下表に示すとおりです。

| パラメータ           | タイプ   | 意味                                                        |
| -------------- | ------ | ----------------------------------------------------------- |
| userID         | String | ユーザーID                                                     |
| videoViewDomID | String | ローカルユーザーデータは、このDOM IDノードにレンダリングされたvideoタグを介して再生されます |

#### stopLocalView({userID, videoViewDomID})

ローカルユーザーのカメラデータによってレンダリングされたDOMノードを削除します。

```javascript javascript
trtcCalling.stopLocalView({userID, videoViewDomID})
```

パラメータは下表に示すとおりです。

| パラメータ           | タイプ   | 意味                                              |
| -------------- | ------ | ------------------------------------------------- |
| userID         | String | ユーザーID                                           |
| videoViewDomID | String | このDOM ID ノードのvideoタグを削除し、ビデオの再生を停止します |

#### openCamera()
ローカルカメラをオンにします。

```javascript javascript
trtcCalling.openCamera()
```

####  closeCamera()
カメラの停止。

```javascript javascript
trtcCalling.closeCamera()
```

####  setMicMute(isMute) 
マイクをオン/オフします。

```javascript javascript
trtcCalling.setMicMute(true) // マイクのオン
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ    | 意味                                         |
| ------ | ------- | -------------------------------------------- |
| isMute | Boolean | <li/>true: マイクのオフ <li/>false: マイクのオン |


[](id:event)
## TRTCCallingイベントリスト

次のコードを参照して、TRTCCallingコンポーネントからさまざまなイベントをキャプチャすることができます。

```javascript javascript
import TrtcCalling from 'trtc-calling-js';
// etc
function handleInviteeReject({userID}) {

}
trtcCalling.on(TrtcCalling.EVENT.REJECT, handleInviteeReject)
```

### 招待側イベント

|                     CODE                      |   イベント受領側   |           説明            |
| :-------------------------------------------: | :------------: | :-----------------------: |
|               [REJECT](#reject)               |     招待側     |     被招待ユーザーは通話拒否      |
|              [NO_RESP](#no_resp)              |     招待側     |    被招待ユーザーはタイムアウト後に応答なし     |
|            [LINE_BUSY](#line_busy)            |     招待側     | 被招待ユーザーは通話中、ビジー状態  |
|              [INVITED](#invited)              |     被招待側     |      招待通知を受領済み       |
|       [CALLING_CANCEL](#calling_cancel)       |     被招待側     |     今回の通話をキャンセル済み      |
|      [CALLING_TIMEOUT](#calling_timeout)      |     被招待側     |    今回の通話はタイムアウト後に応答なし     |
|           [USER_ENTER](#user_enter)           | 招待側と被招待側 |         ユーザー入室          |
|           [USER_LEAVE](#user_leave)           | 招待側と被招待側 |       ユーザー退室        |
|             [CALL_END](#call_end)             | 招待側と被招待側 |       今回の通話終了        |
|           [KICKED_OUT](#kicked_out)           | 招待側と被招待側 |   ログインを繰り返したことにより、ルームから強制退室    |
| [USER_VIDEO_AVAILABLE](#user_video_available) | 招待側と被招待側 | リモートユーザーによるカメラのオン/オフ |
| [USER_AUDIO_AVAILABLE](#user_audio_available) | 招待側と被招待側 | リモートユーザーによるマイクのオン/オフ |

### 一般的なイベントコールバック

#### USER_ENTER

ユーザーが入室しました。

```javascript javascript
function handleUserEnter({userID}) {

}
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味    |
| ------ | ------ | ------- |
| userID | String | ユーザーID |

#### USER_LEAVE

ユーザーが退室しました。

``` javascript javascript
function handleUserLeave({userID}) {

}
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味    |
| ------ | ------ | ------- |
| userID | String | ユーザーID |

#### CALL_END

今回の通話は終了しました。

```javascript javascript
function handleCallEnd() {

}
```

#### KICKED_OUT

ログインを繰り返したことにより、ルームから強制退室させられました。

```javascript javascript
function handleKickedOut() {

}
```

#### USER_VIDEO_AVAILABLE

リモートユーザーがカメラをオン/オフにします。

``` javascript javascript
function handleUserVideoChange({userID, isVideoAvailable}) {

}
```

パラメータは下表に示すとおりです。

| パラメータ             | タイプ    | 意味                                                         |
| ---------------- | ------- | ----------------------------------------------------------- |
| userID           | String  | ユーザーID                                                     |
| isVideoAvailable | Boolean | <li/>true：リモートユーザーによるカメラオン<li/>false：リモートユーザーによるカメラオフ |

#### USER_AUDIO_AVAILABLE

リモートユーザーがマイクをオン/オフにしました。

```javascript javascript
function handleUserAudioChange({userID, isAudioAvailable}) {

}
```

パラメータは下表に示すとおりです。

| パラメータ             | タイプ    | 意味                                                           |
| ---------------- | ------- | ------------------------------------------------------------- |
| userID           | String  | ユーザーID                                                       |
| isAudioAvailable | Boolean | <li>true：リモートユーザーによるマイクオン <li> false：リモートユーザーによるマイクオフ |

### 招待側イベントコールバック

#### REJECT

ユーザーが通話を拒否しました。

```javascript javascript
function handleInviteeReject({userID}) {

}
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味    |
| ------ | ------ | ------- |
| userID | String | ユーザーID |

#### NO_RESP

招待されたユーザーは応答しませんでした。

```javascript javascript
function handleNoResponse({userID}) {

}
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味    |
| ------ | ------ | ------- |
| userID | String | ユーザーID |

#### LINE_BUSY

被招待側は通話中で、ビジー状態です。

```javascript javascript
function handleInviteeLineBusy({userID}) {

}
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味    |
| ------ | ------ | ------- |
| userID | String | ユーザーID |

### 被招待側イベントコールバック

#### INVITED
招待通知を受領しました。

``` javascript javascript
function handleNewInvitationReceived({
    sponsor, userIDList, isFromGroup, inviteData, inviteID
}) {

}
```

パラメータは下表に示すとおりです。

| パラメータ        | タイプ    | 意味                                                                                                       |
| ----------- | ------- | ---------------------------------------------------------------------------------------------------------- |
| sponsor     | String  | 招待者                                                                                                     |
| userIDList  | Array   | 同時に招待された人                                                                                           |
| isFromGroup | Boolean | IMグループの招待の有無                                                                                           |
| inviteData  | Object  | <li/>新しいユーザーへの招待： {version, callType, roomID} <li/>最後のユーザーとの通話終了：{version, callType, callEnd} |
| inviteID    | String  | 招待ID、1回招待を表示                                                                                      |

#### CALLING_CANCEL

今回の通話はキャンセルされました。

``` javascript javascript
function handleInviterCancel() {

}
```

#### CALLING_TIMEOUT

今回の通話はタイムアウトで、応答はありませんでした。

``` javascript javascript
function handleCallTimeout() {

}
```

## TRTCCalling エラーコードリスト

EVENTのERRORフィールドを監視することによって、コンポーネントからスローされたエラーを処理することができます。サンプルコードは次のとおりです。

``` javascript javascript
import TrtcCalling from 'trtc-calling-js';
let onError = function(error) {
  console.log(error)
};
trtcCalling.on(TRTCCalling.EVENT.ERROR, onError);
```

## よくあるご質問

#### 通話がつながらなかったり、強制オフラインになったりするのはなぜですか？
コンポーネントは現在、マルチインスタンスのログインや**オフラインプッシュのシグナリング**機能をサポートしていません。現在のログインアカウントの一意性をご確認ください。
> ?
> - **マルチインスタンス**：1つのUserIDで繰り返しログインしたり、異なるターミナルからログインしたりすると、シグナリングの混乱が生じます。
> - **オフラインプッシュ**：インスタンスはオンラインの場合にのみメッセージを受信できます。インスタンスがオフラインのときに受信したシグナリングは、オンラインになった後は再度プッシュされません。
