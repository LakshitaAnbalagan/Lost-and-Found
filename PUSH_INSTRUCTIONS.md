# How to Push to GitHub - Step by Step

## Your SSH Key (Copy this to GitHub)
```
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIF0ydRirMCXCNxeiYxzD5I+f2Nnt8sOrddrov/kZxf3v lakshitaanbalagan6@gmail.com
```

## Step 1: Add SSH Key to GitHub

1. **Copy the SSH key above** (the entire line starting with `ssh-ed25519`)

2. **Go to GitHub:**
   - Visit: https://github.com/settings/keys
   - Click **"New SSH key"** button

3. **Add the key:**
   - **Title:** `My Computer` (or any name you like)
   - **Key:** Paste the SSH key you copied
   - Click **"Add SSH key"**

## Step 2: Test Connection (Optional)
```powershell
ssh -T git@github.com
```
You should see: "Hi lakshitaka! You've successfully authenticated..."

## Step 3: Commit and Push

```powershell
cd "D:\Lost and Found\Lost_and_Found\ideathon"

# Add all files
git add .

# Commit
git commit -m "Ready for deployment - Lost and Found app"

# Push to GitHub
git push -u origin main
```

## If SSH Still Doesn't Work - Use Personal Access Token

### Alternative Method:

1. **Get Token:**
   - Go to: https://github.com/settings/tokens/new
   - Name: `Lost_and_Found`
   - Check: **`repo`** checkbox
   - Click: **"Generate token"**
   - **COPY THE TOKEN** (starts with `ghp_...`)

2. **Switch back to HTTPS:**
   ```powershell
   git remote set-url origin https://github.com/lakshitaka/Lost_and_Found.git
   ```

3. **Push (use token as password):**
   ```powershell
   git push -u origin main
   ```
   When asked for password, paste your **token** (not your GitHub password)

## Need Help?
- SSH Key already added? Try pushing directly!
- Still having issues? Use the Personal Access Token method above.

