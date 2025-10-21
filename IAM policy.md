
- Terraform Iam policy in aws and change as per requirment
- In aws create a role and create a policy and attach policy to role and attach role to instance  
```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Statement1",
      "Effect": "Allow",
      "Action": [
        "ec2:*",
        "s3:*",
        "logs:*",
        "cloudwatch:*",
        "iam:PassRole",
        "elasticloadbalancing:*"
      ],
      "Resource": ["*"]
    }
  ]
}
```

---
