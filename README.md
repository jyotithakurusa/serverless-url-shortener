# serverless-url-shortener
Serverless URL shortener built on AWS — API Gateway, Lambda, and DynamoDB with CloudFront caching. Infrastructure provisioned end-to-end in Terraform with remote state on S3 plus DynamoDB locking. CI/CD pipeline runs `terraform plan` on PR and `terraform apply` on merge via GitHub Actions.
