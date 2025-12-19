# GitHub Setup Guide - Fixing Push Issues

## Problem: Permission Denied (403 Error)

You're getting a 403 error because:
1. The repository might not exist yet
2. Your GitHub credentials might be expired
3. You might not have write access to the repository

## Solutions

### Solution 1: Create the Repository on GitHub First

1. Go to https://github.com/new
2. Repository name: `Lost_and_Found`
3. Make it **Public** or **Private** (your choice)
4. **DO NOT** initialize with README, .gitignore, or license
5. Click **"Create repository"**

### Solution 2: Use Personal Access Token (Recommended)

GitHub no longer accepts passwords for HTTPS. You need a Personal Access Token:

1. **Generate Token:**
   - Go to: https://github.com/settings/tokens
   - Click **"Generate new token"** → **"Generate new token (classic)"**
   - Name it: `Lost_and_Found_Deploy`
   - Select scopes: Check **`repo`** (full control of private repositories)
   - Click **"Generate token"**
   - **COPY THE TOKEN** (you won't see it again!)

2. **Use Token for Push:**
   ```powershell
   # When prompted for password, use the token instead
   git push -u origin main
   ```

3. **Or Update Remote URL with Token:**
   ```powershell
   git remote set-url origin https://<YOUR_TOKEN>@github.com/lakshitaka/Lost_and_Found.git
   ```

### Solution 3: Use SSH Instead of HTTPS

1. **Check if you have SSH key:**
   ```powershell
   ls ~/.ssh
   ```

2. **If no SSH key, generate one:**
   ```powershell
   ssh-keygen -t ed25519 -C "lakshitaanbalagan6@gmail.com"
   # Press Enter to accept default location
   # Press Enter twice for no passphrase (or set one)
   ```

3. **Add SSH key to GitHub:**
   ```powershell
   cat ~/.ssh/id_ed25519.pub
   # Copy the output
   ```
   - Go to: https://github.com/settings/keys
   - Click **"New SSH key"**
   - Paste the key
   - Click **"Add SSH key"**

4. **Update Remote to SSH:**
   ```powershell
   git remote set-url origin git@github.com:lakshitaka/Lost_and_Found.git
   ```

5. **Test SSH Connection:**
   ```powershell
   ssh -T git@github.com
   ```

6. **Push:**
   ```powershell
   git push -u origin main
   ```

### Solution 4: Use GitHub CLI (gh)

1. **Install GitHub CLI:**
   - Download from: https://cli.github.com/
   - Or use: `winget install GitHub.cli`

2. **Authenticate:**
   ```powershell
   gh auth login
   ```

3. **Push:**
   ```powershell
   git push -u origin main
   ```

## Quick Fix Commands

### If repository doesn't exist:
```powershell
# Create repo on GitHub first, then:
git remote remove origin
git remote add origin https://github.com/lakshitaka/Lost_and_Found.git
git push -u origin main
```

### If using Personal Access Token:
```powershell
# When git asks for password, paste your token
git push -u origin main
```

### If switching to SSH:
```powershell
git remote set-url origin git@github.com:lakshitaka/Lost_and_Found.git
git push -u origin main
```

## Verify Your Setup

```powershell
# Check remote URL
git remote -v

# Check if you can connect
git ls-remote origin
```

## Still Having Issues?

1. **Check repository exists:** Visit https://github.com/lakshitaka/Lost_and_Found
2. **Check your access:** Make sure you're logged into the correct GitHub account
3. **Try creating a new repository** with a different name
4. **Use GitHub Desktop** as an alternative GUI tool

