# GitHub Upload Instructions

## Quick Start

### 1. Initialize Git Repository

```bash
cd "/Users/vivek/Documents/CURSOR BASE/14 dec"
git init
git add .
git commit -m "Initial commit: AI Search Quality Evaluator Framework"
```

### 2. Create GitHub Repository

1. Go to https://github.com/new
2. Repository name: `ai-search-quality-evaluator` (or your choice)
3. Description: `AI Search Quality Evaluation Framework with GUI - Evaluate AI Search quality metrics including Chrome's AI search mode`
4. Choose Public or Private
5. **Don't** initialize with README, .gitignore, or license (we have them)
6. Click "Create repository"

### 3. Connect and Push

```bash
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/ai-search-quality-evaluator.git
git push -u origin main
```

Replace `YOUR_USERNAME` with your GitHub username.

## What Will Be Uploaded

### ✅ Included
- All source code
- Configuration files
- Documentation (README, guides)
- GitHub Actions workflow
- License file
- Package.json

### ❌ Excluded (via .gitignore)
- `node_modules/` - Dependencies
- `reports/` - Generated reports
- `eval/ai-search/test-sets/*.json` - User uploads
- `.env` files - Environment variables
- IDE files (`.vscode/`, `.idea/`)
- OS files (`.DS_Store`)

## Before Pushing - Final Checks

### 1. Update Repository URL
Edit `package.json` and update the repository URL:
```json
"repository": {
  "type": "git",
  "url": "https://github.com/YOUR_USERNAME/ai-search-quality-evaluator.git"
}
```

### 2. Verify Files to Commit
```bash
git status
# Should show all source files, but NOT node_modules, reports, etc.
```

### 3. Test Installation
```bash
# In a clean directory, test that it works
npm install
npm start
```

## GitHub Repository Settings

### Recommended Settings
1. **Description**: "AI Search Quality Evaluation Framework with GUI"
2. **Topics**: Add these tags:
   - `ai-search`
   - `evaluation`
   - `quality-metrics`
   - `browser-automation`
   - `puppeteer`
   - `testing-framework`
   - `javascript`
   - `nodejs`

3. **About Section**:
   - Website: (optional)
   - Topics: (see above)

### Secrets for CI/CD (Optional)
If you want CI/CD to work:
1. Go to Settings → Secrets and variables → Actions
2. Add secrets:
   - `SEARCH_MODE`: `chrome` (or `api`)
   - `AI_SEARCH_API_ENDPOINT`: (if using API mode)
   - `AI_SEARCH_API_KEY`: (if using API mode)

## Post-Upload

### 1. Add Badges (Optional)
Add to README.md:
```markdown
![Node.js](https://img.shields.io/badge/node-%3E%3D18.0.0-brightgreen)
![License](https://img.shields.io/badge/license-MIT-blue)
```

### 2. Create First Release
1. Go to Releases → Create a new release
2. Tag: `v1.0.0`
3. Title: `v1.0.0 - Initial Release`
4. Description: "Initial release of AI Search Quality Evaluator"

## Verification

After uploading, verify:
- [ ] All files are present
- [ ] README displays correctly
- [ ] Code is properly formatted
- [ ] No sensitive data exposed
- [ ] CI/CD workflow is valid (if enabled)

## Troubleshooting

### If push fails:
```bash
# Check remote
git remote -v

# Force push (if needed, be careful!)
git push -u origin main --force
```

### If files are too large:
- Check `.gitignore` is working
- Verify `node_modules` is excluded
- Check for large files: `find . -size +10M -not -path "./node_modules/*"`

## Ready! 🚀

Your project is now ready for GitHub. All necessary files are in place and properly configured.

