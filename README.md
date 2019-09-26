# aws-s3-replication

AWS CloudFormation templates that set up AWS S3 replication between two S3 buckets in two different AWS accounts.

## Files

`source-bucket.yml` is an AWS CloudFormation template that creates an S3 bucket that acts as a Source S3 Bucket for S3 replication.  It also defines the required IAM Role that gets attached to the S3 Replication Configuration for the Source Bucket.

`destination-bucket.yml` is an AWS CloudFormation template that creates an S3 bucket that acts as a Destination S3 Bucket for S3 replication.  It also defines the required S3 Bucket Policy that gets attached to the S3 bucket to allow the Source Bucket replicate files into it.

## Instructions

First, deploy a CloudFormation stack using `destination-bucket.yml` in the account where you want to have a Destination S3 bucket.  Fill in all of the required CloudFormation Parameters based on their descriptions.  Once deployed, grab the S3 destination bucket's ARN value from the Outputs of the CloudFormation stack.

Next, deploy a CloudFormation stack using `source-bucket.yml` in another account where you want to have the Source S3 bucket.  Fill in all of the required CloudFormation Parameters based on their descriptions, including using the Destination Bucket ARN value obtained from the previous step.

If everything succeeded, any file that you put into the Source S3 Bucket will get replicated to the Destination S3 Bucket.

## Note on encryption

Note that this solution uses SSE-S3 encrpytion for both S3 buckets.  Using AWS KMS is possible when using S3 replication but would require additional configuration.  All S3 replication traffic is always encrypted.
