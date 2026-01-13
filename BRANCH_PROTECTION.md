# Branch Protection Setup Guide

This guide walks you through setting up branch protection rules for the `main` and `dev` branches to enforce the Git workflow.

---

## Why Branch Protection?

Branch protection rules prevent:
- 🚫 Direct commits to protected branches
- 🚫 Merging without code review
- 🚫 Merging failing builds
- 🚫 Deleting important branches

They enforce:
- ✅ Pull request workflow
- ✅ Mandatory code reviews
- ✅ Automated checks before merge
- ✅ Clean, auditable history

---

## Setup Instructions

### Prerequisites

- Repository administrator access
- GitHub repository: `https://github.com/alirezarezvani/claude-code-mastery`

### Step 1: Access Branch Protection Settings

1. Go to your repository on GitHub
2. Click **Settings** (top right)
3. In the left sidebar, click **Branches**
4. Under "Branch protection rules", click **Add rule**

### Step 2: Protect `main` Branch

#### Basic Settings
- **Branch name pattern:** `main`

#### Rules to Enable

##### 1. Require a pull request before merging
- ✅ Check this box
- **Required approvals:** 1
- ✅ Dismiss stale pull request approvals when new commits are pushed
- ✅ Require review from Code Owners (if CODEOWNERS file exists)
- ⚠️ **Optional:** Require approval from specific reviewers

##### 2. Require status checks to pass before merging
- ✅ Check this box
- ✅ Require branches to be up to date before merging
- **Status checks to require:** (Add after CI/CD setup)
  - `markdown-lint` (if configured)
  - `link-validator` (if configured)
  - `test-examples` (if configured)

##### 3. Require conversation resolution before merging
- ✅ Check this box
- All review comments must be resolved before merging

##### 4. Require signed commits (Optional but Recommended)
- ✅ Check this box
- Ensures commit authenticity

##### 5. Require linear history (Optional)
- ⚠️ Prevents merge commits, requires rebase
- Consider enabling for cleaner history

##### 6. Include administrators
- ✅ Check this box
- Even admins must follow the rules

##### 7. Restrict who can push to matching branches
- ✅ Check this box
- **Do NOT add any users/teams**
- This prevents ALL direct pushes (PRs still work)

##### 8. Allow force pushes
- ❌ Leave UNCHECKED
- Prevents history rewriting

##### 9. Allow deletions
- ❌ Leave UNCHECKED
- Prevents accidental branch deletion

#### Click "Create" to save

---

### Step 3: Protect `dev` Branch

Repeat Step 1 with these settings:

#### Basic Settings
- **Branch name pattern:** `dev`

#### Rules to Enable

##### 1. Require a pull request before merging
- ✅ Check this box
- **Required approvals:** 1
- ✅ Dismiss stale pull request approvals when new commits are pushed
- ✅ Require review from Code Owners (optional)

##### 2. Require status checks to pass before merging
- ✅ Check this box
- ⚠️ **Optional:** Require branches to be up to date before merging
  - Less strict than `main` to allow faster iteration

##### 3. Require conversation resolution before merging
- ✅ Check this box

##### 4. Require signed commits (Optional)
- ⚠️ Optional for `dev`

##### 5. Include administrators
- ✅ Check this box

##### 6. Restrict who can push to matching branches
- ⚠️ **Optional** for `dev`
- Consider allowing certain team members to push directly
- Or keep strict like `main`

##### 7. Allow force pushes
- ❌ Leave UNCHECKED

##### 8. Allow deletions
- ❌ Leave UNCHECKED

#### Click "Create" to save

---

## Verification

### Test the Protection

1. **Try to push directly to main:**
   ```bash
   git checkout main
   echo "test" >> README.md
   git add README.md
   git commit -m "test"
   git push origin main
   ```
   **Expected result:** Push rejected ✅

