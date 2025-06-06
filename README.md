# terraform-aws-simple-s3-bucket

A simple Terraform module to create an AWS S3 bucket.

## Usage

```hcl
module "s3_bucket" {
  source      = "app.terraform.io/YOUR_ORG_NAME/s3-bucket/aws"
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
