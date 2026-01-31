# Implementation Guide for GitHub Marketplace Integrations

This guide provides step-by-step instructions for implementing the recommended GitHub Marketplace integrations for the MSRC Microsoft Security Updates API repository.

## Table of Contents
1. [Prerequisites](#prerequisites)
2. [Phase 1: Critical Security & Quality](#phase-1-critical-security--quality)
3. [Phase 2: Enhanced Automation](#phase-2-enhanced-automation)
4. [Phase 3: Team Productivity](#phase-3-team-productivity)
5. [Phase 4: API & Documentation](#phase-4-api--documentation)
6. [Verification](#verification)
7. [Troubleshooting](#troubleshooting)

## Prerequisites

- Repository admin access or appropriate permissions
- GitHub account with necessary privileges
- Basic understanding of GitHub Actions and workflows

## Phase 1: Critical Security & Quality

### 1.1 Enable Dependabot (5 minutes)

**Status**: ✅ Already configured in `.github/dependabot.yml`

**Verification Steps**:
1. Go to repository Settings → Security & analysis
2. Enable "Dependabot alerts"
3. Enable "Dependabot security updates"
4. Enable "Dependabot version updates"
5. Verify `.github/dependabot.yml` is present

**Expected Outcome**: Dependabot will start scanning for vulnerable dependencies and create PRs for updates.

### 1.2 Enable CodeQL Analysis (10 minutes)

**Status**: ✅ Workflow configured in `.github/workflows/codeql.yml`

**Setup Steps**:
1. Go to repository Settings → Security & analysis
2. Click "Set up" under "Code scanning"
3. Choose "Advanced" and use the existing workflow
4. The workflow will run on push, PR, and weekly schedule

**Expected Outcome**: CodeQL will analyze code for security vulnerabilities on each push and PR.

### 1.3 Enable GitHub Actions CI/CD (Already Done)

**Status**: ✅ Workflow configured in `.github/workflows/powershell-ci.yml`

**Verification**:
1. Go to Actions tab in repository
2. Verify "PowerShell CI" workflow appears
3. Workflow runs on push and PR to main/master branches

**What it does**:
- Runs PSScriptAnalyzer for code quality
- Executes Pester tests
- Validates module manifest
- Tests on Windows, Linux, and macOS

### 1.4 Configure Issue Templates (Already Done)

**Status**: ✅ Templates configured in `.github/ISSUE_TEMPLATE/`

**Available Templates**:
- Bug Report
- Feature Request
- Documentation Issue
- API Issue

**Verification**:
1. Click "New Issue" in the Issues tab
2. Verify template options appear

## Phase 2: Enhanced Automation

### 2.1 Install SonarCloud

**Time**: 15 minutes

**Steps**:
1. Visit https://github.com/marketplace/sonarcloud
2. Click "Set up a plan"
3. Choose "Free for public repositories"
4. Select this repository
5. Complete the SonarCloud setup wizard
6. Add SonarCloud workflow:

```yaml
# .github/workflows/sonarcloud.yml
name: SonarCloud
on:
  push:
    branches: [ master, main ]
  pull_request:
    branches: [ master, main ]
jobs:
  sonarcloud:
    runs-on: windows-latest
    steps:
    - uses: actions/checkout@v4
      with:
        fetch-depth: 0
    - name: SonarCloud Scan
      uses: SonarSource/sonarcloud-github-action@master
      env:
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        SONAR_TOKEN: ${{ secrets.SONAR_TOKEN }}
```

### 2.2 Enable Release Drafter (Already Done)

**Status**: ✅ Workflow configured in `.github/workflows/release-drafter.yml`

**Verification**:
1. Merge a PR to main/master
2. Check Releases tab for draft release
3. Release notes are auto-generated from PR titles

### 2.3 Install Codecov

**Time**: 10 minutes

**Steps**:
1. Visit https://github.com/marketplace/codecov
2. Click "Set up a plan" (free for open source)
3. Authorize Codecov to access the repository
4. Add Codecov step to PowerShell CI workflow:

```yaml
- name: Upload Coverage to Codecov
  uses: codecov/codecov-action@v3
  with:
    files: ./coverage.xml
    flags: unittests
    name: codecov-umbrella
```

### 2.4 Install GitGuardian

**Time**: 10 minutes

**Steps**:
1. Visit https://github.com/marketplace/gitguardian
2. Click "Set up a plan" (free for public repositories)
3. Authorize GitGuardian
4. Select this repository
5. GitGuardian will start scanning for secrets automatically

## Phase 3: Team Productivity

### 3.1 Set Up GitHub Projects

**Time**: 20 minutes

**Steps**:
1. Go to Projects tab in repository
2. Click "New project"
3. Choose "Board" template
4. Create columns: "To Do", "In Progress", "Review", "Done"
5. Enable automation:
   - Auto-add new issues to "To Do"
   - Move to "In Progress" when PR is opened
   - Move to "Review" when PR is ready
   - Move to "Done" when PR is merged

### 3.2 Configure VS Code Settings (Already Done)

**Status**: ✅ Settings configured in `.vscode/`

**Available Configurations**:
- `.vscode/extensions.json` - Recommended extensions
- `.vscode/settings.json` - Workspace settings
- `.vscode/tasks.json` - PowerShell tasks

**For Contributors**:
1. Open repository in VS Code
2. VS Code will prompt to install recommended extensions
3. Click "Install All" to get the full developer experience

### 3.3 Enable GitHub Codespaces (Already Done)

**Status**: ✅ Dev container configured in `.devcontainer/devcontainer.json`

**Usage**:
1. Click "Code" → "Codespaces" → "New codespace"
2. Codespace will provision with:
   - PowerShell environment
   - .NET SDK
   - Azure CLI
   - GitHub CLI
   - All recommended VS Code extensions
   - Pester and PSScriptAnalyzer pre-installed

### 3.4 Install Microsoft Teams Integration

**Time**: 10 minutes

**Steps**:
1. Open Microsoft Teams
2. Go to the channel where you want notifications
3. Click "..." → "Connectors" → "Configure"
4. Search for "GitHub" and click "Configure"
5. Authorize with GitHub
6. Select this repository
7. Choose notification types:
   - Pull requests
   - Issues
   - Commits
   - Releases

## Phase 4: API & Documentation

### 4.1 Create Postman Collection

**Time**: 30 minutes

**Steps**:
1. Download and install Postman
2. Import the Swagger definition:
   - File → Import
   - Select `docs/swagger.yaml`
3. Create a new collection "MSRC Security Updates API"
4. Add environment variables:
   - `api_key` - Your MSRC API key
   - `base_url` - https://api.msrc.microsoft.com
5. Add pre-request script for authentication
6. Save collection and share with team
7. (Optional) Publish to Postman workspace

**Example Collection Structure**:
```
MSRC Security Updates API/
├── Get Security Updates
├── Get CVRF Document
├── Get Update by ID
└── Get Updates by Date Range
```

### 4.2 Set Up SwaggerHub (Optional)

**Time**: 15 minutes

**Steps**:
1. Visit https://app.swaggerhub.com/
2. Create free account
3. Click "Create New" → "Import and Document API"
4. Upload `docs/swagger.yaml`
5. Configure auto-sync with GitHub:
   - Settings → Integrations → GitHub
   - Authorize SwaggerHub
   - Select repository and file path
6. Enable public documentation

### 4.3 Configure ReadMe.io (Optional)

**Time**: 20 minutes

**Steps**:
1. Visit https://readme.com/
2. Create account
3. Import API documentation from Swagger
4. Customize documentation:
   - Add getting started guide
   - Add code examples
   - Configure API playground
5. Set up GitHub sync for automatic updates

## Verification

After implementing each phase, verify the following:

### Phase 1 Verification
- [ ] Dependabot PRs are being created
- [ ] CodeQL scans run successfully
- [ ] PowerShell CI workflow passes
- [ ] Issue templates appear when creating new issues

### Phase 2 Verification
- [ ] SonarCloud analysis runs on PRs
- [ ] Release drafts are auto-generated
- [ ] Code coverage is tracked
- [ ] No secrets detected by GitGuardian

### Phase 3 Verification
- [ ] Project board updates automatically
- [ ] VS Code prompts for extension installation
- [ ] Codespaces launch successfully
- [ ] Teams notifications are received

### Phase 4 Verification
- [ ] Postman collection works for API testing
- [ ] API documentation is accessible
- [ ] Swagger definition is up to date

## Troubleshooting

### Dependabot Issues

**Problem**: Dependabot not creating PRs
**Solution**: 
- Check Settings → Security & analysis → Dependabot is enabled
- Verify `.github/dependabot.yml` syntax
- Check for existing open Dependabot PRs (may hit limit)

### CodeQL Scan Failures

**Problem**: CodeQL workflow fails
**Solution**:
- Check workflow logs for specific errors
- Ensure C# files compile successfully
- Verify CodeQL action version is latest

### PowerShell CI Failures

**Problem**: Tests fail in CI but pass locally
**Solution**:
- Check PowerShell version differences
- Verify module dependencies are installed
- Review cross-platform compatibility (Windows vs Linux)

### Codespaces Issues

**Problem**: Codespace fails to build
**Solution**:
- Check `.devcontainer/devcontainer.json` syntax
- Verify image is available
- Check postCreateCommand errors in build log

### API Testing Issues

**Problem**: Postman requests fail
**Solution**:
- Verify API key is valid and not expired
- Check base URL is correct
- Review API rate limits
- Ensure proper authentication headers

## Best Practices

1. **Regular Maintenance**
   - Review Dependabot PRs weekly
   - Address CodeQL findings promptly
   - Keep workflows up to date
   - Monitor code coverage trends

2. **Team Onboarding**
   - Share this guide with new contributors
   - Encourage use of Codespaces for quick setup
   - Promote VS Code extension recommendations
   - Document team-specific workflows

3. **Security**
   - Never commit API keys or secrets
   - Review GitGuardian alerts immediately
   - Keep dependencies updated
   - Run security scans before releases

4. **Quality**
   - Maintain test coverage above 70%
   - Address PSScriptAnalyzer warnings
   - Use PR templates consistently
   - Require reviews before merging

## Support Resources

- **GitHub Docs**: https://docs.github.com
- **GitHub Marketplace**: https://github.com/marketplace
- **PowerShell Gallery**: https://www.powershellgallery.com/
- **VS Code Extensions**: https://marketplace.visualstudio.com/vscode
- **Azure DevOps**: https://docs.microsoft.com/azure/devops

## Next Steps

After completing implementation:

1. ✅ Enable branch protection rules
2. ✅ Configure required status checks
3. ✅ Set up automated deployments to PowerShell Gallery
4. ✅ Create documentation for contributors
5. ✅ Schedule regular dependency audits
6. ✅ Set up monitoring and alerting

---

For questions or issues with this implementation guide, please open an issue using the "Documentation Issue" template.
