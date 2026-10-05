# Git + GitHub + VS Code — સંપૂર્ણ Gujarati Guide

આ document નો હેતુ એ છે કે Git અને GitHub નું setup એક વાર કર્યા પછી તમે કોઈપણ WordPress / React / અન્ય project માટે આ steps ફરીથી ઉપયોગ કરી શકો.

---

# 1. Git શું છે?

**Git** = તમારા computer પર code ના changes track કરવા માટેનું version-control system.

**GitHub** = Git repositories online રાખવાની જગ્યા.

સરળ રીતે:

```text
તમારું Project Folder
        │
        ▼
       Git
        │
        │ commit
        ▼
   Local Repository
        │
        │ push
        ▼
     GitHub Repo
        │
        │ pull
        ▼
   બીજા Computer પર Project
```

### ત્રણ મહત્વની જગ્યાઓ

```text
Working Folder
     │
     │ git add
     ▼
Staging Area
     │
     │ git commit
     ▼
Local Git Repository
     │
     │ git push
     ▼
GitHub Repository
```

---

# 2. Windows System માં Git Install કરવું

તમે Windows Terminal / PowerShell / Command Prompt માં આ command ચલાવી શકો:

```bash
winget install --id Git.Git -e
```

### શું થયું?

આ command થી system માં **Git install** થયું.

Git સાથે સામાન્ય રીતે **Git Bash** પણ install થાય છે.

### Installation check

Terminal બંધ કરીને ફરી open કરો અને:

```bash
git --version
```

જો version દેખાય, જેમ કે:

```text
git version 2.x.x
```

તો Git successfully install છે.

---

# 3. Git ની Basic Global Configuration

Git install થયા પછી તમારું નામ અને email એક વખત set કરો.

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

ઉદાહરણ:

```bash
git config --global user.name "Janki"
git config --global user.email "your-github-email@example.com"
```

> અહીં GitHub account સાથે ઉપયોગ કરતા email address રાખવું વધુ યોગ્ય છે.

### Check કરવું

```bash
git config --global user.name
git config --global user.email
```

બધી Git settings જોવા:

```bash
git config --global --list
```

---

# 4. GitHub Login / Connection

Git install કરવાથી GitHub account automatically connect થતું નથી.

VS Code માં **Publish to GitHub** અથવા GitHub-related action કરતી વખતે browser ખૂલે અને GitHub login કરવાની option આવે.

તમારા GitHub account થી login કરો અને authorization complete કરો.

એક વખત VS Code માં GitHub account connect થયા પછી તમે VS Code મારફતે repositories publish/manage કરી શકો છો.

---

# 5. VS Code માં Existing Project ને GitHub સાથે Connect કરવું

ધારો કે તમારા computer માં project છે:

```text
C:\Projects\zakra
```

VS Code માં:

```text
File
  ↓
Open Folder
  ↓
zakra
```

Project open થયા પછી:

```text
Ctrl + Shift + G
```

દબાવો.

આથી **Source Control** panel open થશે.

---

# 6. Existing Project માટે VS Code ની સૌથી સરળ રીત

જો project હજુ Git repository નથી, તો Source Control માં repository initialize/publish કરવાની option દેખાઈ શકે છે.

VS Code માં:

```text
Ctrl + Shift + G
        ↓
Initialize Repository / Publish to GitHub
        ↓
GitHub Login
        ↓
Repository Name
        ↓
Private / Public પસંદ કરો
        ↓
Publish
```

જો **Publish to GitHub** option વાપરો તો VS Code સામાન્ય રીતે:

```text
Git repository initialize
        +
GitHub repository create
        +
Remote connection setup
        +
Initial files push
```

આ બધું સરળ રીતે કરી આપે છે.

### આ રીત existing project માટે સરળ છે

તમારે manually:

```bash
git init
git remote add origin ...
```

વગેરે કરવાની જરૂર ઘણી વાર રહેતી નથી.

---

