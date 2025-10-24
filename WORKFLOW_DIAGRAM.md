# 🔄 CI/CD Workflow Diagram

## Access Control Flow

```
┌─────────────────────────────────────────────────────────────┐
│                    GitHub Repository                         │
│                         (main branch)                        │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
        ┌─────────────────────────────────────────┐
        │         User Attempts to Push           │
        └─────────────────────────────────────────┘
                              │
                ┌─────────────┴─────────────┐
                │                           │
                ▼                           ▼
    ┌───────────────────────┐   ┌───────────────────────┐
    │   Allowed Users:      │   │  Restricted Users:    │
    │   • YOUR_USERNAME     │   │  • RESTRICTED_USER_1  │
    │   • SECOND_ALLOWED    │   │  • RESTRICTED_USER_2  │
    └───────────────────────┘   └───────────────────────┘
                │                           │
                ▼                           ▼
    ┌───────────────────────┐   ┌───────────────────────┐
    │  ✅ Can Push Direct   │   │  ❌ Must Create PR    │
    │  (if bypass enabled)  │   │  (always required)    │
    └───────────────────────┘   └───────────────────────┘
                │                           │
                │                           ▼
                │               ┌───────────────────────┐
                │               │  Create Pull Request  │
                │               └───────────────────────┘
                │                           │
                │                           ▼
                │               ┌───────────────────────┐
                │               │   CI/CD Pipeline      │
                │               │   Runs Automatically  │
                │               └───────────────────────┘
                │                           │
                │                           ▼
                │               ┌───────────────────────┐
                │               │  Code Owners Review   │
                │               │  (Required)           │
                │               └───────────────────────┘
                │                           │
                │                           ▼
                │               ┌───────────────────────┐
                │               │  ✅ Approved & Pass   │
                │               │  ❌ Changes Needed    │
                │               └───────────────────────┘
                │                           │
                └───────────────┬───────────┘
                                ▼
                    ┌───────────────────────┐
                    │   Merge to main       │
                    └───────────────────────┘
                                │
                                ▼
                    ┌───────────────────────┐
                    │  Deploy to Production │
                    └───────────────────────┘
```

## CI/CD Pipeline Jobs Flow

```
Push/PR to main
      │
      ▼
┌─────────────────────────────────────────────────────────┐
│  Job 1: Install Dependencies                            │
│  • Setup Node.js/Python                                 │
│  • Install packages                                     │
│  • Cache dependencies                                   │
│  ⏱️ ~1-2 minutes                                         │
└─────────────────────────────────────────────────────────┘
      │
      ├──────────────┬──────────────┐
      ▼              ▼              ▼
┌───────────┐  ┌───────────┐  ┌───────────┐
│  Job 2:   │  │  Job 3:   │  │  Job 4:   │
│  Lint     │  │  Test     │  │  Build    │
│           │  │           │  │           │
│ ⏱️ ~30s   │  │ ⏱️ ~2-5m  │  │ ⏱️ ~1-3m  │
└───────────┘  └───────────┘  └───────────┘
      │              │              │
      └──────────────┴──────────────┘
                     │
                     ▼
         ┌─────────────────────┐
         │  All Jobs Pass? ✅   │
         └─────────────────────┘
                     │
                     ▼
         ┌─────────────────────┐
         │  Is main branch?    │
         └─────────────────────┘
                     │
              ┌──────┴──────┐
              │             │
           Yes▼          No ▼
    ┌──────────────┐  ┌──────────────┐
    │  Job 5:      │  │  Stop here   │
    │  Deploy      │  │  (PR only)   │
    │              │  └──────────────┘
    │ ⏱️ ~2-5m     │
    └──────────────┘
              │
              ▼
    ┌──────────────┐
    │  🚀 Live!    │
    └──────────────┘
```

## Pull Request Review Flow

```
Developer creates PR
         │
         ▼
┌────────────────────────┐
│  Automatic Checks      │
│  • PR Labeler runs     │
│  • Size label added    │
│  • Author label added  │
└────────────────────────┘
         │
         ▼
┌────────────────────────┐
│  CI/CD Pipeline        │
│  • Install             │
│  • Lint                │
│  • Test                │
│  • Build               │
└────────────────────────┘
         │
    ┌────┴────┐
    │         │
  Pass▼    Fail▼
┌────────┐ ┌──────────────────┐
│Reviews │ │ Fix & Push Again │
│Requested│ └──────────────────┘
└────────┘         │
    │              │
    ▼              │
┌────────────────────────┐
│  Code Owner Review     │
│  • Must approve        │
│  • Can request changes │
│  • Can comment         │
└────────────────────────┘
         │
    ┌────┴────┐
    │         │
Approved▼  Changes▼
┌────────┐ ┌──────────────┐
│ Ready  │ │ Push Updates │
│to Merge│ └──────────────┘
└────────┘         │
    │              │
    └──────┬───────┘
           ▼
    ┌────────────────────────┐
    │  Merge Button Enabled  │
    │  • Squash & Merge      │
    │  • Merge Commit        │
    │  • Rebase & Merge      │
    └────────────────────────┘
           │
           ▼
    ┌────────────────────────┐
    │  Merged to main! 🎉    │
    │  → Triggers deployment │
    └────────────────────────┘
```

