# Deployment Guide - Lost and Found Application

This guide will help you deploy your Lost and Found Flask application to Render.

## Prerequisites

1. A GitHub account
2. A Render account (sign up at https://render.com)
3. Your code pushed to a GitHub repository

## Deployment Steps

### Option 1: Deploy using Render.yaml (Recommended)

1. **Push your code to GitHub**
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin <your-github-repo-url>
   git push -u origin main
   ```

2. **Deploy on Render**
   - Go to https://dashboard.render.com
   - Click "New +" → "Blueprint"
   - Connect your GitHub repository
   - Render will automatically detect `render.yaml` and deploy your application

3. **What Render.yaml does:**
   - Creates a web service
   - Sets up a PostgreSQL database
   - Configures environment variables
   - Runs build commands
   - Starts the application with Gunicorn

### Option 2: Manual Deployment

1. **Create a PostgreSQL Database**
   - In Render dashboard, click "New +" → "PostgreSQL"
   - Name it: `lost-and-found-db`
   - Note the connection string

2. **Create a Web Service**
   - Click "New +" → "Web Service"
   - Connect your GitHub repository
   - Configure:
     - **Name**: `lost-and-found`
     - **Environment**: `Python 3`
     - **Build Command**: `pip install -r requirements.txt`
     - **Start Command**: `gunicorn app:app`
     - **Root Directory**: `ideathon` (if your repo structure requires it)

3. **Set Environment Variables**
   - `SECRET_KEY`: Generate a secure random key (you can use: `python -c "import secrets; print(secrets.token_hex(32))"`)
   - `DATABASE_URL`: Use the connection string from your PostgreSQL database
   - `PYTHON_VERSION`: `3.11.1`

4. **Deploy**
   - Click "Create Web Service"
   - Render will build and deploy your application

## Post-Deployment

1. **Access your application**
   - Your app will be available at: `https://your-app-name.onrender.com`

2. **Initialize the database**
   - The database tables will be created automatically on first run
   - Admin user will be created automatically:
     - Email: `admin@kongu.edu`
     - Password: `admin123`
   - **IMPORTANT**: Change the admin password after first login!

3. **Run migrations (if needed)**
   - If you need to run migrations manually, use Render's shell:
     ```bash
     flask db upgrade
     ```

## Environment Variables

| Variable | Description | Required |
|----------|-------------|----------|
| `SECRET_KEY` | Flask secret key for sessions | Yes |
| `DATABASE_URL` | PostgreSQL connection string | Yes (auto-set by Render) |
| `PYTHON_VERSION` | Python version to use | Optional |

## Security Notes

⚠️ **IMPORTANT**: 
- Change the default admin password (`admin123`) immediately after deployment
- The `SECRET_KEY` should be a strong random string
- Never commit `.env` files or sensitive data to Git

## Troubleshooting

### Database Connection Issues
- Ensure `DATABASE_URL` is set correctly
- Check that PostgreSQL database is running
- Verify connection string format (should start with `postgresql://`)

### Build Failures
- Check that all dependencies in `requirements.txt` are correct
- Ensure Python version matches `runtime.txt`
- Review build logs in Render dashboard

### Application Not Starting
- Check that `gunicorn` is installed (it's in requirements.txt)
- Verify `Procfile` or start command is correct
- Review application logs in Render dashboard

## Alternative Hosting Options

### Heroku
1. Install Heroku CLI
2. Create `Procfile` (already exists)
3. Run: `heroku create`
4. Run: `git push heroku main`

### Railway
1. Connect GitHub repository
2. Railway auto-detects Flask apps
3. Add PostgreSQL database
4. Set environment variables

### DigitalOcean App Platform
1. Connect GitHub repository
2. Select Python environment
3. Add PostgreSQL database
4. Configure build and start commands

## Support

For issues specific to:
- **Render**: https://render.com/docs
- **Flask**: https://flask.palletsprojects.com
- **This Application**: Check the code comments in `app.py`

