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
- If not already done, create a new AWS Access Key (Access Key and Secret Key).
- In Travis, open the Project and add a new secret environment variable (found in Settings) called `AWS_SECRET_KEY` and enter your secret key.
- Add the following section to your `.travis.yml`:
   ```yaml
    deploy:
      provider: s3
      access_key_id: ACCESS_KEY
      secret_access_key: $AWS_SECRET_KEY
      bucket: BUCKET_NAME
      skip_cleanup: true
      acl: public_read
      local_dir: dist/webapp
    ```
  Replace `ACCESS_KEY` with your Access Key and `BUCKET_NAME` with your bucket name.
  - `local_dir` refers to the local directory which content is synced to the bucket. Adapt it to the respective output directory of your project. If this value is left out the whole working directory will by synchronized.
  - By default the deployment is only enabled for the master branch. To enable it for other branches add an `on` section (see `.travis.yml` in this example). 
