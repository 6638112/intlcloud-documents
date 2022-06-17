## 学習目標

VODでは、リンク不正アクセス防止設定をサポートし、有効時間、再生人数、再生時間などの制御を実装しています。本段階のチュートリアルを学習すると、リンク不正アクセス防止を有効にした後に、Super playerを使用してビデオを再生する方法を理解できるようになります。

これを読む前に、先にSuper playerガイドの[段階1：Super playerを使用したビデオ再生](https://intl.cloud.tencent.com/document/product/266/38098)セクションを確実に学習しておいてください。このチュートリアルでは[段階1](https://intl.cloud.tencent.com/document/product/266/38098)セクションでアクティブ化したアカウントおよびアップロードしたビデオを使用します。

## 手順1：リンク不正アクセス防止の有効化

アカウントにおけるデフォルトの配信ドメイン名でKeyリンク不正アクセス防止を有効にしたケースを例にします。
>!本番環境の現行のネットワークドメイン名に対してリンク不正アクセス防止を直接有効にしないでください。現行のネットワークのビデオが再生できなくなります。

1. VODコンソールにログインし、【配信と再生の設定】>[【ドメイン名の管理】](https://console.cloud.tencent.com/vod/distribute-play/domain)と選択し、「デフォルトの配信ドメイン名」の下の【設定】をクリックして、設定画面に入ります。
<img src="https://main.qcloudimg.com/raw/06259e41a62ea14ce8eb19ef6480182c.png" width="800" />
2. 「Keyリンク不正アクセス防止」の右側の【編集】をクリックして、【Keyリンク不正アクセス防止の有効化】を開き、【ランダムKeyの生成】をクリックしてランダムKey（2WExxx48eW）を生成します。生成できたKeyをコピーしてから、【OK】をクリックすると保存が有効になります。
![](https://qcloudimg.tencent-cloud.cn/raw/1b4f1f0d9e3d36c153b1e91f64160f00.png)

## 手順2：プレビューによる再生体験

前の手順では、デフォルトの配信ドメインに対するリンク不正アクセス防止を有効化しました。ここでは、3種類の端末のSuper playerを使用して、再生の効果を素早く体験します。

1. 【メディア資産管理】>[【ビデオ管理】](https://console.cloud.tencent.com/vod/media)と選択して、**手順1**のアップロードおよび処理済みのビデオを探し、「操作」バーの下の【管理】をクリックして、【Super playerプレビュー】を選択します。
2. 【Super player設定】はdefaultを選択します。
>? defaultはプリセットのSuper player設定で、テンプレート10のアダプティブビットレートストリーミングへのトランスコードの出力、テンプレート10のキャプチャしたスプライトイメージの出力に使用します。

 <img src="https://qcloudimg.tencent-cloud.cn/raw/e66e46d10480c5fb00a2881b275a9cdc.png" width="500" />
3. デフォルトの配信ドメイン名がリンク不正アクセス防止を有効にしているため、【再生制御】のタブで、プレビュー時のリンク不正アクセス防止の期限切れ時間、テスト視聴時間などの選定をサポートしています。ここではデフォルトのパラメータを維持します（再生のリンク不正アクセス防止の期限切れ時間はデフォルトで1日、プレビュー時間、最大再生可能IP数は入力しません）。
 <img src="https://qcloudimg.tencent-cloud.cn/raw/f08e553a9519fb9974935374f4b4051d.png" width="522" />
4. 【Webプレーヤー】の中で、プレーヤーの中央のボタンをクリックすると、Web端末での再生が体験できます。
<img src="https://main.qcloudimg.com/raw/976ec23a988bcb494c4b225e635a5dba.png" width="522" />
5. 【モバイルプレイヤー】の中で、【QRコードをスキャンしてダウンロードする】をクリックして、「Tencent Cloud Toolkit」をインストールします。
<img src="https://qcloudimg.tencent-cloud.cn/raw/f0e72b414ee3dc8084dda39d8a5d5c91.png" style="zoom:67%;" />
6. モバイル端末で再生・体験するには、携帯電話でTencent Cloud Toolkitを開き、【Player】>【Super Player】を選択してから、右上隅のボタンをクリックしてQRコードをスキャンします。
 <img src="https://qcloudimg.tencent-cloud.cn/raw/06e77f14c2e1020e8936ce1ab30a6ca3.png" width="522" />

## 手順3：Demoを使用して検証

リンク不正アクセス防止を有効にした後、ビデオを再生できるようにするためには、Super playerに有効期限内の署名を使用する必要があります。署名ツールを使用して署名クイック発行できます。

1. [Super player - 署名生成ツール](https://vods.cloud.tencent.com/signature/super-player-sign.html)の画面を開き、パラメータを入力します。

 * 【ユーザーappId】：ビデオが属するappId：1400xxx357を入力します（使用するのがサブアプリケーションの場合は、サブアプリケーションのappIdを入力します）。
 * 【ビデオfileId】：ビデオのfileId：528xxx3757278095を入力します。
 * 【現在のUnixタイムスタンプ】：ツールが自動的に生成した現在のUnix時間（1591516390）。入力不要です。
 * 【署名期限切れUnix タイムスタンプ】：署名自身の期限切れ時間。未入力可、デフォルトは1日後に期限切れ。
 * 【リンク期限切れ時間】：Keyリンク不正アクセス防止期限切れ時間。6時間後の16進数Unix 時間：5edcf146を入力します。
 * 【リンク不正アクセス防止Key】：前のステップで取得したリンク不正アクセス防止Key：2WExxx48eWを入力します。

2. 【署名の生成】をクリックします。生成された署名が「署名生成結果」のテキストボックスに表示されます。


Super Playerの署名を取得すると、[Web](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-base.html)、[Android](https://github.com/LiteAVSDK/Player_Android)、[iOS](https://github.com/LiteAVSDK/Player_iOS)の3種類の端末のSuper PlayerのDemoを使用してそれぞれ検証することができます。詳細については、Demoのソースコードをご参照ください。
>?コンソールの【メディア資産管理】>[【ビデオ管理】](https://console.cloud.tencent.com/vod/media)>【Super playerプレビュー】の中で、プレビューのビデオに対応するWebプレーヤーのソースコードを取得でき、これを直接参照して使用できるようにしています。
<img src="https://main.qcloudimg.com/raw/c5756910c7958aae198804c91b76a89e.png" width="500" />

## まとめ

このチュートリアルの学習を終え、リンク不正アクセス防止を有効にすると、Super playerを使用してビデオを再生する方法を把握したことになります。

次のことをしたい場合：
- ビデオ再生時のコンテンツと形式をカスタマイズする場合は、[段階3：再生コンテンツと形式のカスタマイズ](https://intl.cloud.tencent.com/document/product/266/38293)をご参照ください。
- ビデオを暗号化し、暗号化後のビデオを再生する場合は、[段階4：暗号化したビデオの再生](https://intl.cloud.tencent.com/document/product/266/38294)をご参照ください。


