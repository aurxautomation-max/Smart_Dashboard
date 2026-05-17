# Smart Leads Dashboard

## Deployment Instructions

### Render Setup

1. **Create a New Web Service**:
   - Go to [Render](https://render.com/).
   - Create a new **Web Service**.

2. **Connect GitHub Repository**:
   - Link your GitHub repository to Render.

3. **Environment**:
   - Set the following environment variables:
     - `NODE_ENV=production`
     - `PORT=5000`

4. **Build Command**:

   ```bash
   npm run build
   ```

5. **Start Command**:

   ```bash
   npm start
   ```

6. **Free Plan Compatibility**:
   - Ensure the service uses the free plan.

### GitHub Push Commands

```bash
# Initialize Git repository (if not already done)
git init

git add .
git commit -m "Prepare for Render deployment"

git branch -M main
git remote add origin <your-repo-url>
git push -u origin main
```

### Final Folder Structure

```
smart-dashboard/
├── docker-compose.yml
├── package.json
├── smart-leads-backend/
│   ├── Dockerfile
│   ├── dist/
│   │   ├── public/
│   │   └── index.js
│   ├── src/
│   │   ├── database/
│   │   │   └── sqlite.ts
│   │   ├── index.ts
│   │   └── ...
│   └── ...
├── smart-leads-dashboard/
│   ├── src/
│   │   └── ...
│   └── vite.config.ts
└── README.md
```

### Required Package Installs

```bash
# Install dependencies
npm install
```
