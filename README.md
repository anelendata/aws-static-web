# Script to host a static web site via AWS CloudFront CDN

## First things first!
- I'm not responsible for your AWS cost. Please be responsible. (Monthly cost should be less than a cup of coffee...)
- This script assumes you have sufficient AWS knowledge.
(Route 53, Certificate Manager, CloudFormation, S3, CloudFront, etc)

## Files

```
├── LICENSE
├── README.md
├── bin
│   ├── cfn_create_stack
│   ├── cfn_update_stack
│   └── publish
├── cfn
│   └── cloudformation-template-s3-cloudfront-ssl.yml
├── dot_env_template
└── s3_config
    └── cors.json
```

## Prereq:
1. Create an AWS account and have admin access
2. Install AWS CLI (See https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html )
3. Get AWS Keys and set AWS profile and credentials (See https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-files.html)
4. A Route53 managed domain name
5. Local web asset files

## Deployment

### Step 1:

Copy ./dot_env_template to .env/prod
Edit the parameters in the file everything except CLOUDFRONT_DIST_ID.
You don't need to have existing CloudFormation Stack, SSL Certificate, and bucket.

### Step 2:

Run the Script to create a SSL certificate, S3 bucket and Cloudfront distribution:
```
bin/cfn_create_stack .env/prod
```

Check CloudFormation Console to monitor the progress and troubleshoot issues
https://<your-aws-region>.console.aws.amazon.com/cloudformation/


### Step 3:

Log in to AWS Console and get CloudFront Distribution ID (https://<your-aws-region>.console.aws.amazon.com/cloudfront/)
Update .env by filling CLOUDFRONT_DIST_ID.

### Step 4:

Publish the content and invalidate CloudFront cache:
```
bin/publish .env/prod
```

To update the content, you just need to repeat Step 4.


# About this project

This project is developed by
ANELEN and friends. Please check out the ANELEN's
[open innovation philosophy and other projects](https://anelen.co/open-source.html)

![ANELEN](https://avatars.githubusercontent.com/u/13533307?s=400&u=a0d24a7330d55ce6db695c5572faf8f490c63898&v=4)
---

Copyright &copy; 2023~ Anelen Co., LLC
