Besides the system parameter templates provided by TencentDB for Redis, you can create custom parameter templates to configure parameters in batches as needed.

You can apply a parameter template to configure and manage the parameters of a database engine. A template is like a container of the values of database engine parameters, which can be applied to one or more database instances.

Parameter templates support the following features:
- Support the default parameter templates.
- Create custom templates by modifying the default parameters.
- Save parameter configurations as templates.
- Import parameters from templates to apply to one or more instances.
>!
>- If the parameters in the template are updated, the instance parameters are not updated unless they are manually re-applied to the instances. 
>- You can apply the parameter changes to single or multiple instances by importing a template.

## Creating a Custom Parameter Template
To use your own database parameter template, you can create a parameter template, modify the parameter values, and apply the template to instances.

1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), select **Parameter Templates** on the left sidebar, and click **Create Template**.
![](https://qcloudimg.tencent-cloud.cn/raw/4f5eabc8bba157d095e430ca8d2c5e28.png)
2. In the pop-up dialog box, specify the following configurations, and click **Create and Set Parameters**.
 - **Template Name**: Enter a unique template name.
 - **Database Version**: Select a database version.
 - **Template Description**: Enter a brief description of the parameter template.
![](https://qcloudimg.tencent-cloud.cn/raw/ce72179be683129ed8d0884e60ef5e0c.png)
3. On the displayed parameter configuration page, make sure that all parameter values are correct and the parameter template is created successfully.
![](https://qcloudimg.tencent-cloud.cn/raw/d55f34b4c0f297c6043f1fac730cb7d7.png)

## Default Template
This page displays the default templates applicable to Redis 2.8 standard architecture, Redis 4.0 standard architecture, Redis 4.0 cluster architecture, Redis 5.0 standard architecture, and Redis 5.0 cluster architecture.
![](https://qcloudimg.tencent-cloud.cn/raw/8886085e6cb3cb394f362804a16dad17.png)

>!On the **Default Template** page, you can click **View Details** to view a template, but on the displayed details page, you cannot do any operation.

## Applying a Parameter Template to Instances
### Applying to existing instances
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis) and select **Parameter Templates** on the left sidebar.
2. In the parameter template list, locate the desired template, and click **Apply to Instance** in the **Operation** column. Or, click **View Details**, enter the template details page, and click **Apply to Instance**.
![](https://qcloudimg.tencent-cloud.cn/raw/60e53fbfc50fd72e1a0e75532ce0e29e.png)
3. On the displayed page, specify the execution mode and instances, make sure that all parameter values are correct, and click **Submit**.
 - **Redis Instance**: Select one or more instances that need to apply the parameter template in the specified region.
 - **Parameter Comparison**: View the changed parameter values of the selected instance.
>!Before applying a parameter template to multiple instances, make sure that the instances do support those parameters.
>
![](https://qcloudimg.tencent-cloud.cn/raw/5ba226d16856effb3a19b4dcc765a608.png)

### Applying to new instances
On the [instance purchase page](https://buy.cloud.tencent.com/redis), select a default or custom parameter template for the new instances.
- Click the selection box next to **Parameter Template** and a drop-down list with a search box will pop up. The list shows the names and IDs of all existing parameter templates.
- Enter the parameter template name or ID in the search box to search for a template.

![](https://qcloudimg.tencent-cloud.cn/raw/44bdb23e6fcc01e1efdbb2d041d567ef.png)

## Copying a Parameter Template
To include most of the custom parameters and values of an existing parameter template in a new template, you can copy the existing template and modify it.

### Option 1. Copying an existing parameter template
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), select **Parameter Templates** on the left sidebar, click the parameter template name or **View Details** in the **Operation** column in the template list, and enter the parameter template details page.
2. Click **Save as Template**.
3. In the pop-up dialog box, specify the following configurations: 
  - **Template Name**: Enter a unique template name.
  - **Template Description**: Enter a brief description of the parameter template.
4. After confirming that everything is correct, click **Save**.

### Option 2. Saving parameters of an instance as a parameter template
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), select **Instance List** on the left sidebar, click an instance ID, and enter the instance management page.
2. On the **Parameter Settings** tab, click **Save as Template**.
3. In the pop-up dialog box, specify the following configurations: 
 - **Template Name**: Enter a unique template name.
 - **Template Description**: Enter a brief description of the parameter template.
4. After confirming that everything is correct, click **Create and Save**.
>!Default templates do not support the **Save as Template** feature.

## Modifying Parameter Values in a Parameter Template
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), select **Parameter Templates** on the left sidebar, click the parameter template name or **View Details** in the **Operation** column in the template list, and enter the parameter template details page.
2. Click **Batch Modify Parameters** or <img src="https://main.qcloudimg.com/raw/788902e3f8c335cf17de420f7181c2a8.png"  style="margin:0;"> in the **Current Value** column to modify parameter values.
>!Default templates do not support the **Batch Modify Parameters** feature, and the **Current Value** column cannot be modified.

## Deleting a Parameter Template
If a parameter template is created redundantly or no longer needed, it can be easily deleted.
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis) and select **Parameter Templates** on the left sidebar.
2. In the parameter template list, locate the desired template and click **Delete** in the **Operation** column.
3. Click **OK** in the pop-up dialog box.


## Related APIs

| API | Description |
| :----------------------------------------------------------- | :------------------- |
| [ApplyParamsTemplate](https://www.tencentcloud.com/document/product/239/41922) | Applies a parameter template to instances |
| [CreateParamTemplate](https://www.tencentcloud.com/document/product/239/41921) | Creates a parameter template |
| [DeleteParamTemplate](https://www.tencentcloud.com/document/product/239/41920) | Deletes a parameter template |
| [DescribeInstanceParamRecords](https://www.tencentcloud.com/document/product/239/32083) | Queries the list of parameter modifications |
| [DescribeParamTemplates](https://www.tencentcloud.com/document/product/239/41919) | Queries the list of parameter templates |
| [ModifyInstanceParams](https://www.tencentcloud.com/document/product/239/32079) | Modifies instance parameters |
| [ModifyParamTemplate](https://www.tencentcloud.com/document/product/239/41918) | Modifies a parameter template |



