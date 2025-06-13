# 🚨 EMERGENCY CREDENTIAL ROTATION CHECKLIST

## ⚠️ IMMEDIATE ACTIONS REQUIRED (Do these NOW!)

Your Azure credentials were exposed in Git history and are potentially compromised.

### 1. **Azure Communication Services - URGENT**
- [ ] Log into Azure Portal immediately
- [ ] Go to your ACS resource: `donerbestelling` 
- [ ] Navigate to "Keys and Connection Strings"
- [ ] Click "Regenerate Primary Key" 
- [ ] Copy the NEW connection string
- [ ] Update your Azure App Service settings with the new connection string

### 2. **Phone Number Security**
- [ ] The phone number `+0031646322061` was exposed
- [ ] Consider if this is a personal/sensitive number
- [ ] If needed, get a new business phone number through Azure Communication Services

### 3. **Repository Cleanup Options**

#### Option A: Complete Repository Reset (RECOMMENDED)
```powershell
# 1. Create a new repository on GitHub with a different name
# 2. Clone this directory to a new location
# 3. Remove .git folder and start fresh
cd "d:\GithubRepos\donorbestelsite"
Remove-Item -Recurse -Force .git
git init
git add .
git commit -m "Initial commit - cleaned repository"
git remote add origin https://github.com/yourusername/NEW-REPO-NAME.git
git push -u origin main
```

#### Option B: History Rewrite (RISKY - only if repo is private)
```powershell
cd "d:\GithubRepos\donorbestelsite"
git filter-branch --force --index-filter 'git rm --cached --ignore-unmatch app-settings-reference.json server.js DEPLOYMENT_GUIDE.md' --prune-empty --tag-name-filter cat -- --all
git push origin --force --all
```

### 4. **Verify Cleanup**
After choosing an option above:
- [ ] Check GitHub repository - no sensitive data visible
- [ ] Verify new Azure credentials work
- [ ] Test SMS functionality with new credentials
- [ ] Update any documentation with new resource names

### 5. **Prevention**
- [ ] Set up branch protection rules
- [ ] Add pre-commit hooks to scan for secrets
- [ ] Regular security audits using SECURITY.md checklist

## 🔥 PRIORITY ORDER:
1. **Rotate Azure ACS credentials (5 minutes)**
2. **Choose repository cleanup option (15 minutes)**  
3. **Test new setup (10 minutes)**
4. **Implement prevention measures (30 minutes)**

**Time is critical - exposed credentials could be used maliciously!**
