# Custom Domain Setup Guide: Connecting Squarespace Domain to GitHub Pages

This guide will help you connect your Squarespace domain **www.pink-sesame.com** to your GitHub Pages website.

## Overview

Your website is hosted on GitHub Pages and you want to use your Squarespace domain to access it. This requires:
1. Enabling GitHub Pages for your repository
2. Configuring DNS records in Squarespace
3. Adding the custom domain in GitHub Pages settings

## Step 1: Enable GitHub Pages

1. Go to your repository: https://github.com/ankur-mehrotra/pink-sesame-website
2. Click on **Settings** (top navigation)
3. In the left sidebar, click **Pages**
4. Under **Source**, select:
   - Branch: **main**
   - Folder: **/ (root)**
5. Click **Save**
6. Wait a few minutes for the initial deployment

## Step 2: Configure DNS in Squarespace

### Access Squarespace DNS Settings

1. Log in to your Squarespace account
2. Go to **Settings** → **Domains** → **DNS Settings**
3. Find your domain: **pink-sesame.com**

### Add DNS Records

You need to add the following DNS records:

#### A Records (for apex domain)

Add **FOUR A records** pointing to GitHub's IP addresses:

| Type | Host | Value           | TTL  |
|------|------|-----------------|------|
| A    | @    | 185.199.108.153 | 3600 |
| A    | @    | 185.199.109.153 | 3600 |
| A    | @    | 185.199.110.153 | 3600 |
| A    | @    | 185.199.111.153 | 3600 |

#### CNAME Record (for www subdomain)

| Type  | Host | Value                                   | TTL  |
|-------|------|-----------------------------------------|------|
| CNAME | www  | ankur-mehrotra.github.io                | 3600 |

### Important Notes:

- **Host "@"** represents the root/apex domain (pink-sesame.com)
- **Host "www"** represents the www subdomain (www.pink-sesame.com)
- Remove any existing A or CNAME records that conflict with these
- Squarespace may have some default records - you can keep MX, TXT, and other records

## Step 3: Add Custom Domain in GitHub Pages

1. Go back to your repository: https://github.com/ankur-mehrotra/pink-sesame-website
2. Navigate to **Settings** → **Pages**
3. Under **Custom domain**, enter: `www.pink-sesame.com`
4. Click **Save**
5. GitHub will automatically check DNS configuration
6. Once verified, check the box for **Enforce HTTPS** (recommended)

## Step 4: Wait for DNS Propagation

- DNS changes can take **1-24 hours** to propagate worldwide
- You can check DNS propagation status at: https://dnschecker.org
- Enter your domain and check if the DNS records are visible globally

## Verification Steps

After DNS propagates, verify your setup:

1. **Test www subdomain**: Visit https://www.pink-sesame.com
2. **Test apex domain**: Visit https://pink-sesame.com (should redirect to www)
3. **Check HTTPS**: Ensure the padlock icon appears in your browser

## Troubleshooting

### DNS Not Resolving

- **Wait longer**: DNS propagation can take up to 24 hours
- **Clear browser cache**: Try incognito/private browsing mode
- **Check DNS records**: Use `dig www.pink-sesame.com` or `nslookup www.pink-sesame.com`

### "Domain's DNS Record Could Not Be Retrieved" Error

- Verify all A records and CNAME record are correct in Squarespace
- Ensure there are no conflicting records
- Wait for full DNS propagation

### HTTPS Not Working

- Make sure DNS has fully propagated first
- In GitHub Pages settings, uncheck and re-check "Enforce HTTPS"
- Wait a few minutes for certificate provisioning

### Website Shows 404 Error

- Verify GitHub Pages is enabled (Settings → Pages)
- Check that the CNAME file exists in your repository
- Ensure the domain in CNAME file matches what's in GitHub Pages settings

## DNS Record Format Examples

### If Squarespace uses different terminology:

**For A Records:**
```
Type: A
Name: @ (or leave blank for root)
Points to: 185.199.108.153
```

**For CNAME Record:**
```
Type: CNAME
Name: www
Points to: ankur-mehrotra.github.io
```

## Additional Resources

- [GitHub Pages Custom Domain Documentation](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site)
- [Squarespace DNS Settings Help](https://support.squarespace.com/hc/en-us/articles/205812378-DNS-settings)
- [DNS Propagation Checker](https://dnschecker.org)

## Summary

✅ CNAME file created in repository (www.pink-sesame.com)
✅ GitHub Pages enabled
⏳ Configure DNS in Squarespace (follow steps above)
⏳ Add custom domain in GitHub Pages settings
⏳ Wait for DNS propagation (1-24 hours)
⏳ Enable HTTPS enforcement

Once complete, your website will be accessible at https://www.pink-sesame.com!
