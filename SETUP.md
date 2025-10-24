# GitHub CI/CD Pipeline Setup Guide

This guide will walk you through setting up your GitHub repository with the CI/CD pipeline and access controls.

## 📋 Prerequisites

- Repository hosted on GitHub
- Admin access to the repository
- GitHub usernames for all collaborators

## ✅ Step 1: Placeholders Already Replaced!

All usernames have been configured for this project:

### Configured Users:
- **Main Owner**: [@subham2023](https://github.com/subham2023) - Direct push access
- **Second Owner**: [@sidhyaashu](https://github.com/sidhyaashu) - Direct push access
- **Restricted User 1**: [@Abhishek-Royy](https://github.com/Abhishek-Royy) - Requires PR approval
- **Restricted User 2**: [@Sayandip05](https://github.com/Sayandip05) - Requires PR approval

You can proceed directly to Step 2!

## 📦 Step 2: Initial Repository Setup

1. **Initialize Git (if not already done):**
   ```bash
   git init
   git add .
   git commit -m "Initial commit with CI/CD pipeline"
   ```

2. **Create GitHub repository:**
   - Go to https://github.com/new
   - Create a new repository
   - Do NOT initialize with README (we already have files)

3. **Push to GitHub:**
   ```bash
   git branch -M main
   git remote add origin https://github.com/subham2023/client-360.git
   git push -u origin main
   ```

## 👥 Step 3: Add Collaborators

1. Go to your repository on GitHub
2. Navigate to **Settings** → **Collaborators and teams**
3. Click **Add people**
4. Add each user with appropriate permissions:

   **Users with direct push access:**
   - `@subham2023` (you, already owner)
   - `@sidhyaashu` → Add with **Admin** or **Write** role

   **Users who need approval:**
   - `@Abhishek-Royy` → Add with **Write** role
   - `@Sayandip05` → Add with **Write** role

## 🛡️ Step 4: Configure Branch Protection Rules

This is the most important step for access control!

1. Go to **Settings** → **Branches**
2. Click **Add branch protection rule**
3. Configure as follows:

### Branch name pattern:
```
main
```

### Protection settings to enable:

#### ✅ **Require a pull request before merging**
- Check this box
- **Required approvals:** Set to `1`
- ✅ **Dismiss stale pull request approvals when new commits are pushed**
- ✅ **Require review from Code Owners**
- ✅ **Require approval of the most recent reviewable push**

#### ✅ **Require status checks to pass before merging**
- Check this box
- ✅ **Require branches to be up to date before merging**
- Add these required status checks (they appear after your first CI/CD run):
  - `Install Dependencies`
  - `Lint Code`
  - `Run Tests`
  - `Build Project`

#### ✅ **Require conversation resolution before merging**
- Check this box

#### ✅ **Do not allow bypassing the above settings**
- Check this box (ensures rules apply to everyone)

#### ❌ **Allow force pushes** 
- UNCHECK this box (prevent force pushes)
- If checked, uncheck "Specify who can force push"

#### ❌ **Allow deletions**
- UNCHECK this box (prevent branch deletion)

#### ⚠️ **IMPORTANT: Allow specific users to bypass**
At the bottom of the page, you'll see "Allow specified actors to bypass required pull requests"

**DO NOT check this** - we want everyone to follow the rules. However, if you want the two allowed users to push directly:

1. Check **"Allow specified actors to bypass required pull requests"**
2. Click **Add** and select:
   - `@subham2023`
   - `@sidhyaashu`
3. This allows them to push directly without PR

> **Note:** Even with bypass enabled, it's recommended to use PRs for code review. Bypass should only be used for hotfixes or urgent changes.

4. Click **Create** or **Save changes**

## 🔐 Step 5: Configure Repository Settings

### 5.1 Enable/Disable Features

Go to **Settings** → **General**:

- ✅ **Issues** (for bug tracking)
- ✅ **Projects** (for project management)
- ✅ **Preserve this repository** (optional but recommended)
- ✅ **Allow merge commits** (choose your preference)
- ✅ **Allow squash merging** (recommended)
- ❌ **Allow rebase merging** (optional)
- ✅ **Automatically delete head branches** (cleanup after merge)

### 5.2 Pull Request Settings

Scroll down to **Pull Requests** section:
- ✅ **Always suggest updating pull request branches**
- ✅ **Allow auto-merge**
- ✅ **Automatically delete head branches**

## 🔑 Step 6: Add Secrets (for deployment)

If you're deploying, you'll need to add secrets:

1. Go to **Settings** → **Secrets and variables** → **Actions**
2. Click **New repository secret**
3. Add secrets based on your deployment target:

### For Vercel:
- Name: `VERCEL_TOKEN`
- Value: Your Vercel token from https://vercel.com/account/tokens

### For AWS:
- Name: `AWS_ACCESS_KEY_ID`
- Value: Your AWS access key
- Name: `AWS_SECRET_ACCESS_KEY`
- Value: Your AWS secret key

### For Heroku:
- Name: `HEROKU_API_KEY`
- Value: Your Heroku API key

### For Codecov (optional):
- Name: `CODECOV_TOKEN`
- Value: Your Codecov token from https://codecov.io/

## 🎯 Step 7: Customize the CI/CD Pipeline

Edit `.github/workflows/ci-cd.yml` based on your project type:

### For Node.js/JavaScript/TypeScript projects:
1. Uncomment all Node.js related steps (lines with `if: hashFiles('package.json')`)
2. Ensure your `package.json` has these scripts:
   ```json
   {
     "scripts": {
       "test": "jest",          // or your test command
       "build": "webpack",       // or your build command
       "lint": "eslint ."       // or your lint command
     }
   }
   ```

### For Python projects:
1. Uncomment all Python related steps (lines with `if: hashFiles('requirements.txt')`)
2. Ensure you have `requirements.txt` with your dependencies
3. For testing, install pytest: `pip install pytest`

### For other languages:
1. Add appropriate setup actions from GitHub Marketplace:
   - Go: `actions/setup-go@v5`
   - Java: `actions/setup-java@v4`
   - Ruby: `ruby/setup-ruby@v1`
   - .NET: `actions/setup-dotnet@v4`

## 📝 Step 8: Test the Setup

### Test 1: Direct Push (Allowed Users)
If you enabled bypass for allowed users:
```bash
# As @subham2023 or @sidhyaashu
git checkout main
echo "test" >> test.txt
git add test.txt
git commit -m "Test direct push"
git push origin main
```
This should succeed without PR.

### Test 2: Pull Request (Restricted Users)
As `@Abhishek-Royy` or `@Sayandip05`:
```bash
# Clone the repository
git clone https://github.com/YOUR_USERNAME/REPO_NAME.git
cd REPO_NAME

# Create a feature branch
git checkout -b feature/test-branch

# Make changes
echo "test" >> test.txt
git add test.txt
git commit -m "Test PR workflow"

# Push to feature branch
git push origin feature/test-branch
```

Then on GitHub:
1. Open a Pull Request from `feature/test-branch` to `main`
2. Wait for CI/CD checks to run
3. Request review from code owners (automatic if CODEOWNERS is set up)
4. Merge after approval

### Test 3: Failed CI (Anyone)
Make a commit that fails tests to ensure CI blocks merging:
```bash
git checkout -b test/failing-ci
# Break something that would fail tests
git add .
git commit -m "Test failing CI"
git push origin test/failing-ci
```
Create a PR and verify that the merge button is blocked until CI passes.

## 🔍 Verification Checklist

After setup, verify:

- [ ] Branch protection rules show on the main branch
- [ ] CODEOWNERS file is recognized (check PR review requests)
- [ ] CI/CD pipeline runs on push and PR
- [ ] Restricted users cannot push directly to main
- [ ] Restricted users' PRs require approval from code owners
- [ ] Allowed users can push directly (if bypass enabled)
- [ ] Status checks must pass before merging
- [ ] Deployment runs only after merge to main
- [ ] All secrets are properly configured

## 🚨 Troubleshooting

### Problem: CI/CD doesn't run
- Check `.github/workflows/ci-cd.yml` is in the correct directory
- Verify YAML syntax at https://www.yamllint.com/
- Check Actions tab for error messages

### Problem: Can't see status checks in branch protection
- Push a commit to trigger the workflow first
- Wait for the workflow to complete at least once
- Then the status check names will appear in settings

### Problem: Everyone can push to main
- Double-check branch protection rules are enabled
- Ensure "Do not allow bypassing" is checked (unless you want specific bypass)
- Verify you saved the branch protection rule

### Problem: Code owners not getting review requests
- Ensure CODEOWNERS file is in `.github/CODEOWNERS` (note the dot)
- Check usernames have @ prefix in CODEOWNERS
- Verify "Require review from Code Owners" is enabled in branch protection

### Problem: Deployment not working
- Check secrets are properly set in repository settings
- Verify secret names match those in workflow file
- Check deployment service credentials are valid

## 📚 Additional Resources

- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [Branch Protection Rules](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches)
- [CODEOWNERS Documentation](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners)
- [GitHub Secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets)

## 🎉 Next Steps

Once everything is set up:

1. **Document your workflow** - Add contributing guidelines
2. **Set up notifications** - Configure Slack/Discord/Email alerts
3. **Add badges** - Show CI/CD status in your README
4. **Monitor** - Regularly check Actions tab for failures
5. **Iterate** - Adjust rules based on team feedback

## 🆘 Need Help?

If you encounter issues:
1. Check the Actions tab for detailed logs
2. Review GitHub's documentation
3. Check if all usernames are correct (including @ symbol)
4. Ensure you have admin access to the repository

---

**Last Updated:** October 2025
**Maintenance:** Review this setup quarterly to ensure security best practices

