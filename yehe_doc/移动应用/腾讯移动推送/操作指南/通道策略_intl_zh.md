由于 OPPO、vivo、小米等厂商平台相继公布推送的额度限制，为了更合理的分配厂商通道资源，腾讯移动推送（TPNS）推出任务级通道策略功能，用户可以根据当前厂商通道剩余配额，决定每个推送任务的通道分配，提高抵达率。
## 通道策略概览
TPNS 目前提供了两个通道策略，包括智能分配和自定义通道策略，通道策略规则如下表所示：

<span id="zhineng"></span>
### 智能分配
系统在保障推送抵达率的基础上智能分配每个设备的下发通道，以节省厂商通道资源。

| 通道 | 在线 | 离线 |
|---------|---------|---------|
| 华为 | 优先走厂商通道，失败走 TPNS 通道补推 | 优先走厂商通道，失败走 TPNS 通道补推 |
| 魅族 | 优先走厂商通道，失败走 TPNS 通道补推 | 优先走厂商通道，失败走 TPNS 通道补推 |
| 小米 | 优先走 TPNS 通道 | 优先走厂商通道，失败走 TPNS 通道补推 |
| OPPO | 优先走 TPNS 通道 | 优先走厂商通道，失败走 TPNS 通道补推 |
| vivo | 优先走 TPNS 通道 | 优先走厂商通道，失败走 TPNS 通道补推 |
| 其他 | TPNS 通道 | TPNS 通道离线队列|

<span id="zidingyi"></span>
### 自定义
由于部分厂商通道资源有限，您可以根据业务需求选择该条推送可以通过哪些通道下发，厂商通道额度查询详见 [厂商通道限额说明](https://intl.cloud.tencent.com/document/product/1024/35829)。

| 通道 | 开启 | 关闭 |
|---------|---------|---------|
| 华为 | <li>在线：优先走厂商通道，失败走 TPNS 通道补推 <li>离线：优先走厂商通道，失败走 TPNS 通道补推| <li>在线：TPNS 通道 <li>离线：TPNS 通道 |
| 魅族 |  <li>在线：优先走厂商通道，失败走 TPNS 通道补推 <li>离线：优先走厂商通道，失败走 TPNS 通道补推| <li>在线：TPNS 通道 <li>离线：TPNS 通道 |
| 小米 |  <li>在线：优先走 TPNS 通道 <li>离线：优先走厂商通道，失败走 TPNS 通道补推| <li>在线：TPNS 通道 <li>离线：TPNS 通道 |
| OPPO |<li>在线：优先走 TPNS 通道 <li>离线：优先走厂商通道，失败走 TPNS 通道补推| <li>在线：TPNS 通道 <li>离线：TPNS 通道 |
| vivo | <li>在线：优先走 TPNS 通道 <li>离线：优先走厂商通道，失败走 TPNS 通道补推|<li>在线：TPNS 通道 <li>离线：TPNS 通道 |
| 其他 |  <li>在线：TPNS 通道 <li>离线： TPNS 通道离线队列| <li>在线：TPNS 通道 <li>离线：TPNS 通道</li> |

## 开始使用
### 控制台使用
完成推送内容的填写后，可在控制台 >【消息推送】>【新建推送】>【高级设置】通道策略处选择策略。
#### 智能分配
选择【智能分配】，系统会智能分配每个设备的下发通道，详见 [智能分配](#zhineng) 的规则。
![](https://main.qcloudimg.com/raw/91b7d0b402a054035ecab44ffc6051ad.png)

#### 自定义
选择【自定义】，点击【查看详情】可以查看详细的厂商额度信息。
![](https://main.qcloudimg.com/raw/f99f1cba9cda46b23aea7d23f9a44b31.png)
可以根据当前厂商通道剩余配额，以及推送任务的优先级，自定义选择需要推送的通道，详见 [自定义](#zidingyi) 的规则。
![](https://main.qcloudimg.com/raw/6e36aac8a3b70197dfb565fb579b2ac2.png)

### Rest API 使用
在 Rest API 可选参数中设置channel_rules参数，可参考 PushAPI 文档中的 [channel_rules 参数说明](https://intl.cloud.tencent.com/document/product/1024/33764)。
推送示例如下：
```json
{
    "audience_type": "token",
    "token_list": [
        "05da87c0ae5973bd2dfa9e08d884aada5bb2"
    ],
    "message_type": "notify",
    "channel_rules": [
        {
            "channel": "mz",
            "disable": true
        },
        {
            "channel": "xm",
            "disable": false
        }
    ],
    "message": {
        "title": "推送标题",
        "content": "推送内容",
        "android": {
             "custom_content":"{\"key\":\"value\"}"
        }
    }
}
```
