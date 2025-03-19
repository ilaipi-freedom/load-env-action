# Load Environment Variables Action

This GitHub Action allows you to load environment variables from either a secret or a provided string content. It creates a temporary `.env` file and loads the variables using the [dotenv action](https://github.com/xom9ikk/dotenv).

## Features

- Load environment variables from a secret or direct string content
- Priority-based loading: env_content > secret_name
- Configurable failure mode (strict/skip) when no environment variables are found
- Creates temporary `.env` file to avoid workspace pollution
- Supports both strict and skip modes for handling missing environment variables

## Usage

```yaml
- uses: ilaipi-freedom/load-env-action@v1.0.0
  with:
    env_content: |
      KEY1=value1
      KEY2=value2
    secret_name: 'ENV'  # Optional, defaults to 'ENV'
    load_mode: 'strict' # Optional, defaults to 'strict'
```

## Inputs

| Name | Description | Required | Default |
|------|-------------|----------|---------|
| `env_content` | Content of environment variables, defaults to reading from a secret | false | '' |
| `secret_name` | Name of the secret to read from if env_content is not provided | false | '' |
| `load_mode` | Sets whether the program should fail when no env content is found (strict) or continue (skip) | false | 'strict' |

## Outputs

None

## Examples

### Using Secret

```yaml
- uses: ilaipi-freedom/load-env-action@v1.0.0
  with:
    secret_name: 'MY_ENV'
```

### Using Direct Content

```yaml
- uses: ilaipi-freedom/load-env-action@v1.0.0
  with:
    env_content: |
      API_KEY=123456
      DB_URL=mongodb://localhost:27017
```

### Using Skip Mode

```yaml
- uses: ilaipi-freedom/load-env-action@v1.0.0
  with:
    load_mode: 'skip'
```

## License

MIT