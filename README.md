# -AWS-S3-bucket
Prerequisite :

AWS Account - services = IAM, KMS, BUCKET, BUCKET POLICY

GitHub Account - services = Repository, secrets, GitHub actions workflows
 Go to aws -> iam -> user -> create one user along with access keys
aws->s3-> create -> name your bucket > create
name: Portfolio 
on:
  push:
    branches:
    - main
    - master
jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout
      uses: actions/checkout@v1

    - name: configure AWS credentials
      uses: aws-actions/configure-aws-credentials@v1
      with:
        aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
        aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
        aws-region: us-east-1

    - name: Deploy my website into s3 bucket
      run: aws s3 sync . s3://pg-portfolio --delete

     {
     "Version": "2012-10-17",
     "Statement": [
         {
             "Sid": "PublicReadGetObject",
             "Effect": "Allow",
             "Principal": "*",
             "Action": "s3:GetObject",
             "Resource": "arn:aws:s3:::pg-portfolio/*"
         }
     ]
 }



