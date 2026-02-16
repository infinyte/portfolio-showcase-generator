# 📦 Installation Guide

Complete instructions for installing the Portfolio Showcase Generator skill in Claude AI.

---

## 📋 Table of Contents

- [Prerequisites](#prerequisites)
- [Installation Methods](#installation-methods)
  - [Method 1: Copy/Paste (Recommended)](#method-1-copypaste-recommended)
  - [Method 2: File Upload](#method-2-file-upload)
- [Verification](#verification)
- [Troubleshooting](#troubleshooting)
- [Updating the Skill](#updating-the-skill)
- [Uninstalling](#uninstalling)

---

## ✅ Prerequisites

Before installing, ensure you have:

1. **Active Claude Account**
   - Claude Pro, Team, or Enterprise subscription
   - Access to [claude.ai](https://claude.ai)

2. **File Creation Access**
   - Your account must have access to Claude's computer use features
   - Verify by asking Claude: *"Can you create files?"*

3. **Skill File**
   - Download [`SKILL.md`](SKILL.md) from this repository
   - Or copy the content directly from GitHub

---

## 🚀 Installation Methods

### Method 1: Copy/Paste (Recommended)

**Time Required:** 2-3 minutes

#### Step 1: Download the Skill

1. Navigate to [`SKILL.md`](SKILL.md) in this repository
2. Click the "Raw" button (top right of file viewer)
3. Select all text (Ctrl+A / Cmd+A)
4. Copy to clipboard (Ctrl+C / Cmd+C)

#### Step 2: Open Claude

1. Go to [claude.ai](https://claude.ai)
2. Start a **new conversation**
3. Ensure you're NOT in a project (skills install globally)

#### Step 3: Request File Creation

Send this message to Claude:

```
Please create a file at the following path with the content I'll provide:

Path: /mnt/skills/user/portfolio-showcase-generator/SKILL.md

[Paste the SKILL.md content here]
```

#### Step 4: Claude Creates the File

Claude will:
1. Create the directory structure
2. Save the skill file
3. Confirm installation

**Example Response:**
```
✅ I've created the skill file at 
/mnt/skills/user/portfolio-showcase-generator/SKILL.md

The Portfolio Showcase Generator skill is now installed and 
available in all your conversations!
```

#### Step 5: Verify Installation

Ask Claude:
```
Do you have access to the portfolio-showcase-generator skill?
```

**Expected Response:**
```
Yes! I can see the portfolio-showcase-generator skill. 
It's ready to transform your technical projects into 
compelling portfolio materials...
```

---

### Method 2: File Upload

**Time Required:** 3-4 minutes

#### Step 1: Prepare the File

1. Download [`SKILL.md`](SKILL.md) to your computer
2. Rename it to `SKILL.md` if needed

#### Step 2: Upload to Claude

1. Start a new Claude conversation
2. Use the file upload feature (📎 paperclip icon)
3. Upload `SKILL.md`

#### Step 3: Request Installation

Send this message:
```
I've uploaded the portfolio-showcase-generator skill. 
Please install it to /mnt/skills/user/portfolio-showcase-generator/SKILL.md
```

#### Step 4: Claude Installs

Claude will:
1. Read the uploaded file
2. Create the directory structure
3. Copy the skill to the correct location
4. Confirm installation

---

## ✅ Verification

### Quick Verification

Ask Claude any of these questions:

**Option 1:**
```
List all my custom skills
```

**Option 2:**
```
Show me the portfolio-showcase-generator skill description
```

**Option 3:**
```
Can you use the portfolio-showcase-generator skill?
```

### Test the Skill

Try a quick test:

```
Use the portfolio-showcase-generator skill to create an 
executive summary for a project where I built a REST API 
that reduced response time by 60% and served 1000 concurrent users.
```

**Expected Output:**
- Claude uses the skill
- Generates a professional executive summary
- Includes quantified metrics
- Formatted appropriately

---

## 🔧 Troubleshooting

### Issue 1: "I don't see that skill"

**Cause:** The skill file may not be in the correct location.

**Solution:**
1. Ask Claude: `View /mnt/skills/user`
2. Check if `portfolio-showcase-generator` directory exists
3. If not, reinstall using Method 1
4. Ensure path is exactly: `/mnt/skills/user/portfolio-showcase-generator/SKILL.md`

---

### Issue 2: "I can't create files"

**Cause:** Your Claude subscription may not include file creation features.

**Solution:**
1. Verify you have Claude Pro, Team, or Enterprise
2. Check your account settings
3. Try in a new conversation (not a project)
4. Contact Claude support if issue persists

---

### Issue 3: Skill doesn't work as expected

**Cause:** Skill file may be incomplete or corrupted.

**Solution:**
1. Re-download `SKILL.md` from the repository
2. Verify the file size (should be ~14KB, 400+ lines)
3. Reinstall using Method 1
4. Clear browser cache and try again

---

### Issue 4: "Permission denied" error

**Cause:** Attempting to install in a restricted directory.

**Solution:**
1. Ensure path is `/mnt/skills/user/...` (not `/mnt/skills/public/...`)
2. User directory is your personal skill space
3. Don't use `/home/claude/` for skill installation

---

### Issue 5: Skill not persisting between conversations

**Cause:** Skill may be installed in temporary directory.

**Solution:**
1. Verify installation path: `/mnt/skills/user/portfolio-showcase-generator/SKILL.md`
2. Do NOT install to `/home/claude/`
3. Reinstall in the correct location

---

## 🔄 Updating the Skill

When a new version is released:

### Step 1: Check Current Version

Ask Claude:
```
What version of the portfolio-showcase-generator skill do I have?
```

### Step 2: Download New Version

1. Visit the [GitHub repository](../../)
2. Download the latest `SKILL.md`
3. Check the [CHANGELOG](CHANGELOG.md) for updates

### Step 3: Replace Old Version

```
Please replace /mnt/skills/user/portfolio-showcase-generator/SKILL.md 
with this updated content:

[Paste new SKILL.md content]
```

### Step 4: Verify Update

```
Show me the portfolio-showcase-generator skill description
```

---

## 🗑️ Uninstalling

To remove the skill:

### Step 1: Request Deletion

Ask Claude:
```
Please delete /mnt/skills/user/portfolio-showcase-generator/
```

### Step 2: Verify Removal

```
List my custom skills
```

The portfolio-showcase-generator should no longer appear.

---

## 📱 Platform-Specific Notes

### Claude Web (claude.ai)

- ✅ Full support for skill installation
- ✅ Skills persist across all conversations
- ✅ Works in both desktop and mobile browsers

### Claude Mobile App

- ✅ Skills installed on web are accessible
- ⚠️ File upload may be limited on mobile
- 💡 Use copy/paste method (Method 1)

### Claude Desktop App

- ✅ Full support for skill installation
- ✅ Same installation process as web
- ✅ Better file handling capabilities

---

## 🎓 Pro Tips

### Tip 1: Install in Fresh Conversation

Always install skills in a new conversation (not inside a project) to ensure global availability.

### Tip 2: Verify Before Using

After installation, verify the skill works with a simple test before relying on it for important work.

### Tip 3: Keep a Backup

Save a copy of `SKILL.md` locally in case you need to reinstall.

### Tip 4: Check for Updates

Star the GitHub repository to be notified of updates and improvements.

### Tip 5: Customize If Needed

Advanced users can modify `SKILL.md` to customize behavior:
- Adjust output lengths
- Add company-specific sections
- Modify tone or formatting preferences

---

## 📞 Need Help?

- **GitHub Issues**: [Report problems](../../issues)
- **Discussions**: [Ask questions](../../discussions)
- **Documentation**: See [README.md](README.md) for usage examples

---

## ✨ What's Next?

Now that the skill is installed:

1. 📖 Read [EXAMPLES.md](EXAMPLES.md) for usage scenarios
2. 🚀 Try the [Quick Start](README.md#quick-start) examples
3. 📊 Generate your first portfolio piece!

---

**Installation complete! Ready to transform your projects into portfolio gold.** 🎯
