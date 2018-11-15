Run this to create just a code repository
```
aws cloudformation create-stack --profile "default" \
  --stack-name "infrastructure-repo-bakeoff-stack" \
  --capabilities CAPABILITY_IAM \
  --template-body file://infrastructure_repo.yml \
  --parameters file://parameters.yml
```

Provision HTTP Git credentials through IAM

Clone your repo and add code
```
git clone <CloneUrlHttp>
```

Create a template.yml file in your repo with the following contents
```
AWSTemplateFormatVersion: 2010-09-09
Description: ''
Resources:
  Artifacts:
    Type: AWS::S3::Bucket
    Properties:
      BucketName: 'mcwhirter-infrastructure-repo'
```

Run this to update the stack with new resources
```
aws cloudformation update-stack --profile "default" \
  --stack-name "infrastructure-repo-bakeoff-stack" \
  --capabilities CAPABILITY_IAM \
  --template-body file://infrastructure_repo.yml \
  --parameters file://parameters.yml
```


Source: https://github.com/stelligent/cloudformation_templates/blob/master/labs/codecommit/codecommit-cpl-cfn.json
