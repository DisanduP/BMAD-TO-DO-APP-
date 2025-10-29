# Azure Static Web Apps Deployment Guide

## Project Overview
- **Project**: test-react-deployment
- **Framework**: React (Create React App)
- **Build Tool**: react-scripts 5.0.1
- **Generated on**: October 29, 2025

## Prerequisites
- Azure account with active subscription
- Azure Static Web Apps service enabled
- Node.js 18+ installed locally
- Git repository (recommended)

## Local Development
```bash
# Install dependencies
npm install

# Start development server
npm start

# Run tests
npm test

# Build for production
npm run build
```

## Azure Deployment Configuration

### Generated Configuration (azure-static-web-apps.yml)
```yaml
name: test-react-deployment
build:
  command: npm run build
  output_location: build
routes:
  - route: /*
    serve: /build/index.html
    statusCode: 200
triggers:
  - type: http
    paths:
      - api/*
    noCache: true
```

### Configuration Explanation
- **Build Command**: `npm run build` - Uses react-scripts to create optimized production build
- **Output Location**: `build/` - Standard CRA build directory
- **Routes**: SPA fallback configuration ensures client-side routing works
- **Triggers**: Basic HTTP trigger setup for potential API routes

## Automated Deployment Options 🚀

### Option 1: One-Click Azure CLI Deployment (Recommended)
**Run this single command for instant deployment:**
```bash
./deploy-to-azure.sh
```

**What it does:**
- Automatically creates Azure resources
- Deploys your build folder instantly
- Provides live URL immediately
- Handles all configuration automatically

**Requirements:**
- Azure CLI installed (`az login` completed)
- Build folder ready (`npm run build`)

### Option 2: GitHub Actions CI/CD (For Teams)
**Already configured!** The `.github/workflows/azure-static-web-apps.yml` file is ready.

**Setup required secrets in GitHub:**
1. Go to your GitHub repo → Settings → Secrets and variables → Actions
2. Add: `AZURE_STATIC_WEB_APPS_API_TOKEN` (get from Azure Portal)

**Benefits:**
- Automatic deployment on every push to main
- Pull request previews
- Team collaboration friendly
- Version controlled deployments

## 🚀 Deployment Options

### **Option 1: Azure Portal (Immediate - 2 minutes)**

**Perfect for testing and one-off deployments**

1. **Open Azure Portal**: https://portal.azure.com
2. **Search** for "Static Web Apps"
3. **Click "Create"**
4. **Configure**:
   - **Subscription**: Choose your active subscription
   - **Resource Group**: Create new or use existing
   - **Name**: `bmad-react-demo` (or your choice)
   - **Region**: East US (or nearest to you)
   - **Source**: Choose "Other"
5. **Upload Build**: Drag and drop the entire `build/` folder
6. **Deploy**: Click "Create" - your app will be live in 2 minutes!

**✅ Result**: Live HTTPS URL instantly!

---

### **Option 2: GitHub Actions CI/CD (Automated)**

**Perfect for teams and continuous deployment**

#### Step 1: Create GitHub Repository
```bash
# Run the setup script
../setup-github-repo.sh

# Or manually:
git init
git add .
git commit -m "React app with Azure deployment"
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO.git
git push -u origin main
```

#### Step 2: Configure Azure Secrets
1. Go to your GitHub repo → **Settings** → **Secrets and variables** → **Actions**
2. Add new secret: `AZURE_STATIC_WEB_APPS_API_TOKEN`
3. Get the token from: Azure Portal → Your Static Web App → **GitHub Actions** tab

#### Step 3: Automatic Deployment
- Every `git push` to `main` triggers deployment
- Pull requests get preview deployments
- Check **Actions** tab for deployment status

**✅ Result**: Fully automated deployment pipeline!

---

### **Current Status**
- ✅ **Build Ready**: `build/` folder contains optimized production files
- ✅ **Azure Config**: `azure-static-web-apps.yml` configured for React SPA
- ✅ **GitHub Actions**: Workflow ready for automated deployments
- ✅ **Documentation**: Complete deployment guides included

### **Quick Test Commands**
```bash
# Test build locally
npm run build

# Start local development
npm start

# Deploy via portal (manual)
# → Upload build/ folder to Azure Portal

# Deploy via GitHub (automated)
# → Push to GitHub repo with secrets configured
```

## Post-Deployment Verification

### Check Deployment Status
1. Go to Azure Portal → Your Static Web App
2. Check "Deployment history" tab
3. Verify build completed successfully
4. Check for any build errors

### Test the Live Site
1. Visit the generated URL (e.g., `https://your-app-name.azurestaticapps.net`)
2. Test navigation and routing
3. Verify all assets load correctly
4. Check browser console for errors

### Common Issues & Solutions

#### Issue: 404 on page refresh
**Solution**: The routing configuration handles this. If still occurring, ensure the route rule is correct.

#### Issue: Assets not loading
**Solution**: Check that all files in `build/` were uploaded. Verify relative paths.

#### Issue: Build fails in Azure
**Solution**: Ensure Node.js version in Azure matches local version. Check build logs.

#### Issue: Environment variables not working
**Solution**: Configure environment variables in Azure Portal under "Configuration"

## Maintenance

### Updating Your App
1. Make changes locally
2. Test build: `npm run build`
3. Commit and push to GitHub (if using GitHub integration)
4. Azure will automatically rebuild and deploy

### Monitoring
- Check Azure Portal for deployment status
- Monitor usage and performance metrics
- Review application logs for errors

### Scaling
Azure Static Web Apps automatically scale based on traffic. No manual scaling required.

## Security Considerations
- All traffic served over HTTPS by default
- Custom domains supported
- Authentication providers available (Azure AD, GitHub, Twitter)
- API routes protected by Azure Functions security

## Cost Optimization
- Free tier available for personal projects
- Pay only for custom domains and premium features
- Bandwidth included in free tier limits

---
*This guide was generated by the Azure Deployer Agent for React projects*
