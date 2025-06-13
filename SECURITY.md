# 🔒 Security Checklist

## ✅ **Pre-Commit Security Checklist**

Before committing code to Git, always verify:

### 🔍 **Check for Sensitive Data:**
- [ ] No Azure connection strings in code
- [ ] No real phone numbers in configuration files
- [ ] No API keys or secrets in source code
- [ ] No production passwords in files
- [ ] No personal email addresses or contact information

### 🛡️ **Environment Security:**
- [ ] All sensitive values use environment variables
- [ ] `.env` files are in `.gitignore`
- [ ] Template files (`.env.example`) contain only placeholder values
- [ ] Production settings are configured in Azure App Service only

### 📁 **File Security:**
- [ ] No files named `app-settings.json` (production values)
- [ ] No files named `local.settings.json` (Azure Functions local settings)
- [ ] All example/template files use placeholder values

## 🚨 **If Sensitive Data Was Committed:**

### Immediate Actions:
1. **Rotate all exposed credentials immediately**
   - Generate new Azure Communication Services keys
   - Update phone numbers if personal ones were exposed
   - Change admin passwords

2. **Clean Git History** (if repository is not public yet):
   ```bash
   # Remove sensitive files from Git history
   git filter-branch --force --index-filter \
   'git rm --cached --ignore-unmatch app-settings.json' \
   --prune-empty --tag-name-filter cat -- --all
   
   # Force push to remote (DANGER: only if repo is private and you're sure)
   git push origin --force --all
   ```

3. **If Repository is Already Public:**
   - Assume all exposed data is compromised
   - Rotate ALL credentials immediately
   - Consider creating a new repository with clean history

## 🔧 **Regular Security Maintenance:**

### Monthly Review:
- [ ] Review `.gitignore` file completeness
- [ ] Audit environment variable usage
- [ ] Check for hardcoded secrets in new code
- [ ] Verify template files don't contain real values

### Before Making Repository Public:
- [ ] Run: `git log --grep="password\|key\|secret" --all`
- [ ] Search codebase: `grep -r "endpoint=https://" .`
- [ ] Search for phone patterns: `grep -r "+[0-9]" .`
- [ ] Verify all connection strings are placeholder values

## 🎯 **Best Practices:**

1. **Never commit production configuration files**
2. **Always use environment variables for secrets**
3. **Provide template/example files with placeholder values**
4. **Use Azure App Service Application Settings for production**
5. **Keep development and production credentials separate**
6. **Regularly rotate access keys and connection strings**

## 📞 **Emergency Contact:**
If you discover a security issue or accidental exposure:
- Immediately rotate all affected credentials
- Document the incident and steps taken
- Consider security implications for users/customers
