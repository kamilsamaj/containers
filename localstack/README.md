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
