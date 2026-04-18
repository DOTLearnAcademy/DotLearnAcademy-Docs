# CloudFront Distribution Strategy

## Distribution
Single CloudFront distribution with multiple origins and path-based routing.

## Path Behaviours

| Path Pattern  | Origin              | Cache TTL          | Notes                                      |
|---------------|---------------------|--------------------|--------------------------------------------|
| /api/*        | EC2 instance (HTTP) | No cache (TTL=0)   | All API calls bypass CloudFront cache      |
| /static/*     | S3 (assets bucket)  | 1 year (immutable) | Angular build outputs use hashed filenames |
| /video/*      | S3 (videos bucket)  | Signed URLs only   | 1-hour expiry per signed URL               |
| /* (default)  | S3 (SPA bucket)     | 5 minutes          | Serves Angular index.html for all routes   |

## Security
- OAI (Origin Access Identity) on all S3 origins — S3 never directly public
- Signed URLs for video content — prevents hotlinking
- HTTPS only — HTTP redirected to HTTPS at CloudFront level

## Notes
- No WAF attached — cost saving for dev/portfolio
- No custom SSL certificate needed initially — use CloudFront default domain