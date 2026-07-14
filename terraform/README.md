# Terraform Infrastructure Setup

This directory contains the Terraform configuration for deploying the portfolio website to AWS S3 and CloudFront.

## Architecture

- **S3 Bucket**: Stores the static website files (HTML, CSS, images)
- **CloudFront Distribution**: CDN for global content delivery with HTTPS
- **Origin Access Identity (OAI)**: Secure access from CloudFront to S3, blocking direct public access
- **Versioning & Encryption**: Enabled for data protection and compliance

## Files

- `main.tf` — Main infrastructure: S3, CloudFront, OAI, policies
- `variables.tf` — Variable definitions and validation rules
- `outputs.tf` — Outputs for CloudFront domain, S3 bucket info, and website URL
- `terraform.tfvars` — Variable values (customize before deployment)

## Quick Start

### 1. Update Configuration

Edit `terraform.tfvars` and set your unique S3 bucket name:

```hcl
bucket_name = "my-portfolio-website-2026"  # Must be globally unique
```

### 2. Initialize Terraform

```bash
cd terraform
terraform init
```

### 3. Review Plan

```bash
terraform plan
```

### 4. Deploy

```bash
terraform apply
```

This will:
- Create the S3 bucket with security best practices
- Create a CloudFront distribution
- Output the CloudFront domain name for your website

### 5. Upload Website Files

After deployment, upload your website files to the S3 bucket:

```bash
aws s3 sync .. s3://your-bucket-name --exclude "terraform/*" --exclude ".git/*"
```

Or use the AWS Console to upload files to the bucket.

## Outputs

After deployment, view the outputs:

```bash
terraform output
```

Key outputs:
- `cloudfront_domain_name` — Your website URL prefix
- `website_url` — Full HTTPS URL to your website

## Security Features

✓ S3 bucket is private (public access blocked)
✓ CloudFront OAI provides secure access to S3
✓ HTTPS/TLS enforced via CloudFront
✓ Versioning enabled for disaster recovery
✓ Server-side encryption enabled
✓ All resources tagged for organization and cost tracking

## Troubleshooting

**Bucket name already exists**: S3 bucket names are globally unique. Choose a different name in `terraform.tfvars`.

**Access Denied errors**: Ensure your AWS credentials have permissions for S3, CloudFront, and IAM.

**CloudFront takes time to deploy**: CloudFront distribution creation can take 10-20 minutes.

## Cleanup

To remove all resources:

```bash
terraform destroy
```

**⚠️ Warning**: This will delete the S3 bucket and all its contents. Ensure you've backed up your website files.

## Next Steps

- Configure a custom domain name (add Route 53 and ACM certificate)
- Set up GitHub Actions for automated deployments
- Add cache invalidation to CI/CD pipeline
