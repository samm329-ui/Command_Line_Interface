# Git and GitHub: The Complete Beginner's Handbook

> **Who is this for?** Anyone who has never used Git or GitHub before. No coding background needed.
> You will go from zero to confidently collaborating on real projects by the end of this guide.

---

## Table of Contents

- [1.0 — Why Does Version Control Exist?](#10--why-does-version-control-exist)
- [2.0 — Installing Git](#20--installing-git)
- [3.0 — First-Time Setup](#30--first-time-setup)
- [4.0 — The Three Stages of Git](#40--the-three-stages-of-git)
- [5.0 — Basic Git Commands](#50--basic-git-commands)
- [6.0 — .gitignore and .gitkeep](#60--gitignore-and-gitkeep)
- [7.0 — Undoing Changes](#70--undoing-changes)
- [8.0 — Branches](#80--branches)
- [9.0 — Merging Branches](#90--merging-branches)
- [10.0 — Merge Conflicts](#100--merge-conflicts)
- [11.0 — What is GitHub?](#110--what-is-github)
- [12.0 — Creating a GitHub Account](#120--creating-a-github-account)
- [13.0 — Creating a Repository on GitHub](#130--creating-a-repository-on-github)
- [14.0 — HTTPS vs SSH](#140--https-vs-ssh)
- [15.0 — Pushing Code to GitHub](#150--pushing-code-to-github)
- [16.0 — git fetch — Safely Checking Remote Changes](#160--git-fetch--safely-checking-remote-changes)
- [17.0 — git pull — Downloading and Merging at Once](#170--git-pull--downloading-and-merging-at-once)
- [18.0 — Forking a Repository](#180--forking-a-repository)
- [19.0 — Cloning a Repository](#190--cloning-a-repository)
- [20.0 — Pull Requests](#200--pull-requests)
- [21.0 — Git Stash](#210--git-stash)
- [22.0 — Git Rebase](#220--git-rebase)
- [Appendix A — Full Command Cheat Sheet](#appendix-a--full-command-cheat-sheet)

---

## 1.0 — Why Does Version Control Exist?

### 1.1 — The Problem Every Developer Faces

Imagine you are writing a long essay for school. You start with a first draft, save the file, and work on it the next day. On day three, you realise the first draft was actually better than what you have now, but you already saved over it. It is gone. You cannot get it back. This exact same thing happens with code — except the consequences are far worse. A working application can break overnight because a developer saved changes on top of a version that actually worked.

Now multiply this problem by three people. Three developers are working on the same project, each on their own laptop. Developer A finishes some changes and emails the file to Developer B. Developer B makes their own changes and emails it back. Developer C did not get the memo and also changed the same file. Now there are three different versions of the same file floating around in inboxes, USB drives, and desktop folders — and nobody knows which one is correct.

This is what software development looked like before version control systems existed. It was painful, slow, and full of mistakes.

### 1.2 — All the Specific Problems (Without Git)

Let us look at each problem one by one so you understand exactly what Git is solving:

**Problem 1 — Lost Work**

A developer creates a file and writes some code. The next day, they make changes and save the file. The original version is gone forever. If the new code has a bug, there is no way to go back to the working version. The developer has to figure out from memory what the original code said.

**Problem 2 — Messy File Names**

To avoid losing work, developers start creating multiple copies of the same file:

```
app.txt
app_v2.txt
app_final.txt
app_final_REALLY_FINAL.txt
app_final_fixed_for_real_v3.txt
```

After a few weeks, there are dozens of files. Nobody knows which one is the latest. Nobody knows what changed between `app_v2.txt` and `app_v3.txt`. The folder becomes impossible to manage.

**Problem 3 — No History**

When a bug appears in the code, there is no record of who changed what and when. A developer cannot look back and say "three days ago, this line was changed from X to Y — that must be the bug." Debugging becomes a guessing game.

**Problem 4 — Collaboration is a Nightmare**

Developer A finishes some work and sends the file to Developer B via email or USB drive. Developer B makes their changes. Now Developer B has to manually compare their file with Developer A's file, line by line, to figure out what changed and what to keep. For a file with 1000 lines, this takes hours and is full of human errors.

**Problem 5 — Storage Waste**

Keeping twenty copies of the same file wastes enormous amounts of storage space. A project folder that should be 10 MB becomes 200 MB because of all the duplicate files.

**Problem 6 — No Backup**

If a developer's laptop crashes, gets stolen, or dies, every single line of code they wrote is gone. There is no backup. The project has to start from scratch.

### 1.3 — The Solution: Git

Git is a tool that solves every single problem listed above. It is installed on your computer and it watches a folder. Whenever you tell it to, Git takes a complete snapshot of every file in that folder and stores it permanently. You can have thousands of snapshots without wasting storage, because Git is extremely smart about only storing what actually changed.

```
┌─────────────────────────────────────────────────────────────────┐
│                        WITHOUT GIT                              │
├──────────────────┬──────────────────┬───────────────────────────┤
│  Developer A     │  Developer B     │  Developer C              │
│  app_v1.txt      │  app_nobita.txt  │  app_suneo.txt            │
│  app_v2.txt      │  app_new.txt     │  server.txt               │
│  app_final.txt   │  styles.txt      │  database.txt             │
│                  │  styles_new.txt  │                           │
│                  │                  │                           │
│  HOW DO THEY SHARE? Email / USB / WhatsApp                      │
│  HOW DO THEY MERGE? Manually, line by line                      │
│  WHAT IF LAPTOP DIES? Everything is lost                        │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│                         WITH GIT                                │
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│   Developer A    ──push──▶   GitHub (Cloud)   ◀──pull──  Dev B  │
│       │                           │                     │       │
│  (local copy)              (central copy)          (local copy) │
│                                   │                             │
│                                Dev C                            │
│                            (local copy)                         │
│                                                                  │
│  ✓ Every change is tracked        ✓ Easy to go back in time     │
│  ✓ Full history preserved         ✓ Collaboration is simple     │
│  ✓ No wasted storage              ✓ Automatic cloud backup      │
└─────────────────────────────────────────────────────────────────┘
```

### 1.4 — Git vs GitHub: They Are Not the Same Thing

This is the most common confusion for beginners, so let us clear it up right now.

**Git** is a program you install on your computer. It lives on your laptop and tracks changes to your files locally. It does not need the internet. It does not need any account. It is just software, like Microsoft Word, but for tracking code changes.

**GitHub** is a website — specifically `github.com`. It is a place on the internet where you can upload and store your Git projects. Think of it like Google Drive, but designed specifically for code. It adds features like sharing, collaboration, and online backup.

```
┌────────────────────────────────────────────────────────────────┐
│                                                                │
│   GIT                              GITHUB                      │
│   ────────────────                 ──────────────────────────  │
│   • Software on your computer      • Website (github.com)      │
│   • Works completely offline       • Needs internet            │
│   • No account needed              • Free account required     │
│   • Tracks changes locally         • Stores code in the cloud  │
│   • Like a diary on your desk      • Like a library anyone     │
│                                      can read (or just you)    │
│                                                                │
│   ANALOGY:                                                     │
│   Git   = Your personal notebook where you draft your work     │
│   GitHub = The library where you store published copies        │
│                                                                │
└────────────────────────────────────────────────────────────────┘
```

You can use Git without GitHub (everything stays on your laptop). But GitHub needs Git — it is built around the Git system. In this guide you will learn both, starting with Git.

---

## 2.0 — Installing Git

### 2.1 — Installing on Windows

Windows does not come with Git pre-installed. You need to download and install it manually. Here is the step-by-step process:

**Step 1** — Open your web browser and go to `https://git-scm.com`

**Step 2** — You will see a big download button. Click it. The website automatically detects that you are on Windows and downloads the correct installer file. The file will be named something like `Git-2.44.0-64-bit.exe`.

**Step 3** — Once the file downloads, find it in your Downloads folder and double-click it to run it.

**Step 4** — A setup wizard will open. Click **Next** on every single screen without changing anything. The default settings are carefully chosen and are perfect for beginners. Do not worry about what each option means — just keep clicking Next.

**Step 5** — On the final screen, click **Install**. Wait about 30 seconds for it to finish.

**Step 6** — Click **Finish**.

**What you now have:**

After installing, you will have a new program on your computer called **Git Bash**. This is a special black terminal window where you will type all your Git commands. To open it, click the Start Menu, type "Git Bash", and press Enter. You will see something like this:

```
┌─────────────────────────────────────────────────┐
│                   Git Bash                      │
│─────────────────────────────────────────────────│
│                                                 │
│  user@LAPTOP MINGW64 ~                          │
│  $                                              │
│                                                 │
│  (cursor blinks here — this is where you type)  │
│                                                 │
└─────────────────────────────────────────────────┘
```

This is your terminal. Every Git command in this guide will be typed here.

> **Important:** On Windows, always use **Git Bash** for your Git commands — not the regular Command Prompt or PowerShell. Some Git commands do not work correctly in those other terminals.

### 2.2 — Installing on macOS

Mac computers often come with Git already installed. Let us check first before downloading anything.

**Step 1** — Open the Terminal application. Press `Cmd + Space` to open Spotlight Search, type "Terminal", and press Enter.

**Step 2** — Type this command and press Enter:

```bash
git --version
```

**If you see output like this**, Git is already installed and you can skip ahead:

```
git version 2.39.3
```

**If Git is not installed**, your Mac will show a popup dialog asking you to install developer tools. Click **Install** and follow the prompts. This downloads and installs Git automatically. It may take a few minutes.

### 2.3 — Installing on Linux

On Linux, you install Git through your distribution's package manager. Open a terminal and run the appropriate command:

**Ubuntu or Debian:**
```bash
sudo apt update
sudo apt install git
```

**Fedora:**
```bash
sudo dnf install git
```

Type your password when prompted, wait for the installation to finish, and Git is ready.

### 2.4 — Verifying the Installation

No matter which operating system you use, you can confirm that Git installed correctly with one simple command. Open your terminal (Git Bash on Windows, Terminal on Mac/Linux) and type:

```bash
git --version
```

Press Enter. You should see something like:

```
git version 2.44.0
```

The exact version number does not matter — as long as you see a version number, Git is working correctly. If you see an error like "command not found", the installation did not work and you should try the installation steps again.

> **Note about the `$` symbol:** In many tutorials and guides, commands are shown with a dollar sign like `$ git --version`. The dollar sign is **not** part of the command. It is just a symbol that means "this is something you type in the terminal." Always ignore the `$` and only type what comes after it.

---

## 3.0 — First-Time Setup

### 3.1 — Why You Need to Introduce Yourself to Git

Before you start using Git, you need to tell it your name and email address. This is a one-time setup that you do once and never have to repeat on the same computer.

Why does Git need this information? Because every time you save a snapshot of your code (called a "commit"), Git permanently records three things along with the snapshot: what changed, when it changed, and **who** made the change. That last part — who — is your name and email.

This is extremely important when working in a team. If there are five developers on a project and a bug appears in the code, everyone needs to be able to look at the history and see exactly who changed which line on which day. Without this information, tracking down bugs would be impossible.

### 3.2 — Setting Your Name

Open your terminal (Git Bash on Windows, Terminal on Mac/Linux) and type this command. Replace the name in quotes with your actual name:

```bash
git config --global user.name "Your Name Here"
```

Press Enter. You will not see any output — that is completely normal. Silence means success in the terminal.

**Example:**
```bash
git config --global user.name "Arjun Sharma"
```

### 3.3 — Setting Your Email

Now set your email address. Use the same email that you will use when you create your GitHub account (we will do that later):

```bash
git config --global user.email "your.email@example.com"
```

**Example:**
```bash
git config --global user.email "arjun.sharma@gmail.com"
```

### 3.4 — What Does `--global` Mean?

The `--global` part of the command is a "flag" — a switch that modifies how the command works. When you write `--global`, you are telling Git: "Apply this setting to every single project on this computer." You only need to run these two commands once per computer. Every project you ever create on this machine will automatically use your name and email.

If you did not use `--global`, the setting would only apply to the one specific project folder you are currently inside. That is rarely what you want.

### 3.5 — Confirming Your Settings

To make sure everything was saved correctly, type:

```bash
git config --list
```

This displays all your Git settings. You should see your name and email in the list:

```
user.name=Arjun Sharma
user.email=arjun.sharma@gmail.com
```

If you see your name and email, you are all set and ready to start using Git.

### 3.6 — How This Connects to GitHub Later

Here is something important that most beginner guides do not mention: the email you set here must **exactly match** the email you use to create your GitHub account. 

When you push your code to GitHub later, GitHub looks at the email address attached to each commit and uses it to link that commit to your GitHub profile. This is how your name appears next to your work on GitHub. If the emails do not match, your commits will show up as "ghost commits" — they exist, but they are not connected to your GitHub profile and will not show up on your activity chart.

So when you create your GitHub account in Chapter 12, make sure to use the same email address you just used in this setup step.

---

## 4.0 — The Three Stages of Git

### 4.1 — The Most Important Concept in All of Git

Before you learn a single Git command, you must understand the three stages. This is the foundation that makes everything else make sense. If you skip this, every command will feel confusing and random. If you truly understand this, every command will feel logical and obvious.

Every file in your Git project exists in one of three places at any given moment:

```
┌─────────────────────────────────────────────────────────────────────┐
│                                                                     │
│   STAGE 1               STAGE 2               STAGE 3              │
│   ─────────────         ─────────────────      ──────────────────── │
│   Working               Staging                Repository           │
│   Directory             Area                   (.git folder)        │
│                                                                     │
│   Where you             Files waiting           Permanently saved   │
│   edit files            to be saved             snapshots           │
│                                                                     │
│   "The workshop"        "The packing area"      "The archive vault" │
│                                                                     │
│   ────── git add ──────▶             ──── git commit ──────▶        │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

### 4.2 — Stage 1: The Working Directory

The Working Directory is simply the folder on your computer where your project lives. When you open a file and start typing, those changes happen in the Working Directory. When you create a new file, it appears in the Working Directory.

Git can detect that files have changed or that new files exist, but it has not done anything with those changes yet. Think of it like a whiteboard — you can write things on it, erase things, rewrite things, and none of it is permanent. Someone could walk past and wipe the board clean, and everything would be gone.

**Real-world analogy:** You are a chef in a kitchen. The Working Directory is your kitchen counter. Ingredients are spread out, things are being chopped and prepared, it is a bit messy — but nothing has been plated and served yet.

**What Git shows you in this stage:**

If you run `git status` when a file is in the Working Directory but not yet staged, you will see:

```
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        app.txt
```

The word "Untracked" means: "Git can see this file exists, but I have not been asked to watch it or save it yet."

### 4.3 — Stage 2: The Staging Area

The Staging Area (also called the "Index") is a preparation zone. It is where you carefully select which changed files you want to include in your next snapshot. 

This stage exists because Git gives you very fine control over what you save. Imagine you changed five files today — fixed a bug in two of them, added a new feature in two others, and accidentally broke one. You might want to save the bug fixes as one snapshot and the new feature as a separate snapshot, without including the broken file at all. The Staging Area lets you do exactly that.

**Real-world analogy:** You are still in the kitchen. The Staging Area is the tray that you are loading with plates before they go out to the restaurant. You have carefully chosen exactly which dishes are ready to be served. The tray is packed and ready — but you have not sent it out yet.

You move files into the Staging Area using the `git add` command.

**What Git shows you in this stage:**

```
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   app.txt
```

The phrase "Changes to be committed" means: "These files are in the Staging Area and will be included in the next snapshot."

### 4.4 — Stage 3: The Repository

The Repository is where permanent snapshots live. It is stored inside a hidden folder called `.git` inside your project folder. When you run the `git commit` command, Git takes everything in the Staging Area, bundles it into a snapshot with your name, the current date, and a message you write, and stores it permanently in the Repository.

Once something is committed, it is saved forever. You can always come back to it. Even if you delete every file in your project, you can restore them from the Repository's history.

**Real-world analogy:** The tray has been sent out from the kitchen, the food has been served, and everything has been photographed and documented. The record of that meal now exists in the restaurant's permanent archive.

**What Git shows you after committing:**

```
[main a1b2c3d] Add app.txt with initial code
 1 file changed, 1 insertion(+)
```

### 4.5 — Visualising the Complete Flow

Here is a complete picture of how a file moves through all three stages:

```
┌──────────────────────────────────────────────────────────────────────┐
│                                                                      │
│  You create or          git add              git commit              │
│  edit a file            ─────────▶           ──────────▶            │
│                                                                      │
│  ┌───────────────┐   ┌──────────────────┐   ┌──────────────────┐    │
│  │               │   │                  │   │                  │    │
│  │   WORKING     │   │    STAGING       │   │   REPOSITORY     │    │
│  │   DIRECTORY   │   │    AREA          │   │   (.git)         │    │
│  │               │   │                  │   │                  │    │
│  │  app.txt  ✏  │──▶│  app.txt  ✓     │──▶│  Snapshot #1     │    │
│  │  notes.txt 📝 │   │                  │   │  Snapshot #2     │    │
│  │               │   │                  │   │  Snapshot #3     │    │
│  └───────────────┘   └──────────────────┘   └──────────────────┘    │
│                                                                      │
│  Status: Untracked    Status: Staged          Status: Committed      │
│  or Modified          (ready to save)         (permanent)            │
│                                                                      │
└──────────────────────────────────────────────────────────────────────┘
```

### 4.6 — The Golden Rule You Must Never Forget

You must always do `git add` **before** `git commit`. The Staging Area must have something in it, or the commit will do nothing. Trying to skip straight from editing a file to committing it will not work. The flow is always:

```
Edit file  →  git add  →  git commit
```

There are no shortcuts around this. It may seem like an extra step, but this design gives you tremendous power — you can choose exactly what goes into each snapshot, even if you changed dozens of files.

---

## 5.0 — Basic Git Commands

### 5.1 — `git init` — Start Tracking a Folder

This is the very first command you run on a new project. It tells Git: "Start watching this folder. I want to track changes here."

```bash
git init
```

**What happens when you run this:**

Git creates a hidden folder called `.git` inside your project folder. This is Git's database — it stores all the snapshots, history, and settings for your project. You will never need to open or edit the `.git` folder manually. Just know that it is there and that deleting it would erase all of Git's tracking data for that project.

**Step-by-step example:**

```bash
# Step 1: Create a project folder
mkdir my-first-project

# Step 2: Move into that folder
cd my-first-project

# Step 3: Initialize Git
git init
```

**Output:**
```
Initialized empty Git repository in /Users/you/my-first-project/.git/
```

You only run `git init` once per project. After that, Git is always watching the folder.

> **Important:** Run `git init` only inside the specific project folder you want to track. Do not run it in your home folder, Desktop, or any folder that contains many other folders — Git would try to track everything inside, which is almost never what you want.

### 5.2 — `git status` — See What Is Happening

`git status` is the command you will run more often than any other. It tells you the current state of your project: which files are new, which have been modified, which are staged and ready to commit, and which are completely unchanged.

```bash
git status
```

**What the different outputs mean:**

When there is nothing happening:
```
On branch main
nothing to commit, working tree clean
```
This means all your files match the last snapshot. No changes have been made.

When you create a new file:
```
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        hello.txt
```
This means hello.txt exists in your Working Directory but Git has never been asked to track it.

When you stage a file:
```
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   hello.txt
```
This means hello.txt is in the Staging Area, ready to be committed.

When you modify a file that was already committed:
```
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
        modified:   hello.txt
```
This means hello.txt was tracked before, you changed it, but you have not staged the new changes yet.

**Get in the habit of running `git status` constantly.** Run it before you add files. Run it after you add files. Run it before you commit. It always tells you exactly where you stand.

### 5.3 — `git add` — Move Files to the Staging Area

`git add` is how you move files from the Working Directory into the Staging Area, telling Git: "Include this file in the next snapshot."

**Add a single specific file:**
```bash
git add hello.txt
```

**Add multiple specific files at once:**
```bash
git add hello.txt goodbye.txt styles.txt
```

**Add ALL changed files in the current folder:**
```bash
git add .
```

The dot (`.`) means "everything in the current directory." This is a shortcut that stages all new and modified files at once. It is the most commonly used form.

**Step-by-step example:**

```bash
# You created a file called notes.txt
# Check status
git status
# Output: notes.txt is shown as untracked

# Stage the file
git add notes.txt

# Check status again
git status
# Output: notes.txt is now shown as "Changes to be committed"
```

### 5.4 — `git commit` — Permanently Save a Snapshot

`git commit` takes everything in the Staging Area and permanently saves it as a snapshot in the Repository. Every commit requires a message describing what you changed and why.

```bash
git commit -m "Your message describing what changed"
```

The `-m` flag lets you write the commit message directly in the command. Without `-m`, Git would open a text editor and ask you to type the message there (which is confusing for beginners).

**Good commit messages (what to aim for):**
```
git commit -m "Add login page to the website"
git commit -m "Fix calculation error in score counter"
git commit -m "Update homepage banner image"
git commit -m "Remove broken contact form"
```

**Bad commit messages (what to avoid):**
```
git commit -m "stuff"
git commit -m "fix"
git commit -m "asdf"
git commit -m "changes"
```

Write your messages as if you are finishing the sentence: "This commit will ___." A good message lets anyone looking at the history immediately understand what that snapshot contains, without reading the code.

**Complete first-time example:**

```bash
# Inside your project folder (git init already run)

# Create a file (use any text editor, save as readme.txt)
# File content: "My first project"

# Check what is new
git status

# Stage the file
git add readme.txt

# Commit with a message
git commit -m "Add readme file"
```

**Output:**
```
[main (root-commit) a1b2c3d] Add readme file
 1 file changed, 1 insertion(+)
 create mode 100644 readme.txt
```

This output tells you: the commit was made on the `main` branch, the commit ID starts with `a1b2c3d`, the message was "Add readme file", and one file was changed.

### 5.5 — `git log` — View the History

`git log` shows you a list of all commits that have been made in the current project, from newest to oldest.

```bash
git log
```

**Output looks like this:**
```
commit f3e2d1c8a9b4c5d6e7f8a9b0c1d2e3f4a5b6c7d8
Author: Arjun Sharma <arjun@gmail.com>
Date:   Mon Jan 15 14:30:22 2024 +0530

    Add homepage

commit a1b2c3d4e5f6a7b8c9d0e1f2a3b4c5d6e7f8a9b0
Author: Arjun Sharma <arjun@gmail.com>
Date:   Mon Jan 15 12:00:00 2024 +0530

    Add readme file
```

Each block shows the commit ID (a long string of letters and numbers), the author's name and email, the date and time, and the commit message.

**To exit the log, press the `Q` key.**

**The compact one-line version (much easier to read):**

```bash
git log --oneline
```

**Output:**
```
f3e2d1c Add homepage
a1b2c3d Add readme file
```

This shows just the short commit ID and the message, one commit per line. Use this version most of the time.

### 5.6 — `git diff` — See Exactly What Changed

`git diff` shows you the actual line-by-line changes in your files — what was removed and what was added — for files that have been modified but not yet staged.

```bash
git diff
```

**How to read the output:**

Lines starting with `-` (minus sign, shown in red) were **removed**.
Lines starting with `+` (plus sign, shown in green) were **added**.

**Example:**

Say you had a file with one line: `Hello World`
Then you changed it to: `Hello Git`

Running `git diff` would show:
```
- Hello World
+ Hello Git
```

This is exactly how code review works — you can see every single change before saving it.

> **Note:** `git diff` only shows changes for files in the Working Directory that have NOT been staged yet. Once you run `git add`, those changes are moved to the Staging Area and `git diff` will no longer show them. To see changes that are already staged, use `git diff --staged`.

### 5.7 — The Complete Daily Workflow

Here is the full sequence of commands you will use every single working day:

```bash
# 1. Start by creating or editing your files in your text editor

# 2. See what changed
git status

# 3. Stage the files you want to include
git add .

# 4. Double-check what is about to be committed
git status

# 5. Save the snapshot with a clear message
git commit -m "Describe what you changed"

# 6. Verify the commit was saved
git log --oneline
```

---

## 6.0 — .gitignore and .gitkeep

### 6.1 — What is `.gitignore`?

Not every file in your project folder should be tracked by Git. Some files should be kept private (like passwords), some are too large, and some are auto-generated files that can be recreated at any time. The `.gitignore` file is how you tell Git which files and folders to completely ignore.

**Common things you would want to ignore:**

- Password files and API keys (if pushed to GitHub, anyone in the world can read them)
- Temporary files created by your code editor
- Log files that change constantly
- The `node_modules` folder (contains thousands of auto-downloaded files that can be recreated)
- Configuration files with personal settings

**Real danger of not using .gitignore:**

If a developer pushes a file containing their cloud service passwords to GitHub, and the repository is public, hackers scan GitHub constantly for exactly this kind of mistake. Within minutes, a bot could find those passwords and use them to break into the developer's account. This has happened to many real developers, sometimes costing thousands of dollars in damage. `.gitignore` prevents this entirely by ensuring sensitive files never leave your computer.

### 6.2 — Creating a `.gitignore` File

The `.gitignore` file lives at the root of your project folder (the same folder where you ran `git init`). Its name starts with a dot, which makes it a hidden file.

**Step 1:** Create a file named exactly `.gitignore` (no other extension) in your project folder using your text editor.

**Step 2:** Add the names or patterns of files you want to ignore, one per line:

```
# This is a comment — lines starting with # are ignored

# Ignore a specific file
passwords.txt

# Ignore an entire folder
temp/

# Ignore all files with a specific extension
*.log

# Ignore a config folder
config/

# Ignore files starting with a certain word
secret*
```

**Step 3:** Stage and commit the `.gitignore` file itself:

```bash
git add .gitignore
git commit -m "Add gitignore file"
```

From this point on, any file listed in `.gitignore` will be completely invisible to Git. Running `git status` will not show those files, and `git add .` will not include them.

**Common patterns in `.gitignore`:**

```
┌───────────────────────────────────────────────┐
│  Pattern          │  What It Ignores           │
├───────────────────┼────────────────────────────┤
│  filename.txt     │  That exact file           │
│  folder/          │  Entire folder             │
│  *.log            │  All .log files            │
│  temp*            │  Files starting with temp  │
│  **/*.secret      │  .secret files anywhere    │
│  !important.log   │  Exception: keep this one  │
└───────────────────────────────────────────────┘
```

### 6.3 — What is `.gitkeep`?

Git has one quirk: **it does not track empty folders**. If you create an empty folder in your project, Git acts as if it does not exist. It will not show up in `git status`, and it will not be included in any commit.

**Why this is a problem:**

Imagine you are setting up a project structure and you create an `uploads/` folder where files will be saved later (by users of your application). The folder is empty right now, but you want it to exist in the repository so that other developers — or a server — also have that folder when they clone the project. Without any file inside it, Git will not track it, and it will not be included when other people download the project.

**The solution:**

Create an empty file named `.gitkeep` inside the empty folder. This file has no content and no special meaning to Git — it is just a placeholder. Its presence forces Git to include the folder in the repository.

```bash
# Create the empty folder
mkdir uploads

# Create the placeholder file inside it
touch uploads/.gitkeep

# Now Git can track the folder
git add uploads/.gitkeep
git commit -m "Add uploads directory"
```

> **Note:** `.gitkeep` is not a built-in Git feature. It is just a convention — an agreement among developers about what to call this kind of placeholder file. You could technically name it anything, but `.gitkeep` is universally recognised and tells every developer who sees it: "This file is here only to keep the folder in the repository."

---

## 7.0 — Undoing Changes

### 7.1 — The Power of Git's History

One of Git's greatest features is the ability to undo mistakes. The key is knowing where your changes currently are — in the Working Directory, the Staging Area, or the Repository — because the command to undo changes is different for each location.

```
┌─────────────────────────────────────────────────────────────────────┐
│                                                                     │
│  Working Directory   Staging Area        Repository                 │
│  ─────────────────   ──────────────      ─────────────────────────  │
│                                                                     │
│  git restore         git restore          git reset                 │
│  filename.txt        --staged             (3 modes)                 │
│                      filename.txt                                   │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

### 7.2 — Unstaging a File (Staging Area → Working Directory)

You accidentally staged a file you did not mean to include in the next commit. `git restore --staged` moves it back out of the Staging Area into the Working Directory, where it just sits without being tracked for the next commit.

```bash
# Unstage a single file
git restore --staged wrong-file.txt

# Unstage all staged files at once
git restore --staged .
```

The file still exists and your changes are still there — the file has just been moved back to the "untracked" state. Your work is not lost.

### 7.3 — Discarding Changes in the Working Directory

You made changes to a file, but you changed your mind completely and want to throw away those changes and return the file to exactly how it was when you last committed it.

```bash
# Discard changes in one file
git restore filename.txt

# Discard ALL changes in all modified files
git restore .
```

> ⚠️ **Critical Warning:** `git restore` on a Working Directory file is **permanent**. Your unsaved changes are deleted and cannot be recovered. There is no "undo" for this command. Use it only when you are absolutely certain you do not want those changes.

### 7.4 — Undoing a Commit: Git Reset (Three Modes)

`git reset` undoes one or more commits from the Repository. There are three ways to use it, each with different behavior about what happens to the files that were in those commits.

```
┌──────────────────────────────────────────────────────────────────────┐
│                                                                      │
│  BEFORE RESET:                                                       │
│                                                                      │
│  Repository: [Commit 1] → [Commit 2] → [Commit 3]  ← HEAD           │
│                                                                      │
│  AFTER "git reset HEAD~1" (undo the last commit):                    │
│                                                                      │
│  Repository: [Commit 1] → [Commit 2]  ← HEAD                        │
│                                                                      │
│  But where did Commit 3's FILES go? That depends on the mode.        │
│                                                                      │
└──────────────────────────────────────────────────────────────────────┘
```

**`HEAD~1`** means "one commit before the current position." HEAD is just a pointer that says "you are here."

**Mode 1 — Soft Reset: Keep files staged**

```bash
git reset --soft HEAD~1
```

What happens: The last commit is removed from the Repository. The files from that commit are moved back to the **Staging Area**. Your work is preserved and ready to be committed again (perhaps with a better message or after more changes).

Use this when: You committed too early, you made a typo in the commit message, or you want to add more changes before making the commit final.

**Mode 2 — Mixed Reset (the default): Keep files unstaged**

```bash
git reset HEAD~1
```

What happens: The last commit is removed from the Repository. The files from that commit are moved back to the **Working Directory** (unstaged). Your work is preserved, but you will need to `git add` them again if you want to commit them.

Use this when: You want to completely re-examine your changes before staging and committing them again.

**Mode 3 — Hard Reset: Delete everything**

```bash
git reset --hard HEAD~1
```

What happens: The last commit is removed from the Repository. The files are **deleted entirely** — from both the Staging Area and the Working Directory. It is as if that commit never happened and the files never existed.

> ⚠️ **Danger:** `git reset --hard` is permanent and irreversible. The deleted changes cannot be recovered. Only use this when you are absolutely sure you want to erase all trace of those changes.

**Visual comparison of the three modes:**

```
┌────────────────────────────────────────────────────────────────────┐
│                  git reset HEAD~1 (undo last commit)               │
├────────────────┬─────────────────┬───────────────────────────────  │
│  --soft        │  (no flag)      │  --hard                         │
│                │  mixed          │                                  │
├────────────────┼─────────────────┼──────────────────────────────── │
│  Files go to   │  Files go to    │  Files are                      │
│  Staging Area  │  Working Dir    │  permanently deleted            │
│  (still staged)│  (unstaged)     │  (gone forever)                 │
│                │                 │                                  │
│  Your work is  │  Your work is   │  Your work is LOST              │
│  preserved ✓   │  preserved ✓    │  forever ✗                      │
└────────────────┴─────────────────┴─────────────────────────────────┘
```

### 7.5 — `git revert` — The Safe Way to Undo a Published Commit

`git reset` rewrites history, which is a problem if the commits you are resetting have already been pushed to GitHub and shared with your team. If you reset and push, you will create chaos for everyone who has already downloaded those commits.

`git revert` is the safe alternative. Instead of deleting a commit, it creates a brand new commit that does the opposite of the target commit. The original commit stays in the history — `git revert` just adds a new commit on top that cancels it out.

```bash
# First, find the commit ID you want to undo
git log --oneline

a1b2c3d Fix homepage title     ← you want to undo this one
9e8f7g6 Add login page
5h4i3j2 Initial commit

# Revert the specific commit
git revert a1b2c3d
```

Git will create a new commit with a message like "Revert 'Fix homepage title'". The history now looks like:

```
5h4i3j2  Initial commit
9e8f7g6  Add login page
a1b2c3d  Fix homepage title
x9y8z7w  Revert "Fix homepage title"   ← new commit that undoes a1b2c3d
```

This approach is safe for team collaboration because history is never rewritten — it only grows forward.

**When to use which:**

```
┌──────────────────────────────────────────────────────────────────┐
│  Use git reset when:          Use git revert when:               │
│  ─────────────────────        ────────────────────────           │
│  • Commits are only on        • Commits are on GitHub            │
│    your local computer        • Others have already pulled       │
│  • You have not pushed        • You want to preserve history     │
│    to GitHub yet              • Working in a team                │
└──────────────────────────────────────────────────────────────────┘
```

---

## 8.0 — Branches

### 8.1 — What is a Branch?

A branch is a parallel, independent copy of your project where you can work without affecting the main code.

Here is the situation that makes branches absolutely essential: Your main code is working perfectly. Users are using it. A developer wants to build a new feature. While building that feature, the code will be half-finished, broken, and not ready for users. If the developer works directly on the main code, the application will be broken for users while the feature is being built.

The solution is to create a branch. A branch is like a separate timeline for your project. You diverge from the main timeline, work freely, make mistakes, experiment — and when you are done and everything works, you merge your branch back into the main timeline. The main code stayed intact the whole time.

```
┌──────────────────────────────────────────────────────────────────────┐
│                                                                      │
│  Without branches:                                                   │
│  main: A ─── B ─── (broken) ─── (still broken) ─── C               │
│              ↑                                                       │
│         Feature work on main = users see broken code                │
│                                                                      │
│  With branches:                                                      │
│  main:    A ─── B ───────────────────── C ─── D   (always working)  │
│                  \                     /                             │
│  feature:         E ─── F ─── G ─── H             (work freely here)│
│                                                                      │
│  The main branch stays clean while feature work happens separately. │
│                                                                      │
└──────────────────────────────────────────────────────────────────────┘
```

### 8.2 — What is the `main` Branch?

When you first run `git commit` in a project, Git automatically creates a branch called `main` (older projects may call it `master`). This is the default branch — the primary timeline of your project where the stable, working code lives.

You can verify which branch you are on at any time:

```bash
git branch
```

Output:
```
* main
```

The `*` (asterisk) points to the branch you are currently on. Right now, there is only one branch: main.

### 8.3 — When Does a Branch Actually Get Created?

This is a detail many tutorials skip: **a branch is not actually created until you make your first commit.** You can run `git init` and even `git add` files, but until you make at least one commit, there is technically no branch. The moment you run your first `git commit`, the `main` branch is born.

### 8.4 — Creating a New Branch

```bash
# Create a branch (you stay on your current branch)
git branch feature-login

# Create a branch AND immediately switch to it (most common)
git checkout -b feature-login
```

The second command (`checkout -b`) is what you will use in real work. It creates the new branch and immediately moves you into it.

**What happens when you create a branch:**

The new branch starts as an exact copy of wherever you are in the current branch. If you are on `main` and `main` has three commits, the new branch will also have those three exact commits. They are identical at the moment of branching. From that point on, each branch grows independently.

```
At the moment of branching:
┌────────────────────────────────────────────────┐
│                                                │
│  main:          A ─── B ─── C                  │
│                              ↑                 │
│                       (you are here)           │
│                                                │
│  After: git checkout -b feature-login          │
│                                                │
│  main:          A ─── B ─── C                  │
│                              \                 │
│  feature-login:               (here, same C)   │
│                                                │
│  Both branches are identical. No difference    │
│  yet. The divergence happens as you commit     │
│  on the new branch.                            │
│                                                │
└────────────────────────────────────────────────┘
```

### 8.5 — Switching Between Branches

```bash
# Switch to an existing branch
git checkout main

# Switch using newer syntax
git switch main
```

**What happens when you switch branches:**

This feels like magic when you first experience it. When you are on `feature-login` and you switch back to `main`, files that you created on `feature-login` will literally disappear from your folder. When you switch back to `feature-login`, they reappear. Git is swapping out files as you switch branches, showing you exactly the state of each branch.

**Step-by-step demonstration:**

```bash
# You are on main — one file exists: app.txt

git checkout -b feature-login
# Create a new file in this branch
# (use text editor to create login.txt)

git add login.txt
git commit -m "Add login page"

# Now switch back to main
git checkout main

# login.txt has disappeared from your folder!
# That file only exists on the feature-login branch.

git checkout feature-login
# login.txt is back!
```

This is not magic — Git is carefully restoring the exact file state of whichever branch you switch to.

### 8.6 — Listing All Branches

```bash
# See all local branches
git branch

# Output:
  main
* feature-login   ← the * shows you are on this one
```

### 8.7 — Deleting a Branch

Once you have merged a branch into `main` and you no longer need it, you can delete it to keep things clean:

```bash
# Delete a fully merged branch (safe)
git branch -d feature-login

# Force delete even if not merged (use with care)
git branch -D feature-login
```

**Why can you not delete a branch you are currently on?**

You cannot delete a branch while you are standing on it — that would be like pulling the floor out from under your feet. Switch to a different branch first, then delete.

```bash
git checkout main    # move away from the branch first
git branch -d feature-login   # now you can delete it
```

**Why might deletion fail?**

If you try `git branch -d feature-login` and the branch has commits that have not been merged into `main`, Git will refuse to delete it with an error like "not fully merged." This safety feature prevents you from accidentally losing work. You either merge the branch first, or use `-D` (capital D) to force delete it (which will permanently discard those unmerged commits).

### 8.8 — Which Branch Gets Cloned?

When you create a new branch from an existing one, the new branch inherits **all the commits and files** from the parent branch at the exact moment of creation. This is important to remember:

- Branch created from `main` at Commit 3: starts with commits 1, 2, 3
- Branch created from `feature-login` after Commit 5: starts with all commits from `feature-login` including commit 5

The new branch is always an exact copy of its parent at the time of branching.

---

## 9.0 — Merging Branches

### 9.1 — What is Merging?

When you finish working on a branch and everything looks good, you want to bring those changes back into the main branch. This process is called **merging**. Git combines the work from two branches into one.

There are four types of merges. Each one works differently and is appropriate for different situations. Understanding all four will make you a significantly better developer than the vast majority of people who only know one.

### 9.2 — Setup: Create the Practice Project First

Before learning each merge type, create this practice project so you can follow along:

```bash
# Create the project folder
mkdir git-merge-demo
cd git-merge-demo
git init

# Create the first file and make the initial commit
echo "Initial Code" > app.txt
git add .
git commit -m "initial commit"
```

> **What `echo "text" > file.txt` does:** This is a terminal command that creates a file named `file.txt` with the text "text" inside it. It is a quick way to create files without opening a text editor.

### 9.3 — Avoiding the Vim Editor During Merges

During some merges (specifically three-way merges), Git will open a program called Vim to ask you for a commit message. Vim is a text editor that runs inside the terminal, and it is notoriously confusing for beginners. To avoid it, always add `-m "your message"` directly to your merge command:

```bash
git merge branch-name -m "your merge message here"
```

If Vim does open unexpectedly, you can exit it by pressing `ESC`, then typing `:wq`, then pressing `Enter`. This saves and exits. If you want to exit without saving, press `ESC`, type `:q!`, and press `Enter`.

### 9.4 — Type 1: Fast-Forward Merge

A fast-forward merge is the simplest type. It happens when the branch you are merging into (`main`) has not had any new commits since the feature branch was created. In this case, there is no "combining" to do — Git simply moves the main branch pointer forward to point to the latest commit on the feature branch.

**When does this happen?**

You create a feature branch. You make some commits on it. Meanwhile, nobody makes any commits to `main`. When you merge, Git sees that `main` is directly behind the feature branch in a straight line and simply slides `main` forward. No new merge commit is created.

```
Before merge:
main:      A
            \
feature:    B --- C

After fast-forward merge:
main:      A --- B --- C
            (main now points to C, same as feature)
```

**Step-by-step implementation:**

```bash
# Step 1: Create and switch to feature branch
git switch -c feature

# Step 2: Create a new file and commit
echo "Feature Code" > feature.txt
git add .
git commit -m "added feature file"

# Step 3: Switch back to main
git switch main

# Step 4: Merge — no -m needed here (fast-forward creates no commit message)
git merge feature
```

**Output:**
```
Updating a1b2c3d..f4e5d6c
Fast-forward
 feature.txt | 1 +
 1 file changed, 1 insertion(+)
```

The word `Fast-forward` in the output confirms this type of merge happened.

```bash
# Verify with the visual graph
git log --oneline --graph --all

# Output:
* f4e5d6c (HEAD -> main, feature) added feature file
* a1b2c3d initial commit
```

Notice that both `main` and `feature` now point to the same commit `f4e5d6c` — they are identical.

### 9.5 — Type 2: Three-Way Merge

A three-way merge happens when both the main branch AND the feature branch have received new commits after the branch was created. They have "diverged" — they are no longer on a straight line. Git cannot just slide a pointer forward; it has to actually combine two different histories. To do this, it creates a special new commit called a **merge commit**.

The name "three-way" comes from the fact that Git looks at three specific snapshots: the latest commit on `main`, the latest commit on the feature branch, and the "common ancestor" — the last commit they both shared before they diverged.

```
Before three-way merge:
main:          A --- B --- C
                        \
login-feature:            D

After three-way merge:
main:          A --- B --- C --- M   (M = merge commit, has two parents: C and D)
                        \       /
login-feature:            D ---
```

**Step-by-step implementation:**

```bash
# Step 1: Create login-feature branch
git switch -c login-feature

# Step 2: Add a file on the feature branch
echo "Login Feature" > login.txt
git add .
git commit -m "added login"

# Step 3: Switch back to main and add a DIFFERENT file (this is what causes the divergence)
git switch main
echo "Main Update" > main.txt
git add .
git commit -m "main updated"

# Step 4: Merge with -m to avoid Vim editor
git merge login-feature -m "three way merge completed"
```

**Output:**
```
Merge made by the 'ort' strategy.
 login.txt | 1 +
 1 file changed, 1 insertion(+)
```

The phrase "Merge made by the 'ort' strategy" confirms a three-way merge happened and a new merge commit was created.

```bash
# See the branching graph
git log --oneline --graph --all

# Output:
*   e7f8a9b (HEAD -> main) three way merge completed
|\
| * c3d4e5f (login-feature) added login
* | b2c3d4e main updated
|/
* a1b2c3d initial commit
```

The `|\` and `|/` lines in the graph show where the branches split and joined.

### 9.6 — Type 3: Squash Merge

Squash merge is not a completely different kind of merge — it is a mode you add to either a fast-forward or three-way merge. When you squash, all the individual commits from the feature branch are "squashed" (compressed) into a single new commit on the main branch. The feature branch's individual commit history does not appear in main's history.

**When should you use squash?**

When you are building a feature, you might make many small, messy commits like "fix typo", "undo previous change", "try a different approach", "oops another fix". These intermediate commits are useful during development but clutter the main branch's history. Squash merging lets you put all that work into one clean, well-described commit.

```
Feature branch before squash:
ui-feature:    A --- (navbar) --- (footer) --- (sidebar)

After squash merge onto main:
main:          A --- B --- "UI Feature Complete"
                            ↑
                   All 3 commits combined into this one
                   (navbar, footer, sidebar commits disappear from main)
```

**Step-by-step implementation:**

```bash
# Step 1: Create ui-feature branch
git switch -c ui-feature

# Step 2: Make multiple commits
echo "Navbar" > navbar.txt
git add . && git commit -m "navbar added"

echo "Footer" > footer.txt
git add . && git commit -m "footer added"

echo "Sidebar" > sidebar.txt
git add . && git commit -m "sidebar added"

# Step 3: Switch to main
git switch main

# Step 4: Squash merge
git merge --squash ui-feature
```

**Output:**
```
Squash commit -- not updating HEAD
Automatic merge went well; stopped before committing as requested
```

Notice that `--squash` stages all the changes but does NOT create a commit automatically. You must run `git commit` yourself:

```bash
# Step 5: Commit manually with ONE clean message
git commit -m "UI Feature Complete"
```

```bash
# Verify: the 3 individual commits do NOT appear in main's history
git log --oneline --graph --all

# Output:
* d1e2f3a (HEAD -> main) UI Feature Complete
* a1b2c3d initial commit
```

The navbar, footer, and sidebar commits are nowhere to be found in main's history. Only the single clean commit appears. (If you switch to ui-feature and check the log there, you would still see all three — they exist on that branch, just not in main.)

### 9.7 — Type 4: Octopus Merge

An octopus merge lets you merge more than two branches into one branch at the same time, in a single command. Git creates one merge commit that has multiple parents — one for each branch that was merged.

**When to use it:**

When you have several independent feature branches that do not conflict with each other, and you want to integrate them all into main at once rather than merging them one by one.

```
Before octopus merge:
feature-a:   A --- X
feature-b:   A --- Y
feature-c:   A --- Z

After octopus merge onto main:
             X
            / \
main:   A --+   M   (one merge commit with 3 parents: X, Y, Z)
            |\ /
             Y|
              Z
```

**Step-by-step implementation:**

```bash
# Create feature-a
git switch -c feature-a
echo "A Feature" > a.txt
git add . && git commit -m "feature a"

# Create feature-b (from main)
git switch main
git switch -c feature-b
echo "B Feature" > b.txt
git add . && git commit -m "feature b"

# Create feature-c (from main)
git switch main
git switch -c feature-c
echo "C Feature" > c.txt
git add . && git commit -m "feature c"

# Switch to main and merge ALL THREE at once
git switch main
git merge feature-a feature-b feature-c -m "octopus merge all features"
```

**Output:**
```
Trying simple merge with feature-a
Trying simple merge with feature-b
Trying simple merge with feature-c
Merge made by the 'octopus' strategy.
```

> **Limitation:** Octopus merge only works when there are no conflicts between the branches. If any two branches edited the same line in the same file, the merge will fail and you will need to merge them one at a time and resolve conflicts.

### 9.8 — Summary Comparison Table

```
┌────────────────┬──────────────────┬────────────────────┬────────────────────────────┐
│  Merge Type    │  Merge Commit?   │  When to Use       │  Command                   │
├────────────────┼──────────────────┼────────────────────┼────────────────────────────┤
│  Fast Forward  │  No              │  Feature only,     │  git merge feature         │
│                │                  │  main untouched    │                            │
├────────────────┼──────────────────┼────────────────────┼────────────────────────────┤
│  Three-Way     │  Yes             │  Both branches     │  git merge feature         │
│                │                  │  have new commits  │    -m "message"            │
├────────────────┼──────────────────┼────────────────────┼────────────────────────────┤
│  Squash        │  One clean       │  Hide messy        │  git merge --squash        │
│                │  commit          │  commit history    │  feature                   │
│                │  (you write it)  │                    │  then: git commit -m "msg" │
├────────────────┼──────────────────┼────────────────────┼────────────────────────────┤
│  Octopus       │  Yes             │  Merge 3+          │  git merge a b c           │
│                │  (multi-parent)  │  independent       │    -m "message"            │
│                │                  │  branches at once  │                            │
└────────────────┴──────────────────┴────────────────────┴────────────────────────────┘
```

---

## 10.0 — Merge Conflicts

### 10.1 — What is a Merge Conflict?

A merge conflict happens when two branches have both changed the **same line** in the **same file**, and Git does not know which version to keep. Git stops the merge, marks the conflicting sections in the file, and asks you to make the decision manually.

This is not a bug or an error — it is Git doing exactly the right thing. Git is saying: "I found two contradictory instructions for the same part of this file. I cannot decide for you. Please look at both versions and tell me what the final result should be."

### 10.2 — When Do Conflicts Happen?

Conflicts happen during a **three-way merge** (or any merge where both branches have new commits). They do **not** happen during a fast-forward merge, because in a fast-forward, only one branch has new commits — there is nothing to conflict with.

**The specific condition for a conflict:**

- Developer A changes line 7 of `homepage.txt` to say "Welcome to our site"
- Developer B also changes line 7 of `homepage.txt` to say "Hello and welcome"
- Both changes are committed on separate branches
- When these branches are merged, Git sees two different instructions for line 7 and does not know which one you want

### 10.3 — Creating a Conflict (Step by Step)

```bash
# Start from a clean project with one commit
# app.txt contains: "Python"
echo "Python" > app.txt
git add . && git commit -m "initial: python"

# Create a feature branch and change app.txt
git checkout -b feature-scoring
# Edit app.txt: change "Python" to "React"
echo "React" > app.txt
git add . && git commit -m "set to React"

# Switch back to main and change app.txt too
git checkout main
# Edit app.txt: change "Python" to "Java"
echo "Java" > app.txt
git add . && git commit -m "set to Java"

# Attempt to merge — this will cause a conflict
git merge feature-scoring
```

**Output when a conflict occurs:**
```
Auto-merging app.txt
CONFLICT (content): Merge conflict in app.txt
Automatic merge failed; fix conflicts and then commit the result.
```

### 10.4 — Reading the Conflict Markers

Git has modified the conflicted file. Open it and you will see special markers that Git added:

```
<<<<<<< HEAD
Java
=======
React
>>>>>>> feature-scoring
```

Understanding each marker:

```
┌──────────────────────────────────────────────────────────────────┐
│                                                                  │
│  <<<<<<< HEAD          ← Start of YOUR version (current branch) │
│  Java                  ← What YOUR branch says this line is     │
│  =======               ← Separator between the two versions     │
│  React                 ← What the INCOMING branch says          │
│  >>>>>>> feature-scoring  ← End of INCOMING version             │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

"HEAD" always refers to your current branch (where you are). The branch name after `>>>>>>>` is the branch you are merging in.

### 10.5 — Resolving the Conflict

**Step 1:** Open the conflicted file in VS Code. You will see the conflict markers, and VS Code will add buttons above the conflict:

- **Accept Current Change** — keep your version, discard the incoming version
- **Accept Incoming Change** — discard your version, keep the incoming version
- **Accept Both Changes** — keep both lines (one after the other)

**Step 2:** Click whichever option represents your decision, or manually edit the file to the exact result you want.

For example, if you decide "React" is correct, click **Accept Incoming Change**. The file will now contain just:
```
React
```

All the conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`) will be removed. If you resolve manually (without the VS Code buttons), you must remove all conflict markers yourself. The file must contain only the final code — no `<<<<<<<` or `=======` lines.

**Step 3:** Stage the resolved file:
```bash
git add app.txt
```

**Step 4:** Complete the merge with a commit:
```bash
git commit -m "Resolve conflict: use React as language"
```

### 10.6 — Checking Which Files Have Conflicts

If the merge conflict involves many files, use `git status` to see all of them:

```bash
git status

# Output:
Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both modified:   app.txt
        both modified:   styles.txt
```

Every file listed under "Unmerged paths" has conflicts that need to be resolved.

### 10.7 — Abandoning a Merge

If you start a merge, see that there are dozens of conflicts, and decide you do not want to merge right now:

```bash
git merge --abort
```

This cancels the entire merge and restores your repository to exactly the state it was in before you ran `git merge`. No harm done.

---

## 11.0 — What is GitHub?

### 11.1 — Moving from Local to Cloud

So far, everything you have done with Git has been on your own computer. Your commits, your branches, your history — all of it lives only on your laptop. This is useful, but it has three major limitations:

1. If your laptop dies, everything is gone
2. If you want to collaborate with other developers, there is no central place to share code
3. If you want to show your work to the world (or to a potential employer), you have no way to do that

GitHub solves all three problems. It is a website that hosts Git repositories in the cloud. Think of it as a Google Drive for code — but much smarter, because it understands Git and provides collaboration tools built specifically for developers.

### 11.2 — Git vs GitHub: The Full Picture

```
┌────────────────────────────────────────────────────────────────────┐
│                                                                    │
│   GIT                              GITHUB                          │
│   ───────────────────              ────────────────────────        │
│   Software on your computer        Website: github.com            │
│   Works offline                    Needs internet                  │
│   No account required              Free account required           │
│   Tracks changes locally           Stores repos in the cloud       │
│   Created by Linus Torvalds        Owned by Microsoft              │
│   Exists since 2005                Launched in 2008                │
│                                                                    │
│   RELATIONSHIP:                                                    │
│   Git is the technology. GitHub uses that technology and adds      │
│   a website, a visual interface, and collaboration features.       │
│   You can use Git without GitHub. GitHub cannot exist without Git. │
│                                                                    │
└────────────────────────────────────────────────────────────────────┘
```

### 11.3 — Why Use GitHub?

**Reason 1 — Backup:** Your code is stored in the cloud. If your laptop catches fire tomorrow, you log into GitHub from any computer and everything is there.

**Reason 2 — Collaboration:** Multiple developers can work on the same project simultaneously. GitHub acts as the central hub where everyone's work meets. Developer A pushes their changes up. Developer B pulls those changes down. Everyone stays in sync.

**Reason 3 — Portfolio:** GitHub is essentially the portfolio of the software world. Employers and university admissions teams look at your GitHub profile to understand your abilities. A GitHub profile full of commits and projects says far more than a resume. Your GitHub shows what you actually built, how consistently you work, and how you collaborate with others.

**Reason 4 — Open Source:** GitHub is home to millions of open source projects. The software that powers the internet, from Linux to React to Python packages, lives on GitHub. Once you learn Git and GitHub, you can contribute to these projects, fix bugs, add features, and have your name attached to software used by millions.

### 11.4 — The Local-Remote Relationship

Two important vocabulary words you will use constantly:

**Local** = your laptop, your computer, wherever you are physically sitting

**Remote** = GitHub, the internet, the cloud copy of your repository

```
┌──────────────────────────────────────────────────────────────────────┐
│                                                                      │
│   Your Laptop (Local)         GitHub (Remote)                        │
│   ─────────────────────       ──────────────────────────────────     │
│   Local Repository            Remote Repository                      │
│   Local Branches              Remote Branches                        │
│   Local Commits               Remote Commits                         │
│                                                                      │
│   Syncing between them:                                              │
│                                                                      │
│   Laptop ──── git push ───▶ GitHub   (send your work up)            │
│   Laptop ◀─── git pull ──── GitHub   (bring others' work down)      │
│                                                                      │
└──────────────────────────────────────────────────────────────────────┘
```

---

## 12.0 — Creating a GitHub Account

### 12.1 — Step-by-Step Account Creation

**Step 1:** Open your web browser and go to `https://github.com`

**Step 2:** Click the **Sign up** button in the top right corner of the page.

**Step 3:** Enter your email address and click **Continue**.

**Step 4:** Create a strong password (minimum 8 characters, mix of letters, numbers, and symbols) and click **Continue**.

**Step 5:** Choose a username. This is your public identity on GitHub — it will appear in the URL of every repository you create: `github.com/your-username/your-project`. Choose carefully.

**Step 6:** Complete the puzzle verification (GitHub's version of a CAPTCHA) to confirm you are a human.

**Step 7:** Check your inbox for a verification email from GitHub. Open it and enter the 6-digit code on the GitHub website.

**Step 8:** Your account is ready.

### 12.2 — Choosing Your Username Wisely

Your GitHub username is visible to every employer, professor, and developer in the world. Treat it like a professional name.

**Good usernames:**
```
arjun-sharma
priyasingh-dev
rahulkumar
```

**Bad usernames:**
```
coolboyxxx99
xXdragonslayerXx
randomguy2003
```

You can always change your username later, but URLs of existing repositories may break if you do, so choose well from the start.

### 12.3 — Why Your git config Email Must Match GitHub

In Chapter 3, you set up your email in Git:

```bash
git config --global user.email "your.email@gmail.com"
```

This email **must be the same** as the email you used to create your GitHub account.

Here is why it matters: GitHub reads the email address attached to every commit you make and uses it to link that commit to your GitHub profile. This is how the green squares on your GitHub activity calendar (called the "contribution graph") get filled in. It is how your name appears next to commits when others browse your repository. It is how the world sees your work as yours.

If the emails do not match, your commits become "ghost commits" — they exist in the repository, but GitHub does not know they belong to you. They will not appear on your profile and will not count toward your contribution graph.

```
┌──────────────────────────────────────────────────────────────────────┐
│                                                                      │
│   git config email: arjun@gmail.com                                 │
│   GitHub account email: arjun@gmail.com    ← SAME = commits linked  │
│                                                                      │
│   git config email: arjun@gmail.com                                 │
│   GitHub account email: arjun@yahoo.com   ← DIFFERENT = ghost       │
│                                               commits, no credit     │
│                                                                      │
└──────────────────────────────────────────────────────────────────────┘
```

### 12.4 — Setting Up Your Profile

After creating your account:

1. Click your profile picture (top right corner) → **Settings**
2. Add your full name under **Public profile**
3. Write a short bio: "Computer Science student" or "Learning to code" is perfectly fine
4. Optionally upload a profile photo

A filled-out profile looks more professional and builds trust when other developers find your work.

---

## 13.0 — Creating a Repository on GitHub

### 13.1 — Creating a New Repository Online

**Step 1:** Log in to GitHub. Click the `+` button near the top right of the page (next to your profile picture).

**Step 2:** Select **New repository** from the dropdown menu.

**Step 3:** Fill in the form:

- **Repository name:** Use lowercase letters and hyphens, like `my-first-project` or `school-tracker`. No spaces.
- **Description (optional):** A one-sentence summary of what this project does.
- **Public or Private:** Public means anyone in the world can see the code. Private means only you (and people you explicitly invite) can see it. For learning and portfolio projects, use Public.
- **Do NOT check "Add a README file"** for now — we will add files from our own computer.

**Step 4:** Click **Create repository**.

Your repository is now live at `https://github.com/your-username/your-repo-name`.

### 13.2 — Understanding What GitHub Shows You Next

After creating the repository, GitHub shows you a page with instructions. It looks overwhelming but it is just showing you several ways to connect your local code to this new remote repository. You only need to follow one set of instructions. We will do the most common scenario: connecting an existing local project to this new remote.

### 13.3 — Connecting Your Local Repository to GitHub

You have a project on your laptop with some commits. Now you want that project to live on GitHub too.

**Step 1:** On the GitHub repository page, find the URL. Click the dropdown that says "HTTPS" and make sure "HTTPS" is selected (we will switch to SSH later). Copy the URL — it looks like: `https://github.com/your-username/your-repo.git`

**Step 2:** Open your terminal, navigate to your project folder, and add the GitHub URL as a "remote":

```bash
git remote add origin https://github.com/your-username/your-repo.git
```

Breaking this command down:
- `git remote add` — we are adding a remote connection
- `origin` — the nickname for this remote. Every developer uses "origin" as the standard nickname for the main remote. You could name it anything, but do not — use "origin".
- The URL — the address of the repository on GitHub

**Step 3:** Verify the remote was added:

```bash
git remote -v
```

**Output:**
```
origin  https://github.com/your-username/your-repo.git (fetch)
origin  https://github.com/your-username/your-repo.git (push)
```

You see two lines for origin: one for "fetch" (downloading) and one for "push" (uploading). They are the same URL — Git just lists them separately because they can theoretically be different.

**Step 4:** Push your code:

```bash
git push -u origin main
```

This uploads all your local commits to GitHub. The `-u` flag (meaning "set upstream") tells Git that from now on, when you type just `git push`, it should automatically push to `origin main` without you having to specify those words every time. You only need `-u` the first time.

**Step 5:** Refresh the GitHub repository page in your browser. Your files are now there.

### 13.4 — Removing a Remote Connection

If you need to change the remote URL or remove it:

```bash
# Remove the remote
git remote remove origin

# Verify it is gone
git remote -v
# (shows nothing)

# Add a new remote
git remote add origin https://github.com/new-url/repo.git
```

---

## 14.0 — HTTPS vs SSH

### 14.1 — The Problem with HTTPS

When you use the HTTPS URL to connect to GitHub, every single time you push code, GitHub asks you to prove who you are. It wants your username and a "Personal Access Token" (GitHub's version of a password for terminal use). This gets extremely repetitive. If you push code 15 times a day, that is 15 authentication prompts.

### 14.2 — How SSH Solves This

SSH (Secure Shell) uses a completely different approach. Instead of a password, it uses a pair of mathematically linked files called a "key pair":

- **Private key:** Stays on your computer. Never shared with anyone. Ever.
- **Public key:** You give this to GitHub. It is designed to be shared — it is useless without the private key.

```
┌──────────────────────────────────────────────────────────────────────┐
│                                                                      │
│   THE KEY PAIR ANALOGY:                                              │
│                                                                      │
│   Your Private Key = A unique physical key                          │
│   Your Public Key  = The lock that only your key opens              │
│                                                                      │
│   You give GitHub your lock (public key).                           │
│   You keep your key (private key) on your computer.                 │
│   Every time you connect to GitHub, your computer presents           │
│   the key to the lock. If they match, you are let in.               │
│   No password needed. No prompts. Instant and automatic.            │
│                                                                      │
│   Even if someone sees your lock (public key), they cannot          │
│   duplicate your key (private key). The math makes it              │
│   computationally impossible to reverse-engineer one from the other. │
│                                                                      │
└──────────────────────────────────────────────────────────────────────┘
```

### 14.3 — HTTPS vs SSH Comparison

```
┌────────────────────┬─────────────────────────────┬─────────────────────────────┐
│                    │  HTTPS                      │  SSH                        │
├────────────────────┼─────────────────────────────┼─────────────────────────────┤
│  URL looks like    │  https://github.com/...     │  git@github.com:user/...    │
├────────────────────┼─────────────────────────────┼─────────────────────────────┤
│  Authentication    │  Username + token           │  Key pair                   │
│                    │  EVERY push                 │  Set up once, never again   │
├────────────────────┼─────────────────────────────┼─────────────────────────────┤
│  Setup effort      │  Very easy, no setup        │  5 minutes once             │
├────────────────────┼─────────────────────────────┼─────────────────────────────┤
│  Daily use         │  Password prompts           │  No prompts ever            │
├────────────────────┼─────────────────────────────┼─────────────────────────────┤
│  Security          │  Good                       │  Better                     │
├────────────────────┼─────────────────────────────┼─────────────────────────────┤
│  Best for          │  Quick one-time use or      │  Daily development work     │
│                    │  someone else's computer    │  Any serious project        │
└────────────────────┴─────────────────────────────┴─────────────────────────────┘
```

### 14.4 — Generating Your SSH Key

**Step 1:** Open your terminal and run this command. Replace the email with your GitHub email:

```bash
ssh-keygen -t ed25519 -C "your.email@gmail.com"
```

**Step 2:** The terminal asks three questions. Press **Enter** for all three to accept the defaults:

```
Enter file in which to save the key: (press Enter)
Enter passphrase: (press Enter — leave blank)
Enter same passphrase again: (press Enter)
```

**Step 3:** You will see output like:

```
Your identification has been saved in /Users/you/.ssh/id_ed25519
Your public key has been saved in /Users/you/.ssh/id_ed25519.pub
```

Two files have been created in a hidden folder called `.ssh`:
- `id_ed25519` — your **private key** (never share this with anyone, ever)
- `id_ed25519.pub` — your **public key** (you will give this to GitHub)

### 14.5 — Adding the Key to the SSH Agent

The SSH agent is a background program that manages your keys so you do not have to re-provide them in every terminal session:

```bash
# Start the SSH agent
eval "$(ssh-agent -s)"

# Add your private key to the agent
ssh-add ~/.ssh/id_ed25519
```

Output:
```
Agent pid 12345
Identity added: /Users/you/.ssh/id_ed25519
```

### 14.6 — Copying Your Public Key

```bash
# On Mac or Linux:
cat ~/.ssh/id_ed25519.pub
```

This prints your public key to the screen. It looks like a long string of random characters. Select the entire output and copy it (Ctrl+C or Cmd+C).

On Windows (in Git Bash):
```bash
cat ~/.ssh/id_ed25519.pub | clip
```

This copies it directly to your clipboard.

### 14.7 — Adding the Public Key to GitHub

**Step 1:** Go to `https://github.com` and log in.

**Step 2:** Click your profile picture → **Settings**.

**Step 3:** In the left sidebar, click **SSH and GPG keys**.

**Step 4:** Click the green **New SSH key** button.

**Step 5:** Give it a title (like "My Laptop" or today's date so you know when it was created).

**Step 6:** Paste your public key into the **Key** field.

**Step 7:** Click **Add SSH key**. GitHub may ask for your password to confirm.

### 14.8 — Testing the SSH Connection

```bash
ssh -T git@github.com
```

If everything worked, you will see:

```
Hi your-username! You've successfully authenticated, but GitHub does not provide shell access.
```

Your GitHub username appearing in that message confirms the SSH connection is working perfectly. From now on, every `git push` and `git pull` will happen without any password prompts.

### 14.9 — Switching an Existing Repository from HTTPS to SSH

If you already added a remote with an HTTPS URL and want to switch to SSH:

```bash
# Check the current remote URL
git remote -v

# Change it to SSH
git remote set-url origin git@github.com:your-username/your-repo.git

# Verify the change
git remote -v
```

---

## 15.0 — Pushing Code to GitHub

### 15.1 — What Does "Push" Mean?

Pushing means uploading your local commits to the GitHub repository. After you commit on your laptop, the commits exist only on your laptop. Pushing sends them to GitHub so they are backed up in the cloud and visible to your collaborators.

```
Your Laptop                         GitHub
───────────────                     ──────────────
Commit 1   ┐
Commit 2   ├── git push ──────▶    Commit 1
Commit 3   ┘                       Commit 2
                                   Commit 3
```

### 15.2 — The Push Command

**First push (sets up the connection):**

```bash
git push -u origin main
```

This pushes the `main` branch to the remote named `origin`. The `-u` flag establishes a "tracking relationship" so that future pushes are simpler.

**Every push after the first:**

```bash
git push
```

Just two words. Because of the `-u` you used the first time, Git already knows where to send it.

**Pushing a specific branch:**

```bash
git push origin feature-login
```

This pushes the `feature-login` branch to GitHub. GitHub will create that branch remotely if it does not exist yet.

### 15.3 — The Complete Daily Workflow with GitHub

```bash
# Morning: start by downloading the latest code from GitHub
git pull

# Now work: create files, edit, write code...

# Check what you changed
git status

# Stage your changes
git add .

# Double check
git status

# Save a snapshot with a message
git commit -m "Add user profile page"

# Upload to GitHub
git push
```

This is the full cycle every professional developer repeats multiple times every day.

### 15.4 — What Happens After You Push?

After running `git push`, go to your GitHub repository page in your browser and refresh it. You will see your latest commit appear in the repository. You can browse every file, see every line of code, and click on any commit to see exactly what changed.

GitHub also shows a "contribution graph" on your profile — a grid of green squares where each square represents a day, and darker squares mean more commits were made that day. This graph is how employers and the community see your consistency and dedication as a developer.

---

## 16.0 — git fetch — Safely Checking Remote Changes

### 16.1 — What is git fetch?

`git fetch` downloads changes from GitHub to your computer but does **not** automatically merge those changes into your current branch. It brings the remote changes to your machine so you can inspect them first, then decide when and how to integrate them.

Think of it like receiving a package: `git fetch` is the delivery driver dropping the package at your door. The package is there, but you have not opened it yet or brought it inside.

### 16.2 — When to Use git fetch

Use `git fetch` when:
- You want to see what changed on GitHub before merging
- You are in the middle of your own work and do not want to suddenly merge remote changes
- You want to review a teammate's work before it enters your local code

### 16.3 — Using git fetch

```bash
# Fetch all changes from all remote branches
git fetch origin

# Fetch changes from one specific branch
git fetch origin main
```

After fetching, you can inspect what was downloaded:

```bash
# See commits on the remote that you do not have locally
git log HEAD..origin/main

# See them in compact form
git log HEAD..origin/main --oneline
```

**Output (example):**
```
c3d4e5f  Alice: Add search feature
a1b2c3d  Bob: Fix login bug
```

Now you can see exactly what changed remotely before merging.

### 16.4 — Merging After a Fetch

Once you have reviewed the changes and are ready to bring them into your local branch:

```bash
git merge origin/main -m "merge remote changes"
```

### 16.5 — Visualising git fetch vs git pull

```
┌──────────────────────────────────────────────────────────────────────┐
│                                                                      │
│   git fetch:                         git pull:                       │
│                                                                      │
│   GitHub ──────▶ your computer       GitHub ──────▶ your computer   │
│   (changes stored            )       (changes merged automatically)  │
│   (in origin/main, not merged)                                       │
│                                                                      │
│   You must manually run:                                             │
│   git merge origin/main                                              │
│   when you are ready.                                                │
│                                                                      │
│   git pull = git fetch + git merge (done automatically)              │
│                                                                      │
└──────────────────────────────────────────────────────────────────────┘
```

---

## 17.0 — git pull — Downloading and Merging at Once

### 17.1 — What is git pull?

`git pull` is a combination of two commands: `git fetch` (download) + `git merge` (integrate). It downloads all new commits from GitHub and immediately merges them into your current local branch — all in one step.

This is what you use at the start of every working day to make sure your local code is up to date with whatever your teammates pushed while you were away.

### 17.2 — Using git pull

```bash
# Pull changes from the main branch
git pull origin main

# Or just (if upstream is configured):
git pull
```

**Output when there is nothing new:**
```
Already up to date.
```

**Output when new commits were downloaded:**
```
remote: Enumerating objects: 5, done.
Updating a1b2c3d..f3e2d1c
Fast-forward
 newfile.txt | 1 +
 1 file changed, 1 insertion(+)
```

### 17.3 — The Golden Rule: Always Pull Before You Push

Before you start any work session, run `git pull`. Before you push your changes, run `git pull`. This keeps your local code synchronized with the remote and dramatically reduces the chances of merge conflicts.

If you and a teammate are both pushing to the same branch, and you push without pulling first, your push will be rejected with an error like "Updates were rejected because the remote contains work that you do not have locally." The fix is always: pull first, then push.

### 17.4 — git pull vs git fetch: When to Use Which

```
┌───────────────────────────────────────────────────────────────────┐
│                                                                   │
│   Use git pull when:              Use git fetch when:             │
│   ─────────────────               ─────────────────────           │
│   • Starting your work day        • You are in the middle of      │
│   • You trust the remote            your own work                 │
│     changes are ready             • You want to review changes    │
│   • Quick sync with the             before merging them           │
│     team is all you need          • You want maximum control      │
│                                     over when/how to merge        │
│                                                                   │
└───────────────────────────────────────────────────────────────────┘
```

---

## 18.0 — Forking a Repository

### 18.1 — What is a Fork?

A fork is your own personal copy of someone else's GitHub repository, stored under your GitHub account. When you fork a repository, GitHub creates an exact duplicate of it in your account. You have full ownership of your fork and can change anything in it without affecting the original.

Forking is how the entire open source software world works. Millions of developers fork public repositories, make improvements, and then propose those improvements back to the original project.

### 18.2 — Why Not Just Clone?

You might wonder: why can't you just clone the original repository, make changes, and push them directly?

The answer: **you cannot push to someone else's repository unless they have explicitly given you permission.** GitHub's security system prevents it. If you try to push to a repository you do not own, you will get a "Permission denied" error.

Forking solves this by creating a copy that **you** own. You can push to your fork freely. Then you use a "Pull Request" (covered next chapter) to politely ask the original repository owner to consider pulling your changes into their project.

```
┌──────────────────────────────────────────────────────────────────────┐
│                                                                      │
│   DIRECT CLONE (will fail for repositories you don't own):           │
│   Someone's GitHub repo ──clone──▶ Your laptop ──push──▶ REJECTED   │
│                                                                      │
│   FORK + CLONE (correct approach):                                   │
│                                                                      │
│   Someone's            Fork            Your fork           Your      │
│   GitHub repo ──────▶ button ──────▶  on GitHub ──clone──▶ laptop   │
│                                           │                  │       │
│                                           ◀────── push ──────┘       │
│                                           │                          │
│                    Pull Request back to original owner               │
│                                                                      │
└──────────────────────────────────────────────────────────────────────┘
```

### 18.3 — How to Fork a Repository

**Step 1:** Go to the repository you want to fork on GitHub (for example: `https://github.com/originalowner/project-name`).

**Step 2:** Click the **Fork** button in the top right corner of the page (next to the star button).

**Step 3:** GitHub shows a screen asking where to fork it. Your account should be selected. Optionally change the name. Click **Create fork**.

GitHub creates a copy at `https://github.com/your-username/project-name`. It looks identical to the original, but it is yours.

**Step 4:** On your fork's page, click the green **Code** button, select SSH (if you set up SSH) or HTTPS, and copy the URL.

**Step 5:** Clone your fork to your laptop:

```bash
git clone git@github.com:your-username/project-name.git
cd project-name
```

You now have a local copy of your fork.

### 18.4 — Keeping Your Fork Updated

The original repository keeps getting updated by its maintainer. Your fork does not automatically receive those updates. To stay up to date, add the original repository as a second remote called `upstream`:

```bash
# Add the original repository as "upstream"
git remote add upstream git@github.com:originalowner/project-name.git

# Verify your remotes
git remote -v
# origin    git@github.com:your-username/project-name.git (your fork)
# upstream  git@github.com:originalowner/project-name.git (the original)

# Download updates from the original
git fetch upstream

# Merge those updates into your local main
git checkout main
git merge upstream/main

# Push the updates to your fork on GitHub
git push origin main
```

Now your fork is in sync with the original.

---

## 19.0 — Cloning a Repository

### 19.1 — What is Cloning?

Cloning means downloading a complete copy of a repository from GitHub to your computer. Unlike `git pull` (which only downloads new changes to an existing local repository), `git clone` creates a brand new local repository from scratch, including every file, every branch, and the entire commit history.

You use `git clone` when:
- You just forked a repository and want a local copy to work in
- A colleague shared their repository link with you
- You want to explore or contribute to an open source project

### 19.2 — Cloning a Repository

```bash
# Clone using SSH (recommended if you have SSH set up)
git clone git@github.com:username/repository-name.git

# Clone using HTTPS (if you have not set up SSH yet)
git clone https://github.com/username/repository-name.git
```

**What happens:**

```
Before:  Empty folder on your laptop

After:   repository-name/
         ├── .git/          (Git's tracking data)
         ├── file1.txt
         ├── file2.txt
         └── folder/
             └── file3.txt
```

Git downloads the entire project including all its history.

**After cloning, move into the folder:**

```bash
cd repository-name
```

### 19.3 — What is Set Up After Cloning?

When you clone a repository, Git automatically:
- Creates the local folder with all the files
- Initializes a Git repository inside it (`git init` is done for you)
- Adds the source URL as the `origin` remote (you can verify with `git remote -v`)
- Checks out the main branch

You do not need to run `git init` or `git remote add origin` — cloning does all of that automatically.

---

## 20.0 — Pull Requests

### 20.1 — What is a Pull Request?

A Pull Request (often shortened to PR) is a formal proposal on GitHub asking the owner of a repository to review your changes and merge them into their codebase.

The name is a bit confusing: you are not "pulling" anything. The name comes from the idea that you are asking the repository owner to "pull" your changes into their project. In modern usage, some platforms call it a "Merge Request" which is more descriptive.

A Pull Request is not just about code. It creates a dedicated discussion space where:
- The owner can read through every line you changed
- They can leave comments on specific lines
- They can ask you to make adjustments
- The whole team can discuss the proposed change
- The change can be approved, modified, or rejected

This review process is one of the most important parts of professional software development. Almost no serious codebase accepts direct pushes to the main branch — everything goes through PR review.

### 20.2 — Creating a Pull Request: Step by Step

This assumes you have forked a repository, cloned it, made changes on a new branch, and pushed that branch to your fork.

**Step 1:** Push your feature branch to your fork:

```bash
# You have committed your changes on feature-login branch
git push origin feature-login
```

**Step 2:** Go to your fork on GitHub. You will see a yellow banner that says "feature-login had recent pushes" with a green **Compare & pull request** button. Click it.

If you do not see the banner, go to the **Pull requests** tab and click **New pull request**.

**Step 3:** Verify the settings:
- **base repository:** the original repository (where you want to send the changes)
- **base:** main (the branch in the original repo you want to merge into)
- **head repository:** your fork
- **compare:** feature-login (your branch with the changes)

**Step 4:** Write a clear title describing what your PR does:
```
Add login page with form validation
```

**Step 5:** Write a description explaining:
- What you changed and why
- How to test it
- Any relevant context

**Step 6:** Click **Create pull request**.

Your PR is now open. The repository owner will be notified.

### 20.3 — Reviewing and Merging a Pull Request (Repository Owner's View)

When a PR arrives, the repository owner:

**Step 1:** Goes to the **Pull requests** tab in their repository.

**Step 2:** Clicks on the PR to open it.

**Step 3:** Reads the description, then clicks **Files changed** to see every line that was added (green), removed (red), or unchanged (white).

**Step 4:** Optionally leaves comments on specific lines by hovering over a line number and clicking the `+` button.

**Step 5:** If changes are needed, clicks **Request changes** with feedback. If it looks good, clicks **Approve**.

**Step 6:** Once approved, clicks **Merge pull request** → **Confirm merge**.

The changes are now part of the original repository's main branch.

### 20.4 — After Your PR is Merged

Once your PR is merged, the changes live in the original repository. You should sync your fork:

```bash
# Update your local main with the newly merged code
git checkout main
git pull upstream main     # fetch from original repository
git push origin main       # push to your fork to keep it updated
```

---

## 21.0 — Git Stash

### 21.1 — The Problem That Stash Solves

Imagine you are in the middle of working on a new feature. Your files have changes, some are staged, it is a work in progress. Suddenly, an urgent bug is reported and you need to fix it on the main branch immediately.

You cannot switch branches while you have uncommitted changes — or if you do, your messy work-in-progress changes might come along with you and interfere. You also do not want to commit the half-finished feature, because it is not ready.

`git stash` solves this perfectly: it takes all your current uncommitted changes, tucks them away in a temporary storage space, and cleans your working directory completely. You switch branches, fix the bug, then come back and "pop" your stash to restore everything exactly as it was.

### 21.2 — Stashing Your Changes

```bash
# Save all current changes to the stash
git stash
```

**Output:**
```
Saved working directory and index state WIP on feature-login: a1b2c3d Add initial structure
```

After this, your working directory is completely clean — as if you had not made any changes since the last commit. You can now switch branches freely.

### 21.3 — Viewing Your Stashes

```bash
git stash list
```

**Output:**
```
stash@{0}: WIP on feature-login: a1b2c3d Add initial structure
stash@{1}: WIP on main: 9e8f7g6 Fix navbar
```

You can have multiple stashes. They are numbered from newest (0) to oldest.

### 21.4 — Restoring Stashed Changes

```bash
# Apply the most recent stash and KEEP it in the stash list
git stash apply

# Apply the most recent stash and REMOVE it from the stash list
git stash pop

# Apply a specific stash by number
git stash apply stash@{1}
```

The difference between `apply` and `pop`:
- `apply` restores your changes but keeps the stash saved (in case you want to apply it to another branch too)
- `pop` restores your changes and deletes the stash entry (the most common usage)

### 21.5 — Complete Stash Workflow

```bash
# You are working on a feature branch
# Files have changes but are not ready to commit

# Urgent bug reported! You need to fix main right now.
git stash    # save your work-in-progress

# Now your directory is clean
git checkout main

# Fix the urgent bug
# Edit bug-affected-file.txt
git add .
git commit -m "Fix critical login bug"
git push

# Bug is fixed. Now go back to your feature
git checkout feature-login

# Restore your stashed work
git stash pop

# Continue where you left off
```

### 21.6 — Cleaning Up Stashes

```bash
# Delete a specific stash
git stash drop stash@{0}

# Delete ALL stashes at once
git stash clear
```

---

## 22.0 — Git Rebase

### 22.1 — What is Rebasing?

Rebasing is an alternative to merging. Both operations bring two branches together, but they do it differently:

- **Merge** creates a merge commit and preserves the exact history of when each branch was worked on
- **Rebase** rewrites history to make it look like your feature branch was created from the latest commit on main, producing a clean, straight-line history with no merge commits

```
BEFORE REBASE:

main:           A --- B --- C
                         \
feature-login:            D --- E --- F

AFTER rebasing feature-login onto main:

main:           A --- B --- C
                             \
feature-login:                D' --- E' --- F'
                              (moved to after C)

The commits D, E, F are recreated (D', E', F') on top of C.
The original D, E, F are discarded.
```

### 22.2 — Why Use Rebase?

The result of rebasing is a perfectly linear commit history. When you eventually merge the rebased branch into main, it will be a clean fast-forward merge with no merge commit. The history looks like all the work happened in a single straight line, which makes it much easier to read and understand.

```
HISTORY WITHOUT REBASE (with merges):            HISTORY WITH REBASE:

*   Merge branch 'login-feature'                 * f3e2d1c Add form validation
|\                                               * c4d5e6f Add login page
| * c4d5e6f Add login page                       * b1c2d3e Main bug fix
| * d5e6f7a Add login form                       * a0b1c2d Initial commit
* | b1c2d3e Main bug fix
|/
* a0b1c2d Initial commit

Messy with diverging lines                       Clean, linear, easy to read
```

### 22.3 — How to Rebase

```bash
# You are on feature-login branch
git checkout feature-login

# Rebase your feature branch onto the latest main
git rebase main
```

**Output:**
```
Successfully rebased and updated refs/heads/feature-login.
```

If there are conflicts during rebase, Git will pause and ask you to resolve them (the same way as merge conflicts). After resolving, you run `git rebase --continue` to proceed. If you want to cancel the rebase and go back to the original state, run `git rebase --abort`.

### 22.4 — The Critical Warning About Rebase

> ⚠️ **Never rebase commits that you have already pushed to GitHub and that other people have pulled.**

Rebase rewrites history — it creates new commits with new IDs to replace the old ones. If someone else already has the old commits, and you push the rewritten commits, their repository will have both the old and new versions and everything will be confused.

```
┌──────────────────────────────────────────────────────────────────────┐
│                                                                      │
│   SAFE to rebase:         NOT safe to rebase:                       │
│   ─────────────────       ──────────────────────────────            │
│   Commits that exist      Commits already pushed to GitHub          │
│   only on your local      and pulled by teammates                   │
│   machine                                                           │
│                                                                      │
│   Golden rule: If in doubt, use merge instead of rebase.            │
│   Merge is always safe. Rebase is powerful but requires caution.    │
│                                                                      │
└──────────────────────────────────────────────────────────────────────┘
```

### 22.5 — Typical Rebase Workflow

```bash
# Make sure main is up to date
git checkout main
git pull

# Switch to your feature branch
git checkout feature-login

# Rebase: move your work on top of latest main
git rebase main

# If conflicts occur, resolve them, then:
git rebase --continue

# Once done, switch back to main and merge
git checkout main
git merge feature-login   # this will now be a clean fast-forward merge
git push
```

---

## Appendix A — Full Command Cheat Sheet

### A.1 — Setup and Configuration

```
┌─────────────────────────────────────────────────────────────────────┐
│  COMMAND                              │  WHAT IT DOES               │
├───────────────────────────────────────┼─────────────────────────────┤
│  git config --global user.name "Name" │  Set your name              │
│  git config --global user.email "..."  │  Set your email             │
│  git config --list                    │  View all settings          │
└───────────────────────────────────────┴─────────────────────────────┘
```

### A.2 — Starting a Project

```
┌─────────────────────────────────────────────────────────────────────┐
│  COMMAND                              │  WHAT IT DOES               │
├───────────────────────────────────────┼─────────────────────────────┤
│  git init                             │  Start tracking a folder    │
│  git clone <url>                      │  Download a repo from GitHub│
└───────────────────────────────────────┴─────────────────────────────┘
```

### A.3 — Daily Basics

```
┌─────────────────────────────────────────────────────────────────────┐
│  COMMAND                              │  WHAT IT DOES               │
├───────────────────────────────────────┼─────────────────────────────┤
│  git status                           │  See what changed           │
│  git add filename.txt                 │  Stage one file             │
│  git add .                            │  Stage all files            │
│  git commit -m "message"              │  Save a snapshot            │
│  git log                              │  View full history          │
│  git log --oneline                    │  Compact history            │
│  git diff                             │  See line-by-line changes   │
└───────────────────────────────────────┴─────────────────────────────┘
```

### A.4 — Undoing Changes

```
┌─────────────────────────────────────────────────────────────────────┐
│  COMMAND                              │  WHAT IT DOES               │
├───────────────────────────────────────┼─────────────────────────────┤
│  git restore --staged file.txt        │  Unstage a file             │
│  git restore file.txt                 │  Discard changes (danger!)  │
│  git reset --soft HEAD~1              │  Undo commit, keep staged   │
│  git reset HEAD~1                     │  Undo commit, keep unstaged │
│  git reset --hard HEAD~1              │  Undo commit, delete files  │
│  git revert <commit-id>               │  Safely undo a commit       │
└───────────────────────────────────────┴─────────────────────────────┘
```

### A.5 — Branches

```
┌─────────────────────────────────────────────────────────────────────┐
│  COMMAND                              │  WHAT IT DOES               │
├───────────────────────────────────────┼─────────────────────────────┤
│  git branch                           │  List all branches          │
│  git branch <name>                    │  Create a branch            │
│  git checkout <name>                  │  Switch to a branch         │
│  git checkout -b <name>               │  Create and switch          │
│  git switch -c <name>                 │  Create and switch (new way)│
│  git merge <branch>                   │  Merge branch into current  │
│  git branch -d <name>                 │  Delete merged branch       │
│  git branch -D <name>                 │  Force delete branch        │
└───────────────────────────────────────┴─────────────────────────────┘
```

### A.6 — Merging

```
┌─────────────────────────────────────────────────────────────────────┐
│  COMMAND                              │  WHAT IT DOES               │
├───────────────────────────────────────┼─────────────────────────────┤
│  git merge <branch>                   │  Fast-forward or three-way  │
│  git merge <branch> -m "message"      │  Merge with explicit message│
│  git merge --squash <branch>          │  Squash merge               │
│  git merge a b c -m "message"         │  Octopus merge              │
│  git merge --abort                    │  Cancel a merge in progress │
└───────────────────────────────────────┴─────────────────────────────┘
```

### A.7 — Working with GitHub

```
┌─────────────────────────────────────────────────────────────────────┐
│  COMMAND                              │  WHAT IT DOES               │
├───────────────────────────────────────┼─────────────────────────────┤
│  git remote add origin <url>          │  Connect to GitHub          │
│  git remote -v                        │  View remotes               │
│  git remote remove origin             │  Remove a remote            │
│  git remote set-url origin <url>      │  Change remote URL          │
│  git push -u origin main              │  First push (sets upstream) │
│  git push                             │  Push (after first time)    │
│  git pull                             │  Fetch + merge              │
│  git fetch origin                     │  Download without merging   │
│  git fetch origin main                │  Fetch specific branch      │
└───────────────────────────────────────┴─────────────────────────────┘
```

### A.8 — Stash and Rebase

```
┌─────────────────────────────────────────────────────────────────────┐
│  COMMAND                              │  WHAT IT DOES               │
├───────────────────────────────────────┼─────────────────────────────┤
│  git stash                            │  Save work-in-progress      │
│  git stash list                       │  See all stashes            │
│  git stash pop                        │  Restore and delete stash   │
│  git stash apply                      │  Restore, keep stash        │
│  git stash drop stash@{0}             │  Delete specific stash      │
│  git stash clear                      │  Delete all stashes         │
│  git rebase main                      │  Rebase current onto main   │
│  git rebase --continue                │  Continue after conflict    │
│  git rebase --abort                   │  Cancel rebase              │
└───────────────────────────────────────┴─────────────────────────────┘
```

### A.9 — The Standard Workflow From Start to Finish

```bash
# ── STARTING A NEW PROJECT FROM SCRATCH ──────────────────────────────

mkdir my-project
cd my-project
git init
# Create your files...
git add .
git commit -m "Initial commit"
git remote add origin git@github.com:your-username/my-project.git
git push -u origin main


# ── STARTING EACH WORK DAY ───────────────────────────────────────────

git pull                        # Get latest from teammates
git checkout -b feature-xyz     # Create a branch for your work


# ── DURING WORK (repeat as many times as needed) ─────────────────────

# Edit files...
git status                      # See what changed
git add .                       # Stage everything
git commit -m "Add xyz feature" # Save a snapshot


# ── WHEN THE FEATURE IS READY ────────────────────────────────────────

git push origin feature-xyz     # Push branch to GitHub
# Create a Pull Request on GitHub
# Wait for review and approval
# Merge the PR on GitHub


# ── AFTER THE PR IS MERGED ───────────────────────────────────────────

git checkout main               # Switch back to main
git pull                        # Get the merged code
git branch -d feature-xyz       # Clean up the branch
```

---

> **What to do next:**
>
> Reading this guide has given you the full picture of Git and GitHub. But reading is only 10% of learning — the other 90% is doing. The fastest way to truly internalize these concepts is to:
>
> 1. Create a practice project and make 10 commits
> 2. Create three branches, make changes on each, and merge them all
> 3. Find a teammate and practice pushing, pulling, and resolving a merge conflict together
> 4. Fork any public repository on GitHub and explore it
> 5. Make a small improvement to an open source project and open a Pull Request
>
> Every professional developer felt confused by Git at first. Every one of them got comfortable by doing, breaking things, and figuring out how to fix them. You will too.