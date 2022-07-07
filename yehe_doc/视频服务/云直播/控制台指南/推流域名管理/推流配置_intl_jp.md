CSSプッシュの情報セキュリティを保護するため、CSSプッシュドメイン名はデフォルトでプッシュ認証が有効になっています。プッシュアドレス詳細ページのプッシュアドレスジェネレーターによって、オンラインで対応するプッシュアドレスを生成できます。プッシュアドレスを使用してオンラインでプッシュすることで、CSSストリームをCSSサービスに転送でき、ライブストリーミングビデオのアップロードが可能となります。

## 注意事項

- CSSは、デフォルトでテストドメイン名`xxxx.tlivepush.com`を提供しています。このドメイン名でプッシュテストを行うことはできますが、正式なサービスでこのドメイン名をプッシュドメイン名として使用することはお勧めしません。 
>- 生成されたプッシュアドレスは、設定した有効期限内は使用可能です。期限が切れた場合、新しいプッシュアドレスを再度生成する必要があります。

## 前提条件

CSSサービスがアクティブになっていること。

## 認証設定
1. [**ドメイン名管理**](https://console.cloud.tencent.com/live/domainmanage)に進み、設定したい**プッシュドメイン名**または**管理**をクリックしてドメイン名詳細ページに進みます。 
2. **プッシュ設定**をクリックして、**認証設定**のタグを表示し、右側の**編集**をクリックします。
	![](https://main.qcloudimg.com/raw/f57795fb5a6497ff59a1612c5d805ad2.png)
3. プッシュ認証設定ページに入り、![](https://main.qcloudimg.com/raw/5637a9d55de965fa5d35725a955f4c00.png)ボタンをクリックしてプッシュ認証の有効/無効を選択します。
4. マスターKEYおよびスレーブKEYの情報を修正して、**保存**をクリックすれば、設定が有効になります。
![](https://main.qcloudimg.com/raw/a12dc5bb7d739ca7d526f35e9f22e81e.png)
>? マスターKEYは入力必須、スレーブKEYはオプションです。マスター/スレーブKEYによって、KEYが漏洩した際もKEYをスムーズに交換でき、業務に影響が出ません。

## プッシュアドレスジェネレーター

### 操作手順
1. [**ドメイン名管理**](https://console.cloud.tencent.com/live/domainmanage)に進み、設定したいプッシュドメイン名を選択するか、**管理**をクリックし、ドメイン名詳細ページに進みます。
2. **プッシュ設定**>**プッシュアドレスジェネレーター**を選択し、次のとおり設定を行います。
   1. 期限を選択します（例：`2021-06-30 19:26:02`）。
   2. カスタマイズされたStreamNameを入力します（例：liveteststream）。
   3. **プッシュアドレスの発行**をクリックすると、StreamNameの付いたRTMPプッシュアドレスが発行されます。
![](https://main.qcloudimg.com/raw/6f5ac8dcac2082aedca950c5341946ab.png)
3. プッシュドメイン名のプッシュ認証が有効になっていない場合は、**プッシュ設定**>**プッシュアドレス解決**タグで、当該プッシュドメイン名でのRTMP、UDPという2種類のプッシュアドレスを確認することができます。再生アドレスの中のStreamName（ストリーム名）を置き換えてプッシュアドレスをバインドすると、その後すぐに再生アドレス経由でライブストリーミング画面を見ることができるようになります。 
![](https://main.qcloudimg.com/raw/aa129bd839cb307993bfed247e636a41.png)



## プッシュアドレスの説明

RTMPプッシュアドレスの形式は次のようになります。
```
rtmp://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
```
そのうち：
- domain：CSSプッシュドメイン名。
- AppName：ライブストリーミングのアプリケーション名。デフォルトはliveで、カスタマイズ可能です。
- StreamName：CSSストリームを識別するために用いる、ユーザー定義のストリーム名。
- txSecret：プッシュ認証を有効にした後に発行される認証文字列。
- txTime：プッシュアドレスのタイムスタンプは、コンソールのプッシュアドレスの有効時間です。

>!
>- ドメイン名認証を有効にしている場合、実際の期限はtxTime + Keyの有効時間と等しくなります。
>- コンソールでは、利用しやすいように、設定時間を実際の期限としています。**ドメイン名認証を有効にした場合、プッシュアドレスの計算時に、公式に基づきtxTimeが逆算されます**。
>- 有効期限までにプッシュプルストリームを行った場合、プッシュプルストリームが正常であり、中断や停止がなければ、有効期限が過ぎても正常なプッシュプルストリームの状態を維持することができます。



## プッシュアドレスのサンプルコード
Tencent CloudはPHP、Java、Go言語のプッシュアドレスのサンプルコードを提供します。サンプルコードを直接参照して、プッシュアドレスのアクセスを完了することができます。具体的な操作は次のとおりです。

1. **[ドメイン名管理](https://console.cloud.tencent.com/live/domainmanage)**に進みます。
2. プッシュドメイン名を選択するか、右側の**管理**をクリックしてドメイン名詳細ページに進みます。
3. **プッシュ設定**を選択し、一番下までプルダウンして**プッシュアドレスサンプルコード**タグを表示します。
4. 以下のように、タグ切り替えボタンをクリックして、PHP、Java、Goサンプルコードを表示します。
<dx-codeblock>
::: PHP php
/**
* プッシュアドレスの取得
* keyと有効期限が渡されない場合、リンク不正アクセス防止のないURLが返されます
* @param domainプッシュに使用するドメイン名
*        streamName さまざまなプッシュアドレスを区別するために使用する一意のストリーム名
*        key セキュリティキー
*        time 有効期限 sample 2016-11-12 12:00:00
* @return String url
*/
function getPushUrl($domain, $streamName, $key = null, $time = null){
    if($key && $time){
          $txTime = strtoupper(base_convert(strtotime($time),10,16));
          //txSecret = MD5( KEY + streamName + txTime )
          $txSecret = md5($key.$streamName.$txTime);
          $ext_str = "?".http_build_query(array(
                "txSecret"=> $txSecret,
                "txTime"=> $txTime
          ));
    }
    return "rtmp://".$domain."/live/".$streamName . (isset($ext_str) ? $ext_str : "");
}

echo getPushUrl("123.test.com","123456","69e0daf7234b01f257a7adb9f807ae9f","2016-09-11 20:08:07");
:::
::: Java java
package com.test;

import java.io.UnsupportedEncodingException;
import java.security.MessageDigest;
import java.security.NoSuchAlgorithmException;

public class Test {

      public static void main(String[] args) {
            System.out.println(getSafeUrl("txrtmp", "11212122", 1469762325L));
      }

      private static final char[] DIGITS_LOWER =
            {'0', '1', '2', '3', '4', '5', '6', '7', '8', '9', 'a', 'b', 'c', 'd', 'e', 'f'};

      /*
      * KEY+ streamName + txTime
      */
      private static String getSafeUrl(String key, String streamName, long txTime) {
            String input = new StringBuilder().
                              append(key).
                              append(streamName).
                              append(Long.toHexString(txTime).toUpperCase()).toString();

            String txSecret = null;
            try {
                  MessageDigest messageDigest = MessageDigest.getInstance("MD5");
                  txSecret  = byteArrayToHexString(
                              messageDigest.digest(input.getBytes("UTF-8")));
            } catch (NoSuchAlgorithmException e) {
                  e.printStackTrace();
            } catch (UnsupportedEncodingException e) {
                  e.printStackTrace();
            }

            return txSecret == null ? "" :
                              new StringBuilder().
                              append("txSecret=").
                              append(txSecret).
                              append("&").
                              append("txTime=").
                              append(Long.toHexString(txTime).toUpperCase()).
                              toString();
      }

      private static String byteArrayToHexString(byte[] data) {
            char[] out = new char[data.length << 1];

            for (int i = 0, j = 0; i < data.length; i++) {
                  out[j++] = DIGITS_LOWER[(0xF0 & data[i]) >>> 4];
                  out[j++] = DIGITS_LOWER[0x0F & data[i]];
            }
            return new String(out);
      }
}
:::
::: GO go
package a

import (
	"crypto/md5"
	"fmt"
	"strconv"
	"strings"
	"time"
)

func GetPushUrl(domain, streamName, key string, time int64)(addrstr string){
	var ext_str string
	if key != "" && time != 0{
		txTime := strings.ToUpper(strconv.FormatInt(time, 16))
		txSecret := md5.Sum([]byte(key + streamName + txTime))
		txSecretStr := fmt.Sprintf("%x", txSecret)
		ext_str = "?txSecret=" + txSecretStr + "&txTime=" + txTime
	}
	addrstr = "rtmp://" + domain + "/live/" + streamName + ext_str
	return
}
/*
*domain: 123.test.com
*streamName: streamname
*key: 69e0daf7234b01f257a7adb9f807ae9f
*time: 2022-04-26 14:57:19 CST
*/
func main(){
	domain, streamName, key := "123.test.com", "streamname", "69e0daf7234b01f257a7adb9f807ae9f"
	//CST: ChinaStandardTimeUT, "2006-01-02 15:04:05 MST" must be const
	t, err := time.Parse("2006-01-02 15:04:05 MST", "2022-04-26 14:57:19 CST")
	if err != nil{
		fmt.Println("time transfor error!")
		return
	}
	fmt.Println(GetPushUrl(domain, streamName, key, t.Unix()))
	return
}
:::
</dx-codeblock>



## 後続の操作
プッシュアドレスを生成した後、業務シナリオに応じてCSSプッシュを使用することができます。具体的な操作については、[CSSプッシュ](https://intl.cloud.tencent.com/document/product/267/31558)をご参照ください。

