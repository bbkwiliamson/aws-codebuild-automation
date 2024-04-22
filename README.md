# aws-codebuild-automation
deploying to cloudformation using codebuild


# buildspec.yml

in this file, all you need to do is replace **AccountID** on (IF-STATEMENTS) to be or reflect those of your own actual accountIDs, otherwise there is nothing to change from the code perspective

this file must be deployed into the codecommit repo used by codebuild

# role-cross-account.yml

this file just creates a role that you need in an account that codebuild will need to deploy to. for example that means, you must deploy this template in TEST, PROD, DEV, OR SIT accounts, this obviously depends on how many accounts you use.
the region parameter you can also change it to be the one you are using or prefer

# s3-encryption-bucket.yml

this file is the one being deployed to create s3 bucket just to test if the whole set-up works fine.
the file must also be uploaded to the codecommit repo used by codebuild
the key name of this file, must be the same as the one on the codebuild environment variables **S3_BUCKET ** value