# 7. GitHub Repository બનાવવાની બીજી રીત

GitHub website પરથી પહેલા repository બનાવી શકાય.

GitHub પર:

```text
https://github.com/new
```

અહીં:

```text
Repository name → zakra
Visibility       → Private અથવા Public
Add README       → existing project માટે સામાન્ય રીતે unticked રાખો
```

પછી:

```text
Create repository
```

---

# 8. Website પરથી Repository 만들્યા પછી Existing Project Connect કરવું

જો GitHub પર repository પહેલા બનાવી છે અને local project પણ પહેલેથી છે, તો local project માં:

```bash
cd "C:\Projects\zakra"
```

પછી:

```bash
git init
```

Files check:

```bash
git status
```

બધી files staging માં:

```bash
git add .
```

First commit:

```bash
git commit -m "Initial commit"
```

GitHub repository ને remote તરીકે add કરો:

```bash
git remote add origin https://github.com/YOUR-USERNAME/zakra.git
```

Branch ને `main` કરો:

```bash
git branch -M main
```

પછી GitHub પર push:

```bash
git push -u origin main
```

---

# 9. `git init` શું કરે છે?

```bash
git init
```

આ command તમારા current project folder ને Git repository બનાવે છે.

તે પછી project માં hidden `.git` folder બને છે.

Visual:

```text
zakra/
│
├── wp-content/
├── wp-admin/
├── wp-includes/
├── ...
│
└── .git/       ← Git repository information
```

> `.git` folder manually delete ન કરવો, જો તમે repository tracking બંધ કરવા માંગતા ન હો.

---

# 10. `.gitignore` ખૂબ મહત્વનું છે

GitHub પર બધું upload કરવું જરૂરી નથી.

WordPress project માં ઘણી files/folders Git માં ન રાખવી યોગ્ય હોય છે, ખાસ કરીને:

```text
wp-config.php
.env
node_modules/
cache/
logs/
backup files
local configuration files
```

Project root માં:

```text
.gitignore
```

file બનાવી શકાય.

ઉદાહরণ:

```gitignore
.env
node_modules/
*.log
wp-content/cache/
wp-content/uploads/cache/
```

> WordPress project પ્રમાણે `.gitignore` customize કરવું જોઈએ. `wp-config.php` ignore કરતા પહેલાં deployment/server workflow ધ્યાનમાં લો.

---

# 11. Git Status — સૌથી મહત્વની Command

કોઈપણ સમયે:

```bash
git status
```

ચલાવો.

તે તમને બતાવશે:

```text
modified
new file
deleted
untracked
```

ઉદાહરણ:

```text
modified: style.css
modified: functions.php
new file: custom.js
```

---

# 12. Changes GitHub પર મોકલવાની Complete Process

દર everytime સામાન્ય flow:

```text
Code Change
    ↓
git status
    ↓
git add .
    ↓
git commit -m "Describe changes"
    ↓
git push
```

Commands:

```bash
git status
git add .
git commit -m "Update website changes"
git push
```

---

# 13. Commit Message શું છે?

Commit એટલે તમારા changes નો એક saved checkpoint.

```bash
git commit -m "Fix mobile menu issue"
```

અહીં:

```text
Fix mobile menu issue
```

તમારો **commit message** છે.

સારા examples:

```bash
git commit -m "Fix header responsive layout"
git commit -m "Update contact form styling"
git commit -m "Add new project section"
git commit -m "Fix PHP 8 compatibility issue"
git commit -m "Update WordPress theme files"
```

Commit message ટૂંકો અને change શું કર્યું તે સમજાય એવો રાખો.

---

# 14. VS Code માં Commit કેવી રીતે કરવું?

Shortcut:

```text
Ctrl + Shift + G
```

Source Control panel માં changed files દેખાશે.

Flow:

```text
Changed Files
     ↓
Review Changes
     ↓
Stage (+)
     ↓
Commit Message લખો
     ↓
Commit
```

