---
title: How to configure credentials using a secrets store 
---
import Prerequisites from '../../connecting_to_your_data/components/prerequisites.jsx'

Choose which Secret Manager you are using:
 1. [AWS Secrets Manager](#1-aws-secrets-manager)
 2. [GCP Secret Manager](#2-gcp-secret-manager)
 3. [Azure Key Vault](#3-azure-key-vault)

---

### 1. AWS Secrets Manager

This guide will explain how to configure your ``great_expectations.yml`` project config to substitute variables from AWS Secrets Manager.

<Prerequisites>

- [Set up a working deployment of Great Expectations](../../../tutorials/getting_started/intro.md)
- [Knowledge on how to populate credentials](../configuring_data_contexts/how_to_configure_credentials_using_a_yaml_file_or_environment_variables.md)
- Configured a secret store and secrets in the cloud:
    - [AWS](https://docs.aws.amazon.com/secretsmanager/latest/userguide/tutorials_basic.html)

</Prerequisites>

:::warning

Secrets store substitution uses the configurations from your ``great_expectations.yml`` project config **after** all other types of substitution are applied (from environment variables or from the ``config_variables.yml`` config file)

The secrets store substitution works based on keywords. It tries to retrieve secrets from the secrets store for the following values :

- AWS: values starting with ``secret|arn:aws:secretsmanager`` if the values you provide don't match with the keywords above, the values won't be substituted.

:::

#### Setup

To use AWS Secrets Manager, you may need to install the ``great_expectations`` package with its ``aws_secrets`` extra requirement:

```bash
pip install great_expectations[aws_secrets]
```

In order to substitute your value by a secret in AWS Secrets Manager, you need to provide an arn of the secret like this one:
``secret|arn:aws:secretsmanager:123456789012:secret:my_secret-1zAyu6``

:::note

The last 7 characters of the arn are automatically generated by AWS and are not mandatory to retrieve the secret, thus ``secret|arn:aws:secretsmanager:region-name-1:123456789012:secret:my_secret`` will retrieve the same secret.

:::

You will get the latest version of the secret by default.

You can get a specific version of the secret you want to retrieve by specifying its version UUID like this: ``secret|arn:aws:secretsmanager:region-name-1:123456789012:secret:my_secret:00000000-0000-0000-0000-000000000000``

If your secret value is a JSON string, you can retrieve a specific value like this:
``secret|arn:aws:secretsmanager:region-name-1:123456789012:secret:my_secret|key``

Or like this:
``secret|arn:aws:secretsmanager:region-name-1:123456789012:secret:my_secret:00000000-0000-0000-0000-000000000000|key``

**Example:**

```yaml
# great_expectations/great_expectations.yml

datasources:
  dev_postgres_db:
    class_name: SqlAlchemyDatasource
    data_asset_type:
      class_name: SqlAlchemyDataset
      module_name: great_expectations.dataset
    module_name: great_expectations.datasource
    credentials:
      drivername: secret|arn:aws:secretsmanager:${AWS_REGION}:${ACCOUNT_ID}:secret:dev_db_credentials|drivername
      host: secret|arn:aws:secretsmanager:${AWS_REGION}:${ACCOUNT_ID}:secret:dev_db_credentials|host
      port: secret|arn:aws:secretsmanager:${AWS_REGION}:${ACCOUNT_ID}:secret:dev_db_credentials|port
      username: secret|arn:aws:secretsmanager:${AWS_REGION}:${ACCOUNT_ID}:secret:dev_db_credentials|username
      password: secret|arn:aws:secretsmanager:${AWS_REGION}:${ACCOUNT_ID}:secret:dev_db_credentials|password
      database: secret|arn:aws:secretsmanager:${AWS_REGION}:${ACCOUNT_ID}:secret:dev_db_credentials|database
  prod_postgres_db:
    class_name: SqlAlchemyDatasource
    data_asset_type:
      class_name: SqlAlchemyDataset
      module_name: great_expectations.dataset
    module_name: great_expectations.datasource
    credentials:
      drivername: secret|arn:aws:secretsmanager:${AWS_REGION}:${ACCOUNT_ID}:secret:PROD_DB_CREDENTIALS_DRIVERNAME
      host: secret|arn:aws:secretsmanager:${AWS_REGION}:${ACCOUNT_ID}:secret:PROD_DB_CREDENTIALS_HOST
      port: secret|arn:aws:secretsmanager:${AWS_REGION}:${ACCOUNT_ID}:secret:PROD_DB_CREDENTIALS_PORT
      username: secret|arn:aws:secretsmanager:${AWS_REGION}:${ACCOUNT_ID}:secret:PROD_DB_CREDENTIALS_USERNAME
      password: secret|arn:aws:secretsmanager:${AWS_REGION}:${ACCOUNT_ID}:secret:PROD_DB_CREDENTIALS_PASSWORD
      database: secret|arn:aws:secretsmanager:${AWS_REGION}:${ACCOUNT_ID}:secret:PROD_DB_CREDENTIALS_DATABASE
```

---

### 2. GCP Secret Manager

This guide will explain how to configure your ``great_expectations.yml`` project config to substitute variables from GCP Secrets Manager.

<Prerequisites>

- [Set up a working deployment of Great Expectations](../../../tutorials/getting_started/intro.md)
- [Knowledge on how to populate credentials](../configuring_data_contexts/how_to_configure_credentials_using_a_yaml_file_or_environment_variables.md)
- Configured a secret store and secrets in the cloud:
    - [GCP](https://cloud.google.com/secret-manager/docs/quickstart)

</Prerequisites>

:::warning

Secrets store substitution uses the configurations from your ``great_expectations.yml`` project config **after** all other types of substitution are applied (from environment variables or from the ``config_variables.yml`` config file)

The secrets store substitution works based on keywords. It tries to retrieve secrets from the secrets store for the following values :

- GCP: values matching the following regex ``^secret\|projects\/[a-z0-9\_\-]{6,30}\/secrets`` if the values you provide don't match with the keywords above, the values won't be substituted.

:::

#### Setup

To use GCP Secret Manager, you may need to install the ``great_expectations`` package with its ``gcp`` extra requirement:

```bash
pip install great_expectations[gcp]
```

In order to substitute your value by a secret in GCP Secret Manager, you need to provide a name of the secret like this one:
``secret|projects/project_id/secrets/my_secret``

You will get the latest version of the secret by default.

You can get a specific version of the secret you want to retrieve by specifying its version id like this: ``secret|projects/project_id/secrets/my_secret/versions/1``

If your secret value is a JSON string, you can retrieve a specific value like this:
``secret|projects/project_id/secrets/my_secret|key``

Or like this:
``secret|projects/project_id/secrets/my_secret/versions/1|key``

**Example:**

```yaml
# great_expectations/great_expectations.yml

datasources:
  dev_postgres_db:
    class_name: SqlAlchemyDatasource
    data_asset_type:
      class_name: SqlAlchemyDataset
      module_name: great_expectations.dataset
    module_name: great_expectations.datasource
    credentials:
      drivername: secret|projects/${PROJECT_ID}/secrets/dev_db_credentials|drivername
      host: secret|projects/${PROJECT_ID}/secrets/dev_db_credentials|host
      port: secret|projects/${PROJECT_ID}/secrets/dev_db_credentials|port
      username: secret|projects/${PROJECT_ID}/secrets/dev_db_credentials|username
      password: secret|projects/${PROJECT_ID}/secrets/dev_db_credentials|password
      database: secret|projects/${PROJECT_ID}/secrets/dev_db_credentials|database
  prod_postgres_db:
    class_name: SqlAlchemyDatasource
    data_asset_type:
      class_name: SqlAlchemyDataset
      module_name: great_expectations.dataset
    module_name: great_expectations.datasource
    credentials:
      drivername: secret|projects/${PROJECT_ID}/secrets/PROD_DB_CREDENTIALS_DRIVERNAME
      host: secret|projects/${PROJECT_ID}/secrets/PROD_DB_CREDENTIALS_HOST
      port: secret|projects/${PROJECT_ID}/secrets/PROD_DB_CREDENTIALS_PORT
      username: secret|projects/${PROJECT_ID}/secrets/PROD_DB_CREDENTIALS_USERNAME
      password: secret|projects/${PROJECT_ID}/secrets/PROD_DB_CREDENTIALS_PASSWORD
      database: secret|projects/${PROJECT_ID}/secrets/PROD_DB_CREDENTIALS_DATABASE
```

---

### 3. Azure Key Vault

This guide will explain how to configure your ``great_expectations.yml`` project config to substitute variables from Azure Key Vault.

<Prerequisites>

- [Set up a working deployment of Great Expectations](../../../tutorials/getting_started/intro.md)
- [Knowledge on how to populate credentials](../configuring_data_contexts/how_to_configure_credentials_using_a_yaml_file_or_environment_variables.md)
- Configured a secret store and secrets in the cloud:
    - [Azure](https://docs.microsoft.com/azure/key-vault/secrets/quick_create_portal)

</Prerequisites>

:::warning

Secrets store substitution uses the configurations from your ``great_expectations.yml`` project config **after** all other types of substitution are applied (from environment variables or from the ``config_variables.yml`` config file)

The secrets store substitution works based on keywords. It tries to retrieve secrets from the secrets store for the following values :

- Azure : values matching the following regex ``^secret\|https:\/\/[a-zA-Z0-9\-]{3,24}\.vault\.azure\.net`` if the values you provide don't match with the keywords above, the values won't be substituted.

:::


#### Setup

To use Azure Key Vault, you may need to install the ``great_expectations`` package with its ``azure_secrets`` extra requirement:

```bash
pip install great_expectations[azure_secrets]
```

In order to substitute your value by a secret in Azure Key Vault, you need to provide a name of the secret like this one:
``secret|https://my-vault-name.vault.azure.net/secrets/my-secret``

You will get the latest version of the secret by default.

You can get a specific version of the secret you want to retrieve by specifying its version id (32 lowercase alphanumeric characters) like this: ``secret|https://my-vault-name.vault.azure.net/secrets/my-secret/a0b00aba001aaab10b111001100a11ab``

If your secret value is a JSON string, you can retrieve a specific value like this:
``secret|https://my-vault-name.vault.azure.net/secrets/my-secret|key``

Or like this:
``secret|https://my-vault-name.vault.azure.net/secrets/my-secret/a0b00aba001aaab10b111001100a11ab|key``


**Example:**

```yaml
# great_expectations/great_expectations.yml

datasources:
  dev_postgres_db:
    class_name: SqlAlchemyDatasource
    data_asset_type:
      class_name: SqlAlchemyDataset
      module_name: great_expectations.dataset
    module_name: great_expectations.datasource
    credentials:
      drivername: secret|https://${VAULT_NAME}.vault.azure.net/secrets/dev_db_credentials|drivername
      host: secret|https://${VAULT_NAME}.vault.azure.net/secrets/dev_db_credentials|host
      port: secret|https://${VAULT_NAME}.vault.azure.net/secrets/dev_db_credentials|port
      username: secret|https://${VAULT_NAME}.vault.azure.net/secrets/dev_db_credentials|username
      password: secret|https://${VAULT_NAME}.vault.azure.net/secrets/dev_db_credentials|password
      database: secret|https://${VAULT_NAME}.vault.azure.net/secrets/dev_db_credentials|database
  prod_postgres_db:
    class_name: SqlAlchemyDatasource
    data_asset_type:
      class_name: SqlAlchemyDataset
      module_name: great_expectations.dataset
    module_name: great_expectations.datasource
    credentials:
      drivername: secret|https://${VAULT_NAME}.vault.azure.net/secrets/PROD_DB_CREDENTIALS_DRIVERNAME
      host: secret|https://${VAULT_NAME}.vault.azure.net/secrets/PROD_DB_CREDENTIALS_HOST
      port: secret|https://${VAULT_NAME}.vault.azure.net/secrets/PROD_DB_CREDENTIALS_PORT
      username: secret|https://${VAULT_NAME}.vault.azure.net/secrets/PROD_DB_CREDENTIALS_USERNAME
      password: secret|https://${VAULT_NAME}.vault.azure.net/secrets/PROD_DB_CREDENTIALS_PASSWORD
      database: secret|https://${VAULT_NAME}.vault.azure.net/secrets/PROD_DB_CREDENTIALS_DATABASE
```
