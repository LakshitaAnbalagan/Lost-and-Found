# Quick Fix for GitHub Push Error

## The Problem
GitHub no longer accepts passwords for HTTPS authentication. You need a **Personal Access Token**.

## Quick Solution (3 Steps)

### Step 1: Get Your Token
1. Visit: https://github.com/settings/tokens/new
2. Name: `Lost_and_Found_Deploy`
3. Check: **`repo`** (gives full repository access)
4. Click: **"Generate token"**
5. **COPY THE TOKEN** (starts with `ghp_...`)

### Step 2: Push with Token
```powershell
cd "D:\Lost and Found\Lost_and_Found\ideathon"
git add .
git commit -m "Ready for deployment"
git push -u origin main
```

**When it asks for password:** Paste your **token** (not your GitHub password)

### Step 3: Save Credentials (Optional)
To avoid entering token every time:
```powershell
git config --global credential.helper wincred
```

## Alternative: Use SSH (One-Time Setup)

### Generate SSH Key:
```powershell
ssh-keygen -t ed25519 -C "lakshitaanbalagan6@gmail.com"
# Press Enter 3 times
```

### Copy Public Key:
```powershell
cat ~/.ssh/id_ed25519.pub
# Copy the entire output
```

### Add to GitHub:
1. Go to: https://github.com/settings/keys
2. Click "New SSH key"
3. Paste the key
4. Click "Add SSH key"

### Switch to SSH:
```powershell
cd "D:\Lost and Found\Lost_and_Found\ideathon"
git remote set-url origin git@github.com:lakshitaka/Lost_and_Found.git
git push -u origin main
```

## Need Help?
- Full guide: See `GITHUB_SETUP.md`
- GitHub Token Docs: https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token

