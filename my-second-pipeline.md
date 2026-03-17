
# 🐷 My Second Pipeline
Learning GitHub Actions with Figlet

This pipeline builds on your first GitHub Actions workflow by introducing:
- a custom run name
- branch-specific trigger rules
- installing a CLI tool (figlet)
- reading text from a repository file and using it in a command

---
## 📁 1. Create the workflow file
Create this file in your repository:
```
.github/workflows/second.yml
```

---
## 🧩 2. Add this workflow
```yaml
name: My Second Pipeline

run-name: ${{ github.actor }} is automating workflows with ${{ github.workflow }}

on: 
  push:
    branches: 
      - main

jobs:
  render-figlet-banner:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v5

      - name: Install figlet
        run: sudo apt-get update && sudo apt-get install -y figlet

      - name: Print figlet banner from notes.txt
        run: |
          TEXT="$(cat notes.txt)"
          figlet "$TEXT"

  render-cowsay-banner:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v5

      - name: Install cowsay
        run: sudo apt-get update && sudo apt-get install -y cowsay

      - name: Print cowsay banner from notes.txt
        run: |
          TEXT="$(cat notes.txt)"
          cowsay "$TEXT"
```

---
## 🔍 3. How this workflow works
### ✔ Workflow name
Displayed in the Actions tab.

### ✔ Run name
Uses `${{ github.actor }}` (who triggered the run) and `${{ github.workflow }}` (the workflow name) so each run label shows both pieces of context at a glance. These are part of GitHub's **contexts** — variables that give you information about the run, repo, and environment. See all [available contexts](https://docs.github.com/en/actions/reference/workflows-and-actions/contexts#available-contexts).

### ✔ Trigger
Runs on pushes to the **main** branch only.

### ✔ Job structure
This workflow has two jobs, each running independently on a clean Ubuntu runner:

**Job 1: render-figlet-banner**
1. **Checkout** the repository
2. **Install figlet** (an ASCII-art banner tool)
3. **Print a figlet banner** using text from `notes.txt`

**Job 2: render-cowsay-banner**
1. **Checkout** the repository
2. **Install cowsay** (a talking-cow ASCII tool)
3. **Print a cowsay banner** using text from `notes.txt`

Because neither job declares `needs:`, they run in parallel. This shows how a workflow can do more than one thing at once.

---
## ▶️ 4. Try it out
Push any change to your repo, then:
1. Go to the **Actions** tab
2. Open the workflow run
3. Look for your ASCII banner in the logs

---
## ⭐ Extra challenges
Use the figlet commands from the reference section below to customise the output in your workflow.

### 🔤 Change the font
Update the figlet step to use a different font:
```yaml
- name: Print figlet banner from notes.txt
  run: |
    TEXT="$(cat notes.txt)"
    figlet -f slant "$TEXT"
```
Try `big`, `banner`, `block`, `mini`, `shadow`, or `script` in place of `slant`.

### ↔️ Change the alignment
Centre or right-align your banner:
```yaml
figlet -c "$TEXT"
figlet -r "$TEXT"
```

### 🌈 Add colours using lolcat
Pipe the figlet output through lolcat for a rainbow effect:
```yaml
- name: Install figlet and lolcat
  run: sudo apt-get update && sudo apt-get install -y figlet lolcat

- name: Print rainbow banner
  run: |
    TEXT="$(cat notes.txt)"
    figlet "$TEXT" | lolcat
```

---
🎉 Your second pipeline now feels closer to real CI while still being easy and fun!

---
## 🔤 Useful figlet commands

Try these out locally or add them as steps in your workflow.

**Basic output**
```bash
figlet "Hello World"
```

**Change font** (`-f`)
```bash
figlet -f slant "Hello"
figlet -f big "Hello"
figlet -f mini "Hello"
```

**Centre align** (`-c`)
```bash
figlet -c "Hello"
```

**Right align** (`-r`)
```bash
figlet -r "Hello"
```

**Set output width** (`-w`)
```bash
figlet -w 60 "Hello"
```

**Read from a file**
```bash
figlet "$(cat notes.txt)"
```

**Pipe text in**
```bash
echo "Hello" | figlet
```

**Combine with lolcat for colour**
```bash
figlet "Rainbow" | lolcat
```

Popular fonts worth trying: `slant`, `big`, `banner`, `block`, `mini`, `shadow`, `script`.

Browse more fonts and examples at [figlet.org/examples.html](https://www.figlet.org/examples.html).