જો તમે command line ઉપયોગ કરવા માંગતા હો:

```bash
git add .
git commit -m "Your message"
```

---

# 15. Push શું છે?

**Push = Local computer ના commits GitHub પર મોકલવા.**

```bash
git push
```

Visual:

```text
Computer
   │
   │ git push
   ▼
GitHub
```

---

# 16. Pull શું છે?

**Pull = GitHub પરના latest changes તમારા local project માં લાવવા.**

```bash
git pull
```

Visual:

```text
GitHub
   │
   │ git pull
   ▼
Computer
```

---

# 17. Push અને Pull ક્યારે કરવું?

### તમે code change કર્યો:

```text
Code change
   ↓
git add .
   ↓
git commit
   ↓
git push
```

### બીજા developer / બીજા computer to changes આવ્યા:

```text
GitHub
   ↓
git pull
   ↓
તમારું local project update
```

---

# 18. VS Code માં Push / Pull Buttons ન વાપરવા હોય તો

Terminal માં commands use કરી શકો.

### Push

```bash
git push
```

### Pull

```bash
git pull
```

### Commit

```bash
git add .
git commit -m "Your commit message"
```

### Complete update

```bash
git add .
git commit -m "Update project"
git push
```

---

# 19. Current Repository કઈ છે તે Check કરવું

આ command:

```bash
git remote -v
```

Example:

```text
origin  https://github.com/username/zakra.git (fetch)
origin  https://github.com/username/zakra.git (push)
```

આથી તમને ખબર પડશે કે current local project કયા GitHub repository સાથે connected છે.

---

# 20. Current Branch Check કરવી

```bash
git branch
```

Example:

```text
* main
```

`*` જે branch આગળ છે તે current branch છે.

નવી Git versions માં current branch જાણવા:

```bash
git branch --show-current
```

---

# 21. એક Git Repository માંથી બીજી Repository પર Switch કરવું

આ બહુ મહત્વનું છે.

ધારો કે હાલ:

```text
Project A
    ↓
GitHub Repo A
```

અને હવે તમારે:

```text
Project B
    ↓
GitHub Repo B
```

પર કામ કરવું છે.

### સૌથી પહેલા Project B folder open કરો

VS Code:

```text
File → Open Folder → Project B
```

પછી Terminal:

```bash
cd "C:\Projects\Project-B"
```

Check:

```bash
git status
```

---

# 22. Project B પહેલેથી Git Repository છે કે નહીં?

Check:

```bash
git status
```

જો Git repository છે તો status મળશે.

Remote check:

```bash
git remote -v
```

જો output આવે:

```text
origin https://github.com/username/project-b.git
```

તો Project B already GitHub સાથે connected છે.

---

# 23. Project B ને બીજી GitHub Repository સાથે Connect કરવું

ધારો કે current remote ખોટી repository છે.

પહેલા check:

```bash
git remote -v
```

જૂનું remote remove:

```bash
git remote remove origin
```

નવું remote add:

```bash
git remote add origin https://github.com/YOUR-USERNAME/NEW-REPO.git
```

Check:

```bash
git remote -v
```

પછી:

```bash
git branch -M main
git push -u origin main
```

---

# 24. Existing Project ને New GitHub Repo સાથે Connect — Short Version

આ સૌથી ઉપયોગી sequence છે:

```bash
cd "C:\Projects\MyProject"

git init
git add .
git commit -m "Initial commit"

git branch -M main

git remote add origin https://github.com/YOUR-USERNAME/REPOSITORY.git

git push -u origin main
```

---

# 25. Repository Already Connected હોય તો

જો remote પહેલેથી set છે:

```bash
git remote -v
```

પછી માત્ર:

```bash
git add .
git commit -m "Update project"
git push
```

---

# 26. એક Project ને બીજી GitHub Repository સાથે જોડવું

જો તમે current repository બદલવા માંગો:

### Step 1

```bash
git remote -v
```

### Step 2 — Old remote remove

