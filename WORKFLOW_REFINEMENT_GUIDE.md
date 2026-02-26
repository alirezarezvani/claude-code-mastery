# Workflow Refinement Guide — Step-by-Step Implementation

This guide walks you through refining your Git workflow with branch protection, code review automation, CI/CD, and quality checks.

**Time Required:** 30-45 minutes
**Skill Level:** Intermediate
**Prerequisites:** GitHub App installed, repository admin access

---

## 📋 Implementation Checklist

Track your progress:

- [ ] **Step 1:** Configure Branch Protection Rules (Manual — 10 min)
- [ ] **Step 2:** Set Code Review Requirements (Manual — 5 min)
- [ ] **Step 3:** Set Up GitHub Actions CI/CD (Automated — 5 min)
- [ ] **Step 4:** Create PR Templates (Automated — 2 min)
- [ ] **Step 5:** Create CODEOWNERS File (Automated — 2 min)
- [ ] **Step 6:** Configure Required Status Checks (Manual — 5 min)
- [ ] **Step 7:** Set Up Workflow Automation (Automated — 5 min)
- [ ] **Step 8:** Update Documentation (Automated — 2 min)
- [ ] **Step 9:** Test the Complete Workflow (Manual — 10 min)

---

## Step 1: Configure Branch Protection Rules

**⚙️ Manual Configuration Required**

### For `main` Branch

1. **Navigate to Settings**
   ```
   GitHub Repository → Settings → Branches
   ```

2. **Add Branch Protection Rule**
   - Click **"Add rule"** or **"Add branch protection rule"**

3. **Branch Name Pattern**
   ```
   main
   ```

4. **Enable These Settings:**

   #### Protect matching branches
   - ✅ **Require a pull request before merging**
     - Required number of approvals: **1**
     - ✅ Dismiss stale pull request approvals when new commits are pushed
     - ✅ Require review from Code Owners
     - ⚠️ Leave "Require approval of the most recent reviewable push" **unchecked** (optional, can be strict)

   #### Status checks
   - ✅ **Require status checks to pass before merging**
     - ✅ Require branches to be up to date before merging
     - **Status checks to require:** (Will configure in Step 6 after Actions are set up)
       - [ ] `lint` ← Add after Step 3
       - [ ] `markdown-lint` ← Add after Step 3
       - [ ] `link-check` ← Add after Step 3

   #### Additional settings
   - ✅ **Require conversation resolution before merging**
   - ✅ **Require signed commits** (Recommended for security)
   - ⚠️ **Require linear history** (Optional — prevents merge commits)
   - ✅ **Do not allow bypassing the above settings**
   - ✅ **Restrict who can push to matching branches**
     - **Do NOT add any users/teams** — this blocks ALL direct pushes
   - ❌ **Allow force pushes** — Leave UNCHECKED
   - ❌ **Allow deletions** — Leave UNCHECKED

5. **Lock Branch (Optional)**
   - ✅ **Lock branch** — Prevents any pushes (even via PR)
   - ⚠️ Only enable if you want to completely freeze `main`

6. **Save Changes**
   - Click **"Create"** or **"Save changes"**

### For `dev` Branch

Repeat the process with slightly relaxed rules:

1. **Branch Name Pattern:** `dev`

2. **Enable These Settings:**
   - ✅ Require a pull request before merging
     - Required approvals: **1**
     - ✅ Dismiss stale pull request approvals
     - ⚠️ Require review from Code Owners (Optional for dev)

   - ✅ Require status checks to pass before merging
     - ⚠️ Require branches to be up to date (Optional — allows faster iteration)
     - Status checks: Same as `main`

   - ✅ Require conversation resolution before merging
   - ⚠️ Require signed commits (Optional for dev)
   - ✅ Do not allow bypassing settings
   - ⚠️ Restrict who can push (Optional — some teams allow direct dev pushes)
   - ❌ Allow force pushes — UNCHECKED
   - ❌ Allow deletions — UNCHECKED

3. **Save Changes**

### Verification

Test that protection works:

```bash
# Try to push directly to main (should fail)
git checkout main
echo "test" >> README.md
git add README.md
git commit -m "test"
git push origin main
# Expected: "remote: error: GH006: Protected branch update failed"
```

✅ **Step 1 Complete!**

---

## Step 2: Set Code Review Requirements

**⚙️ Manual Configuration Required**

### Configure Default Reviewers

1. **Navigate to Settings**
   ```
   GitHub Repository → Settings → General → Pull Requests
   ```

2. **Enable Auto-Merge**
   - ✅ **Allow auto-merge**
   - Lets approved PRs merge automatically

3. **Enable Auto-Delete**
   - ✅ **Automatically delete head branches**
   - Cleans up feature branches after merge

4. **Suggest Updating Branches**
   - ✅ **Always suggest updating pull request branches**
   - Helps keep PRs in sync with target

