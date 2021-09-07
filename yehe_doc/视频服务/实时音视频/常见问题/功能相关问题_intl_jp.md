[](id:que1)
### TRTCのRoomIDとは何ですか。指定できる値の区間はいくつですか。
RoomID、即ちルームナンバーは、1つのルームを一意的に示すために利用します。ルームナンバーの値の範囲は、1～4294967295です。開発者が自主的にメンテナンスとアサインを行います。

[](id:que2)
### TRTCのルーム参加UserIDとは何ですか。指定できる値の範囲はいくつですか。 
UserID、即ちユーザーIDは、1つのTRTCアプリケーションの中で、1人のユーザーを一意的に示すために利用します。長さは32バイト以下にすることを推奨します。英字、数字またはアンダーバーを使用してください。大文字小文字は区別されます。


[](id:que3)
### TRTCのルームのライフサイクルはどのくらいですか。
- ルームに最初に参加したユーザーがそのルームのオーナーとなりますが、このユーザーが自主的にルームを解散することはできません。
- 通話モードの場合：すべてのユーザーが自主的に退室したときは、バックエンドでルームが速やかに解散されます。
- **ライブストリーミングモードの場合**：最後に退室したユーザーがキャスターロールの場合、バックエンドでルームが速やかに解散されます。最後に退室したユーザーが視聴者ロールの場合、バックエンドで10分間待ってからルームが解散されます。
- ルーム内の1人のユーザーの接続が異常により切断された場合、90秒後にサーバーがこのユーザーを現在のルームから消去します。ルーム内のすべてのユーザーの接続が異常に切断された場合、90秒後にサーバーが現在のルームを自動的に解散します。
- ユーザーが参加したいルームが存在しない時は、バックエンドで1つのルームを自動作成します。

[](id:que4)
### TRTCではサブスクリプトしないオーディオ・ビデオストリーミングをサポートしていますか。 
「瞬次ON」効果を実現するため、デフォルトでは、ルームに参加すると自動サブスクリプトに設定されています。setDefaultStreamRecvModeのインターフェースで、手動サブスクリトモードに切り替えることが可能です。

[](id:que5)
### TRTCでは、Relayed PushのストリームIDのカスタマイズをサポートしていますか。  
サポートしています。enterRoomのパラメータTRTCParamsでstreamIdを指定することも、startPublishingインターフェースを呼び出して、パラメータにstreamIdを渡すことも可能です。

[](id:que6)
### TRTCライブストリーミングはどのようなロールをサポートしていますか。ロールの違いは何ですか。
ライブストリーミングのシーン（TRTCAppSceneLIVEとTRTCAppSceneVoiceChatRoom）は、TRTCRoleAnchor（キャスター）とTRTCRoleAudience（視聴者）という2つのロールをサポートしています。違いとしては、キャスターのロールはオーディオ・ビデオデータのアップロードとダウンロードを同時に行うことができますが、視聴者のロールは他人のデータのダウンロードと再生のみをサポートしていることです。switchRole() を呼び出すことにより、ロールを切り替えることができます。

[](id:que7)
### TRTCのRoleはどう理解すればいいですか。 
ライブストリーミングのシーンでのみ、キャスターと視聴者のロールを設定できます。キャスターのロール TRTCRoleAnchorは オーディオ・ビデオのアップストリーム、ダウンストリームの権限をもち、最大で同時に50人をサポートしています。視聴者TRTCRoleAudienceは、オーディオ・ビデオのダウンストリームの権限しかもちませんが、最大で同時に最大10万人をサポートしています。


[](id:que8)
### TRTCのルームではどのようなユースケースをサポートしていますか。  
以下のシーンをサポートしています。
- TRTCAppSceneVideoCall ：ビデオ通話シーン。1対1のビデオ通話、300人のビデオミーティング、オンライン診察、ビデオチャット、リモート面接などに適しています。
- TRTCAppSceneLIVE ：ビデオ・インタラクティブストリーミング。低遅延のビデオライブストリーミング、10万人の双方向対話型クラス、ビデオライブストリーミングのPK、ビデオお見合い、双方向対話型クラス、リモートトレーニング、超大型ミーティングなどに適しています。
- TRTCAppSceneAudioCall ：音声通話シーン。1対1の音声通話、300人の音声ミーティング、音声チャット、音声ミーティング、オンライン版人狼ゲームなどに適しています。
- TRTCAppSceneVoiceChatRoom：ボイス・インタラクティブストリーミング。低遅延の音声ライブストリーミング、音声ライブストリーミングのマイク接続、音声チャットルーム、カラオケ、FMラジオなどに適しています。


