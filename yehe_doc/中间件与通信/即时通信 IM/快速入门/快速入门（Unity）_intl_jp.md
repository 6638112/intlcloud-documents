ここでは、主にTencent Cloud IM Demo(Unity)を素早く実行する方法をご紹介します。

## 環境要件

| プラットフォーム | バージョン |
|---------|---------|
| Unity | 2019.4.15f1以降のバージョン。 |
|Android|Android Studio 3.5以降のバージョン。Appの要件はAndroid 4.1以降のバージョンのデバイスです。|
|iOS|Xcode 11.0以降のバージョン。プロジェクトに有効な開発者署名を設定済みであることを確認してください。|

##  前提条件

[Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/document/product/378/17985)を行い、[実名認証](https://intl.cloud.tencent.com/document/product/378/3629)が完了済みであること。

## 操作手順


[](id:step1)
### 手順1：IMアプリケーションの作成
1. [IMコンソール](https://console.cloud.tencent.com/im)にログインします。
>?アプリケーションをすでに保有している場合は、そのSDKAppIDを記録してから[キー情報の取得](#step2)を実行してください。
>同じTencent Cloudのアカウントで、最大300個のIMアプリケーションを作成することができます。すでにアプリケーションが300個ある場合は、使用する必要のないアプリケーションを[使用停止して削除](https://intl.cloud.tencent.com/document/product/1047/34540)すると、新しいアプリケーションを作成することができます。**アプリケーションを削除した後、そのSDKAppIDに対応するすべてのデータとサービスは失われます。慎重に操作を行ってください。**
>
2. **新しいアプリケーションの作成**をクリックし、**アプリケーションの作成**のダイアログボックスにアプリケーション名を入力し、**OK**をクリックします。
![](https://main.qcloudimg.com/raw/15e61a874a0640d517eeb67e922a14bc.png)
3. 左側ナビゲーションバーで **[支援ツール](https://console.cloud.tencent.com/im/tool-usersig)** > **UserSig生成&検証**の順にクリックし、UserIDおよびそれに対応するUserSigを作成します。署名情報をコピーして、[手順5](#step5)で使用します。
![](https://main.qcloudimg.com/raw/2286644d987d24caf565142ae30c4392.png)

[](id:step2)
### 手順2：Unityプロジェクトの作成
UnityからUnityプロジェクトを作成し、プロジェクトのある場所を記録しておきます。

[](id:step3)
### 手順3：依存ファイルの修正
1. IDE（例：Visual Studio Code）からプロジェクトを開きます。
![](https://qcloudimg.tencent-cloud.cn/raw/1a21933037a72a6bd4c8ed14f08c6ca7.png)
2. ディレクトリに基づいてPackages/manifest.jsonを見つけて次のように依存を修正します。
```json
{
    "dependencies":{
    "com.tencent.imsdk.unity":"https://github.com/TencentCloud/TIMSDK.git#unity" 
  }
}
```

[](id:step4)
### 手順4：依存のロード
Unity Editorでプロジェクトを開き、依存のロードが完了してから、Tencent Cloud IMのロードが完了したことを確認します。
![](https://qcloudimg.tencent-cloud.cn/raw/d98dfb17bbee6c0319e370de6f2ba9dd.jpg)

[](id:step5)
### 手順5：スクリプトのテスト
1. [テストスクリプト(TestApi.cs)](https://github.com/TencentCloud/TIMSDK/blob/master/Unity/im_unity_sdk_plus/Assets/Demo/TestApi.cs)および[構成ファイル(Config.cs)](https://github.com/TencentCloud/TIMSDK/blob/master/Unity/im_unity_sdk_plus/Assets/Demo/Config.cs)を取得し、Config.csでパラメータSDKAppID、UserID、UserSig、toUserIDを完了してから、TestApi.csとテストシナリオのCameraを関連付けます。
    ![](https://qcloudimg.tencent-cloud.cn/raw/b4d770775523fdd76b75f1d80f07c925.jpg)

2. Unity Editorの[実行]ボタンをクリックして、当該シナリオでの実行を開始します。[Init]（SDKの初期化）、[Login]（IMにログイン）、およびその他のテストボタンをクリックしてテストを行います。

  <img src="https://qcloudimg.tencent-cloud.cn/raw/40fb0f381096840418b66b804d403140.png" alt="image-20220616115353114" style="zoom:50%;" />
	
## よくあるご質問

### サポートされているプラットフォームはどれ？
現時点ではiOS、Android、Windows、Macをサポートしています。

### AndroidでBuild And Runをクリックすると、使用できるデバイスが見つからないというエラーが発生します。
デバイスが他のリソースに使用されないことを保証するか、またはBuildをクリックしてapkパッケージを生成してから、エミュレーター内にドラッグして実行します。

### iOSで初回実行時にエラーが発生します。
上のDemoで設定を実行した後もエラーが発生する場合、**Product**>**Clean**をクリックし、プロダクトを削除してから改めてBuildするか、またはXcodeをオフにして改めて開いて再度Buildします。
### 2019.04バージョンのUnity、iOSプラットフォームでエラーが発生します。
Library/PackageCache/com.unity.collab-proxy@1.3.9/Editor/UserInterface/Bootstrap.cs(23,20): error CS0117: 'Collab' does not contain a definition for 'ShowChangesWindow'
Editorツールバーで**Window**>**Package Manager**をクリックし、Unity Collaborateを1.2.16にダウングレードします。

### 2019.04バージョンのUnity、iOSプラットフォームでエラーが発生します。
Library/PackageCache/com.unity.textmeshpro@3.0.1/Scripts/Editor/TMP_PackageUtilities.cs(453,84): error CS0103: The name 'VersionControlSettings' does not exist in the current context
ソースコードを開き、`|| VersionControlSettings.mode != "Visible Meta Files"`の部分のコードを削除すれば完了です。
