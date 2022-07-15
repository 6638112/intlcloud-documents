>? [CSS価格計算ツール](https://buy.cloud.tencent.com/price/css/calculator)によって、標準ライブストリーミングおよびライブイベントストリーミングの関連料金の見積を行うことができます。

CSSの課金項目には、基本サービス料金と付加価値サービス料金が含まれます。Tencent Cloudのその他製品と連携させて提供する付加価値機能には、拡張サービス料金が発生します。料金の構成は下図のとおりです。

![](https://qcloudimg.tencent-cloud.cn/raw/7970d2961c95cd19a4e7568f3ea60467.png)


- [基本サービス料金](#base)：CSS（標準ライブストリーミングとライブイベントストリーミング）の使用後に発生するライブストリーミング消費費用。標準ライブストリーミングとライブイベントストリーミングでは、トラフィックまたは帯域幅ピーク値の2種類の課金方式を切り替えることができます。
- [付加価値サービス料金](#appreciation)：CSSトランスコード、レコーディング、スクリーンキャプチャ、ポルノ検出、タイムシフト、プル転送などの付加価値機能を使用した時の料金。これらの機能はデフォルトでは無効になっており、使用する場合のみ課金されます。
- [拡張サービス料金](#extensions)：他のTencent Cloud製品と連携させて提供する付加価値機能は、他のクラウド製品では、それぞれの課金ルールに従って、別途関連料金が課金されます。

[](id:base)
## 基本サービス料金

基本サービス料金は、CSSのサービスによって、標準ライブストリーミングサービス料金とライブイベントストリーミングサービス料金に分かれます。

<table>
<tr><th width="20%">課金項目</th><th width="60%">課金説明</th><th>支払い方法</th></tr>
<tr>
<td>標準ライブストリーミングトラフィック<br>（デフォルト）</td>
<td>
<li/>標準ライブストリーミングのプッシュストリームおよびプルストリームで発生するアップリンクおよびダウンリンクのトラフィック消費は、デフォルトではダウンリンクの再生料金のみかかります。
<li/>中国本土、中国本土以外の課金標準はそれぞれ異なります。
</td>
<td>
<li><a href="https://intl.cloud.tencent.com/document/product/267/2818">後払い-日次決済</a></li>
<li/>後払い-月次決済
</td>
</tr><tr>
<td>標準ライブストリーミング帯域幅ピーク値</td>
<td>
<li/>標準ライブストリーミングのプッシュストリームおよびプルストリームで発生するアップリンクおよびダウンリンクの帯域幅ピーク値は、デフォルトではダウンリンクの再生料金のみかかります。
<li/>中国本土、中国本土以外の課金標準はそれぞれ異なります。
</td><td>
<li/><a href="https://intl.cloud.tencent.com/document/product/267/2818">後払い-日次決済</a>
<li/>後払い-月次決済
</td>
</tr><tr>
<td>ライブイベントストリーミングトラフィック<br>（デフォルト）</td>
<td>
<li/>ライブイベントストリーミングのプッシュストリームおよびプルストリームで発生するアップリンクおよびダウンリンクのトラフィック消費は、デフォルトではダウンリンクの再生料金のみかかります。
<li/>中国本土、中国本土以外の課金標準はそれぞれ異なります。
</td>
<td>
<li/><a href="https://intl.cloud.tencent.com/document/product/267/39969">後払い-日次決済</a>
<li/>後払い-月次決済
</td>
</tr><tr>
<td>ライブイベントストリーミング帯域幅ピーク値</td>
<td>
<li/>ライブイベントストリーミングのプッシュストリームおよびプルストリームで発生するアップリンクおよびダウンリンクの帯域幅ピーク値は、デフォルトではダウンリンクの再生料金のみかかります。
<li/>中国本土、中国本土以外の課金標準はそれぞれ異なります。
</td>
<td>
<li/><a href="https://intl.cloud.tencent.com/document/product/267/39969">後払い-日次決済</a>
<li/>後払い-月次決済
</td>
</tr></table>


>! 
>- ライブイベントストリーミングは超低遅延リンクを採用しているため、トラフィック/帯域幅料金は標準ライブストリーミングより若干高くなります。
>- CSSでは、毎月のニーズが高いユーザーに対して、より柔軟な月次決済方式を提供しています。 必要な場合は、Tencent Cloudのビジネスマネージャーに連絡して、課金方式の変更をサポートしてもらうことができます。
>- 課金方式を選択し直す必要がある場合は、[課金の変更](https://intl.cloud.tencent.com/document/product/267/30411)をご参照ください。  

[](id:appreciation)

## 付加価値サービス料金

<table>
<tr><th colspan=2 width="20%">課金項目</th><th width="60%">課金説明</th><th>支払い方法</th></tr>
<tr>
<td rowspan=3>CSSトランスコード</td>
<td>標準トランスコーディング</td>
<td><ul style="margin:0">
<li/>CSSの標準トランスコーディング機能を使用したときに課金されます。
<li/><a href="https://intl.cloud.tencent.com/document/product/267/31064">CSSウォーターマーク</a>、<a href="https://intl.cloud.tencent.com/document/product/267/31071">標準トランスコーディング</a>、<a href="https://intl.cloud.tencent.com/document/product/267/37665">ライブミクスストリーミング</a>などの機能を使用したときは、標準トランスコーディングの料金が発生します。
<li/>発生した料金は<b>トランスコーディングの時間に応じて課金され</b>、CSSストリームを出力する画面サイズに対応する価格が料金の単価となります。
</ul></td>
<td>
  <li><a href="https://intl.cloud.tencent.com/document/product/267/39604">後払い-日次決済</a></li></ul>
	<li/>後払い-月次決済
</td>
</tr><tr>
<td>高速高画質トランスコーディング</td>
<td><ul style="margin:0">
<li/>ライブストリーミングの高速高画質トランスコーディング機能を使用したときに課金されます。
<li/> <a href="https://intl.cloud.tencent.com/document/product/267/31071">高速高画質トランスコーディング</a>の機能を使用したときは、高速高画質トランスコーディングの料金が発生します。
<li/>発生した料金は<b>トランスコーディングの時間に応じて課金され</b>、CSSストリームを出力する画面サイズに対応する価格が料金の単価となります。
</ul><td>
<li><a href="https://intl.cloud.tencent.com/document/product/267/39604">後払い-日次決済</a></li>
<li/>後払い-月次決済
</td>
</tr><tr>
<td>オーディオトランスコード</td>
<td>
<li/>ライブストリーミングのオーディオトランスコード機能を使用したときに課金されます。
<li></li><a href="https://intl.cloud.tencent.com/document/product/267/31071">オーディオトランスコード</a>、オーディオミクスストリーミングなどの機能を使用するときは、いずれもオーディオトランスコード料金が発生します。
<li/>発生した料金は、<b>オーディオトランスコードの時間に応じて課金されます</b>。
<td>
<li><a href="https://intl.cloud.tencent.com/document/product/267/39604">後払い-日次決済</a></li>
<li/>後払い-月次決済
</td>
</tr><tr>
  <td colspan=2>CSSレコーディング</td>
  <td>
    <li>CSSレコーディングでは、レコーディングテンプレートに従ってレコーディングファイルを生成し、VODに保存します。</li>
    <li>レコーディングで発生するサービス料金は、<b>標準ライブストリーミングレコーディングのチャンネル数のピーク値に応じて課金されます</b>。</li>
  </td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/39605">後払い-月次決済</a></td>
</tr><tr>
<td colspan=2>CSSスクリーンキャプチャ</td>
<td>
  <li>CSSスクリーンキャプチャは、テンプレートに従って定期的にCSSストリームのスクリーンをキャプチャし、画像をCOSに保存します。</li>
  <li>スクリーンキャプチャで発生するサービス料金は、<b>スクリーンキャプチャの枚数に応じて課金されます</b>。毎月の最初の1,000枚は無料です。</li>
</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/39606">後払い-月次決済</a></td>
</tr><tr>
  <td colspan=2>インテリジェントポルノ検出</td>
  <td>スクリーンキャプチャによるポルノ検出では、ポルノ検出とスクリーンキャプチャという2つの料金が発生します。
    <li>ポルノ検出で発生するサービス料金は、<b>ポルノ検出の枚数に応じて課金され</b>、毎月の最初の1,000枚は無料です。</li>
    <li>スクリーンキャプチャで発生するサービス料金は、<b>スクリーンキャプチャの枚数に応じて課金されます</b>。毎月の最初の1,000枚は無料です。</li>
</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/39607">後払い-月次決済</a></td>
</tr><tr>
<td colspan=2>ライブストリーミングSDK  License</td>
<td>
モバイルライブストリーミングベーシック版SDKのiOSとAndroidにおける使用権限のロック解除に用いられます。担当者にご連絡いただき、モバイルライブストリーミングSDK Licenseをご購入ください。
</td>
<td>-</td>
</tr><tr>
<tr><td colspan=2>プル転送</td>
<td>タスクのプル転送はタスク時間に応じて料金が発生します。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/41059">後払い-日次決済</a>
</td>
</tr><tr>
<td colspan=2>サードパーティへのプル転送料金</td>
<td>現在のアカウントではないCSSプッシュアドレスはすべてサードパーティアドレスであり、サードパーティへのプル転送の帯域幅に応じた料金が発生します。</td>
<td>
<a href="https://intl.cloud.tencent.com/document/product/267/41059">後払い-月次決済</a>
</td>
</tr><tr>
<td colspan=2>CSSタイムシフト</td>
<td>
CSSタイムシフトはタイムシフト合計時間に基づいて課金されます。
</td>
<td><a href="https://intl.cloud.tencent.com/zh/document/product/267/47534">後払い-日次決済</a>
</td>
</tr>
</table>

[](id:extensions)

## 拡張サービス料金

<table>
<tr><th width="20%">課金項目</th><th width="60%">課金説明</th><th>支払い方法</th></tr>
<tr>
<td>レコーディングの保存</td>
<td>>CSSレコーディングのファイルはVODに保存する必要があり、発生したサービス料金は、<b>データの実際の保存時間とストレージ容量に応じて課金されます</b>。VOD保存料金が別途必要です。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/266/14666">VOD-従量課金</a></td>
</tr><tr>
<td>スクリーンキャプチャの保存</td>
<td> CSSスクリーンキャプチャとポルノ検出で生成したスクリーンキャプチャのファイルはCOSに保存する必要があり、発生したサービス料金は、<strong>データの実際の保存時間とストレージ容量に応じて課金されます</strong>。COSの保存料金が別途必要です。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/32534">COS-従量課金</a></td>
</tr></table>
