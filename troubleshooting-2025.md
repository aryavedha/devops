- cloud cost optimization
- check stopped instances from the AWS Console (Dashboard). Here’s how you can do it:

Steps in AWS Management Console (Dashboard):

Login to your AWS account.

Go to EC2 service (search for "EC2" in the search bar).

In the left-hand menu, click Instances → Instances.

At the top, you’ll see a filter/search bar.

In the filter dropdown (or search box), select Instance state → choose Stopped.

Alternatively, type directly in the search bar:
```
instance-state-name: stopped
```

Now the dashboard will only show Stopped EC2 Instances.


---
- search for stopped EC2 instances using the (AWS CLI), you need to use the describe-instances command with a filter on the instance state.

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
