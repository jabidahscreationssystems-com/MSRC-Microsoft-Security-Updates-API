# Quick Start: GitHub Marketplace Integrations

This guide helps you quickly implement the most impactful GitHub Marketplace integrations for the MSRC Microsoft Security Updates API repository.

## 🚀 5-Minute Setup (Critical Security)

### Step 1: Enable Dependabot
The configuration is already in place at `.github/dependabot.yml`. Simply enable it:

1. Go to **Settings** → **Security & analysis**
2. Enable **Dependabot alerts**
3. Enable **Dependabot security updates**  
4. Enable **Dependabot version updates**

✅ **Done!** Dependabot will now automatically create PRs for dependency updates.

### Step 2: Verify GitHub Actions
The PowerShell CI workflow is already configured. Verify it's running:

1. Go to **Actions** tab
2. You should see "PowerShell CI" workflow
3. It runs automatically on every push and PR

✅ **Done!** Your code is now being tested automatically.

### Step 3: Enable CodeQL
The CodeQL workflow is configured at `.github/workflows/codeql.yml`:

1. Go to **Settings** → **Security & analysis**
2. Enable **Code scanning**
3. Select "Use existing workflow"

✅ **Done!** Your code is now being scanned for security vulnerabilities.

---

## 📊 15-Minute Setup (Enhanced Quality)

### Step 4: Install SonarCloud (10 minutes)

1. Visit https://github.com/marketplace/sonarcloud
2. Click **"Set up a plan"** → Choose **"Free for public repositories"**
3. Grant access to this repository
4. Follow the setup wizard (it will guide you through adding the workflow)
5. SonarCloud will automatically analyze your code on each push

**What you get:**
- Code quality metrics
- Bug detection
- Code coverage tracking
- Technical debt analysis

### Step 5: Install GitGuardian (5 minutes)

1. Visit https://github.com/marketplace/gitguardian
2. Click **"Set up a plan"** → **"Free for public repositories"**
3. Grant access to this repository
4. GitGuardian starts scanning immediately

**What you get:**
- Automatic detection of exposed secrets
- API key monitoring
- Real-time alerts on commits

---

## 💼 30-Minute Setup (Team Productivity)

### Step 6: Create GitHub Project Board (10 minutes)

1. Go to **Projects** tab → **New project**
2. Choose **"Board"** template
3. Add columns: `To Do`, `In Progress`, `Review`, `Done`
4. Enable workflows:
   - Auto-add items: Issues and PRs
   - Auto-move to "In Progress": When PR opened
   - Auto-move to "Done": When PR merged

**What you get:**
- Visual project tracking
- Automated workflow updates
- Team coordination

### Step 7: Set Up VS Code Development (10 minutes)

**Already configured!** Contributors just need to:

1. Open repository in VS Code
2. Click **"Install"** when prompted for recommended extensions
3. Extensions installed:
   - PowerShell
   - GitHub Copilot
   - GitLens
   - REST Client
   - OpenAPI viewer

**What you get:**
- Consistent development environment
- Enhanced PowerShell editing
- AI-powered code suggestions (with Copilot)

### Step 8: Enable GitHub Codespaces (10 minutes)

**Already configured** with `.devcontainer/devcontainer.json`!

To use:
1. Click **Code** → **Codespaces** → **Create codespace on main**
2. Wait for environment to provision (~2 minutes)
3. Start coding immediately!

**What you get:**
- Cloud-based development environment
- Pre-configured PowerShell + .NET
- Zero setup for new contributors
- Consistent development experience

---

## 🔌 Optional Integrations (As Needed)

### Microsoft Teams Notifications
**When:** You want GitHub updates in Teams
**Time:** 10 minutes

1. In Teams, go to your channel
2. Click **"..."** → **"Connectors"** → **"GitHub"**
3. Configure for this repository
4. Choose notification types

### Postman for API Testing
**When:** You need to test the MSRC API
**Time:** 15 minutes

1. Install Postman
2. Import `docs/postman-collection.json` from this repository
3. Add your API key as environment variable
4. Start testing!

### Azure DevOps Integration
**When:** You use Azure DevOps for project management
**Time:** 20 minutes

1. Install Azure Boards app from GitHub Marketplace
2. Link work items to PRs
3. Sync issues between platforms

---

## ✅ Verification Checklist

After setup, verify everything works:

- [ ] **Dependabot**: Check for PRs in "Pull requests" tab
- [ ] **GitHub Actions**: See green checkmarks on commits
- [ ] **CodeQL**: Security tab shows scanning results
- [ ] **Issue Templates**: Click "New Issue" and see templates
- [ ] **VS Code**: Workspace recommends extensions
- [ ] **Codespaces**: Can create and use cloud environment
- [ ] **Project Board**: Auto-updates when issues/PRs change

---

## 🎯 Priority Recommendations

### For Security-Focused Teams
**Must Have:**
1. ✅ Dependabot (automated security updates)
2. ✅ CodeQL (vulnerability scanning)
3. ✅ GitGuardian (secret detection)

### For Microsoft 365 Development
**Recommended:**
1. ✅ Azure DevOps integration
2. ✅ Microsoft Teams notifications
3. ✅ GitHub Copilot (AI assistance)

### For API Development
**Recommended:**
1. ✅ Postman (API testing)
2. ✅ OpenAPI/Swagger tools (already have swagger.yaml)
3. ✅ REST Client extension in VS Code

### For Team Collaboration
**Recommended:**
1. ✅ GitHub Projects (kanban boards)
2. ✅ Release Drafter (automated changelog)
3. ✅ PR templates (standardized reviews)

---

## 💰 Cost Summary

**Free (Already Set Up):**
- ✅ GitHub Actions (public repo = unlimited)
- ✅ Dependabot (built-in, free)
- ✅ CodeQL (public repo = free)
- ✅ Issue/PR templates (free)
- ✅ GitHub Projects (free)
- ✅ Codespaces (60 hours/month free)

**Free (Marketplace Apps):**
- ✅ SonarCloud (open source = free)
- ✅ GitGuardian (public repo = free)
- ✅ Codecov (open source = free)

**Paid (Optional):**
- GitHub Copilot: $10/month per user
- Postman: Free tier available
- Premium tool features: Usually not needed for open source

**Total Cost:** $0 - $10/month per developer

---

## 📚 Next Steps

1. **Complete 5-minute setup** → Get immediate security benefits
2. **Add 15-minute setup** → Improve code quality
3. **Configure team tools** → Enhance collaboration
4. **Explore optional integrations** → Customize to your needs

### Need Help?
- 📖 Full guide: See [IMPLEMENTATION_GUIDE.md](./IMPLEMENTATION_GUIDE.md)
- 🔍 Details: See [GITHUB_MARKETPLACE_RECOMMENDATIONS.md](../GITHUB_MARKETPLACE_RECOMMENDATIONS.md)
- 🐛 Issues: Use issue templates in this repository
- 💬 Questions: Open a discussion on GitHub

---

## 🎉 Success!

You now have:
- ✅ Automated security scanning
- ✅ Continuous integration and testing
- ✅ Code quality monitoring
- ✅ Project management tools
- ✅ Enhanced developer experience
- ✅ Team collaboration features

**Your repository is now optimized for security, quality, and productivity!**
