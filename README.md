Go to AWS Console and create a role 'Admin' with all the needed access rights.

Install [AWS Command Line Interface](http://docs.aws.amazon.com/cli/latest/userguide/installing.html).

Create a file ~/.aws/credentials with the following content:
```
[default]
aws_access_key_id = <your access key>
aws_secret_access_key = <your secret>
```

Create a file ~/.aws/config with the following profile:
```
[profile softwerkskammer]
role_arn = arn:aws:iam::<your amazon account>:role/Admin
region = eu-central-1
source_profile = default
```

Create the infrastructure stack:
```
aws cloudformation deploy --capabilities CAPABILITY_IAM --stack-name infrastructure --template-file ./infrastructure.yml --region eu-central-1 --profile softwerkskammer
```

Create a simple auto scaling group:
```
aws cloudformation deploy --capabilities CAPABILITY_IAM --stack-name autoscalinggroup --template-file ./simpleAutoscalingGroup.yml --region eu-central-1 --profile softwerkskammer
```

Create an ECS Cluster:
```
aws cloudformation deploy --capabilities CAPABILITY_IAM --stack-name ecscluster --template-file ./cluster.yml --region eu-central-1 --profile softwerkskammer
```

Create a service in the ECS Cluster:
```
aws cloudformation deploy --capabilities CAPABILITY_IAM --stack-name service --template-file ./service.yml --region eu-central-1 --profile softwerkskammer
```
