# Quick Deployment Guide

## 🚀 Deploy to Render (Easiest Method)

### Step 1: Push to GitHub
```bash
cd "D:\Lost and Found\Lost_and_Found\ideathon"
git init
git add .
git commit -m "Ready for deployment"
git branch -M main
git remote add origin <YOUR_GITHUB_REPO_URL>
git push -u origin main
```

### Step 2: Deploy on Render
1. Go to https://dashboard.render.com
2. Sign up/Login
3. Click **"New +"** → **"Blueprint"**
4. Connect your GitHub account
5. Select your repository
6. Render will auto-detect `render.yaml`
7. Click **"Apply"**

### Step 3: Wait for Deployment
- Render will automatically:
  - Create a PostgreSQL database
  - Install dependencies
  - Run migrations
  - Start your app

### Step 4: Access Your App
- Your app URL: `https://your-app-name.onrender.com`
- Admin login: `admin@kongu.edu` / `admin123`
- **⚠️ Change admin password immediately!**

---

## 🔐 Generate Secure Secret Key

Run this before deploying:
```bash
python generate_secret_key.py
```

Copy the generated key and add it as `SECRET_KEY` environment variable in Render.

---

## 📋 Checklist Before Deploying

- [ ] Code pushed to GitHub
- [ ] `render.yaml` is in the repository
- [ ] `requirements.txt` is up to date
- [ ] `Procfile` exists
- [ ] Generated secure `SECRET_KEY`
- [ ] Tested locally (app runs without errors)

---

## 🆘 Need Help?

- **Render Docs**: https://render.com/docs
- **Full Guide**: See `DEPLOYMENT.md`
- **Issues**: Check Render dashboard logs

---

## 🌐 Alternative: Deploy to Other Platforms

### Railway
1. Connect GitHub repo
2. Add PostgreSQL
3. Set environment variables
4. Deploy!

### Heroku
1. Install Heroku CLI
2. `heroku create`
3. `heroku addons:create heroku-postgresql`
4. `git push heroku main`

### DigitalOcean
1. Connect GitHub repo
2. Select Python app
3. Add PostgreSQL database
4. Configure and deploy

