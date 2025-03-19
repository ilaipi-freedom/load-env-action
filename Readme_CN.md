# Load Environment Variables Action

这个 GitHub Action 允许你从密钥或提供的字符串内容中加载环境变量。它会创建一个临时的 `.env` 文件，并使用 [dotenv action](https://github.com/xom9ikk/dotenv) 加载这些变量。

## 特性

- 从密钥或直接字符串内容加载环境变量
- 基于优先级的加载：env_content > secret_name
- 可配置的失败模式（strict/skip），用于处理未找到环境变量的情况
- 创建临时的 `.env` 文件以避免污染工作空间
- 支持严格模式和跳过模式来处理缺失的环境变量

## 使用方法

```yaml
- uses: ilaipi-freedom/load-env-action@v1.0.0
  with:
    env_content: |
      KEY1=value1
      KEY2=value2
    secret_name: 'ENV'  # 可选，默认为空字符串
    load_mode: 'strict' # 可选，默认为 'strict'
```

## 输入参数

| 名称 | 描述 | 是否必需 | 默认值 |
|------|------|----------|--------|
| `env_content` | 环境变量的内容，默认从密钥中读取 | 否 | '' |
| `secret_name` | 如果未提供 env_content，则从该密钥中读取 | 否 | 'ENV' |
| `load_mode` | 设置当未找到环境变量内容时是否失败（strict）或继续（skip） | 否 | 'strict' |

## 输出

无

## 示例

### 使用密钥

```yaml
- uses: ilaipi-freedom/load-env-action@v1.0.0
  with:
    secret_name: 'MY_ENV'
```

### 使用直接内容

```yaml
- uses: ilaipi-freedom/load-env-action@v1.0.0
  with:
    env_content: |
      API_KEY=123456
      DB_URL=mongodb://localhost:27017
```

### 使用跳过模式

```yaml
- uses: ilaipi-freedom/load-env-action@v1.0.0
  with:
    load_mode: 'skip'
```

## 许可证

MIT
