
ここではCloud Virtual Machine（CVM）がCloud Object Storage（COS）にアクセスする際に使用するアクセス方法および、プライベートネットワークアクセスの判定方法についてご紹介し、接続性テストのサンプルもご提供します。こちらを参照することで、CVMのCOSへのアクセスに関する情報についてさらに理解を深めることができます。

## アクセス方法の説明
Tencent Cloud内でCOSへのアクセス用のサービスをデプロイしている場合、リージョンごとのアクセス方法には次のような違いがあります。
- **同一リージョン内のアクセス**：同一リージョンの範囲内でのアクセスに対しては自動的にプライベートネットワークアドレスが指定されます。つまり、自動的にプライベートネットワークを使用して接続され、それによるプライベートネットワークトラフィックには料金が発生しません。このため、Tencent Cloudの製品をお選びになる際は、できるだけ同一のリージョンを選択すると料金の節約になります。
- **クロスリージョンアクセス**：現時点ではプライベートネットワークアクセスをサポートしておらず、デフォルトでパブリックネットワークアドレスに解決されます。



## プライベートネットワークアクセスの判定方法
この手順によって、CVMがプライベートネットワークを通じてCOSにアクセスしているかどうかをテストすることができます。
CVMのCOSアクセスを例にとると、プライベートネットワークを使用したCOSアクセスかどうかを判定するには、CVM上で`nslookup`コマンドを使用してCOSドメイン名を解決します。プライベートネットワークIPが返された場合、CVMとCOS間はプライベートネットワークアクセスであり、そうでない場合はパブリックネットワークアクセスであることがわかります。
1. バケットアクセスドメイン名を取得し、そのアドレスを記録します。詳細については、[バケットの概要](https://intl.cloud.tencent.com/document/product/436/38493)をご参照ください。
2. インスタンスにログインし、nslookupコマンドを実行します。`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com`が目的のバケットアドレスであった場合、以下のコマンドを実行します。
```
nslookup examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
```
下図に示す結果が返された場合、その中の`10.148.214.13`と`10.148.214.14`という2つのIPが、プライベートネットワークによるCOSアクセスであることを表しています。
>?プライベートIPアドレスの一般的な形式は`10.*.*.*`、`100.*.*.*`であり、VPCネットワークは一般的に`169.254.*.*`などです。これらの形式のIPはすべてプライベートネットワークに該当します。
>
![](https://main.qcloudimg.com/raw/49a7d7429ec2a96d271f6a63926286ea.png)

## 接続性のテスト
パブリックネットワークからのCOSアクセス、同一リージョンのCVM（基本ネットワーク）からのCOSアクセス、同一リージョンのCVM（VPCネットワーク）からのCOSアクセスのサンプルをご提供します。詳細については、[接続性のテスト](https://intl.cloud.tencent.com/document/product/436/30613)をご参照ください。


## 関連操作
- [COSをローカルディスクとしてWindowsサーバーにマウントさせる](https://intl.cloud.tencent.com/document/product/436/40490)
- [WordPressリモート添付ファイルをCOSに保存する](https://intl.cloud.tencent.com/document/product/436/34082)
