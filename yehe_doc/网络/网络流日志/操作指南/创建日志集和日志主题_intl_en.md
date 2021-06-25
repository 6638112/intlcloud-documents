You need to create logsets and log topics to store and view the flow logs.
  - Logset: specifies the storage location in CLS for flow logs.
  - Log topic: specifies the minimum dimension of log storage, which is used to distinguish log types, such as `Accept` log.

### Directions
1. Log in to the [CLS console](https://console.cloud.tencent.com/cls) and click **Log Topic** on the left sidebar to access the **Log Topic** page. 
2. Select a desired region at the top of the page and click **Create Log Topic**.
3. In the pop-up window, enter log topic name and partition, and click **OK**.
    ![](https://main.qcloudimg.com/raw/e86b5fceb9fdf2eb9cec876737f8c589.png)
    - Log Topic Name: enter `nginx` as an example.
    - Partitions: enter an integer. The default value is 1. For more information about partitions, see [Topic Partition](https://intl.cloud.tencent.com/document/product/614/33779).
    - Partition Auto-Split: enabled by default.
    - Maximum Partitions: enter an integer up to 50.
    - Logset Operation:
       - Select an existing logset: select a target logset from the drop-down list of the **Logset**. The log retention period is determined by the logset retention period.
       - Create logset:
            - Logset Name: enter `cls_test` as an example
            - Log Retention Period: enter an integer. The log will be retained for 30 days by default.

>?
>- After the auto-split feature is enabled, CLS will automatically split a log topic into partitions (up to 50) when the write requests or write traffic exceed the capacity of the log topic.
>- If the number of partitions of a log topic has reached the set maximum value, CLS will no longer trigger auto-split, and the excessive partitions will be rejected with an [error code](https://intl.cloud.tencent.com/document/product/614/12402) returned.

4. On the details page of the log topic, select the **Index Configuration** tab and click **Edit** in the top-right corner.
5. Enable the index feature and click **OK**. Now you can view and search for flow logs.
>?
>- You do not need to install agents or care about the server group status. 
>- If you do not need to publish flow logs to services such as [COS](https://intl.cloud.tencent.com/document/product/436/6222), ignore shipping task.
>

