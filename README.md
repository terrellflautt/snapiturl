# SnapIT URL - Professional URL Shortener

Short links with analytics, branding, and link management for businesses and individuals.

## 🚀 Live Production

**Website:** https://snapiturl.com
**API:** https://api.snapiturl.com
**CDN:** CloudFront + S3

## 📦 Branch Strategy

### `main` - Development Branch
- Active development and new features
- Test changes here before production
- May contain experimental code

### `production` - Production Branch
- **Deploy ONLY from this branch**
- Stable, tested code currently live on snapiturl.com
- Tagged releases (e.g., `v1.0.0-production`)

## 🏷️ Current Production Version

**v1.0.0-production** - 6-Tier Pricing with Bug Fixes

**Features:**
- 6-tier unified pricing (FREE to Enterprise)
- Monthly/yearly billing (20% annual discount)
- Fixed authentication (no CORS errors)
- Sticky top navigation
- Stripe integration (test mode)

## 💰 Pricing Tiers

| Tier | Monthly | Yearly | Features |
|------|---------|--------|----------|
| FREE | $0 | $0 | 50 Short URLs, 20 Dynamic QRs, 100 Form Responses |
| Starter | $3.99 | $39.99 | 1K Short URLs, 500 QRs/month, 1K Form Responses |
| Professional | $9.99 | $99.99 | 5K Short URLs, 2.5K QRs/month, 5K Responses + API |
| Business | $29.99 | $299.99 | 25K Short URLs, 10K QRs/month, Team (15 users) |
| Premium | $49.99 | $499.99 | 100K Short URLs, 50K QRs/month, Team (50 users) |
| Enterprise | $99.99 | $999.99 | Unlimited everything + White-glove support |

## 🛠️ Tech Stack

- **Frontend:** Vanilla HTML/CSS/JavaScript
- **Backend:** AWS API Gateway + Lambda + DynamoDB
- **Auth:** Google OAuth 2.0
- **Payments:** Stripe Checkout
- **CDN:** CloudFront
- **Storage:** S3

## 🔒 Security

**NEVER commit these files:**
- ❌ `config.js` (contains API keys)
- ❌ `.env` files
- ❌ AWS credentials
- ❌ OAuth client secrets

**Safe to commit:**
- ✅ `index.html`
- ✅ `config.template.js`
- ✅ CSS/JS assets
- ✅ Documentation

## 📝 Deployment

### Deploy to Production

```bash
# Switch to production branch
git checkout production

# Merge from main (after testing)
git merge main

# Deploy to S3
aws s3 cp index.html s3://snapiturl.com/index.html --content-type "text/html"
aws s3 cp config.js s3://snapiturl.com/config.js --content-type "application/javascript"

# Invalidate CloudFront cache
aws cloudfront create-invalidation --distribution-id E3MGEG0LRH9XFQ --paths "/*"

# Tag the release
git tag -a v1.x.x-production -m "Release description"
git push origin production --tags
```

## 🌐 Related Projects

- **SnapIT QR:** https://github.com/terrellflautt/snapitqr
- **Shared Infrastructure:** Unified Google OAuth + Stripe subscriptions

## 📄 License

Proprietary - All rights reserved

## 🤝 Support

For issues or questions: snapitsaas@gmail.com