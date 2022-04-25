TUICallingは、Tencent CloudのTRTCとIMを組み合わせたサービスであり、1v1および多人数のビデオ通話をサポートしています。TUICallingはTencent Cloudの2つのクローズドソースSDKに依存するオープンソースのClassです。具体的な実装プロセスについては、[リアルタイムビデオ通話（iOS）](https://intl.cloud.tencent.com/document/product/647/36065)をご参照ください。

- TRTC SDK：[TRTC SDK](https://intl.cloud.tencent.com/document/product/647)を低遅延のオーディオビデオ通話コンポーネントとして使用します。
- IM SDK： [IM SDK](https://intl.cloud.tencent.com/document/product/1047)をシグナリング情報の送信と処理に使用します。

## TUICalling API概要

#### SDK 基本関数

| API                                                          | 説明                   |
| :----------------------------------------------------------- | :------------------------ |
| [sharedInstance](https://intl.cloud.tencent.com/document/product/647/43139) | コンポーネントシングルトン。                |
| [call](https://intl.cloud.tencent.com/document/product/647/43139) | C2C通話に招待します。            |
| [setCallingListener](https://intl.cloud.tencent.com/document/product/647/43139) | リスナーを設定します。              |
| [setCallingBell](https://intl.cloud.tencent.com/document/product/647/43139) | 着信音を設定（30秒以内を推奨） |
| [enableMuteMode](https://intl.cloud.tencent.com/document/product/647/43139) | ミュートモードをオンにする              |
| [enableCustomViewRoute](https://intl.cloud.tencent.com/document/product/647/43139) | カスタムビューをオンにする            |

## TUICallingListener API概要

#### イベントコールバック

| API                                                          | 説明                            |
| :----------------------------------------------------------- | :------------------------------- |
| [shouldShowOnCallView](https://intl.cloud.tencent.com/document/product/647/43139) | 呼び出されたときに応答画面のプルアップをリクエストします           |
| [onCallStart](https://intl.cloud.tencent.com/document/product/647/43139) | 呼び出し開始コールバック。発呼側、着呼側ともにトリガーされます |
| [onCallEnd](https://intl.cloud.tencent.com/document/product/647/43139) | 通話コールバック。発呼側、着呼側ともにトリガーされます     |
| [onCallEvent](https://intl.cloud.tencent.com/document/product/647/43139) | 通話イベントコールバック                     |

## Type API概要

#### 通話タイプ

| enum                | 説明     |
| :------------------ | :------- |
| TUICallingTypeAudio | オーディオ通話 |
| TUICallingTypeVideo | ビデオ通話 |

## Role API概要

#### ユーザーロールタイプ

| enum                  | 説明               |
| :-------------------- | :----------------- |
| TUICallingRoleCall    | 通話発信者（発呼側） |
| TTUICallingRoleCalled | 通話受信者（着呼側） |

## Event API概要

#### イベントタイプ

| enum                       | 説明         |
| :------------------------- | :----------- |
| TUICallingEventCallStart   | 通話開始     |
| TUICallingEventCallSucceed | 通話接続成功 |
| TUICallingEventCallEnd     | 通話終了     |
| TUICallingEventCallFailed  | 通話失敗     |

## SDK基本関数

### sharedInstance

shareInstanceはTUICallingManagerのコンポーネントシングルトンです。


```objc
+ (instancetype)shareInstance;
```

### call

C2C通話に招待します。


```objc
- (void)call:(NSArray<NSString *> *)userIDs type:(TUICallingType)type;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ           | 意味                |
| :------ | :------------- | :------------------ |
| userIDs | NSArray        | 通話ユーザーIDリスト    |
| type    | TUICallingType | 通話タイプ：オーディオ/ビデオ |

### setCallingListener

リスナーを設定します。

```objc
- (void)setCallingListener:(id<TUICallingListerner>)listener;
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ               | 意味                  |
| :------- | :----------------- | :-------------------- |
| listener    | TUICallingListener  | TUIcallingコンポーネントリスナー   |

### setCallingBell

着信音を設定します（30s以内を推奨）。

```objc
- (void)setCallingBell:(NSString *)filePath;
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ     | 意味         |
| :------- | :------- | :----------- |
| filePath    | NSString  | 着信音リソースパス   |

### enableMuteMode

ミュートモードをオンにします。

```objc
- (void)enableMuteMode:(BOOL)enable;
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ | 意味             |
| :----- | :--- | :--------------- |
| enable    | BOOL  | ミュートモード有効化の有無   |

### enableCustomViewRoute

カスタムビューをオンにします。
オンにすると、呼び出し/被呼び出し開始コールバックの中で、CallingViewControllerのインスタンスを受信します。開発者自身が表示方式を決定します。

>! フルスクリーン表示にする必要があります。そうしない場合、表示に異常が生じます。

```objc
- (void)enableCustomViewRoute:(BOOL)enable;
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ | 意味               |
| :----- | :--- | :----------------- |
| enable    | BOOL  | カスタムビュー有効化の有無   |

## TUICallingListenerコールバック関数

### shouldShowOnCallView

呼び出された時の応答ページのプルリクエストに対する同意の有無。

```objc
- (BOOL)shouldShowOnCallView;
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ | 意味     |
| :----- | :--- | :------- |
| 戻り値    | BOOL  |  同意の有無   |

### onCallStart

呼び出し開始コールバック。発呼側、着呼側ともにトリガーされます。

```objc
 - (void)callStart:(NSArray<NSString *> *)userIDs type:(TUICallingType)type role:(TUICallingRole)role viewController:(UIViewController * _Nullable)viewController;
```

パラメータは下表に示すとおりです。

| パラメータ           | タイプ             | 意味                    |
| :------------- | :--------------- | :---------------------- |
| userIDs        | NSArray          | 通話ユーザーIDリスト        |
| type           | TUICallingType   | 通話タイプ：オーディオ/ビデオ     |
| role           | TUICallingRole   | ユーザーロールタイプ：発呼側/着呼側 |
| viewController | UIViewController | 通話ビューViewController  |

### onCallEnd

通話終了コールバック。発呼側、着呼側ともにトリガーされます。enableCustomViewRouteの設定がNOの時、このコールバックメソッドはトリガーされません。

```objc
 - (void)callEnd:(NSArray<NSString *> *)userIDs type:(TUICallingType)type role:(TUICallingRole)role totalTime:(CGFloat)totalTime;
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ           | 意味                    |
| :-------- | :------------- | :---------------------- |
| userIDs   | NSArray        | 通話ユーザーIDリスト        |
| type      | TUICallingType | 通話タイプ：オーディオ/ビデオ     |
| role      | TUICallingRole | ユーザーロールタイプ：発呼側/着呼側 |
| totalTime | CGFloat        | 通話時間。単位：秒      |

### onCallEvent

通話イベントコールバック。enableCustomViewRouteの設定がNOの時、このコールバックメソッドはトリガーされません。

```objc
- (void)onCallEvent:(TUICallingEvent)event type:(TUICallingType)type role:(TUICallingRole)role message:(NSString *)message;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ            | 意味                    |
| :------ | :-------------- | :---------------------- |
| event   | TUICallingEvent | 通話イベントタイプ。          |
| type    | TUICallingType  | 通話タイプ：オーディオ/ビデオ     |
| role    | TUICallingRole  | ユーザーロールタイプ：発呼側/着呼側 |
| message | NSString        | イベントの説明情報          |