[](id:que9)
### TRTCはどのプラットフォームをサポートしますか。
サポートしているプラットフォームは、iOS、Android、Windows(C++)、Windows(C#)、Mac、デスクトップブラウザ、Electron、WeChat Mini Programです。詳細については、[プラットフォームのサポート](https://intl.cloud.tencent.com/document/product/647/35078)をご参照ください。

[](id:que10)
### TRTCの簡易版、プロフェッショナル版、エンタープライズ版の各版の違いは何ですか。 
詳細は [各版の相違対照表](https://intl.cloud.tencent.com/document/product/647/34615)をご参照ください。


[](id:que11)
### TRTCではライブストリーミングのマイク接続をサポートしていますか。
サポートしています。具体的な操作ガイドは以下をご参照ください。
- [オンラインライブストリーミング(iOS&Mac)](https://intl.cloud.tencent.com/document/product/647/35107)
- [オンラインライブストリーミング(Android)](https://intl.cloud.tencent.com/document/product/647/35108)
- [オンラインライブストリーミング(Windows)](https://intl.cloud.tencent.com/document/product/647/35109)
- [オンラインライブストリーミング(デスクトップブラウザ)](https://intl.cloud.tencent.com/document/product/647/35110)


[](id:que12)
### TRTCではルームを同時にいくつ作成できますか。
4,294,967,294室のルームの同時併存をサポートします。ルームの累計数は無制限です。

[](id:que13)
### ルームはどうやって作成しますか。
ルームは、Tencent Cloudのバックエンドがクライアントのルーム参加時に自動作成します。お客様は、手動でルームを作成する必要がなく、クライアントの関連インターフェースを呼び出して「ルームに参加」するだけで済みます。
- [iOS & Mac > enterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d)
- [Android > enterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#abfc1841af52e8f6a5f239a846a1e5d5c)
- [Windows(C++) > enterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#ac73c4ad51eda05cd2bcec820c847e84f)
- [Windows(C#) > enterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a28b2d3ec27af8c9bfd5cf687dd8e002b)
- [Electron > enterRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#enterRoom)
- [デスクトップブラウザ > join](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#join)

  

[](id:que14)

### TRTCのビデオサーバーがサポートする帯域幅は最大でいくつですか。
制限はありません。


[](id:que15)
### TRTCはプライベート化したデプロイをサポートしていますか。
現在サポートしていません。

[](id:que16)
### TRTCでRelayed live streamingをアクティブ化した場合、利用にはドメイン名のICP登録が必要ですか。
Relayed live streamingをアクティブ化する必要がある場合は、国の関連部門の要件に基づき、再生ドメイン名のICP登録をしないと使用できません。詳細は[CDN Relayed live Streaming](https://intl.cloud.tencent.com/document/product/647/35242)をご参照ください。

[](id:que17)
### TRTCの遅延はどのくらいですか。
グローバルなエンドツーエンドの平均遅延は300ms未満です。

[](id:que18)
### TRTCは主動的な呼出機能をサポートしていますか。
シグナリングチャネルを結合して解決する必要がある場合、例えば [IM](https://intl.cloud.tencent.com/zh/document/product/1047) サービスのカスタムメッセージを使用して呼び出す場合は、[SDK](https://intl.cloud.tencent.com/document/product/647/34615) ソースコードのシーンのDemo例を参考にできます。

[](id:que19)

### TRTCの2人用ビデオ通話では、Bluetoothのイヤホンをサポートしていますか。
サポートしています。


[](id:que20)
### TRTCは海外での利用をサポートしていますか。
サポートしています。

[](id:que21)
### TRTCのPCアクセスポートは画面共有機能をサポートしていますか。
サポートしています。次のドキュメントをご参照ください。
- [画面共有(Windows)](https://intl.cloud.tencent.com/document/product/647/37335)
- [画面共有(Mac)](https://intl.cloud.tencent.com/document/product/647/37336)
- [画面共有(デスクトップブラウザ)](https://intl.cloud.tencent.com/document/product/647/35163)

画面共有インターフェースの詳細は[Windows（C++）API](https://intl.cloud.tencent.com/document/product/647/35131) または[Windows（C#）API](https://intl.cloud.tencent.com/document/product/647)をご参照ください。そのほか、[Electronインターフェース](https://intl.cloud.tencent.com/document/product/647/35141)もご使用になれます。

[](id:que23)

### ローカルのビデオファイルをTRTCの中で共有する機能をサポートしていますか。

サポートしています。[ユーザー定義キャプチャ](https://intl.cloud.tencent.com/document/product/647/35158)機能によって実現できます。

[](id:que24)
### TRTCでは、ライブストリーミングでレコーディングしたビデオを、ローカルの携帯電話に保存することはできますか。
ローカルの携帯電話への直接保存はサポートしていません。レコーディング後は、ビデオファイルはデフォルトでVODプラットフォームに保存されますので、ご自分でダウンロードして携帯電話に保存できます。詳細は [クラウドレコーディングおよび再生](https://intl.cloud.tencent.com/document/product/647/35426)をご参照ください。


[](id:que25)
### TRTCでは単純な音声だけのRTCもサポートしていますか。
音声だけもサポートしています。


[](id:que26)
### 1つのルームで同時にいくつの画面を共有できますか。
現在、1つのルームで共有できるのはサブストリームの画面1つのみです。

[](id:que27)
### ウィンドウの共有（SourceTypeWindow）を指定し、ウィンドウのサイズが変化した場合は、ビデオストリームの解像度も変化しますか。
デフォルトでは、SDK内で共有ウィンドウのサイズに従ってエンコーディングパラメータを自動的に調整します。
解像度を固定する必要がある場合は、setSubStreamEncoderParamインターフェースを呼び出し画面共有のエンコーディングパラメータを設定するか、またはstartScreenCaptureを呼び出すときに、対応するエンコーディングパラメータを指定する必要があります。


[](id:que28)
### TRTCでは1080Pをサポートしていますか。
サポートしています。SDKのビデオコーデックパラメータsetVideoEncoderParamで、解像度を設定できます。

[](id:que29)
### TRTCではデータキャプチャのカスタマイズが可能ですか。
一部のプラットフォームはサポートしています。詳細情報は[ユーザー定義キャプチャとレンダリング](https://intl.cloud.tencent.com/document/product/647/35158)をご参照ください。

[](id:que30)
### TRTCは、インタラクティブライブSDKと通信できますか。
できません。

[](id:que31)
### TRTCは、モバイルライブストリーミングと通信できますか。 
TRTCとモバイルライブストリーミングはバックグラウンド方式のアーキテクチャが異なりますので、直接的な相互通信はサポートされていません。TRTCのバックグラウンドからCDNに向けてRelayed Pushすることのみ可能です。



[](id:que32)
### TRTCのルーム参加モードAppSceneにはどのような区別がありますか。
TRTCは、4種類の異なる入室モードをサポートしています。このうち、ビデオ通話（VideoCall）および音声通話（VoiceCall）を総称して通話モードといい、ビデオ・インタラクティブストリーミング（Live）およびボイス・インタラクティブストリーミング（VoiceChatRoom）を総称してライブストリーミングモードといいます。
- 通話モードでのTRTCは、1つのルームに最大で300人の同時オンラインをサポートし最大で50人の同時発言をサポートします。1対1のビデオ通話、300人のビデオミーティング、オンライン問診、リモート面接、ビデオカスタマーサービス、オンライン人狼ゲームなどのユースケースに適合しています。
- ライブストリーミングモードでのTRTCは、1つのルームで最大10万人の同時接続をサポートし、300ms未満のマイク接続遅延、1000ms未満の視聴遅延およびマイクのオン・オフのスムーズな切り替え技術を備えています。低レイテンシーインタラクティブストリーム、10万人のインタラクティブ教室、ビデオ婚活、eラーニング、リモート研修、超大規模ミーティングなどのユースケースに適しています。


[](id:que33)
### TRTCではオーディオビデオ通話のハンズフリーモードをサポートしていますか。
サポートしています。ハンズフリーモードはオーディオルートを設定して実現し、Native SDKはsetAudioRouteインターフェースを使用して切り替え、ミニプログラムは&lt;live-player&gt;タグのsound-mode属性を使用して設定します。

[](id:que34)
### TRTCでは音量のボリューム表示をサポートしていますか。
サポートしています。enableAudioVolumeEvaluationインターフェースから起動できます。

[](id:que35)
###  TRTCではミラーリング画面の設定をサポートしていますか。 
サポートしています。setLocalViewMirrorインターフェースでローカルカメラのプレビュー画面をミラーリングモードに設定するか、またはsetVideoEncoderMirrorインターフェースでエンコーダーが出力する画面をミラーリングモードに設定します。

[](id:que36)
### TRTCでは、通話プロセスの音声をローカルファイルにレコーディングする機能をサポートしていますか。 
サポートしています。startAudioRecordingインターフェースで通話プロセスの全ての音声（ローカル音声、リモート音声、BGMなど）を1つのファイルにレコーディングできます。現在サポートしている音声ファイル形式はPCM、WAV、AACです。

[](id:que37)
### TRTCでは、インタラクティブな音声ビデオ通信のプロセスのビデオをファイルにレコーディングする機能をサポートしていますか。
ご自分のサーバーによるレコーディング（録音/録画）をサポートしています。使用する必要がある場合は、 [チケットを提出](https://console.cloud.tencent.com/workorder/category)でご連絡の上、SDKおよび関連ガイドを取得してください。
[クラウドレコーディングと再生の実現](https://intl.cloud.tencent.com/document/product/647/35426) を使用してビデオをレコーディングすることもできます。

[](id:que38)
### TRTCでは、WeChatのビデオ通話のようなフローティングウィンドウ、大小画面の切り替え等の機能をサポートしていますか。
こういった機能は UIのレイアウトロジックに属しますが、SDKにUIのディスプレイ処理の制限はありません。公式Demoの中では、画面前後のStackと9グリッドのレイアウトモードのサンプルコードを提供し、フローティングウィンドウ、大小画面切り替え、画面ドラッグ等の機能もサポートしています。より詳しい情報は、 [公式Demo](https://github.com/tencentyun/TRTCSDK)をご参照ください。

[](id:que39)
### TRTCで純音声通話を実現させるにはどうすればいいですか。
TRTCには音声チャネルとビデオチャネルの区別はありません。startLocalAudioを呼び出し、startLocalPreview を呼び出さなければ、純音声通話モードになります。

[](id:que40)
### TRTCの純音声通話でRelayed Pushとレコーディングを実現するにはどうすればいいですか。
- 6.9以前のバージョンの場合、ルーム参加時に`json{\"Str_uc_params\":{\"pure_audio_push_mod\":1}}`と記述し、TRTCParams.businessInfoに渡す必要があります。1はRelayed Push、2はRelayed Push+レコーディングを表します。
- TRTC SDK 6.9以降のバージョンでは、ルーム参加時にシーンのパラメータでTRTCAppSceneAudioCallまたは TRTCAppSceneVoiceChatRoomを選択すれば実現できます。

[](id:que41)
### TRTCルームは、キックアウト、発言の禁止、ミュートをサポートしていますか。  
サポートしています。
- 簡単なシグナリング操作の場合、TRTCのカスタムシグナルインターフェースsendCustomCmdMsgを使用できます。開発者が対応する制御シグナリングをカスタマイズして、制御シグナリングを受信した通話者が対応する操作を実行すればOKです。例えば、キックアウトとは、追い出しシグナリングを定義することであり、この信号を受信したユーザーは自動的に退室します。
- より完全な操作ロジックを実行する必要がある場合は、開発者が[IM]（https://intl.cloud.tencent.com/zh/document/product/1047）を使用して関連のロジックを実行し、TRTCルームとIMグループとのマッピングを行い、IMグループでカスタムメッセージを送受信して、対応する操作を実行することをお勧めします。

[](id:que42)

### TRTCでは、プルされたRTMP/FLV形式のストリーミング再生をサポートしていますか。  
サポートしています。現在すでにTRTC SDKの中に TXLivePlayerがパッケージングされています。より多くのプレーヤー機能が必要な場合は、LiteAVSDK_Professionalバージョンを直接使用すれば、すべての機能が含まれています。

[](id:que43)
### TRTCは最大何人の同時通話をサポートできますか。
- 通話モードでは、1ルームあたり最大300人の同時接続、最大50人のカメラまたはマイクの同時使用をサポートしています。
- ライブストリーミングモードでは、1ルームあたり視聴者10万人のオンライン視聴と、キャスター50人のカメラまたはマイクの使用をサポートしています。


[](id:que44)
###  TRTCはライブストリーミングのシーン類のアプリケーションをどのように実現しますか。
TRTCは、特にオンラインライブストリーミングのシーン向けに、10万人向けの低遅延ライブストリーミングソリューションをリリースしました。これにより、キャスターとマイク接続したキャスター間の最小遅延が200ms、通常の視聴者の遅延が1秒以内になるだけでなく、脆弱なネットワークに極めて高い耐性を持つこととなり、モバイル端末の複雑なネットワーク環境に対応します。
操作ガイドの詳細は[ライブストリーミングクイックスタートモード](https://intl.cloud.tencent.com/document/product/647/35107)をご参照ください。

[](id:que45)
### TRTCのカスタムメッセージ送信のインターフェースを利用して、チャットルーム、弾幕等の機能を実現できますか。
できません。TRTCのカスタムメッセージの送信は、簡単な低周波のシグナリング伝送のシーンに適用されます。制限の詳細は[使用制限](https://intl.cloud.tencent.com/document/product/647/35159)をご参照ください。

[](id:que46)
### TRTC SDKのBGM再生では、繰り返し再生をサポートしていますか。BGM再生の進行状況を調整する機能をサポートしていますか。  
サポートしています。繰り返し再生は完了コールバック中に再度呼び出して再生します。再生の進捗はTXAudioEffectManager seekMusicToPosInMSによって設定できます。

>?  setBGMPosition() はv7.3 バージョンで廃止されています。 TXAudioEffectManager seekMusicToPosInMSに切り替わっています。

[](id:que47)
### TRTCにはルームメンバーのルーム入退室をモニタリングするコールバックがありますか。onUserEnter/onUserExitを使用できますか。
あります。TRTCでは onRemoteUserEnterRoom/onRemoteUserLeaveRoom を使用してルームメンバーのルーム入退出を監視しています（アップストリームオーディオ・ビデオ権限があるユーザーのみ起動できます）。
>?onUserEnter/onUserExitは6.8バージョンで廃止され、onRemoteUserEnterRoom/onRemoteUserLeaveRoom経由に切り替わっています。

[](id:que48)
### TRTCでは回線の切断と再接続をどのようにモニタリングしますか。
以下のコールバックのモニタリングによって行います。
- onConnectionLost：SDKとサーバーの間の接続が切断。
- onTryToReconnect：SDKがサーバーへの再接続を試行。
- onConnectionRecovery：SDKとサーバー間の接続回復。

[](id:que49)
### TRTCには最初のフレームのレンダリングのコールバックはありますか。画面のレンダリング開始、音声の再生開始のモニタリングはできますか。
サポートしています。onFirstVideoFrame/onFirstAudioFrameでモニタリングできます。

[](id:que50)
### TRTCではビデオ画面のスクリーンキャプチャ機能をサポートしていますか。
現在iOS/Android端末では、snapshotVideo() を呼び出すことで、ローカルおよびリモートのビデオ画面スクリーンキャプチャをサポートしています。

[](id:que51)
### TRTCではBluetoothイヤホン等の外付けデバイスとの接続に異常はありますか。
現在、TRTCでは主流のBluetoothイヤホンや外付けデバイスとは互換性がありますが、それでも互換性に問題のあるデバイスに遭遇することがあり得ます。公式DemoやWeChat、QQのオーディオビデオ通話の比較を利用し、正常かどうか確認することをお勧めします。

[](id:que52)
### TRTCのオーディオ・ビデオのプロセスでのアップストリーム、ダウンストリームのビットレート、解像度、パケット損失率、オーディオサンプルレート等の情報はどうすれば取得できますか。
SDKのインターフェースonStatistics()でこれらの統計情報を取得できます。

[](id:que53)
### TRTCのBGM再生インターフェースplayBGM() はオンラインミュージックをサポートしていますか。
現在はローカルの音楽のみサポートしています。先にローカルにダウンロードしてから、playBGM()を呼び出して再生することが可能です。

[](id:que54)
### TRTCではローカルでキャプチャする音量の設定機能をサポートしていますか。各リモートユーザーの再生音量の設定機能をサポートしていますか。
サポートしています。setAudioCaptureVolume() インターフェースでSDKのキャプチャ音量を設定可能です。また、setRemoteAudioVolume()インターフェースで特定のリモートユーザーの再生音量を設定できます。

[](id:que55)
### stopLocalPreviewとmuteLocalVideoの違いは何ですか。
- stopLocalPreviewは、ローカルでのビデオキャプチャを停止します。このインターフェースを呼び出すと、自らのローカルとリモートの画面をブラックアウトさせます。
- muteLocalVideoは、バックグラウンドに向けて自らのビデオ画面を送信するかを設定します。このインターフェースを呼び出すと、他のユーザーが視聴していた画面はブラックアウトしますが、自らのローカルのプレビュー画面はまだ見ることができます。

[](id:que56)
### stopLocalAudioとmuteLocalAudioの違いは何ですか。 
- stopLocalAudioは、ローカル音声のキャプチャとアップストリームをオフにします。
- muteLocalAudioでは、音声・ビデオデータの送信は停止されず、ビットレートが極めて低いミュートパケットが引き続き送信されます。

[](id:que57)
### TRTC SDKではどの解像度をサポートしていますか。
[画質の設定](https://intl.cloud.tencent.com/document/product/647/35153)を参照し、より適切な画質になるまで解像度を設定することを推奨します。

[](id:que58)
### TRTC SDKではアップストリームのビデオビットレート、解像度、フレームレートをどのように設定しますか。 
TRTCCloudのsetVideoEncoderParam()インターフェースで、TRTCVideoEncParamパラメータの中のvideoResolution（解像度）、videoFps（フレームレート）、videoBitrate（ビットレート）を設定できます。

[](id:que59)
### SDKの画面の角度と方向の制御はどうすれば実現できますか。  
詳細は、[ビデオ画面の回転とズーム](https://intl.cloud.tencent.com/document/product/647/35154)をご参照ください。

### TRTCでローカルとリモートの画面方向が一致しない場合はどうやって調整しますか。  
詳細は、[ビデオ画面の回転とズーム](https://intl.cloud.tencent.com/document/product/647/35154)をご参照ください。


[](id:que62)
### TRTC には推奨する画質（ビットレート、解像度、フレームレート）関連のパラメータ設定はありますか。
詳細は、[推奨設定](https://intl.cloud.tencent.com/document/product/647/35153#.E6.8E.A8.E8.8D.90.E7.9A.84.E9.85.8D.E7.BD.AE)をご参照ください。

[](id:que63)
### TRTCではネットワークの速度テストをサポートしていますか。どうやって操作しますか。  
詳細は、[通話前ネットワークテスト](https://intl.cloud.tencent.com/document/product/647/35156)をご参照ください。

[](id:que64)
### TRTCではルームに対する権限の検証をサポートしていますか（例：検証に合格してから会員がシーンに参加できるなど）。 
サポートしています。詳細は、[ルーム参加権限の保護](https://intl.cloud.tencent.com/document/product/647/35157)をご参照ください。

[](id:que65)
### TRTCオーディオ・ビデオストリーミングは、CDNを介したプルストリームによる視聴をサポートしていますか。 
サポートしています。詳細は、[CDN relayed live streamingの実装](https://intl.cloud.tencent.com/document/product/647/35242)をご参照ください。

[](id:que66)
### TRTCのカスタムレンダリングはどの形式をサポートしていますか。 
- iOS端末ではi420、NV12、BGRAをサポートしています。
- Android端末ではI420とtexture2dをサポートしています。

[](id:que67)
### TRTCとは何ですか。
Tencent Real-Time Communication（TRTC）は、Tencentが長年に渡り蓄積したネットワークとオーディオ・ビデオ技術をベースに、多人数のオーディオビデオ通話と低遅延インタラクションライブストリーミングの、シナリオ化した2大ソリューションを提供し、Tencent Cloudのサービスを通じて開発者向けに開放します。これにより、開発者が低コスト、低遅延、高品質のインタラクティブな音声ビデオソリューションを迅速に構築するのを支援します。詳細は、[製品概要](https://intl.cloud.tencent.com/document/product/647/35078)をご参照ください。

[](id:que68)
### TRTCのDemoはどのように体験できますか。
具体的な内容は、[Demo体験](https://intl.cloud.tencent.com/document/product/647/35076)をご参照ください。

[](id:que69)
### TRTCはどのようにクイックスタートしますか。
TRTCは各プラットフォームのDemoソースコードを提供します。わずかな時間で自分のミニアプリケーションを直ちに構築することができます。具体的な内容は[初心者向け（入門編）](https://intl.cloud.tencent.com/document/product/647/39386)をご参照ください。

[](id:que70)
### TRTCはどのようにクラウドレコーディングと再生を実現しますか。
具体的な内容は[クラウドレコーディングと再生の実現](https://intl.cloud.tencent.com/document/product/647/35426)をご参照ください。






