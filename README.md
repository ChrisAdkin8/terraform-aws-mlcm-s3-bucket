# terraform-aws-simple-s3-bucket

A simple Terraform module to create an AWS S3 bucket.

The initial aim of this repo is to provide something incredibly simple to demonstrate module life cycle management with a private module registry,
including:

- Using of sentinel policies such that only non-root modules in the private registry can be used 
- Module deprecation
- Module recovation
- Module usage observability

## Usage

### Invoking The Module from A HCP Terraform Private Registry 

```hcl
module "s3_bucket" {
  source      = "app.terraform.io/YOUR_ORG_NAME/simple-s3-bucket/aws"
  bucket_name = "my-unique-bucket-name"
  tags = {
    Environment = "dev"
  }
}
```

### Invoking The Module from The Public Registry 

```hcl
module "s3_bucket" {
  source      = "YOUR_GITHUB_ACCOUNT_NAME/simple-s3-bucket/aws"
  bucket_name = "my-unique-bucket-name"
  tags = {
    Environment = "dev"
  }
}
```

## Inputs

| Name        | Description            | Type         | Default | Required |
|-------------|------------------------|--------------|---------|----------|
| bucket_name | Name of the bucket     | `string`     | n/a     | yes      |
| tags        | Tags for the bucket    | `map(string)`| `{}`    | no       |

## Outputs

| Name         | Description             |
|--------------|-------------------------|
| bucket_name  | The bucket name         |
| bucket_arn   | The ARN of the bucket   |

## Observability

Module usage can be observed either via the HCP Terraform explorer, or by scraping the explorer endpoint:
```
curl -s \
  --header "Authorization: Bearer $TFC_TOKEN" \
  "https://app.terraform.io/api/v2/organizations/$ORG_NAME/explorer?type=modules" \
  | jq
```
