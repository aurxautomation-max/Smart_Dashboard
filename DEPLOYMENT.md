# Smart Leads Dashboard - Render Deployment Guide

This guide walks through deploying the Smart Leads Dashboard as a single full-stack application on Render's FREE plan.

---

## ✅ Project Structure

The application has been restructured into a single full-stack deployment:

```
smart-dashboard/
├── smart-leads-backend/
│   ├── src/
│   │   ├── index.ts              # Express server with static serving
│   │   ├── database/
│   │   │   └── sqlite.ts         # SQLite auto-init & seed
│   │   ├── routes/
│   │   ├── controllers/
│   │   ├── services/
│   │   └── ...
│   ├── dist/
│   │   ├── index.js
│   │   └── public/               # Frontend build output
│   ├── package.json
│   └── tsconfig.json
├── smart-leads-dashboard/
│   ├── src/
│   ├── vite.config.ts            # Builds to ../smart-leads-backend/dist/public
│   ├── package.json
│   └── tsconfig.json
├── package.json                  # Root build & start scripts
└── docker-compose.yml            # Local development
```

---

## 🚀 Deployment Steps

### Step 1: Prepare Your Local Environment

```bash
# Clone or create your repository
git init
git add .
git commit -m "Initial commit: Full-stack app for Render"
```

### Step 2: Create Render Account

1. Go to [render.com](https://render.com)
2. Sign up with GitHub (recommended)
3. Create a new service

### Step 3: Connect GitHub Repository

1. Click **"New +"** → **Web Service**
2. Select **"Connect a repository"**
3. Authorize GitHub and select your repository
4. Click **"Connect"**

### Step 4: Configure Render Service

On the Render deployment page, configure:

**Service Name:**

```
smart-leads-app
```

**Environment:**

```
Node
```

**Build Command:**

```
npm run build
```

**Start Command:**

```
npm start
```

**Environment Variables:**

Click **"Add Environment Variable"** and add:

| Key              | Value                            | Notes                                        |
| ---------------- | -------------------------------- | -------------------------------------------- |
| `NODE_ENV`       | `production`                     | Required for Render                          |
| `PORT`           | `5000`                           | Render assigns dynamically; this is fallback |
| `JWT_SECRET_KEY` | `your_secret_key_here_change_me` | Change this to a strong secret!              |

### Step 5: Deploy

1. Click **"Create Web Service"**
2. Render will automatically:
   - Build your frontend (Vite → `dist/public`)
   - Compile your backend TypeScript
   - Start the Express server
   - Serve the frontend from Express

**Wait ~5-10 minutes for deployment to complete.**

---

## 🛠️ Local Development

### Option 1: Development Mode (Separate Servers)

```bash
# Install all dependencies
npm run install:all

# Start both frontend and backend
npm run dev
```

- Frontend: `http://localhost:5173` (Vite)
- Backend API: `http://localhost:5000/api/v1`

### Option 2: Docker Compose

```bash
# Build and run with Docker
docker-compose up --build
```

- Frontend: `http://localhost` (Nginx)
- Backend API: `http://localhost:5000/api/v1`

---

## 📦 Build Process Explained

When you deploy to Render, this happens:

```bash
npm run build
```

This root script:

1. **Builds Frontend** (Vite)

   ```bash
   cd smart-leads-dashboard
   npm install
   npm run build
   ```

   - Output: `smart-leads-backend/dist/public/`

2. **Builds Backend** (TypeScript → JavaScript)
   ```bash
   cd smart-leads-backend
   npm install
   npm run build
   ```

   - Output: `smart-leads-backend/dist/index.js`

When you start the server:

```bash
npm start
```

This runs:

```bash
node smart-leads-backend/dist/index.js
```

Express then:

- Serves the frontend from `./dist/public/`
- Routes API calls to `/api/v1` endpoints
- Falls back to `index.html` for SPA routing

---

## 🗄️ Database

**SQLite** is used for data persistence:

- **Location:** `smart-leads-backend/storage/database.sqlite`
- **Auto-Create:** Yes, on first run
- **Auto-Seed:** Admin user created on first run
  - **Username:** `admin`
  - **Password:** `admin123`
- **Auto-Delete:** Database deletes after 10 days (development feature)

For production, consider:

- Persisting the database using Render's persistent disks
- Migrating to PostgreSQL via Render's Postgres database service
- Setting up proper backups

---

## 🔧 Environment Variables Reference

Create a `.env` file in the root directory (for local development):

```env
# Environment Configuration
NODE_ENV=development
PORT=5000

# JWT Configuration
JWT_SECRET_KEY=your_super_secret_jwt_key_change_me
JWT_EXPIRES_IN=7d

# For Production (Render)
# NODE_ENV=production
# JWT_SECRET_KEY=<strong-random-key>
```

---

## 📝 GitHub Workflow

### Initial Setup

```bash
# Create repository on GitHub first, then:
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/your-username/your-repo.git
git push -u origin main
```

### Making Changes

```bash
# After making code changes locally:
git add .
git commit -m "Add feature XYZ"
git push origin main
```

**Render will automatically rebuild and redeploy!**

---

## 🚨 Troubleshooting

### Build Fails on Render

**Check:**

1. Go to **Render Dashboard** → Your Service → **Logs**
2. Look for error messages
3. Common issues:
   - Missing `JWT_SECRET_KEY` environment variable
   - TypeScript compilation errors
   - Missing dependencies

**Solution:**

```bash
# Test locally first
npm run build
npm start
```

### Frontend Not Loading

**Check:**

1. Browser console for errors
2. Render logs for Express errors
3. Verify `vite.config.ts` has correct `outDir`

**Solution:**

```bash
# Verify build output
ls smart-leads-backend/dist/public
```

### Database Issues

**Current behavior:**

- SQLite stores data in `storage/database.sqlite`
- On Render's ephemeral filesystem, data persists for **10 days**
- After 10 days, database auto-deletes

**For persistence on Render:**

1. Use **Persistent Disk** (paid feature)
2. Or migrate to **Render Postgres** (free tier available)

---

## 🎯 Features

✅ **Single Service Deployment** - No separate frontend/backend  
✅ **Render Free Plan** - Works on free tier  
✅ **Auto-Scaling** - Express handles all requests  
✅ **SQLite Database** - Zero setup required  
✅ **Hot Reload Dev** - Concurrently run frontend + backend  
✅ **Docker Support** - Local development with docker-compose  
✅ **Production Ready** - Helmet, CORS, error handling configured

---

## 📚 Additional Resources

- [Render Documentation](https://render.com/docs)
- [Express Static Files](https://expressjs.com/en/starter/static-files.html)
- [Vite Build Configuration](https://vitejs.dev/config/)
- [SQLite Node.js](https://github.com/mapbox/node-sqlite3/wiki)

---

## ❓ Quick Reference

| Command               | Purpose                                |
| --------------------- | -------------------------------------- |
| `npm run dev`         | Start frontend + backend (development) |
| `npm run build`       | Build frontend + backend (production)  |
| `npm start`           | Start production server                |
| `npm run client`      | Start frontend only                    |
| `npm run server`      | Start backend only                     |
| `npm run install:all` | Install all dependencies               |

---

**🎉 You're ready to deploy to Render!**
