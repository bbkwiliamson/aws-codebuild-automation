# aws-codebuild-automation
deploying to cloudformation using codebuild


# buildspec.yml

in this file, all you need to do is replace **AccountID** on (IF-STATEMENTS) to be or reflect those of your own actual accountIDs, otherwise there is nothing to change from the code perspective

this file must be deployed into the codecommit repo used by codebuild

# role-cross-account.yml

this file just creates a role that you need in an account that codebuild will need to deploy to. for example that means, you must deploy this template in TEST, PROD, DEV, OR SIT accounts, this obviously depends on how many accounts you use.
the region parameter you can also change it to be the one you are using or prefer

NOTE: the principal must be the accountID of the account that will be deploying.   for example: if i am deploying from account 1111111, the accountID will be 111111. and remember this role is created in the receiving account or destination account, not the source acccount.

# s3-encryption-bucket.yml

this file is the one being deployed to create s3 bucket just to test if the whole set-up works fine.
the file must also be uploaded to the codecommit repo used by codebuild
the key name of this file, must be the same as the one on the codebuild environment variables **S3_BUCKET ** value

also make sure that the bucket name is unique as s3 buckets must be globally unique


# deploy-codecommit-codebuild.yml

firstly you must change the parameter default values to be the ones that suits you.
**DeploymentID** parameter represent the Account ID where you want to make the deployment, so make sure is the right account ID.
**REGION** is the aws region where you want to make the deployment.
**STACK_NAME** is the name of the cloudformation stack that will be created... if you already have a stack in cloudformation that you want to work with, you can copy that name on the default value of this.

this file also is the core of this codebuild pipeline. it creates **S3 BUCKET**, **codecommit repo**, **service role** and the **CodeBuild service project**

NOTE: on the environment variables of the codebuild on this file. there are **ROLE_ARN_DEV**, **ROLE_ARN_SIT**, **ROLE_ARN_PROD**, **ROLE_ARN_TOOLS**, these keys represents the arns of the roles created in the specific account that you want the deployment to be happening. these roles are created by **role-cross-account.yml** mentioned above.

otherwise anything else can remain the same.


from here after everything is deployed on cloudformation, having uploaded the buildspec.yml and s3-encryption-bucket.yml to the codecommit repo, you can go to codebuild service console, check the one you just created and then click START BUILD, this should run successfully and deploy to your specified account


