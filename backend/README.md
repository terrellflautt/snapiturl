# SnapIT URL Backend

## Shared Backend Architecture

**snapiturl.com** and **snapitqr.com** share the same unified backend API.

The backend Lambda functions are located in the **snapitqr** repository at:
```
/mnt/c/Users/decry/Desktop/snapitqr/backend/
```

## Backend Services

All URL shortening operations are handled by the `url-operations` Lambda function in the snapitqr backend.

### API Endpoints (URL Shortener)

- `POST /url/shorten` - Create short URL
- `GET /url/list` - List user's short URLs
- `DELETE /url/{shortCode}` - Delete short URL
- `GET /r/{shortCode}` - Redirect to target URL

### Shared Infrastructure

- **API Gateway**: `hvfj8o1yb0.execute-api.us-east-1.amazonaws.com/production`
- **Lambda Functions**: snapitqr-url-operations
- **DynamoDB Tables**:
  - snapitqr-shorturls (URL storage)
  - snapitqr-users (User accounts)
  - snapitqr-analytics (Analytics events)
- **Authentication**: Shared Google OAuth via snapitqr-auth-operations
- **Stripe Integration**: Shared subscription management

## Deployment

To deploy backend changes, use the snapitqr backend deployment:

```bash
cd /mnt/c/Users/decry/Desktop/snapitqr/backend
serverless deploy --stage production
```

Or use the deploy scripts:

```bash
cd /mnt/c/Users/decry/Desktop/snapitqr/backend
./deploy-production.sh
```

## Frontend Integration

The snapiturl frontend (`frontend/index.html`) connects to the same API endpoints as snapitqr.

**API Base URL**: `https://hvfj8o1yb0.execute-api.us-east-1.amazonaws.com/production`

## Configuration

All backend configuration (API keys, secrets, etc.) is managed via AWS SSM Parameter Store:

- `/snapitqr/jwt-secret` - JWT authentication secret
- `/snapitqr/google-client-id` - Google OAuth client ID
- `/snapitqr/stripe-secret-key` - Stripe API key
- `/snapitqr/stripe-webhook-secret` - Stripe webhook secret

## Development

When developing new features:

1. Backend changes → Edit snapitqr/backend Lambda functions
2. Frontend changes → Edit snapiturl/frontend/index.html
3. Deploy backend first, then frontend

## Resources

- Backend Code: `/mnt/c/Users/decry/Desktop/snapitqr/backend/`
- Frontend Code: `/mnt/c/Users/decry/Desktop/snapiturl/frontend/`
- Serverless Config: `/mnt/c/Users/decry/Desktop/snapitqr/backend/serverless.yml`
- Architecture Docs: `/mnt/c/Users/decry/Desktop/snapitqr-architecture.md`
