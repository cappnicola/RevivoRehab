# Deployment Guide

## Build Process

1. **Standard Build**:
   ```bash
   npm run build
   ```

2. **Fix Deployment Paths**:
   ```bash
   node scripts/fix-deployment.js
   ```

## What the Fix Script Does

The deployment fix script addresses the mismatch between Vite's build output and the server's static file serving expectations:

### Problem
- **Vite builds to**: `dist/public/` (contains index.html and assets)
- **Server expects files in**: `server/public` (relative to server directory)
- **Deployment expects files in**: `dist/` (root of dist directory)

### Solution
The script creates a dual-path solution:

1. **Creates symbolic link**: `server/public` → `../dist/public`
   - Allows the production server to find static files
   - Maintains compatibility with existing server configuration

2. **Copies files to dist root**: `dist/public/*` → `dist/*`
   - Places index.html and assets in the deployment-expected location
   - Ensures Replit deployment can find the index.html file

### Directory Structure After Fix
```
dist/
├── index.html          # ← Copied for deployment
├── assets/             # ← Copied for deployment
├── index.js           # ← Server bundle
└── public/            # ← Original Vite output
    ├── index.html
    └── assets/

server/
└── public → ../dist/public  # ← Symbolic link
```

## Deployment Steps

1. Run build: `npm run build`
2. Run fix: `node scripts/fix-deployment.js`
3. Deploy the project with files now correctly positioned

## Verification

Check that files exist in correct locations:
```bash
# Check deployment files (root of dist)
ls -la dist/index.html dist/assets/

# Check server access (symbolic link)
ls -la server/public

# Check original build output
ls -la dist/public/
```

All three locations should show the static files are accessible.