```bash
git remote remove origin
```

### Step 3 — New remote add

```bash
git remote add origin https://github.com/YOUR-USERNAME/NEW-REPOSITORY.git
```

### Step 4 — Check

```bash
git remote -v
```

### Step 5 — Push

```bash
git branch -M main
git push -u origin main
```

---

# 27. બીજી Repository પર કામ કરવા માટે `git clone`

જો project computer માં નથી અને GitHub પર પહેલેથી છે:

```bash
git clone https://github.com/YOUR-USERNAME/REPOSITORY.git
```

Example:

```bash
git clone https://github.com/YOUR-USERNAME/zakra.git
```

પછી:

```bash
cd zakra
```

અને VS Code માં:

```bash
code .
```

જો `code` command available ન હોય તો VS Code માં:

```text
File → Open Folder
```

થી folder open કરો.

---

# 28. Existing GitHub Project માંથી Latest Changes લેવા

Project folder માં:

```bash
git pull
```

જો પહેલાં changes commit કર્યા નથી તો પહેલાં:

```bash
git status
```

તમારા local changes check કરો.

---

# 29. Branch શું છે?

Branch એટલે project ના code માટે અલગ development line.

Check:

```bash
git branch
```

નવી branch:

```bash
git checkout -b feature-header
```

નવી Git syntax:

```bash
git switch -c feature-header
```

Branch બદલવા:

```bash
git switch main
```

અથવા:

```bash
git checkout main
```

---

# 30. Useful Daily Workflow

દરરોજ project પર કામ શરૂ કરતાં પહેલાં:

```bash
git pull
```

Code કરો.

પછી:

```bash
git status
```

Changes review કરો.

પછી:

```bash
git add .
git commit -m "Describe your changes"
git push
```

### Complete visual

```text
             START WORK
                  │
                  ▼
             git pull
                  │
                  ▼
             Code Changes
                  │
                  ▼
             git status
                  │
                  ▼
              git add .
                  │
                  ▼
        git commit -m "message"
                  │
                  ▼
              git push
                  │
                  ▼
              GitHub
```

---

# 31. ખૂબ ઉપયોગી Commands — Quick Reference

| કામ | Command |
|---|---|
| Git version | `git --version` |
| Git user name | `git config --global user.name` |
| Git email | `git config --global user.email` |
| Current status | `git status` |
| Repository initialize | `git init` |
| Files stage | `git add .` |
| Commit | `git commit -m "message"` |
| Push | `git push` |
| Pull | `git pull` |
| Remote check | `git remote -v` |
| Remote remove | `git remote remove origin` |
| Remote add | `git remote add origin URL` |
| Branch check | `git branch` |
| Current branch | `git branch --show-current` |
| Clone repository | `git clone URL` |
| Branch change | `git switch branch-name` |
| New branch | `git switch -c branch-name` |
| Commit history | `git log --oneline` |

---

# 32. GitHub Repository માં શું દેખાશે?

Local:

```text
MyProject/
├── index.php
├── style.css
├── functions.php
├── assets/
└── .git/
```

Push પછી GitHub:

```text
GitHub
└── MyProject
    ├── index.php
    ├── style.css
    ├── functions.php
    └── assets/
```

`.git` folder GitHub પર normal project file તરીકે upload થતો નથી.

---

# 33. Important: `git add .` પછી શું થાય છે?

```bash
git add .
```

એનો અર્થ:

> Current folder માં થયેલા changes ને next commit માટે staging માં મૂકો.

પછી:

```bash
git commit -m "Update project"
```

એનો અર્થ:

> Staged changes ને local Git history માં save કરો.

પછી:

```bash
git push
```

એનો અર્થ:

> Local commits ને GitHub પર મોકલો.

---

# 34. જો ભૂલથી `git add .` કરી દીધું હોય

જો હજુ commit નથી કર્યો:

```bash
git restore --staged .
```

આથી files stagingમાંથી બહાર આવશે.

