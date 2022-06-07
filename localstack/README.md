# AWS local development environment - localstack

## Start the container

* **Prerequisite:** Create a directory to store persistent data

```shell
mkdir -p ~/.localstack/data
```

* Start the container:

```shell
docker compose up -d
```

## Use the environment:

### AWS CLI

Most of the services listen on `TCP/localhost:4566` by default, so you'll need to configure it as a custom API endpoint.

* You can either set the `--endpoint-url` flag for `aws` CLI:

```shell
aws --endpoint-url=http://localhost:4566 <service> <command>`
```

* Or, you can use the `awslocal` wrapper (available only for AWS CLI v1)

```shell
pipx install awslocal

awslocal <service> <command>
```

## KMS Encryption/Decryption

```shell
awslocal kms create-key

awslocal kms encrypt \
    --key-id='arn:aws:kms:us-east-1:000000000000:key/7ae13db8-cd11-4a82-9976-9ba0291e35ac' \
    --plaintext fileb:///tmp/test.txt

awslocal kms decrypt \
    --ciphertext-blob \
        fileb://<(echo "N2FlMTNkYjgtY2QxMS00YTgyLTk5NzYtOWJhMDI5MWUzNWFjZhojcrHfRja8j1J2fGRok6cGyMn9+TGBlhuLO6V9tU2+/RaG9I+n" | base64 -d) \
    --output text \
    --query Plaintext | base64 -d
```
