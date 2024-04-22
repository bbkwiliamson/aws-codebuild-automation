# aws-codebuild-automation
deploying to cloudformation using codebuild


# buildspec.yml

in this file, all you need to do is replace **AccountID** on (IF-STATEMENTS) to be or reflect those of your own actual accountIDs, otherwise there is nothing to change from the code perspective

this file must be deployed into the codecommit repo used by codebuild

# role-cross-account.yml

this file just creates a role that you need in an account that codebuild will need to deploy to. for example that means, you must deploy this template in TEST, PROD, DEV, OR SIT accounts, this obviously depends on how many accounts you use.
the region parameter you can also change it to be the one you are using or prefer

