# Phase 3 — Environment Setup
### Upgrade your workspace so you can move faster.

---

**What you have coming in:**
- The loop working (describe → Claude writes → Arduino IDE → flash → see data)
- A spec document defining your project
- Arduino IDE already installed

**What you'll have by the end:**
- VS Code installed — a smarter place to read and edit your project files
- Terminal basics — you can navigate your project and run commands without being scared of it
- An optional but powerful next step: Claude Code, which turns Claude from a chat window into an agent that can work directly inside your project files

---

## Why This Phase Exists

Right now your loop has some friction. Every time Claude writes code, you copy it, open Arduino IDE, delete what's there, paste, and upload. That works fine — but it's slow, and it gets slower as your project grows.

This phase removes that friction. By the end, your tools talk to each other directly, and Claude can see and edit your files rather than just handing you text to paste.

---

## Step 1 — Install VS Code

> 🛠 **New tool: VS Code**
> A free text editor that understands code. It shows your whole project folder on the left, color-codes your files so they're easier to read, and connects with Claude Code later. This replaces the basic Notepad / TextEdit approach for anything project-related.
> **Download free at:** code.visualstudio.com
> **When you use it:** Whenever you're reading or editing project files.

**What to do:**

1. Go to **code.visualstudio.com** and download for your OS (Mac or Windows)
2. Install and open it
3. Go to **File → Open Folder** and open the folder where your project lives on your computer

You'll see your project files listed on the left side. Click any `.md` file — your spec doc, a phase guide — and it opens cleanly in the editor. That's your new home base for reading and managing project files.

**One useful extension to install:** Open the Extensions panel (the four-squares icon on the left sidebar, or Cmd+Shift+X on Mac / Ctrl+Shift+X on Windows). Search for **"Arduino"** and install the one by Microsoft. This lets you see and edit your Arduino firmware files from inside VS Code instead of switching back and forth.

---

## Step 2 — Get Comfortable in the Terminal

> 🛠 **New tool: Terminal (Mac) / PowerShell (Windows)**
> A window where you type commands directly to your computer. Looks old-fashioned, isn't hard. You use it to install things, navigate files, and later to run Claude Code.
> **How to open:**
> - **Mac:** Press Cmd+Space, type "Terminal", press Enter
> - **Windows:** Press the Windows key, type "PowerShell", press Enter
> **When you use it:** Installing tools, managing your project, running Claude Code.

The terminal feels intimidating because it has no buttons — just a blinking cursor. But it only does what you tell it. Nothing breaks unless you type something that breaks it, and Claude will always tell you exactly what to type.

**Learn the three commands you'll use 90% of the time:**

Open your terminal and try these one at a time. Each one is safe.

```
pwd
```
*"Print working directory" — shows you where you currently are in your file system. Like asking "where am I?"*

```
ls
```
*(Mac) Lists all the files and folders in your current location.*

```
dir
```
*(Windows) Same thing — lists files and folders.*

```
cd Documents
```
*"Change directory" — moves you into the Documents folder. Replace "Documents" with any folder name you can see in the list.*

```
cd ..
```
*Goes back up one level — like clicking the back button.*

**Your first win in the terminal:** Navigate to your project folder. Find where it lives on your computer (probably in Documents or on your Desktop), then use `cd` to get there. When you run `ls` or `dir` and see your project files listed, you're in.

If you get lost, type `cd ~` (Mac) or `cd %USERPROFILE%` (Windows) to go back to your home folder and start again.

---

## Step 3 — Connect Your Project to GitHub From the Terminal

Right now you're probably managing GitHub through the website. The terminal gives you a faster way. You only need to learn three git commands for now:

First, make sure git is installed. In your terminal:

```
git --version
```

If it prints a version number, you have it. If not:
- **Mac:** It will offer to install it automatically — say yes
- **Windows:** Download from **git-scm.com/download/win** and install

Then, from inside your project folder in the terminal:

```
git add .
git commit -m "describe what you changed"
git push
```

That's it. Those three commands save your work and push it to GitHub every time you want to back things up. You'll use them constantly. Ask Claude to explain what each one does if you want to understand them more deeply.

---

## Step 4 — Claude Code (When You're Ready to Level Up)

> 🛠 **New tool: Claude Code**
> A command-line version of Claude that lives inside your terminal and can directly read, write, and edit your project files. Instead of copying code from a chat window and pasting it somewhere, Claude Code works *inside* your project — it sees what you have, writes to the right files, and can run commands on your behalf.
> **When you use it:** When you're ready to move faster than copy-paste allows.

**One important thing to know before installing:** Claude Code uses the Anthropic API, which is separate from your Claude Pro subscription. It has its own usage-based billing — you pay for what you use, and it's generally affordable for light to moderate use, but it's an additional cost. For the work in this curriculum, charges will be small. Just know it's there.

**Installing Claude Code:**

First, install Node.js (Claude Code needs it to run):
- Go to **nodejs.org** and download the LTS version for your OS
- Install it, then restart your terminal

Then install Claude Code:

```
npm install -g @anthropic-ai/claude-code
```

Then set up your API key:
1. Go to **console.anthropic.com** and create an account
2. Go to **API Keys** and create a new key — copy it
3. In your terminal:

**Mac:**
```
export ANTHROPIC_API_KEY=your-key-here
```

**Windows (PowerShell):**
```
$env:ANTHROPIC_API_KEY="your-key-here"
```

To make it permanent so you don't have to set it every time, ask Claude how to add it to your shell profile (`.zshrc` on Mac or your PowerShell profile on Windows) — it'll walk you through it.

**Using Claude Code for the first time:**

Navigate to your project folder in the terminal and type:

```
claude
```

A prompt appears. Now instead of opening a browser tab and chatting, you talk to Claude from inside your project. It can see your files. Try:

> *"What files are in this project and what does each one do?"*

Claude Code will look at your folder and explain what it finds. That's the difference — it's not guessing, it's reading.

---

## Step 5 — Your First Win ✓

- ✅ VS Code is installed and your project folder is open in it
- ✅ You can navigate to your project folder in the terminal using `cd`
- ✅ You've run `git add . && git commit -m "phase 3 setup" && git push` and your changes are on GitHub
- ✅ (Optional) Claude Code is installed and you've had your first conversation with it inside your project

---

## What's Next

Phase 4 is back to hardware — but now with your own project in mind. You'll go beyond the BME280 and start adding sensors that match your spec document. The loop is the same, but now you're building *your* thing.

Open `04-phase-4-first-sensor.md` when you're ready.

---

> 💡 **Toolkit reminder:** Full tool descriptions for VS Code, Terminal, and Claude Code are in [`00-your-toolkit.md`](00-your-toolkit.md).
