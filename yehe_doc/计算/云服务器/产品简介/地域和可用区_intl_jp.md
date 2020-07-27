## リージョン

### 概要

リージョンとは、物理的なデータセンターの地理的地域です。Tencent Cloudは異なるリージョン間で完全に隔離されて、異なるリージョン間で最大限の安定性とフォールトトレランスを確保しています。アクセスのレイテンシーを低減し、ダウンロード速度を向上するためには、顧客に最も近いリージョンを選択することをお勧めします。

次の表から、またはDescribeRegions APIを使用して[リージョンの完全なリスト](https://intl.cloud.tencent.com/document/product/213/15708)を表示できます。

### 特徴

- 異なるリージョン間のネットワークは完全に隔離されており、異なるリージョン間のクラウド製品は、**デフォルトではプライベートネットワークを介して通信できません**。
- 異なるリージョン間のクラウド製品は、インターネット上の[パブリックIP](https://intl.cloud.tencent.com/document/product/213/5224)を介して相互に通信できますが、異なるVPC内のクラウド製品は、より高速で安定した[Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003)を介して相互に通信できます。
- [Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214)は現在、デフォルトで同一リージョンのトラフィック転送をサポートし、対象リージョンのCVMをバインドします。[クロスリージョンバインド](https://intl.cloud.tencent.com/document/product/214/12014)機能が有効になっている場合、Cloud Load BalancerとCVMのクロスリージョンバインドがサポートされます。

## アベイラビリティーゾーン

### 概要

アベイラビリティーゾーンは、Tencent Cloudが同じリージョン内で電源とネットワークが独立した物理的なデータセンターです。ユーザのビジネスの安定性を確保し、アベイラビリティーゾーン間の障害を互いに隔離させ（大規模な災害または大規模な電源設備の障害を除く）、障害が広がらないようにすることは目的です。独立したアベイラビリティーゾーンでインスタンスを起動することにより、ユーザは単一障害点の影響からアプリケーションを保護できます。
APIインターフェースを介してアベイラビリティーゾーンの完全なリストを確認できます。

### 特徴

同じVPC内のクラウド製品は、プライベートネットワークを介して相互接続されているため、異なるアベイラビリティーゾーンにある場合でも、[プライベートIPアドレス](https://intl.cloud.tencent.com/document/product/213/5225)を直接使用してアクセスすることができます。　　
> プライベートネットワーク相互接続とは、同じアカウントでのリソースの相互接続を指します。異なるアカウントのリソースは、プライベートネットワークで完全に隔離されています。
>

<span id="MainlandChina"></span>
## 中国
<table class="table-striped">
<tbody>
	<tr>
		<th>リージョン</th>
		<th>アベイラビリティーゾーン</th>
	</tr>
	<tr>
		<td rowspan="4">華南地区（広州）<br> ap-guangzhou</td>
		<td>広州1区（品切れ）<br> ap-guangzhou-1</td>
	</tr>	
	<tr>
		<td>広州2区<br> ap-guangzhou-2</td>
	</tr>
	<tr>
		<td>広州3区<br> ap-guangzhou-3</td>
	</tr>
	<tr>
		<td>広州4区<br> ap-guangzhou-4</td>
	</tr>
		<td rowspan="4">華東地区（上海）<br>ap-shanghai</td>
		<td>上海1区<br>ap-shanghai-1</td>
	</tr>
	<tr>
		<td>上海2区<br>ap-shanghai-2</td>
	</tr>
	<tr>
		<td>上海3区<br>ap-shanghai-3</td>
	</tr>
	<tr>
		<td>上海4区<br>ap-shanghai-4</td>
	</tr>
		<tr>
			<td rowspan="2">華東地区（南京）<br>ap-nanjing</td>
			<td>南京1区<br>ap-nanjing-1</td>
	</tr>
	<tr>
			<td>南京2区<br>ap-nanjing-2</td>
	</tr>
	<tr>
			<td rowspan="4">華北地区（北京）<br>ap-beijing</td>
			<td>北京1区<br>ap-beijing-1</td>
	</tr>
	<tr>
			<td>北京2区<br>ap-beijing-2</td>
	</tr>
	<tr>
			<td>北京3区<br>ap-beijing-3</td>
	</tr>
	<tr>
			<td>北京4区<br>ap-beijing-4</td>
	</tr>
	<tr>
		<td rowspan="2">西南地区（成都）<br>ap-chengdu</td>
		<td>成都1区<br>ap-chengdu-1</td>
	</tr>
	<tr>
			<td>成都2区<br>ap-chengdu-2</td>
	</tr>    
	<tr>
			<td >西南地区（重慶）<br>ap-chongqing</td>
			<td>重慶1区<br>ap-chongqing-1</td>
	</tr>
	<tr>
			<td rowspan="2">香港・マカオ・台湾（中国香港）<br>ap-hongkong</td>
			<td>香港1区（中国香港ノードは香港・マカオ・台湾地域をカバーできる）<br>ap-hongkong-1</td>
	</tr>
	<tr>
			<td>香港2区（中国香港ノードは香港・マカオ・台湾地域をカバーできる）<br>ap-hongkong-2</td>
	</tr>
</tbody>
</table>	

<span id="InternationalArea"></span>

## その他の国と地域	
<table class="table-striped">
	<tbody>
	<tr>
			<th>リージョン</th>
			<th>アベイラビリティーゾーン</th>
		</tr>
		<tr>
			<td>東南アジア（シンガポール）<br>ap-singapore</td>
			<td>シンガポール1区（シンガポールのノードは東南アジア地域をカバーできる）<br>ap-singapore-1</td>
		</tr>
		<tr>
			<td >北東アジア（ソウル）<br>ap-seoul</td>
			<td>ソウル1区（ソウルのノードは北東アジア地域をカバーできる）<br>ap-seoul-1</td>
		</tr>
		<tr>
			<td >北東アジア（東京）<br>ap-tokyo</td>
			<td>東京１区（東京のノードは北東アジア地域をカバーできる）<br>ap-tokyo-1</td>
		</tr>
       <tr>
			<td  rowspan="2">南アジア太平洋（ムンバイ）<br>ap-mumbai</td>
			<td>ムンバイ1区（ムンバイのノードは南アジア太平洋地域をカバーできる）<br>ap-mumbai-1</td>
		</tr>
       <tr>
			<td>ムンバイ2区（ムンバイのノードは南アジア太平洋地域をカバーできる）<br>ap-mumbai-2</td>
		</tr>
		<tr>
		  	<td >東南アジア（バンコク）<br>ap-bangkok </td>
				 <td >バンコク1区  （バンコクのノードは東南アジア地域をカバーできる）<br>ap-bangkok-1</td>
		<tr>
			<td>北米地域（トロント）<br>na-toronto</td>
			<td>トロント1区（トロントのノードは北米地域をカバーできる）<br>na-toronto-1</td>
		</tr>
		<tr>
			<td rowspan="2">米国西部（シリコンバレー）<br>na-siliconvalley</td>
			<td>リコンバレー1区（シリコンバレーのノードは米国西部をカバーできる）<br>na-siliconvalley-1</td>
		</tr>
    <tr>
			<td>リコンバレー2区（シリコンバレーのノードは米国西部をカバーできる）<br>na-siliconvalley-2</td>
		</tr>
		<tr>
			<td rowspan="2">米国東部（バージニア）<br>na-ashburn</td>
			<td>バージニア1区 （バージニアのノードは米国東部をカバーできる）<br>na-ashburn-1</td>
		</tr>
		<tr>
			<td>バージニア2区 （バージニアのノードは米国東部をカバーできる）<br>na-ashburn-2</td>
		</tr>
		<tr>
			<td>ヨーロッパ（フランクフルト）<br>eu-frankfurt</td>
			<td>フランクフル1区（フランクフルトのノードはヨーロッパ地域をカバーできる）<br>eu-frankfurt-1</td>
		</tr>
		<td >ヨーロッパ（モスクワ）<br>eu-moscow</td>
		<td>モスクワ1区（モスクワのノードはヨーロッパ地域をカバーできる）<br>eu-moscow-1</td>
		</tr>
	</tbody>
</table>

## リージョンとアベイラビリティーゾーンの選定方法

リージョンとアベイラビリティーゾーンを選択する際に、以下の要因を考慮する必要があります。
- CVMインスタンスの所在地、ユーザーおよびターゲットユーザーの地理的な場所。
アクセス遅延を低減し、アクセス速度を向上するために、CVMを購入する際に、顧客に最も近いリージョンを選択することをお勧めします。
- 使用するその他のクラウド製品。
他のクラウド製品を選択する場合は、各クラウド製品がプライベートネットワークを介して相互に通信できるように、なるべく同じリージョンと同じアベイラビリティーゾーンにあることをお勧めします。その場合、アクセス遅延を低減し、アクセス速度を向上させることができます。
- サービスの高可用性とフォールトトレランス。
VPCが1つしかない場合でも、単一障害点を回避してクロス-AZ災害復旧を実現するために、異なるアベイラビリティゾーンにビジネスを展開することをお勧めします。
-異なるアベイラビリティーゾーン間では、ネットワーク遅延が発生する可能性がありますので、実際のビジネス要件に応じて検討し、高可用性と低遅延との最適なバランスを見つけることをお勧めします。
- 他の国または地域のCVMインスタンスにアクセスする必要がある場合は、他の国または地域のCVMを選択することをお勧めします。[中国本土](#MainlandChina)のCVMインスタンスを使用して、[他の国や地域のサーバー](#InternationalArea)にアクセスする場合、ネットワーク遅延が大幅に増加する可能性があります。ご利用はお勧めしません。

## リソースの可用性
次の表は、Tencent Cloudのどのリソースがグローバルであり、どのリソースがリージョンであり、どのリソースがアベイラビリティゾーンに固有のものかを示しています。

<table>
	<tr><th>リソース</th><th>リソースIDの形式<br><リソースの略語>-8桁の数字と文字</th><th>タイプ</th><th>説明</th></tr>
	<tbody>
	<tr>
	  <td>ユーザーアカウント</td>
	  <td>制限なし</td>
	  <td>グローバルに一意</td>
	  <td>ユーザーは同じアカウントを使用して、Tencent Cloudのグローバルリソースにアクセスできます。</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/6092">SSHキー</a> </td>
	  <td>skey-xxxxxxxx</td>
	  <td>すべてのリージョンで利用可能</td>
	  <td>ユーザーはSSHキーを使用して、アカウント下の任意のリージョンのCVMをバインドできます。</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/4939">CVMインスタンス</a> </td>
	  <td>ins-xxxxxxxx</td>
	  <td>単一のアベイラビリティーゾーンでのみ利用可能</td>
	  <td>ユーザーは特定のアベイラビリティーゾーンでのみCVMインスタンスを作成できます。</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/4941#custom-images">カスタムイメージ</a> </td>
	  <td>img-xxxxxxxx</td>
	  <td>単一リージョンの複数のアベイラビリティーゾーンで利用可能</td>
	  <td>ユーザーはインスタンスのカスタムイメージを作成でき、また、同じリージョンの異なるアベイラビリティーゾーンで使用できます。他のリージョンで使用する必要がある場合は、イメージのコピー機能を利用して、カスタムイメージを他のリージョンにコピーしてください。</td>
	</tr>
	<tr>
	<td> <a href="http://intl.cloud.tencent.com/document/product/213/5733">EIP</a> </td>
	  <td>eip-xxxxxxxx</td>
	  <td>単一リージョンの複数のアベイラビリティーゾーンで利用可能</td>
	  <td>EIPは、同じリージョン内のインスタンスにのみ関連付けることができます。</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/12452?from_cn_redirect=1">セキュリティグループ</a> </td>
	  <td>sg-xxxxxxxx</td>
	  <td>単一リージョンの複数のアベイラビリティーゾーンで利用可能</td>
	  <td>セキュリティグループは、同じリージョン内のインスタンスにのみ関連付けることができます。Tencent Cloudは、ユーザーに3つのデフォルトセキュリティグループを自動的に作成します。</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/362">Cloud Block Storage</a> </td>
	  <td>disk-xxxxxxxx</td>
	  <td>単一リージョンの単一アベイラビリティーゾーンでのみ利用可能</td>
	  <td>ユーザーは、特定のアベイラビリティーゾーンでのみCloud Block Storageを作成でき、また、同じアベイラビリティーゾーンのインスタンスにマウントできます。</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/362/31638">スナップショット</a> </td>
	  <td>snap-xxxxxxxx</td>
	  <td>単一リージョンの複数のアベイラビリティーゾーンで利用可能</td>
	  <td>特定のCloud Block Storageにスナップショットを作成した後、ユーザーは対象リージョンで作成されたスナップショットをを使用して、他の操作（Cloud Block Storageの作成など）を行うことができます。</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/214/524?from_cn_redirect=1">Cloud Load Balancer</a> </td>
	  <td>clb-xxxxxxxx</td>
	  <td>単一リージョンの複数のアベイラビリティーゾーンで利用可能</td>
	  <td>Cloud Load Balancerは、同じリージョン内の異なるアベイラビリティーゾーンのCVMにバインドして、トラフィックを転送することができます。</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/215/535">Virtual Private Cloud</a> </td>
	  <td>vpc-xxxxxxxx</td>
	  <td>単一リージョンの複数のアベイラビリティーゾーンで利用可能</td>
	  <td>Virtual Private Cloudは特定のリージョンに作成され、異なるアベイラビリティーゾーンで同じVirtual Private Cloudに属するリソースを作成できます。</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/215/535#.E5.AD.90.E7.BD.91">サブネット</a> </td>
	  <td>subnet-xxxxxxxx</td>
	  <td>単一リージョンの単一のアベイラビリティーゾーンでのみ利用可能</td>
	  <td>ユーザーは、異なるアベイラビリティーゾーン間でサブネットを作成することができません。</td>
	</tr>
	<tr>
	<td> ルーティングテーブル </td>
	  <td>rtb-xxxxxxxx</td>
	  <td>単一リージョンの複数のアベイラビリティーゾーンで利用可能</td>
	  <td>ユーザーは、ルーティングテーブルを作成するときに特定のVirtual Private Cloudを指定する必要があります。</td>
	</tr>
	</tbody>
</table>


## 関連操作

### インスタンスを他のアベイラビリティーゾーンに移行

すでに起動されたインスタンスは、対象アベイラビリティーゾーンを変更できませんが、ユーザは他の方法でインスタンスを他のアベイラビリティーゾーンに移行させることができます。移行は、元のインスタンスからカスタムイメージを作成し、カスタムイメージを使用して新しいアベイラビリティーゾーンでインスタンスを起動し、新しいインスタンスの設定を更新する手順になります。
1. 現在のインスタンスからカスタムイメージを作成します。詳細については、[カスタムイメージ](https://intl.cloud.tencent.com/document/product/213/4942)をご参照ください。
2. 現在のインスタンスのネットワーク環境が[Virtual Private Clou](https://intl.cloud.tencent.com/document/product/213/5227)であり、また、移行後も現在のプライベートIPアドレスを保持する必要がある場合、ユーザは現在のアベイラビリティーゾーン内のサブネットを削除してから、同じIPアドレス範囲で新しいアベイラビリティーゾーンにサブネットを作成します。サブネットは、使用可能なインスタンスが含まれていない場合にのみ削除できることに注意してください。そのため、現在のサブネット内のすべてのインスタンスを新しいサブネットに移行する必要があります。
3. さきほど作成したカスタムイメージを使用して、新しいアベイラビリティーゾーンに新しいインスタンスを作成します。ユーザは、元のインスタンスと同じタイプと設定を選択できるか、新しいインスタンスタイプと設定を選択できます。詳細については、[インスタンスの作成](https://intl.cloud.tencent.com/document/product/213/4855)をご参照ください。
4. 元のインスタンスがすでにElastic IPアドレスに関連付けられている場合、古いインスタンスとの関連付けを解除してから、新しいインスタンスに関連付ける必要があります。詳細については、[EIP](https://intl.cloud.tencent.com/document/product/213/5733)をご参照ください。
5. （オプション）元のCVMインスタンスが[従量課金](https://intl.cloud.tencent.com/document/product/213/2180)タイプの場合、元のインスタンスを終了することができます。詳細については、[インスタンスの終了](https://intl.cloud.tencent.com/document/product/213/4930)をご参照ください。

### イメージを他のリージョンにコピー

インスタンスの起動や表示などのアクションには、リージョン属性があります。起動するインスタンスのイメージが対象リージョンに存在しない場合、イメージを対象リージョンにコピーする必要があります。詳細については、[イメージのコピー](https://intl.cloud.tencent.com/document/product/213/4943)をご参照ください。
