## 概要

VNCログインは、Tencent Cloudが提供するWebブラウザ経由でCVMにリモート接続する方式です。クライアントにインストールしていないかまたはリモートでログインできない場合や、その他の方法でもログインできない状況において、ユーザーは、VNC経由でCVMにログイン接続して、CVMの状態を観察し、かつCVMアカウントから基本的なCVM管理操作を行うことができます。


## 使用制限

- VNCログインのCVMは現在コピー・ペースト機能、中国語入力ソフト、ファイルのアップロード、ダウンロードをサポートしていません。
- VNCでCVMにログインした時は、メインストリームのブラウザ（Chrome、Firefox、IE 10バージョン以上など）を使用する必要があります。
- VNCログインは単独での端末利用となり、同一時間にVNCを使用してログインできるのは1人のユーザーのみです。

##  前提条件
インスタンスログインの管理者アカウントおよびパスワードを取得していること。
- インスタンス作成時に、システムによるパスワードのランダム発行を選択した場合は、[サイト内メッセージ](https://console.cloud.tencent.com/message)にアクセスして取得してください。
- ログインパスワードを設定済みの場合は、そのパスワードを使用してログインしてください。パスワードを忘れた場合は、[インスタンスのパスワードをリセット](https://intl.cloud.tencent.com/document/product/213/16566)してください。


## 操作手順

1. [CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインします。
2. インスタンスの管理画面で、実際に使用されているビューモードに従って操作します。
<dx-tabs>
::: リストビュー
下図に示すように、ログインしたいLinux CVMを見つけ、右側にある**ログイン**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/bad0e4e6670096461c7e9498d5d47654.png)

:::
::: タブビュー
下図に示すように、ログインしたいLinux CVMタブを選択し、**ログイン**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/2cdbf7a52ed228109fd1bc55a6ed1d6c.png)

:::
</dx-tabs>
3. 開いた「標準ログイン | Linuxインスタンス」ウィンドウで、**VNCログイン**をクリックします。下図のとおりです。
![](https://main.qcloudimg.com/raw/1bd4877abc15d06adb8c54fc7ed1318e.png)
4. 開いたウィンドウの中で、「login」の後ろにユーザー名を入力し、**Enter**を押します。
Linuxインスタンスのデフォルトのユーザー名は`root`、Ubuntuシステムインスタンスのデフォルトのユーザー名は`ubuntu`になります。必要に応じて入力してください。
5.「Password」の後にパスワードを入力し、** Enter**キーを押します。
入力したパスワードはデフォルトの状態では表示されません。ログイン完了後、コマンドプロンプトの左側に現在ログインしているCVMの情報が表示されます。下図のとおりです。
![](https://main.qcloudimg.com/raw/03a8492f66e8342221858709b6068669.png)


## 後続の操作


CVMにログインした後、個人用Webサイトまたはフォーラムを構築したり、その他の操作を実行したりできます。関連操作については、下記をご参照ください：　　
-  [Linuxの一般的な操作およびコマンド](https://intl.cloud.tencent.com/document/product/213/2150) 
- [WordPress Webサイトを構築する](https://intl.cloud.tencent.com/zh/document/product/213/8044)
- [Discuz! フォーラムを構築する](https://intl.cloud.tencent.com/zh/document/product/213/8043)

