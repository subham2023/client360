# ⚡ Quick Start Guide

Get your CI/CD pipeline running in **5 minutes**!

## 🎯 Step-by-Step (5 Minutes)

### ✅ Step 1: Placeholders Already Replaced!

All usernames have been configured:
- **Main Owner**: @subham2023
- **Second Owner**: @sidhyaashu
- **Restricted User 1**: @Abhishek-Royy
- **Restricted User 2**: @Sayandip05

You can skip this step and proceed directly to Step 2!

### Step 2: Customize CI/CD for Your Project (1 minute)

**If you have Node.js/JavaScript:**
1. Open `.github/workflows/ci-cd.yml`
2. Uncomment lines with `# if: hashFiles('package.json') != ''`
3. Make sure your `package.json` has `test`, `build`, and `lint` scripts

**If you have Python:**
1. Open `.github/workflows/ci-cd.yml`
2. Uncomment lines with `# if: hashFiles('requirements.txt') != ''`
3. Make sure you have `requirements.txt` with dependencies

**Other languages:** See [SETUP.md](SETUP.md) for more details

### Step 3: Push to GitHub (1 minute)

```bash
git init
git add .
git commit -m "Add CI/CD pipeline"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/REPO_NAME.git
git push -u origin main
```

Replace `YOUR_USERNAME` and `REPO_NAME` with your actual values.

### Step 4: Configure Branch Protection (1 minute)

1. Go to your repo on GitHub
2. Click **Settings** → **Branches**
3. Click **Add branch protection rule**
4. Branch name: `main`
5. Enable these:
   - ✅ Require pull request before merging
   - ✅ Require status checks to pass
   - ✅ Require review from Code Owners
6. Click **Create**

🎉 **Done!** Your CI/CD pipeline is now active!

---

## 📋 Quick Checklist

Use this to verify everything is working:

- [ ] Replaced all placeholders in `.github/CODEOWNERS`
- [ ] Replaced all placeholders in `.github/workflows/pr-labeler.yml`
- [ ] Customized `.github/workflows/ci-cd.yml` for your tech stack
- [ ] Pushed all files to GitHub
- [ ] Branch protection rules enabled on main
- [ ] Added collaborators in Settings → Collaborators
- [ ] First CI/CD run completed successfully
- [ ] Tested creating a PR

---

## 🧪 Test Your Setup

### Test 1: CI/CD Pipeline
```bash
git checkout -b test/ci-pipeline
echo "test" > test.txt
git add test.txt
git commit -m "Test CI/CD"
git push origin test/ci-pipeline
```
→ Check Actions tab - you should see the pipeline running!

### Test 2: Pull Request Flow
1. Go to your repo on GitHub
2. Click "Compare & pull request"
3. Create the PR
4. Watch CI/CD checks run
5. Verify review is requested from code owners
6. Get approval and merge

### Test 3: Branch Protection
Try pushing directly to main (as a restricted user):
```bash
git checkout main
echo "direct push" > test.txt
git add test.txt
git commit -m "Direct push"
git push origin main
```
→ Should be **blocked** by branch protection! ✅

---

## 🆘 Common Issues & Fixes

### Issue: CI/CD not running
**Fix:** Check that `.github/workflows/ci-cd.yml` is in the correct location (note the dot!)

### Issue: Can't find status checks in branch protection
**Fix:** Wait for the first CI/CD run to complete, then they'll appear

### Issue: Everyone can push to main
**Fix:** Make sure branch protection rule is saved and "Do not allow bypassing" is checked

### Issue: Code owners not getting review requests
**Fix:** Verify usernames in CODEOWNERS have the @ symbol

---

## 📚 Next Steps

Once everything is working:

1. **Add deployment secrets** - See [SETUP.md](SETUP.md) Step 6
2. **Invite collaborators** - Settings → Collaborators → Add people
3. **Customize labels** - Edit `.github/labeler.yml`
4. **Add badges to README** - Show off your CI/CD status!
5. **Set up notifications** - Get alerts when builds fail

---

## 📞 Need More Help?

- **Detailed guide:** See [SETUP.md](SETUP.md)
- **Placeholders:** See [PLACEHOLDER_GUIDE.md](PLACEHOLDER_GUIDE.md)
- **Visual diagrams:** See [WORKFLOW_DIAGRAM.md](WORKFLOW_DIAGRAM.md)
- **GitHub docs:** [actions/documentation](https://docs.github.com/actions)

---

## 🎨 Pro Tips

1. **Use descriptive commit messages** - Makes history easier to read
2. **Keep PRs small** - Easier to review, faster to merge
3. **Write tests** - CI/CD is most valuable with good tests
4. **Review your own PR first** - Catch obvious issues before others see them
5. **Use draft PRs** - For work in progress that's not ready for review

---

**Estimated setup time:** 5 minutes  
**First-time setup:** May take 10-15 minutes if configuring secrets and customizing heavily  

Happy coding! 🚀

