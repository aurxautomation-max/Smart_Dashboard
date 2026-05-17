# 🚀 QUICK START - DEPLOY TO RENDER IN 5 MINUTES

## Prerequisites

- GitHub account
- Render account (free)
- Your code repository

---

## Step 1: Test Locally (2 min)

```bash
# Install all dependencies
npm install

# Build the entire application
npm run build

# Start the production server
npm start
```

✅ If successful, visit: `http://localhost:5000`

---

## Step 2: Push to GitHub (1 min)

```bash
# Initialize and commit
git init
git add .
git commit -m "Full-stack app ready for Render"

# Create main branch
git branch -M main

# Add remote (replace with your repo URL)
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPO.git

# Push to GitHub
git push -u origin main
```

---

## Step 3: Create Render Service (1 min)

1. Go to https://render.com
2. Click **"New +"** → **"Web Service"**
3. Click **"Connect a repository"**
4. Select your repository
5. Click **"Connect"**

---

## Step 4: Configure Deployment (1 min)

Fill in these fields:

| Field         | Value             |
| ------------- | ----------------- |
| Name          | `smart-leads-app` |
| Environment   | `Node`            |
| Build Command | `npm run build`   |
| Start Command | `npm start`       |

Click **"Add Environment Variable"** and add:

```
NODE_ENV = production
JWT_SECRET_KEY = your-super-secret-key-here-change-me-to-something-secure
```

---

## Step 5: Deploy! (✅ Done!)

1. Click **"Create Web Service"**
2. Wait 5-10 minutes for build to complete
3. View live at: `https://your-app-name.onrender.com`

---

## 🎯 Key URLs

| Component      | URL                                         |
| -------------- | ------------------------------------------- |
| **Frontend**   | `https://your-app-name.onrender.com`        |
| **API**        | `https://your-app-name.onrender.com/api/v1` |
| **Admin User** | username: `admin`, password: `admin123`     |

---

## 📝 Default Admin Credentials

```
Email: admin
Password: admin123
```

⚠️ Change this after first login!

---

## ⚡ What Happens During Deployment

1. **Build Phase** (Render runs):

   ```
   npm run build
   ↓
   Frontend builds: Vite → smart-leads-backend/dist/public
   Backend builds: TypeScript → smart-leads-backend/dist/index.js
   ```

2. **Start Phase** (Render runs):
   ```
   npm start
   ↓
   Node runs smart-leads-backend/dist/index.js
   ↓
   Express starts on PORT
   SQLite initializes
   Serves frontend + API
   ```

---

## 🔄 Making Changes

```bash
# Make code changes locally
git add .
git commit -m "Your change description"
git push origin main

# Render automatically redeploys! (no manual action needed)
```

---

## 📊 Monitoring

In Render Dashboard:

- View real-time **Logs**
- Check **Memory** and **CPU** usage
- Review **Build** history

---

## 🗄️ Database

- **Type**: SQLite
- **Location**: `smart-leads-backend/storage/database.sqlite`
- **Auto-created**: Yes (first run)
- **Auto-seeded**: Yes (admin user)
- **Auto-deleted**: After 10 days (development feature)

For production persistence, use:

- Render Postgres (recommended)
- Render Persistent Disk (paid)

---

## ❓ Troubleshooting

### Build Failed

```
1. Check Render Logs (Deployments tab)
2. Common issues:
   - Missing JWT_SECRET_KEY environment variable
   - TypeScript compilation errors
   - Verify locally: npm run build
```

### Blank Page

```
1. Open browser DevTools (F12)
2. Check Console for errors
3. Check Render Logs for Express errors
4. Verify vite.config.ts has correct outDir
```

### Database Error

```
1. Check Express logs
2. Verify storage/ directory exists in backend
3. Local test: npm start
```

---

## 📚 Full Documentation

- **Complete Setup**: See [DEPLOYMENT.md](./DEPLOYMENT.md)
- **All Changes**: See [DEPLOYMENT_COMPLETE.md](./DEPLOYMENT_COMPLETE.md)
- **Local Development**: `npm run dev`
- **Backend Only**: `npm run server`
- **Frontend Only**: `npm run client`

---

## 🎉 You're Live!

Your Smart Leads Dashboard is now running on Render's FREE plan with:

- ✅ Single unified service
- ✅ Frontend served by Express
- ✅ SQLite database included
- ✅ Full authentication system
- ✅ Production-ready security

**Congratulations! 🚀**
