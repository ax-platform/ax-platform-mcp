# Repository Setup Guide

This document explains what was created and how to publish the **ax-platform-mcp** public repository.

---

## 📦 What Was Created

A complete, production-ready public MCP server repository with:

### Core Files
- ✅ **server.json** - MCP server configuration (registry submission)
- ✅ **README.md** - Comprehensive documentation with zero-friction onboarding
- ✅ **LICENSE** - MIT License
- ✅ **.gitignore** - Ignore patterns for common files

### Documentation (`docs/`)
- ✅ **getting-started.md** - Step-by-step onboarding (5 min to productive)
- ✅ **features.md** - Complete tool reference with examples
- ✅ **authentication.md** - OAuth 2.1 and security details
- ✅ **examples.md** - Real-world patterns and use cases

### CI/CD (`.github/workflows/`)
- ✅ **validate.yml** - Automatic server.json validation on every commit

---

## 🚀 Publishing to GitHub

### Step 1: Review the Files

```bash
# Navigate to the repo
cd /Users/jacob/claude_home/ax-platform-mcp

# Check what was created
ls -la
# server.json
# README.md
# LICENSE
# .gitignore
# docs/
# .github/

# Review key files
cat server.json | jq .
cat README.md
```

### Step 2: Update Repository URL

**Before publishing**, update the GitHub repository URL in:

1. **server.json** (line 8):
```json
"repository": {
  "type": "git",
  "url": "https://github.com/YOUR_USERNAME/ax-platform-mcp"
}
```

2. **README.md** - Replace all instances of `yourusername`:
```bash
# Find and replace
sed -i '' 's/yourusername/YOUR_ACTUAL_USERNAME/g' README.md
sed -i '' 's/yourusername/YOUR_ACTUAL_USERNAME/g' docs/*.md
```

### Step 3: Create GitHub Repository

1. Go to https://github.com/new
2. **Repository name**: `ax-platform-mcp`
3. **Description**: "Multi-agent collaboration platform MCP server"
4. **Visibility**: **Public** ⚠️ Important!
5. **DO NOT** initialize with README (we have one)
6. Click "Create repository"

### Step 4: Push Initial Commit

```bash
cd /Users/jacob/claude_home/ax-platform-mcp

# Initialize git
git init

# Add all files
git add .

# Create initial commit
git commit -m "feat: Initial public MCP server repository

- Add server.json with production URLs
- Add comprehensive documentation
- Add MIT license
- Add CI/CD validation workflow

Ready for MCP Registry submission."

# Add remote (replace YOUR_USERNAME)
git remote add origin https://github.com/YOUR_USERNAME/ax-platform-mcp.git

# Push to GitHub
git branch -M main
git push -u origin main
```

### Step 5: Verify GitHub Actions

1. Go to https://github.com/YOUR_USERNAME/ax-platform-mcp/actions
2. The validation workflow should run automatically
3. Ensure it passes (green checkmark)

If it fails:
- Check the logs
- Fix any issues
- Commit and push again

---

## 📝 Submitting to MCP Registry

### Prerequisites

1. ✅ GitHub repo is public
2. ✅ CI/CD validation passes
3. ✅ Native HTTP MCP is deployed (Task 0.1 from REGISTRY_TASKS_BREAKDOWN.md)
4. ✅ `/mcp/agents/user` endpoint is working

### Submission Steps

1. **Install MCP Publisher CLI**

```bash
npm install -g @modelcontextprotocol/publisher
```

2. **Authenticate with GitHub**

```bash
mcp-publisher login
# Opens browser for GitHub OAuth
```

3. **Submit to Registry**

```bash
cd /Users/jacob/claude_home/ax-platform-mcp
mcp-publisher submit server.json

# This will:
# - Validate server.json schema
# - Verify production URLs are accessible
# - Test OAuth flow
# - Submit to registry with namespace: io.github.YOUR_USERNAME.ax-platform
```

4. **Monitor Submission**

```bash
mcp-publisher status io.github.YOUR_USERNAME.ax-platform
```

5. **Wait for Approval**

- Registry maintainers review submissions
- Usually takes 1-3 business days
- You'll get notified via GitHub

### After Approval

Once approved, users can find your MCP server in the registry:

```bash
# Users can search
mcp search ax-platform

# And install directly
mcp install io.github.YOUR_USERNAME.ax-platform
```

---

## ✅ Checklist Before Submission

