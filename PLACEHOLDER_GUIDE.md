# 📝 Placeholder Replacement Guide

✅ **ALL PLACEHOLDERS HAVE BEEN REPLACED!**

This project is now configured with the following GitHub users:
- **Main Owner**: [@subham2023](https://github.com/subham2023)
- **Second Owner**: [@sidhyaashu](https://github.com/sidhyaashu)
- **Restricted User 1**: [@Abhishek-Royy](https://github.com/Abhishek-Royy)
- **Restricted User 2**: [@Sayandip05](https://github.com/Sayandip05)

---

## Original Instructions (For Reference)

Before pushing to GitHub, you MUST replace these placeholders with actual GitHub usernames.

## 🔍 Where to Replace

### 1. `.github/CODEOWNERS`
Replace:
- `YOUR_USERNAME` → Your GitHub username (e.g., `@johnsmith`)
- `SECOND_ALLOWED_USERNAME` → Second approved user (e.g., `@janedoe`)

**Example:**
```
# Before
*       @YOUR_USERNAME @SECOND_ALLOWED_USERNAME

# After
*       @johnsmith @janedoe
```

### 2. `.github/workflows/pr-labeler.yml`
Replace in two locations:
- `YOUR_USERNAME` → Your GitHub username (without @)
- `SECOND_ALLOWED_USERNAME` → Second approved user (without @)
- `RESTRICTED_USER_1` → First restricted user (without @)
- `RESTRICTED_USER_2` → Second restricted user (without @)

**Lines to update:**
- Line 23: `const allowedUsers = ['YOUR_USERNAME', 'SECOND_ALLOWED_USERNAME'];`
- Line 26: `const restrictedUsers = ['RESTRICTED_USER_1', 'RESTRICTED_USER_2'];`
- Line 54: `const codeOwners = ['YOUR_USERNAME', 'SECOND_ALLOWED_USERNAME'];`
- Line 66: `if` condition with restricted users

**Example:**
```javascript
// Before
const allowedUsers = ['YOUR_USERNAME', 'SECOND_ALLOWED_USERNAME'];
const restrictedUsers = ['RESTRICTED_USER_1', 'RESTRICTED_USER_2'];

// After
const allowedUsers = ['johnsmith', 'janedoe'];
const restrictedUsers = ['developer1', 'developer2'];
```

### 3. `README.md` (Optional - for documentation)
Replace in the "Access Control" section:
- `@YOUR_USERNAME`
- `@SECOND_ALLOWED_USERNAME`
- `@RESTRICTED_USER_1`
- `@RESTRICTED_USER_2`

**Example:**
```markdown
# Before
### Direct Push Access
- `@YOUR_USERNAME`
- `@SECOND_ALLOWED_USERNAME`

# After
### Direct Push Access
- `@johnsmith`
- `@janedoe`
```

## ✅ Quick Checklist

Use this checklist to ensure you've replaced everything:

- [ ] `.github/CODEOWNERS` - Both usernames updated (with @)
- [ ] `.github/workflows/pr-labeler.yml` - Line 23 (allowedUsers array)
- [ ] `.github/workflows/pr-labeler.yml` - Line 26 (restrictedUsers array)
- [ ] `.github/workflows/pr-labeler.yml` - Line 54 (codeOwners array)
- [ ] `.github/workflows/pr-labeler.yml` - Line 66 (if condition)
- [ ] `README.md` - Access Control section (optional but recommended)

## 🔍 Quick Find & Replace

You can use these commands to find all placeholders:

### Using grep (Linux/Mac/Git Bash):
```bash
grep -r "YOUR_USERNAME" .github/
grep -r "SECOND_ALLOWED_USERNAME" .github/
grep -r "RESTRICTED_USER_1" .github/
grep -r "RESTRICTED_USER_2" .github/
```

### Using PowerShell (Windows):
```powershell
Get-ChildItem -Path .\.github\ -Recurse | Select-String "YOUR_USERNAME"
Get-ChildItem -Path .\.github\ -Recurse | Select-String "SECOND_ALLOWED_USERNAME"
Get-ChildItem -Path .\.github\ -Recurse | Select-String "RESTRICTED_USER_1"
Get-ChildItem -Path .\.github\ -Recurse | Select-String "RESTRICTED_USER_2"
```

## 💡 Example Setup

Here's a complete example of what your usernames might look like:

| Placeholder | Example Value | Has @ in CODEOWNERS? | Has @ in pr-labeler.yml? |
|------------|---------------|----------------------|--------------------------|
| YOUR_USERNAME | johnsmith | ✅ Yes (@johnsmith) | ❌ No (johnsmith) |
| SECOND_ALLOWED_USERNAME | janedoe | ✅ Yes (@janedoe) | ❌ No (janedoe) |
| RESTRICTED_USER_1 | developer1 | N/A | ❌ No (developer1) |
| RESTRICTED_USER_2 | developer2 | N/A | ❌ No (developer2) |

## ⚠️ Common Mistakes

1. **Forgetting the @ symbol in CODEOWNERS**
   - ❌ Wrong: `*  YOUR_USERNAME`
   - ✅ Correct: `*  @YOUR_USERNAME`

2. **Including @ symbol in pr-labeler.yml**
   - ❌ Wrong: `const allowedUsers = ['@johnsmith'];`
   - ✅ Correct: `const allowedUsers = ['johnsmith'];`

3. **Not updating all occurrences**
   - Make sure to update all 5 locations in pr-labeler.yml!

4. **Typos in usernames**
   - Double-check each username is spelled correctly
   - GitHub usernames are case-insensitive but keep consistent

## 🚀 After Replacement

Once you've replaced all placeholders:

1. ✅ Verify all changes are correct
2. ✅ Run: `git add .`
3. ✅ Run: `git commit -m "Configure CI/CD pipeline with access controls"`
4. ✅ Push to GitHub
5. ✅ Follow SETUP.md to configure branch protection rules

---

**Need help?** Check [SETUP.md](SETUP.md) for the complete setup guide.

