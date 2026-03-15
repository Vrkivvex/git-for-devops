# Day 1 – Linux Basics

## Linux Filesystem

Linux uses a single filesystem starting from:

/

Important directories:

/home  → user files  
/etc   → configuration files  
/usr   → installed programs  
/var   → logs and system data  
/bin   → system binaries  
/tmp   → temporary files  

---

## Basic Commands

pwd → show current directory

ls → list files

cd → change directory

---

## Examples

```bash
pwd
ls
cd /home
```

# Git Basics

Git is a version control system used to track code changes.

## Important Commands

git init → initialize a repository

git add . → add all files to staging area

git commit -m "message" → commit changes

git status → check repository status

git push → upload code to remote repository

---

# Connecting to GitHub

Add remote repository:

```bash
git remote add origin https://github.com/username/repository.git