Filesના actual changes delete નહીં થાય.

---

# 35. Commit પહેલાં Changes Review કરવું

```bash
git status
```

અને detailed changes:

```bash
git diff
```

આથી તમે જોઈ શકો કે code માં શું બદલાયું છે.

---

# 36. Last Commit Check

```bash
git log --oneline
```

Example:

```text
a12bc34 Fix header spacing
d45ef67 Update footer
f78gh90 Initial commit
```

---

# 37. GitHub Repository URL બદલાઈ ગઈ હોય તો

જૂનું URL check:

```bash
git remote -v
```

નવું URL સીધું set કરવા:

```bash
git remote set-url origin https://github.com/YOUR-USERNAME/NEW-REPOSITORY.git
```

પછી:

```bash
git remote -v
```

---

# 38. એક Computer પર ઘણા Projects હોય તો

દરેક project પોતાનું Git repository હોઈ શકે.

Example:

```text
C:\Projects\
│
├── zakra\
│   └── GitHub → zakra
│
├── parish-engineering\
│   └── GitHub → parish-engineering
│
├── travel-bazaar\
│   └── GitHub → travel-bazaar
│
└── project-4\
    └── GitHub → project-4
```

તમારે repository switch કરવા માટે VS Code માં માત્ર correct project folder open કરવો.

પછી:

```bash
git remote -v
```

થી check કરો કે કઈ GitHub repository connected છે.

---

# 39. એક Project માંથી બીજા Project પર Switch કરવાની Practical રીત

ધારો તમે `zakra` પર કામ કરો છો.

### Zakra

```bash
cd "C:\Projects\zakra"
git remote -v
```

તમને:

```text
github.com/username/zakra.git
```

દેખાય.

હવે `parish-engineering` પર જવું છે.

```bash
cd "C:\Projects\parish-engineering"
```

પછી:

```bash
git remote -v
```

તમને:

```text
github.com/username/parish-engineering.git
```

દેખાશે.

**અહીં કોઈ special GitHub logout/login કરવાની જરૂર નથી.**

દરેક project folder પોતાનું remote રાખે છે.

---

# 40. સૌથી મહત્વની સમજ

GitHub account એક હોઈ શકે:

```text
Your GitHub Account
        │
        ├── Repo A
        │
        ├── Repo B
        │
        ├── Repo C
        │
        └── Repo D
```

અને તમારા computer પર:

```text
Project A → Repo A
Project B → Repo B
Project C → Repo C
Project D → Repo D
```

દરેક project માં:

```bash
git remote -v
```

ચલાવીને તમે જાણશો કે તે કઈ repository સાથે connected છે.

---

# 41. જો GitHub પર Repository બનાવતી વખતે README પહેલેથી add કર્યું હોય

જો local project પણ existing હોય અને GitHub repo માં README પહેલેથી હોય, તો histories અલગ હોઈ શકે.

એવામાં સીધું `git push` કરતાં પહેલાં repository state check કરો.

Safe approach:

```bash
git pull origin main --allow-unrelated-histories
```

પછી conflicts આવે તો resolve કરો અને:

```bash
git add .
git commit -m "Merge remote repository"
git push
```

> Existing project માટે GitHub repository બનાવતી વખતે **Add README unticked** રાખવાથી આ situation ઘણીવાર avoid થાય છે.

---

# 42. Git Push Reject થાય તો

Example:

```text
rejected
non-fast-forward
```

સૌથી પહેલા:

```bash
git status
git pull
```

પછી conflict હોય તો resolve કરો.

પછી:

```bash
git add .
git commit -m "Resolve merge conflicts"
git push
```

> અજાણ્યા હો ત્યારે `git push --force` ન ચલાવવું. તે remote history overwrite કરી શકે છે.

---

# 43. `origin` શું છે?

આ command:

```bash
git remote add origin https://github.com/username/zakra.git
```

અહીં:

```text
origin
```

એ GitHub repository માટેનું local nickname છે.