2. **Create a PR without approval:**
   ```bash
   git checkout dev
   git checkout -b test/protection
   echo "test" >> README.md
   git add README.md
   git commit -m "test"
   git push -u origin test/protection
   gh pr create --base dev --title "Test protection"
   # Try to merge without approval
   ```
   **Expected result:** Merge blocked until approved ✅

3. **Create PR to main from feature branch:**
   ```bash
   git checkout -b test/wrong-target
   gh pr create --base main --title "Test"
   ```
   **Expected result:** Can create PR, but should be discouraged by workflow ⚠️

---

## GitHub Actions Integration

GitHub Actions workflows are now configured for automated checks.

### Status Checks Available

The following CI/CD checks run automatically on all PRs:

1. **`lint`** — File naming conventions and structure validation
2. **`markdown-lint`** — Markdown quality and formatting
3. **`link-check`** — Broken link detection
4. **`structure-check`** — Repository structure verification

### Adding Status Checks to Branch Protection

After the first workflow run:

1. **Navigate to Branch Protection**
   ```
   Repository Settings → Branches → main (Edit)
   ```

2. **Enable Status Checks**
   - Under "Require status checks to pass before merging"
   - ✅ Check "Require branches to be up to date before merging"

3. **Select Required Checks**
   - In the search box, add:
     - ✅ `lint`
     - ✅ `markdown-lint`
     - ✅ `link-check`
     - ✅ `structure-check`

4. **Repeat for `dev` Branch**
   - Same checks apply to `dev` branch

5. **Save Changes**

### Workflow Files

All workflows are in `.github/workflows/`:

| Workflow | Purpose | When it Runs |
|----------|---------|--------------|
| `ci.yml` | Main CI pipeline (lint, markdown, links, structure) | On PR to main/dev, push to main/dev |
| `auto-label.yml` | Auto-assigns labels based on changed files | On PR open/update |
| `stale.yml` | Marks stale issues/PRs | Daily at midnight UTC |

### Viewing Workflow Results

1. **In Pull Requests:**
   - PR page shows status checks at the bottom
   - ✅ Green check = all tests passed
   - ❌ Red X = tests failed (click for details)
   - 🟡 Yellow circle = tests running

2. **In Actions Tab:**
   - Go to repository → Actions tab
   - View all workflow runs
   - Click on specific run for detailed logs
   - Filter by workflow, branch, or status

### Troubleshooting Failed Checks

#### Lint Failed
```bash
# Run locally to fix issues
find . -name "* *" -type f  # Find files with spaces
# Rename files to use hyphens instead
```

#### Markdown-Lint Failed
```bash
# Install and run locally
npm install -g markdownlint-cli
markdownlint '**/*.md' --fix
```

#### Link-Check Failed
```bash
# Install and run locally
npm install -g markdown-link-check
markdown-link-check README.md
# Fix broken links in the file
```

#### Structure-Check Failed
```bash
# Verify required files exist
ls -la README.md CONTRIBUTING.md LICENSE
ls -la .github/CODEOWNERS .github/pull_request_template.md
# Add missing files
```

### Manual Workflow Triggers

Some workflows can be triggered manually:

```bash
# Trigger stale workflow manually
gh workflow run stale.yml
```

### Bypassing Checks (Emergency Only)

If you absolutely must merge despite failing checks:

1. Repository Settings → Branches → Edit rule
2. Temporarily disable "Require status checks to pass"
3. Merge your PR
4. **Immediately re-enable** the requirement

⚠️ **Use this only for critical emergencies!**

---

## CODEOWNERS File

The `.github/CODEOWNERS` file is now configured to automatically assign reviewers.

### How It Works

When someone creates a PR, CODEOWNERS automatically:
1. Identifies which files were changed
2. Matches file patterns to owners
3. Requests review from the appropriate owners

### Current Configuration

See `.github/CODEOWNERS` for the complete configuration. Key patterns:

| Pattern | Owner | Description |
|---------|-------|-------------|
| `*` | @alirezarezvani | Global ownership of all files |
| `*.md` | @alirezarezvani | All documentation files |
| `/performance/` | @alirezarezvani | Performance guides |
| `/enterprise/` | @alirezarezvani | Enterprise patterns |
| `/hooks/` | @alirezarezvani | Hook configurations |
| `/.github/` | @alirezarezvani | GitHub configuration |

