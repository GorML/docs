# Adding a function version tag

When creating a new version, it's assigned the `$latest` [tag](../../concepts/function.md#) by default.

{% list tabs %}

- CLI

   {% include [cli-install](../../../_includes/cli-install.md) %}

   {% include [default-catalogue](../../../_includes/default-catalogue.md) %}

   To add a version tag, run the command:

   ```
   yc serverless function version set-tag --id <version ID> --tag <tag>
   ```

   Result:

   ```
   id: b09ch6pmpohfc9sogj5f
   function_id: b097d9ous3gep99khe83
   created_at: "2019-06-13T09:12:38.464Z"
   runtime: python37
   entrypoint: test.handler
   resources:
     memory: "134217728"
   execution_timeout: 5s
   image_size: "4096"
   status: ACTIVE
   tags:
   - beta
   - first
   log_group_id: eolv6578frac08uh5h6s
   ```

- API

   You can add a tag using the [setTag](../../functions/api-ref/Function/setTag.md).

- {{ TF }}

   {% include [terraform-definition](../../../_tutorials/terraform-definition.md) %}

   If you don't have {{ TF }}, [install it and configure the {{ yandex-cloud }} provider](../../../tutorials/infrastructure-management/terraform-quickstart.md#install-terraform).

   To add a version tag:

   1. In the configuration file, add the `tags` section for the `yandex_function` resource and specify the list of tags in `tags = ["<tag_name>"]` format.

      Example function description in the {{ TF }} configuration:

      ```
      resource "yandex_function" "test-function" {
          name               = "test-function"
          description        = "Test function"
          user_hash          = "first-function"
          runtime            = "python37"
          entrypoint         = "main"
          memory             = "128"
          execution_timeout  = "10"
          service_account_id = "<service account ID>"
          tags               = ["my_tag"]
          content {
              zip_filename = "<path to ZIP archive>"
          }
      }
      ```

      For more information about the `yandex_function` resource parameters, see the [provider documentation]({{ tf-provider-link }}/function).

   1. Check the configuration using the command:

      ```
      terraform validate
      ```

      If the configuration is correct, the following message is returned:

      ```
      Success! The configuration is valid.
      ```

   1. Run the command:

      ```
      terraform plan
      ```

      The terminal will display a list of resources with parameters. No changes are made at this step. If the configuration contains errors, {{ TF }} will point them out.

   1. Apply the configuration changes:

      ```
      terraform apply
      ```
   1. Confirm the changes: type `yes` into the terminal and press **Enter**.

   You can verify that the tags are there in the [management console]({{ link-console-main }}) or using this [CLI](../../../cli/quickstart.md) command:

   ```
   yc serverless function version list --function-name <function name>
   ```

- {{ yandex-cloud }} Toolkit

   You can add a tag using the [{{ yandex-cloud }} Toolkit plugin](https://github.com/yandex-cloud/ide-plugin-jetbrains/blob/master/README.en.md) for the IDE family on the [IntelliJ platform](https://www.jetbrains.com/opensource/idea/) from [JetBrains](https://www.jetbrains.com/).

{% endlist %}
