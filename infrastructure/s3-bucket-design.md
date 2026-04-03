# S3 Bucket Structure

## Naming Convention
`dotlearn-{purpose}-{env}` — e.g., `dotlearn-videos-dev`, `dotlearn-videos-prod`

## Buckets

| Bucket                        | Contents                  | Upload                              | Read                          |
|-------------------------------|---------------------------|-------------------------------------|-------------------------------|
| dotlearn-videos-{env}         | MP4 lesson videos         | Lesson Service presigned PUT URL    | CloudFront signed URL         |
| dotlearn-assets-{env}         | Thumbnails, PDFs          | Presigned PUT                       | CloudFront OAI                |
| dotlearn-certificates-{env}   | Generated PDF certificates| Certificate Service                 | Presigned GET URL (24hr)      |
| dotlearn-avatars-{env}        | User profile pictures     | Auth Service presigned PUT          | CloudFront OAI                |
| dotlearn-email-templates-{env}| HTML email templates      | Manual only                         | Notification Service          |

## Access Rules
- All buckets: Block Public Access ON
- Video access: CloudFront signed URLs only (1-hour expiry)
- Certificate access: Presigned GET URL (24-hour expiry)
- No bucket is ever directly public