5. **Save Changes**

### Configure Review Assignment (Optional)

For teams with multiple reviewers:

1. **Navigate to Settings → Code review**
   ```
   Settings → Code review limits
   ```

2. **Set Review Limits**
   - Limit review requests for team members
   - Automatic assignment rotation

⚠️ **Note:** For solo projects, skip this section. Relevant for teams only.

✅ **Step 2 Complete!**

---

## Step 3: Set Up GitHub Actions CI/CD

**🤖 Automated — Files Created Automatically**

I'll create GitHub Actions workflows for:
- Markdown linting
- Link validation
- File structure checks

### Workflow Files to Create

The following files will be created in `.github/workflows/`:

1. **`ci.yml`** — Main CI pipeline
2. **`markdown-lint.yml`** — Markdown quality checks
3. **`link-check.yml`** — Broken link detection
4. **`auto-label.yml`** — Automatic PR labeling

These files are ready to commit. See **Step 3 Implementation** below.

✅ **Step 3 Ready for Implementation!**

---

## Step 4: Create PR Templates

**🤖 Automated — Files Created Automatically**

PR templates ensure consistent, high-quality pull requests.

### Files to Create

1. **`.github/pull_request_template.md`** — Default PR template
2. **`.github/PULL_REQUEST_TEMPLATE/feature.md`** — Feature-specific template
3. **`.github/PULL_REQUEST_TEMPLATE/fix.md`** — Bug fix template
4. **`.github/PULL_REQUEST_TEMPLATE/docs.md`** — Documentation template

These files are ready to commit. See **Step 4 Implementation** below.

✅ **Step 4 Ready for Implementation!**

---

## Step 5: Create CODEOWNERS File

**🤖 Automated — File Created Automatically**

CODEOWNERS automatically assigns reviewers based on file paths.

### File to Create

- **`.github/CODEOWNERS`** — Ownership rules

This file is ready to commit. See **Step 5 Implementation** below.

✅ **Step 5 Ready for Implementation!**

---

## Step 6: Configure Required Status Checks

**⚙️ Manual Configuration Required** (After Step 3)

Once GitHub Actions workflows are running, configure required checks.

### Add Status Checks to Branch Protection

1. **Wait for First Workflow Run**
   - Push the GitHub Actions workflows (Step 3)
   - Wait for them to run at least once
   - GitHub only shows checks that have run

2. **Navigate to Branch Protection**
   ```
   GitHub Repository → Settings → Branches → main (Edit)
   ```

3. **Add Required Status Checks**
   - Under "Require status checks to pass before merging"
   - In the search box, you'll now see:
     - ✅ `lint`
     - ✅ `markdown-lint`
     - ✅ `link-check`
   - Select all three

4. **Repeat for `dev` Branch**
   - Edit `dev` branch protection
   - Add same status checks

5. **Save Changes**

### Verification

Create a test PR and verify checks run:

```bash
git checkout -b test/status-checks
echo "# Test" >> test.md
git add test.md
git commit -m "test: verify status checks"
git push -u origin test/status-checks
gh pr create --base dev --title "Test: Verify status checks"
```

Check that PR shows:
- ✅ All checks must pass
- 🟡 Checks are running
- ✅ Checks passed (or ❌ if there are issues)

✅ **Step 6 Complete!**

---

## Step 7: Set Up Workflow Automation

**🤖 Automated — Files Created Automatically**

Additional automation workflows:
- Auto-assign labels based on file changes
- Auto-request reviewers
- Stale PR management

### Files to Create

1. **`.github/workflows/auto-assign.yml`** — Auto-assign reviewers
2. **`.github/workflows/stale.yml`** — Mark stale PRs/issues
3. **`.github/workflows/label-sync.yml`** — Sync labels across repos

These files are ready to commit. See **Step 7 Implementation** below.

✅ **Step 7 Ready for Implementation!**

---

## Step 8: Update Documentation

**🤖 Automated — Files Updated Automatically**

Update existing documentation with GitHub App specifics:

1. **BRANCH_PROTECTION.md**
   - Add GitHub Actions status checks section
   - Update with actual check names
   - Add troubleshooting for failed checks

2. **GIT_WORKFLOW.md**
   - Add CI/CD integration notes
   - Document status check requirements

3. **CONTRIBUTING.md**
   - Reference PR templates
   - Document CODEOWNERS

✅ **Step 8 Ready for Implementation!**

---

## Step 9: Test the Complete Workflow

**⚙️ Manual Testing Required**

### End-to-End Test

1. **Create a Test Feature Branch**
   ```bash
   git checkout dev
   git pull origin dev
   git checkout -b feature/test-complete-workflow
   ```

