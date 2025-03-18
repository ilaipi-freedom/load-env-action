# Load Environment Variables Action

这个 GitHub Action 从给定的字符串或 GitHub Secret 中加载环境变量。

## 用法

1.  **将 Action 添加到您的 workflow：**

    ```yaml
    jobs:
      load_env:
        runs-on: ubuntu-latest
        steps:
          - name: 加载环境变量
            uses: your-username/load-env-vars-action@v1 # 替换为您的用户名和 action 名称
            with:
              # env_content: ${{ secrets.MY_ENV_VARS }} # 可选：直接指定环境变量内容
              # secret_name: 'MY_ENV_VARS' # 可选：指定不同的 secret 名称
          - name: 使用加载的环境变量
            run: |
              echo "加载的变量: $MY_VARIABLE" # 示例用法
    ```

2.  **设置您的 GitHub Secret：**

    创建一个 GitHub Secret（例如 `ENV` 或由 `secret_name` 指定的名称），其中包含您的环境变量，格式为 `KEY=VALUE`（每行一个）。

## 输入参数

| 参数名          | 描述                                                                    | 默认值           | 是否必填 |
| :------------ | :------------------------------------------------------------------------- | :--------------- | :------- |
| `env_content` | 环境变量的内容，默认为从 secret 中读取。                                     | `${{ secrets.ENV }}` | 否       |
| `secret_name` | 如果未提供 `env_content`，则从此 secret 读取环境变量。                         | `ENV`            | 否       |

## 注意事项

* 这个 Action 使用 `xom9ikk/dotenv` Action 来加载环境变量。
* `load-mode: strict` 选项确保加载所有变量，并且不忽略任何错误。
* 请确保 secret 或 `env_content` 包含有效的 `KEY=VALUE` 对。

## 示例


使用默认的 `secrets.ENV`：

```yaml
- name: Load environment variables
  uses: your-username/load-env-vars-action@v1
```

使用自定义的 secret：

```yaml
- name: Load environment variables
  uses: your-username/load-env-vars-action@v1
  with:
    secret_name: 'MY_ENV_VARS'
```

直接提供环境变量内容：

```yaml
- name: Load environment variables
  uses: your-username/load-env-vars-action@v1
  with:
    env_content: |
      MY_VARIABLE=value
      ANOTHER_VARIABLE=another_value
```
