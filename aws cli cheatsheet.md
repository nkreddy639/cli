# AWS CLI Cheatsheet

@see http://docs.aws.amazon.com/cli/latest/reference/
@see https://github.com/toddm92/aws/wiki/AWS-CLI-Cheat-Sheet




## EC2
@see http://docs.aws.amazon.com/cli/latest/reference/ec2/index.html

##### describe instances
@see http://docs.aws.amazon.com/cli/latest/reference/ec2/describe-instances.html

##### list all instances
```shell
SERVER_LIST=$(aws ec2 describe-instances);
```

##### list instances, that are running, having tag
```shell
SERVER_LIST=$(aws ec2 describe-instances \
  --filters "Name=tag:<tag_name>" \
  "Name=instance-state-name,Values=running");
```

##### list instances, that are running, having tag and value
```shell
SERVER_LIST=$(aws ec2 describe-instances \
  --filters "Name=tag:<tag_name>,Values=<tag_value>" \
  "Name=instance-state-name,Values=running");
```

##### filter results, retrieve Public DNS, using jq
```shell
SERVER_LIST_DNS=$( echo $SERVER_LIST | jq '.Reservations[].Instances[].PublicDnsName'  | tr -d '"');
```

##### filter results, retrieve Public IP Address, using jq
```shell
SERVER_LIST_IP=$( echo $SERVER_LIST | jq '.Reservations[].Instances[].PublicIpAddress'  | tr -d '"');
```

##### create instances
@see http://docs.aws.amazon.com/cli/latest/reference/ec2/create-image.html

##### terminate instances
@see http://docs.aws.amazon.com/cli/latest/reference/ec2/terminate-instances.html

##### delete volume
@see http://docs.aws.amazon.com/cli/latest/reference/ec2/delete-volume.html



<br/>
## IAM

##### list the age of all keys
[source](https://evidentio.squarespace.com/blog/2015/3/20/top-10-aws-security-best-practices-6-rotate-all-the-keys-regularly)
```shell
aws iam get-credential-report --output text | awk '{print $1}' | base64 -D | awk -F, '{printf("%-15s %-25s %-25s %-25s %-25s\n",$1,$9,$10,$11,$12)}'
```