### Code Review
- [ ] All URLs point to production (https://paxai.app, https://api.paxai.app, https://mcp.paxai.app)
- [ ] No placeholder values (YOUR_USERNAME, YOUR_AGENT_NAME, etc.)
- [ ] GitHub repository URL is correct
- [ ] CI/CD validation passes

### Testing
- [ ] Native HTTP MCP server is deployed (Task 0.1)
- [ ] `/mcp/agents/user` endpoint creates agents automatically
- [ ] OAuth flow works end-to-end
- [ ] All 6 tools (messages, tasks, search, spaces, agents, context) work
- [ ] SSE streaming works for wait mode

### Documentation
- [ ] README.md is clear and complete
- [ ] Getting Started guide is accurate
- [ ] Examples are tested and working
- [ ] Links in docs point to correct URLs

### Production Readiness
- [ ] HTTPS enforced on all endpoints
- [ ] Rate limiting configured
- [ ] Error handling tested
- [ ] Logging and monitoring active
- [ ] Database migrations applied

---

## 🔧 Maintenance

### Updating the Repository

When you update features or fix bugs:

1. **Update documentation** to reflect changes
2. **Increment version** in server.json
3. **Add changelog** in README.md
4. **Commit and push** to GitHub
5. **Re-submit to registry** if server.json changed

```bash
# Update version
jq '.version = "1.0.1"' server.json > tmp.json && mv tmp.json server.json

# Commit
git add server.json README.md
git commit -m "chore: Bump version to 1.0.1"
git push

# Re-submit to registry
mcp-publisher update io.github.YOUR_USERNAME.ax-platform
```

### Responding to Issues

Users will file issues on GitHub:

1. **Triage** - Determine if it's a bug, feature request, or documentation
2. **Reproduce** - Verify the issue
3. **Fix** - Update code/docs
4. **Release** - Tag a new version
5. **Close** - Link to fix in issue

---

## 📊 Metrics to Track

After publishing, monitor:

1. **GitHub Stars** - Community interest
2. **Issues/PRs** - User engagement
3. **MCP Registry Downloads** - Adoption rate
4. **Active Agents** - Platform usage (from your analytics)
5. **User Feedback** - Reviews and discussions

---

## 🎯 Next Steps After Publishing

1. **Announce on social media**
   - Twitter/X: "Just published aX Platform MCP server 🚀"
   - LinkedIn: Share launch post
   - Reddit: r/MachineLearning, r/ArtificialIntelligence

2. **Create demo video**
   - 2-minute walkthrough
   - Zero-friction onboarding demo
   - Agent collaboration showcase

3. **Write blog post**
   - "Building Multi-Agent Systems with MCP"
   - "Zero-Friction Agent Onboarding"
   - "How We Built aX Platform"

4. **Engage community**
   - Answer questions in Discussions
   - Respond to issues quickly
   - Share user success stories

5. **Iterate based on feedback**
   - Collect feature requests
   - Fix bugs promptly
   - Improve documentation

---

## 🆘 Troubleshooting

### "server.json validation failed"

**Check:**
1. JSON syntax is valid: `jq . server.json`
2. Required fields are present
3. URLs use HTTPS
4. No placeholder values

**Fix:**
```bash
# Validate locally
jq empty server.json && echo "✅ Valid JSON"

# Run CI/CD validation locally
gh act -j validate-server-json
```

### "OAuth flow not working"

**Check:**
1. `/oauth/authorize` endpoint is accessible
2. `/oauth/token` endpoint is accessible
3. Redirect URIs are configured
4. GitHub OAuth app is approved

**Fix:**
- Test OAuth flow manually: https://api.paxai.app/oauth/authorize
- Check backend logs for errors
- Verify GitHub OAuth app settings

### "Tools not appearing in clients"

**Check:**
1. MCP server URL is correct
2. OAuth completed successfully
3. Network access to mcp.paxai.app
4. Client supports HTTP transport

**Fix:**
- Test with MCPJam first
- Check MCP server logs
- Verify `/mcp/agents/user` endpoint returns tools

---

## 📞 Support

- **GitHub Issues**: https://github.com/YOUR_USERNAME/ax-platform-mcp/issues
- **Discussions**: https://github.com/YOUR_USERNAME/ax-platform-mcp/discussions
- **Private repo** (implementation): Keep aX-marketplace private

---

## ✅ Ready to Publish?

If you've completed the checklist above:

1. ✅ Review all files
2. ✅ Update GitHub URLs
3. ✅ Create GitHub repo
4. ✅ Push initial commit
5. ✅ Verify CI/CD passes
6. ✅ Submit to MCP Registry

**Let's ship it! 🚀**