2. **Make a Test Change**
   ```bash
   echo "# Workflow Test" >> test-workflow.md
   git add test-workflow.md
   git commit -m "test: verify complete workflow"
   git push -u origin feature/test-complete-workflow
   ```

3. **Create Pull Request**
   ```bash
   gh pr create --base dev --title "Test: Complete workflow verification"
   ```

4. **Verify All Checks**
   - [ ] PR template auto-filled
   - [ ] CODEOWNERS assigned as reviewers
   - [ ] CI checks running (lint, markdown-lint, link-check)
   - [ ] Labels auto-assigned
   - [ ] Can't merge without approval
   - [ ] Can't merge with failing checks
   - [ ] Can't merge with unresolved conversations

5. **Approve and Merge**
   - Get approval (or self-approve for testing)
   - Verify merge completes
   - Verify branch auto-deleted

6. **Test Protection on Main**
   ```bash
   git checkout dev
   git pull origin dev
   git checkout -b test/dev-to-main
   echo "# Release test" >> test-release.md
   git add test-release.md
   git commit -m "test: verify dev to main protection"
   git push -u origin test/dev-to-main
   gh pr create --base main --title "Test: Dev to Main protection"
   ```

   Verify:
   - [ ] All checks must pass
   - [ ] Requires review approval
   - [ ] Higher scrutiny on `main`

7. **Clean Up**
   ```bash
   # Delete test files
   git checkout dev
   git branch -D feature/test-complete-workflow test/dev-to-main
   git push origin --delete feature/test-complete-workflow test/dev-to-main
   ```

✅ **Step 9 Complete!**

---

## Implementation Order

### Phase 1: Manual Configuration (15 minutes)
1. ✅ Configure Branch Protection for `main`
2. ✅ Configure Branch Protection for `dev`
3. ✅ Set Code Review Requirements

### Phase 2: Automated Setup (10 minutes)
4. ✅ Create GitHub Actions workflows
5. ✅ Create PR templates
6. ✅ Create CODEOWNERS file
7. ✅ Set up workflow automation
8. ✅ Update documentation

**→ Commit all Phase 2 files in one feature branch**

### Phase 3: Integration (10 minutes)
6. ✅ Configure Required Status Checks (after workflows run)
9. ✅ Test Complete Workflow

---

## Quick Start Commands

Once you're ready to implement Phase 2:

```bash
# Create feature branch for automation setup
git checkout dev
git pull origin dev
git checkout -b feature/setup-ci-cd-and-templates

# Files will be created automatically
# Review changes, then commit
git add .
git commit -m "feat: add CI/CD workflows, PR templates, and CODEOWNERS"
git push -u origin feature/setup-ci-cd-and-templates

# Create PR
gh pr create --base dev --title "Setup CI/CD, PR templates, and automation"
```

---

## Troubleshooting

### "Status checks don't appear in branch protection"
**Solution:** Run the workflows at least once. GitHub only shows checks that have executed.

### "PR template not auto-filling"
**Solution:** Ensure file is named exactly `.github/pull_request_template.md` (lowercase, underscore, no spaces)

### "CODEOWNERS not assigning reviewers"
**Solution:**
1. Ensure file is in `.github/CODEOWNERS` (all caps)
2. Verify "Require review from Code Owners" is enabled in branch protection
3. Check CODEOWNERS syntax (paths must match repository structure)

### "Checks failing on valid files"
**Solution:** Review workflow logs in Actions tab. Common issues:
- Markdown syntax errors
- Broken links (especially internal)
- File naming conventions

### "Can't merge even after approval"
**Solution:** Ensure:
- All required status checks passed
- All conversations resolved
- Branch is up to date with target

---

## Next Steps

After completing this guide:

1. **Monitor CI/CD Performance**
   - Check Actions tab for workflow performance
   - Optimize slow checks
   - Add caching if needed

2. **Refine Automation Rules**
   - Adjust label assignments based on patterns
   - Fine-tune CODEOWNERS as team grows
   - Add more specialized workflows

3. **Document Team-Specific Rules**
   - Add project-specific checks
   - Document review expectations
   - Create onboarding guide

4. **Scale for Growth**
   - Add more granular CODEOWNERS
   - Implement review rotation
   - Set up notification rules

---

## Summary

After completing all steps, you'll have:

✅ Protected branches preventing accidental changes
✅ Mandatory code review on all PRs
✅ Automated CI/CD checks (lint, markdown, links)
✅ Consistent PR descriptions via templates
✅ Automatic reviewer assignment via CODEOWNERS
✅ Auto-labeling and workflow automation
✅ Comprehensive documentation

**Your repository is now production-grade with enterprise-level quality controls!**

---

## Ready to Start?

**👉 Begin with [Step 1: Configure Branch Protection Rules](#step-1-configure-branch-protection-rules)**

For automated file creation, continue to the next section where all files will be generated.
