- cloud cost optimization
- To search for stopped EC2 instances using the AWS CLI, you need to use the describe-instances command with a filter on the instance state.

- Here’s the correct command:
```
aws ec2 describe-instances \
  --filters "Name=instance-state-name,Values=stopped"
```

Explanation:

--filters: Lets you apply conditions.

Name=instance-state-name,Values=stopped: Filters only instances in the stopped state.

If you want only the Instance IDs of stopped instances:
```
aws ec2 describe-instances \
  --filters "Name=instance-state-name,Values=stopped" \
  --query "Reservations[*].Instances[*].InstanceId" \
  --output text
```

 If you also want Instance ID + Name tag for readability:

```
aws ec2 describe-instances \
  --filters "Name=instance-state-name,Values=stopped" \
  --query "Reservations[*].Instances[*].[InstanceId,Tags[?Key=='Name'].Value|[0]]" \
  --output table
```
---
