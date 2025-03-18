# Load Environment Variables Action

This GitHub Action loads environment variables from a given string or a GitHub Secret.

## Usage

1.  **Add the Action to your workflow:**

    ```yaml
    jobs:
      load_env:
        runs-on: ubuntu-latest
        steps:
          - name: Load environment variables
            uses: your-username/load-env-vars-action@v1 # Replace with your username and action name
            with:
              # env_content: ${{ secrets.MY_ENV_VARS }} # Optional: Specify environment variables directly
              # secret_name: 'MY_ENV_VARS' # Optional: Specify a different secret name
          - name: Use loaded variables
            run: |
              echo "Loaded variable: $MY_VARIABLE" # Example usage
    ```

2.  **Set up your GitHub Secret:**

    Create a GitHub Secret (e.g., `ENV` or as specified by `secret_name`) containing your environment variables in the format `KEY=VALUE` (one per line).

## Inputs

| Name          | Description                                                                 | Default          | Required |
| :------------ | :-------------------------------------------------------------------------- | :--------------- | :------- |
| `env_content` | Content of environment variables, defaults to reading from a secret.        | `${{ secrets.ENV }}` | No       |
| `secret_name` | Name of the secret to read from if `env_content` is not provided.          | `ENV`            | No       |

## Notes

* This Action uses the `xom9ikk/dotenv` Action to load environment variables.
* The `load-mode: strict` option ensures that all variables are loaded and no errors are ignored.
* Ensure the secret or `env_content` contains valid `KEY=VALUE` pairs.

## Example

use default `secrets.ENV`：

```yaml
- name: Load environment variables
  uses: your-username/load-env-vars-action@v1
```

use custom secret：

```yaml
- name: Load environment variables
  uses: your-username/load-env-vars-action@v1
  with:
    secret_name: 'MY_ENV_VARS'
```

or directly use envs：

```yaml
- name: Load environment variables
  uses: your-username/load-env-vars-action@v1
  with:
    env_content: |
      MY_VARIABLE=value
      ANOTHER_VARIABLE=another_value
```