તેથી:

```bash
git push origin main
```

નો અર્થ:

```text
origin → GitHub repository
main   → branch
```

સામાન્ય રીતે એક વખત:

```bash
git push -u origin main
```

કરી દીધા પછી આગળ માત્ર:

```bash
git push
```

કરી શકાય છે.

---

# 44. GitHub સાથે Connection Check

આ 3 commands ખૂબ ઉપયોગી છે:

```bash
git status
git branch --show-current
git remote -v
```

જો આ ત્રણની output સમજાય છે, તો current project કઈ સ્થિતિમાં છે તે સરળતાથી જાણી શકો છો.

---

# 45. New Project માટે Complete Checklist

```text
☐ Git installed
☐ git --version works
☐ Git name configured
☐ Git email configured
☐ GitHub login connected
☐ Project opened in VS Code
☐ Git repository initialized/published
☐ GitHub repository created
☐ Remote checked
☐ First commit created
☐ First push completed
```

---

# 46. Daily Checklist

```text
START
  ↓
git pull
  ↓
Work / Coding
  ↓
git status
  ↓
Review changes
  ↓
git add .
  ↓
git commit -m "message"
  ↓
git push
  ↓
DONE
```

---

# 47. સૌથી જરૂરી 6 Commands

જો બધું યાદ ન રહે તો આ 6 commands યાદ રાખો:

```bash
git status
git pull
git add .
git commit -m "Your message"
git push
git remote -v
```

આ commands થી daily Git work નો મોટો ભાગ થઈ જાય છે.

---

# 48. તમારા Current Setup નો Summary

તમારા system પર તમે આ કર્યું:

### Step 1 — Git install

```bash
winget install --id Git.Git -e
```

### Step 2 — Git user setup

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

### Step 3 — GitHub login

VS Code માં GitHub account connect કર્યું.

### Step 4 — Existing project VS Code માં open કર્યું

```text
VS Code → Open Folder
```

### Step 5 — Source Control

```text
Ctrl + Shift + G
```

### Step 6 — Repository publish/connect

VS Code ની GitHub publish option થી repository બનાવી અને project GitHub સાથે connect કર્યું.

### Step 7 — Future changes

```bash
git add .
git commit -m "Describe changes"
git push
```

### Step 8 — GitHub ના latest changes લેવા

```bash
git pull
```

---

# 49. One-Line Memory Trick

```text
PULL → WORK → STATUS → ADD → COMMIT → PUSH
```

અર્થ:

```text
GitHub from latest લો
        ↓
Code કરો
        ↓
Changes જુઓ
        ↓
Changes stage કરો
        ↓
Commit કરો
        ↓
GitHub પર push કરો
```

---

# 50. Final Quick Cheat Sheet

### Git install

```bash
winget install --id Git.Git -e
```

### Check

```bash
git --version
```

### User setup

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

### New local repository

```bash
git init
```

### Check changes

```bash
git status
```

### Stage

```bash
git add .
```

### Commit

```bash
git commit -m "Update project"
```

### Push

```bash
git push
```

### Pull

```bash
git pull
```

### Check GitHub connection

```bash
git remote -v
```

### Change GitHub repository

```bash
git remote set-url origin https://github.com/YOUR-USERNAME/NEW-REPOSITORY.git
```

### Clone existing repository

```bash
git clone https://github.com/YOUR-USERNAME/REPOSITORY.git
```

### Branch

```bash
git branch
git switch main
git switch -c feature-name
```

---

# યાદ રાખવાની મુખ્ય વાત

**Git = તમારા computer પર code history**

**GitHub = online repository**

**Commit = changes નું saved checkpoint**

**Push = local → GitHub**

**Pull = GitHub → local**

**Remote = local project કઈ GitHub repository સાથે connected છે**

અને કોઈપણ સમયે current project વિશે confusion હોય તો:

```bash
git status
git branch --show-current
git remote -v
```

આ ત્રણ commands ચલાવો.
