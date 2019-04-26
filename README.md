# EC2 metadata mock-up

A mock-up of EC2 metadata, all values in this repository are contrived for the purpose of testing scripts.

## Structure

```markdown

repository: https://github.com/SQLHorizons/metadata.git
  .
  └── iam
  │   └── info
  └── placement
  │   └── availability-zone
  ├── ami-id
  ├── instance-id
  ├── instance-type
  ├── local-ipv4
  └── README.md

```

## Querying

```powershell

##  get machine metadata.
$uri = "http://ms-oc27:8081/repository/latest/metadata"
$tags = @(
    "aws_ami=$((Invoke-WebRequest $uri/ami-id).Content)"
    "aws_az=$((Invoke-WebRequest $uri/placement/availability-zone).Content)"
    "iam_instance_profile=$(((Invoke-WebRequest $uri/iam/info).Content | ConvertFrom-Json).InstanceProfileArn)"
    "aws_id=$((Invoke-WebRequest $uri/instance-id).Content)"
    "aws_type=$((Invoke-WebRequest $uri/instance-type).Content)"
    "aws_ip=$((Invoke-WebRequest $uri/local-ipv4).Content)"
    "role=$($ServerParams.role)"
    "dns=$($ServerParams.dns)"
)

Return $tags

```
