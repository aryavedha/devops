
- Terraform Iam policy in aws and change as per requirment 
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
