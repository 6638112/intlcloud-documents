## 命令格式

sync 命令用于同步上传、下载或拷贝文件，与 cp 命令不同的是：sync 命令首先会对比同名文件的 crc64，如果 crc64 值相同则不进行传输。

```plaintext
./coscli sync <source_path> <destination_path> [flag]
```

>? 有关 bucketAlias 的说明，请参见 [配置](https://intl.cloud.tencent.com/document/product/436/43265)。

sync 命令包含以下可选 flag：

| flag 简写 | flag 全称     | flag 用途                      |
| --------- | ------------- | ------------------------------ |
| -h        | --help        | 输出帮助信息                   |
| -c        | --config-path | 指定要使用的配置文件路径       |
|    无       | --include     | 包含特定模式的文件             |
|   无         | --exclude     | 排除特定模式的文件             |
| -r        | --recursive   | 是否递归遍历文件夹下所有文件 |


>?
> - `--include` 和 `--exclude` 支持标准正则表达式的语法，您可以使用它来过滤出符合特定条件的文件。
> - 使用 zsh 时，您可能需要在 pattern 串的两端加上双引号。
```
./coscli sync ~/test/ cos://bucket1/example/ -r --include ".*.mp4"
```

## 操作示例

### 同步上传文件

```plaintext
./coscli sync ~/example.txt cos://bucket1/example.txt
```

### 同步下载文件

```plaintext
./coscli sync cos://bucket1/example.txt ~/example.txt
```

### 桶内同步拷贝文件

```plaintext
./coscli sync cos://bucket1/example.txt cos://bucket1/example_copy.txt
```

### 跨桶同步拷贝文件

```plaintext
./coscli sync cos://bucket1/example.txt cos://bucket2/example_copy.txt
```
