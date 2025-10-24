# Client 360

This repository includes a complete GitHub Actions CI/CD pipeline with access controls.

## 🚀 Quick Start

1. **Set up the pipeline** - Follow instructions in [`SETUP.md`](SETUP.md)
2. **Configure access controls** - Update placeholders with actual GitHub usernames
3. **Push to GitHub** - Let the CI/CD pipeline handle the rest!

## 📊 CI/CD Pipeline

This project uses GitHub Actions for continuous integration and deployment:

- ✅ **Automated Testing** - Runs on every push and pull request
- ✅ **Code Linting** - Ensures code quality standards
- ✅ **Automated Builds** - Builds the project on successful tests
- ✅ **Automated Deployment** - Deploys to production on main branch
- ✅ **Access Controls** - Branch protection with review requirements

## 🛡️ Access Control

### Direct Push Access (No PR Required)
- [@subham2023](https://github.com/subham2023) - Main Owner
- [@sidhyaashu](https://github.com/sidhyaashu) - Second Owner

### PR Required with Approval
- [@Abhishek-Royy](https://github.com/Abhishek-Royy) - Restricted User
- [@Sayandip05](https://github.com/Sayandip05) - Restricted User

## 📁 Repository Structure

```
.
├── .github/
│   ├── workflows/
│   │   └── ci-cd.yml          # Main CI/CD pipeline
│   └── CODEOWNERS             # Code ownership and review requirements
├── SETUP.md                   # Detailed setup instructions
├── TEST_BRANCH_GUIDE.md       # Test branch usage guide
└── README.md                  # This file
```

## 🌿 Branch Strategy

- **`main`** - Production branch (PR required, owners only)
- **`test`** - Open development branch (anyone can push, no restrictions)

## 🔧 Pipeline Jobs

1. **Install Dependencies** - Sets up the project environment
2. **Lint Code** - Checks code quality and style
3. **Run Tests** - Executes test suite
4. **Build Project** - Creates production build
5. **Deploy** - Deploys to production (main branch only)

## 📖 Documentation

- **[START_HERE.md](START_HERE.md)** - Getting started guide (read this first!)
- **[TEAM_CONFIGURATION.md](TEAM_CONFIGURATION.md)** - Team members & access control details
- **[TEST_BRANCH_GUIDE.md](TEST_BRANCH_GUIDE.md)** - How to use the open test branch
- **[SETUP.md](SETUP.md)** - Complete setup guide with step-by-step instructions
- **[QUICK_START.md](QUICK_START.md)** - 5-minute quick setup
- **[CODEOWNERS](.github/CODEOWNERS)** - Code ownership configuration
- **[CI/CD Workflow](.github/workflows/ci-cd.yml)** - Pipeline configuration

## 🔐 Security Features

- ✅ Branch protection on `main`
- ✅ Required pull request reviews
- ✅ Required status checks before merge
- ✅ Code owner approval requirement
- ✅ No force pushes allowed
- ✅ Automatic PR conflict resolution required
- ✅ Open `test` branch for experimentation

## 🤝 Contributing

1. Fork the repository (if external contributor)
2. Create a feature branch: `git checkout -b feature/amazing-feature`
3. Commit your changes: `git commit -m 'Add amazing feature'`
4. Push to the branch: `git push origin feature/amazing-feature`
5. Open a Pull Request

### For Restricted Users
- All changes must go through pull requests
- At least 1 approval from code owners required
- All CI/CD checks must pass

### For Allowed Users
- Can push directly to main (for hotfixes only)
- PRs still recommended for regular development
- All CI/CD checks must pass

## 📊 Workflow Status

<!-- Uncomment and update after first workflow run -->
<!--
[![CI/CD Pipeline](https://github.com/YOUR_USERNAME/REPO_NAME/actions/workflows/ci-cd.yml/badge.svg)](https://github.com/YOUR_USERNAME/REPO_NAME/actions/workflows/ci-cd.yml)
[![PR Labeler](https://github.com/YOUR_USERNAME/REPO_NAME/actions/workflows/pr-labeler.yml/badge.svg)](https://github.com/YOUR_USERNAME/REPO_NAME/actions/workflows/pr-labeler.yml)
[![License](https://img.shields.io/github/license/YOUR_USERNAME/REPO_NAME)](LICENSE)
[![Last Commit](https://img.shields.io/github/last-commit/YOUR_USERNAME/REPO_NAME)](https://github.com/YOUR_USERNAME/REPO_NAME/commits/main)
[![Issues](https://img.shields.io/github/issues/YOUR_USERNAME/REPO_NAME)](https://github.com/YOUR_USERNAME/REPO_NAME/issues)
[![Pull Requests](https://img.shields.io/github/issues-pr/YOUR_USERNAME/REPO_NAME)](https://github.com/YOUR_USERNAME/REPO_NAME/pulls)
-->

## 🆘 Support

If you encounter any issues:
1. Check the [SETUP.md](SETUP.md) troubleshooting section
2. Review the Actions tab for CI/CD logs
3. Open an issue in this repository

## 📝 License

[Add your license here]

---

**Note:** Before pushing to GitHub, make sure to replace all placeholder usernames in:
- `.github/CODEOWNERS`
- This README.md
- SETUP.md (for documentation purposes)

See [SETUP.md](SETUP.md) for complete instructions.

