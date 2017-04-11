Go to AWS Console and create a role 'Admin' with all the needed access rights.
Install AWS cli.

Create a file ~/.aws/config with the follwong profile:
```
[profile softwerkskammer]
role_arn = arn:aws:iam::<your amazon account>:role/Admin
region = eu-central-1
source_profile = default
```

Create the infrastructure stack:
```
aws cloudformation create-stack --capabilities CAPABILITY_IAM --stack-name infrastructure --template-body file://infrastructure.yml --region eu-central-1 --profile softwerkskammer
```
Or update:
```
aws cloudformation update-stack --capabilities CAPABILITY_IAM --stack-name infrastructure --template-body file://infrastructure.yml --region eu-central-1 --profile softwerkskammer
```

Create a simple auto scaling group:
```
aws cloudformation create-stack --capabilities CAPABILITY_IAM --stack-name autoscalinggroup --template-body file://simpleAutoscalingGroup.yml --region eu-central-1 --profile softwerkskammer
```
Or update:
```
aws cloudformation update-stack --capabilities CAPABILITY_IAM --stack-name autoscalinggroup --template-body file://simpleAutoscalingGroup.yml --region eu-central-1 --profile softwerkskammer
```