## Branch Protection Rules Visual

```
┌─────────────────────────────────────────────────────────────┐
│                   main Branch Protection                     │
└─────────────────────────────────────────────────────────────┘

🛡️ Protections Enabled:

  ✅ Require Pull Request Before Merging
     ├─ Required approvals: 1
     ├─ Dismiss stale reviews: ON
     ├─ Require code owner review: ON
     └─ Require review of recent push: ON

  ✅ Require Status Checks
     ├─ Install Dependencies ✓
     ├─ Lint Code ✓
     ├─ Run Tests ✓
     └─ Build Project ✓

  ✅ Require Conversation Resolution
     └─ All comments must be resolved

  ✅ Require Linear History
     └─ No merge commits

  ❌ Allow Force Pushes
     └─ Disabled for everyone

  ❌ Allow Deletions
     └─ main branch cannot be deleted

  ⚙️ Bypass Settings (Optional):
     ├─ YOUR_USERNAME (can bypass PR requirement)
     └─ SECOND_ALLOWED_USERNAME (can bypass PR requirement)
```

## Labels Applied by PR Labeler

```
┌─────────────────────────────────────────────────────────┐
│  Automatic Labels on Pull Requests                      │
└─────────────────────────────────────────────────────────┘

📊 Size Labels:
  • size/small  - Less than 10 files changed
  • size/medium - 10-30 files changed
  • size/large  - More than 30 files changed

👤 Author Labels:
  • trusted-contributor - Allowed users
  • needs-approval      - Restricted users

🏷️ Content Labels (from labeler.yml):
  • documentation - Changes to .md, docs/
  • config        - Changes to config files
  • ci-cd         - Changes to workflows
  • dependencies  - Changes to package.json, etc.
  • frontend      - Changes to .js, .tsx, .css
  • backend       - Changes to .py, .go, .java
  • database      - Changes to .sql, migrations
  • tests         - Changes to test files
  • docker        - Changes to Dockerfile
```

## Security & Access Matrix

```
┌────────────────────────────────────────────────────────────────┐
│                    User Permissions Matrix                      │
├────────────────────────┬──────────────┬──────────────┬─────────┤
│       Action           │ Allowed Users│Restricted    │ External│
│                        │              │Users         │Users    │
├────────────────────────┼──────────────┼──────────────┼─────────┤
│ Push to main (direct)  │ ✅ Yes*      │ ❌ No        │ ❌ No   │
│ Create PR              │ ✅ Yes       │ ✅ Yes       │ ✅ Yes  │
│ Approve PR             │ ✅ Yes       │ ❌ No        │ ❌ No   │
│ Merge PR (approved)    │ ✅ Yes       │ ✅ Yes       │ ❌ No   │
│ Force push to main     │ ❌ No        │ ❌ No        │ ❌ No   │
│ Delete main branch     │ ❌ No        │ ❌ No        │ ❌ No   │
│ Bypass status checks   │ ❌ No        │ ❌ No        │ ❌ No   │
│ Edit workflow files    │ ✅ Yes       │ ⚠️ Via PR    │ ❌ No   │
└────────────────────────┴──────────────┴──────────────┴─────────┘

* Only if bypass setting is enabled in branch protection
```

## Timeline: From Code to Production

```
📝 Developer writes code
   │  0 minutes
   ▼
🌿 Create feature branch
   │  1 minute
   ▼
📤 Push to GitHub
   │  1 minute
   ▼
🔀 Open Pull Request
   │  1 minute
   ▼
🤖 CI/CD starts automatically
   │  5-10 minutes
   ▼
✅ All checks pass
   │  1 minute
   ▼
👀 Code review requested
   │  [Wait for reviewer]
   ▼
✍️ Reviewer approves
   │  1 minute
   ▼
🔀 Merge to main
   │  1 minute
   ▼
🚀 Auto-deploy to production
   │  5-10 minutes
   ▼
🎉 Live in production!

Total active time: ~20-30 minutes
Total elapsed time: Depends on review speed
```

## Quick Reference Commands

```bash
# For Allowed Users (Optional Direct Push)
git checkout main
git pull origin main
# make changes
git add .
git commit -m "Hotfix: critical bug"
git push origin main  # ✅ Goes directly if bypass enabled

# For All Users (Recommended Flow)
git checkout -b feature/new-feature
# make changes
git add .
git commit -m "Add new feature"
git push origin feature/new-feature
# → Open PR on GitHub
# → Wait for CI/CD and approval
# → Merge when ready

# For Restricted Users (Required Flow)
# Same as above - MUST use PR workflow
# Cannot push directly to main even if attempted
```

---

**Legend:**
- ✅ = Allowed
- ❌ = Blocked
- ⚠️ = Allowed with conditions
- 🤖 = Automated
- 👤 = Manual action required

