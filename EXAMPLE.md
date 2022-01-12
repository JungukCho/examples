## Play with Pulumi
This repository is to play Pulumi to understand how it works.

### Installation
1. [Download and Install](https://www.pulumi.com/docs/get-started/install/)
```shell
curl -fsSL https://get.pulumi.com | sh
```

### With Pulumi backend
1. Azure example
* azure-ts-aci
```shell
cd azure-ts-aci
pulumi stack init dev
npm install
pulumi config set azure-native:location westus2
pulumi up
pulumi stack output containerIPv4Address
curl "$(pulumi stack output containerIPv4Address)"
pulumi destroy
```

2. AWS example
* aws-ts-webserver
```shell
aws sts get-caller-identity
pulumi up
pulumi stack output
curl $(pulumi stack output publicIp)
pulumi destroy --yes
pulumi stack rm dev
```


### With S3 backend example
1. [State and Backends](https://www.pulumi.com/docs/intro/concepts/state/#logging-into-the-aws-s3-backend)
* Pulumi standalon mode without using Pulumi backend. For example, we can use a local filesystem or AWS S3.

2. AWS Example
```shell
export AWS_REGION="us-west-2"
aws s3 ls s3://<bucket name>
pulumi config set aws:region us-west-2
pulumi login s3://<bucket name>/aws-webserver
pulumi stack init aws-webserver
pulumi up
pulumi stack output
curl $(pulumi stack output publicIp)
pulumi destroy --yes
pulumi stack rm aws-webserver
```

3. Azure example
```shell
cd azure-ts-aci
pulumi login s3://<bucket name>/azure-ts-aci
pulumi stack init dev
pulumi config set azure-native:location westus2
pulumi up
pulumi stack output containerIPv4Address
curl "$(pulumi stack output containerIPv4Address)"
pulumi destroy --yes
pulumi stack rm azure-ts-aci
```