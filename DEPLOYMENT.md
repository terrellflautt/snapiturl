# SnapIT URL Deployment Guide

## 🎯 Overview

SnapIT URL is the URL shortening counterpart to SnapIT QR, offering professional URL shortening with analytics, custom domains, and integrated QR code generation.

## 🔄 Domain Relationship

- **snapitqr.com**: QR code focused (primary QR generation, secondary URL shortening)
- **snapiturl.com**: URL shortening focused (primary URL shortening, secondary QR generation)

Both domains share:
- ✅ Same user accounts and authentication
- ✅ Same backend APIs and databases
- ✅ Same subscription plans and billing
- ✅ Cross-platform functionality

## 🚀 Key Features

### URL Shortening Focus
- Smart URL shortening with detailed analytics
- Custom domain support (snapiturl.com and snapitqr.com)
- Click tracking and geographic insights
- Integrated QR code generation for short URLs

### User Experience
- URL-optimized SEO and copywriting
- Clean, professional interface
- Simple feedback system (no intrusive popups)
- Cross-linking with SnapIT QR

### Technical Integration
- API endpoints: api.snapiturl.com and api.snapitqr.com
- Shared authentication system
- Real-time analytics and tracking
- Free tier: 3 short URLs + 1 dynamic QR

## 📦 Deployment Requirements

### 1. Configuration Files
```bash
# Required files (not in git):
config.js         # Contains sensitive keys and configuration
```

### 2. Configuration Setup
Copy and configure from template:
```bash
cp config.template.js config.js
# Edit config.js with production values
```

### 3. Required Configuration Values
```javascript
window.SNAPIT_CONFIG = {
    GOOGLE_CLIENT_ID: 'your-google-oauth-client-id',
    STRIPE_PUBLISHABLE_KEY: 'your-stripe-publishable-key',
    WEB3FORMS_ACCESS_KEY: 'your-web3forms-access-key',
    BUSINESS_EMAIL: 'your-business-email@domain.com'
};
```

## 🔧 Deployment Steps

### 1. AWS S3 + CloudFront
```bash
# Upload to S3 bucket for snapiturl.com
aws s3 sync . s3://snapiturl-bucket/ --exclude ".git/*" --exclude "*.md"

# Invalidate CloudFront cache
aws cloudfront create-invalidation --distribution-id YOUR_DISTRIBUTION_ID --paths "/*"
```

### 2. Domain Configuration
- DNS pointing to CloudFront distribution
- SSL certificate configured
- Security headers configured

### 3. Backend Verification
Ensure these APIs are operational:
- `https://api.snapiturl.com/shorten` - URL shortening
- `https://api.snapitqr.com/generate` - QR code generation
- Both APIs should support CORS for snapiturl.com

## ✅ Testing Checklist

### Core Functionality
- [ ] URL shortening with snapiturl.com domain works
- [ ] URL shortening with snapitqr.com domain works
- [ ] Click tracking and analytics functional
- [ ] QR code generation for short URLs works
- [ ] Redirects working properly

### User Experience
- [ ] Google OAuth sign-in works
- [ ] User dashboard shows correct usage limits
- [ ] Free tier limits properly enforced
- [ ] Stripe payment integration ready
- [ ] Feedback button works (sends to business email)

### Cross-Domain Integration
- [ ] Navigation to SnapIT QR works
- [ ] Shared authentication across domains
- [ ] Consistent branding and experience

## 🔍 Monitoring & Analytics

### Health Checks
- URL shortening API response times
- Redirect success rates
- User authentication success rates
- Payment processing status

### Key Metrics
- Short URLs created per day
- Click-through rates
- User sign-up conversions
- Free to paid tier conversions

## 🛠 Maintenance

### Regular Tasks
- Monitor API performance
- Update SSL certificates
- CloudFront cache optimization
- Analytics data review

### Security
- Regular security headers review
- Configuration file security audit
- API rate limiting monitoring
- Authentication system monitoring

---

**Repository**: Private configuration required
**Last Updated**: September 27, 2025
**Contact**: Via feedback button or business email