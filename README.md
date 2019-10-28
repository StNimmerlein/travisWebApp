# Webapp

## Deploy to AWS S3

- In AWS create S3 bucket and set it to `Static Website Hosting` (in Properties).
- In Permissions use the following policy (to be able to push data with access permissions):
  ```json
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Sid": "AllowPublicRead",
                "Effect": "Allow",
                "Principal": {
                    "AWS": "PRINCIPAL_ID"
                },
                "Action": [
                    "s3:AbortMultipartUpload",
                    "s3:DeleteObject",
                    "s3:GetObject",
                    "s3:GetObjectAcl",
                    "s3:PutObject",
                    "s3:PutObjectAcl"
                ],
                "Resource": "arn:aws:s3:::BUCKET_NAME/*"
            }
        ]
    }
    ```
  Replace `BUCKET_NAME` and `PRINCIPAL_ID` with your respective values. The latter one can be your AWS Account ID. In this example project I chose `179261888537` as `PRINCIPAL_ID` and `stnimmerwapp` as `BUCKET_NAME`.
