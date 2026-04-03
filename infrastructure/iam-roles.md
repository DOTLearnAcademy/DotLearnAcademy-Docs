# IAM Roles & Permissions (Least Privilege)

## EC2 Instance Role (all services)
```json
{
  "Actions": [
    "ecr:GetAuthorizationToken",
    "ecr:BatchGetImage",
    "logs:CreateLogGroup",
    "logs:PutLogEvents",
    "secretsmanager:GetSecretValue"
  ]
}
```

## Auth Service Role
```json
{
  "Actions": [
    "ses:SendEmail",
    "secretsmanager:GetSecretValue"
  ],
  "Resource": "dotlearn/jwt-private-key"
}
```

## Lesson Service Role
```json
{
  "Actions": [
    "s3:PutObject",
    "s3:GeneratePresignedUrl"
  ],
  "Resource": "dotlearn-videos-{env}/*"
}
```

## Certificate Service Role
```json
{
  "Actions": [
    "s3:PutObject",
    "s3:GetObject"
  ],
  "Resource": "dotlearn-certificates-{env}/*"
}
```

## Payment Service Role
```json
{
  "Actions": [
    "sqs:SendMessage",
    "secretsmanager:GetSecretValue"
  ],
  "Resource": "dotlearn-payment-*-{env}"
}
```

## Notification Service Role
```json
{
  "Actions": [
    "ses:SendEmail",
    "sqs:ReceiveMessage",
    "sqs:DeleteMessage"
  ],
  "Resource": "consumer queues"
}
```