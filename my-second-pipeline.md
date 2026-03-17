
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

run-name: ${{ github.actor }} is learning GitHub Actions

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
```

---
## 🔍 3. How this workflow works
### ✔ Workflow name
Displayed in the Actions tab.

### ✔ Run name
Uses `${{ github.actor }}` so each run shows who triggered it.

### ✔ Trigger
Runs on pushes to the **main** branch only.

### ✔ Job structure
Like your first pipeline, this job runs on a clean Ubuntu runner. It keeps the checkout step and adds a tooling step:

1. **Checkout** the repository
2. **Install figlet** (a small ASCII-art banner tool)
3. **Print a banner** using figlet

This shows how a pipeline can evolve from a simple message to preparing tools and running richer commands.

---
## ▶️ 4. Try it out
Push any change to your repo, then:
1. Go to the **Actions** tab
2. Open the workflow run
3. Look for your ASCII banner in the logs

---
## ⭐ Extra challenges
### 🔤 Change the banner text
Edit the figlet command:
```
figlet "Your Name Here"
```

### 🌈 Add colours using lolcat
```
sudo apt-get install -y lolcat
figlet "Rainbow CI" | lolcat
```

### 🧱 Add a second job
Instead of using figlet, try cowsay instead!

---
🎉 Your second pipeline now feels closer to real CI while still being easy and fun!