### Enabling CODEOWNERS in Branch Protection

Ensure this is enabled in branch protection settings:

1. Repository Settings → Branches → main (Edit)
2. Under "Require pull request reviews"
3. ✅ Check "Require review from Code Owners"
4. Save changes

### Testing CODEOWNERS

Create a test PR to verify automatic assignment:

```bash
git checkout -b test/codeowners
echo "# Test" >> test.md
git add test.md
git commit -m "test: verify CODEOWNERS"
git push -u origin test/codeowners
gh pr create --base dev --title "Test: CODEOWNERS assignment"
```

Expected: @alirezarezvani is automatically requested as reviewer

### Expanding for Teams

When your team grows, update `.github/CODEOWNERS`:

```
# Documentation team
*.md @alirezarezvani @docs-team

# Hooks team
/hooks/ @alirezarezvani @automation-team

# Enterprise team
/enterprise/ @alirezarezvani @enterprise-team
```

### Troubleshooting

**CODEOWNERS not assigning reviewers?**

- Ensure file is named exactly `.github/CODEOWNERS` (all caps, no extension)
- Verify "Require review from Code Owners" is enabled in branch protection
- Check CODEOWNERS syntax — paths must match repository structure
- Ensure owners have repository access

---

## Additional Settings

### Default Branch

Ensure `main` is the default branch:
1. Repository Settings → Branches
2. Default branch: `main`
3. Click "Update" if needed

### Auto-Delete Branch After Merge

Enable automatic branch deletion:
1. Repository Settings → General
2. Scroll to "Pull Requests"
3. ✅ Check "Automatically delete head branches"

This keeps your repository clean.

---

## Troubleshooting

### "I can't push to dev anymore"

This is intentional! Use the PR workflow:
```bash
git checkout -b feature/my-feature
# Make changes
git push -u origin feature/my-feature
gh pr create --base dev
```

### "I need to make an emergency hotfix"

Even hotfixes follow the workflow:
1. Create branch from `dev`
2. Make fix
3. Create PR to `dev`
4. Get expedited review
5. Merge to `dev`
6. Create PR from `dev` to `main`
7. Merge to `main`

**Note:** You can temporarily disable protection if absolutely necessary:
- Go to Branch protection rules
- Click "Edit" on the rule
- Uncheck "Include administrators"
- Make your change
- Re-enable immediately after

**⚠️ Use this ONLY for critical emergencies**

### "Status checks are failing but I don't have CI/CD yet"

If you configured status checks but haven't set up CI/CD:
1. Edit the branch protection rule
2. Uncheck "Require status checks to pass before merging"
3. Re-enable after CI/CD is configured

---

## Next Steps

After setting up branch protection:

1. ✅ Test the workflow with a dummy PR
2. ✅ Install GitHub App for code review
3. ✅ Set up CI/CD for automated checks
4. ✅ Create CODEOWNERS file (optional)
5. ✅ Document any project-specific rules
6. ✅ Train team members on the workflow

---

## Summary Checklist

- [ ] `main` branch protection enabled
- [ ] `dev` branch protection enabled
- [ ] Require PR reviews (1+ approvals)
- [ ] Require conversation resolution
- [ ] Restrict direct pushes to `main`
- [ ] Auto-delete merged branches enabled
- [ ] Default branch set to `main`
- [ ] Workflow tested with dummy PR
- [ ] Team notified of new workflow

---

## Questions?

- Check [GIT_WORKFLOW.md](./GIT_WORKFLOW.md) for workflow details
- Check [CONTRIBUTING.md](./CONTRIBUTING.md) for contribution guidelines
- Open an issue for questions
- Reach out on [Medium](https://medium.com/@alirezarezvani)

---

**Once configured, your repository will be protected from accidental changes and enforce best practices automatically.**
