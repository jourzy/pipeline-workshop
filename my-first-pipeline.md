
# 🍏 My First Pipeline  
A gentle introduction to GitHub Actions

This tutorial will guide you through creating your *very first pipeline* using **GitHub Actions**. You’ll follow simple steps to make a workflow that runs automatically whenever you push code to GitHub.

By the end, you will have:
- A working GitHub repository  
- Your first CI workflow that runs automatically  
- A sense of achievement after only **30 minutes** 🎉

---
## ✅ Prerequisites
- GitHub account
- Web browser
- (Optional) VSCode
- No programming experience required!

---
## 🚀 1. Create your GitHub repository
1. Go to https://github.com/new
2. Name your repo:
```
pipeline-workshop
```
3. Click **Create Repository**

---
## 📁 2. Add a simple file
1. In the quick set up box, click the **creating a new file** link
2. Name it `notes.txt`
3. Add a few words e.g. :
```
Automating workflows is cooool!
```
4. Commit changes

---
## ⚙️ 3. Create your first workflow
1. Add a file:
```
.github/workflows/first.yml
```
2. Add this workflow:
```yaml
name: My First Pipeline

on: push

jobs:
  output-message:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      - name: Print a message
        run: echo "🎉 My first pipeline is running!"
```
3. Commit the file

---
## ▶️ 4. Watch it run
- Click the **Actions** tab
- Open the running workflow
- See your message printed!

---
## 🔄 5. Trigger it again
Edit `notes.txt`, commit, and watch the workflow rerun.

---
## ⭐ Extra Challenges
### Challenge 1: Add a (fake) test step
```yaml
- name: Run tests
  run: echo "Running tests... All tests passed!"
```
### Challenge 2: Count characters
```yaml
- name: Count characters
  run: wc -c notes.txt
```

---
## 🎉 You did it!
You've created your first CI workflow. This is the perfect foundation for learning testing, deployment, and automation.

