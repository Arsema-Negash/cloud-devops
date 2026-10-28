# Week 1: Linux Hands-on Lab

## Objective
Practice basic Linux commands for file management and process identification.

## Commands Used

### 1. Create the project directory
```bash
mkdir -p ~/cloud-devops/week1
cd ~/cloud-devops/week1
pwd
```

### 2. Create and write to a file
```bash
touch notes.txt
echo "Week 1 Linux Hands-on Lab" > notes.txt
cat notes.txt
```

### 3. Create a directory and move the file
```bash
mkdir scripts
mv notes.txt scripts/
```

### 4. Search for the file
```bash
find ~/cloud-devops/week1 -name "notes.txt"
```

### 5. Find a running process and its PID
```bash
ps
```

## Screenshots
The `screenshots/` folder contains evidence of all six completed tasks.

## What I Learned
- Creating directories and managing files.
- Searching for files using Linux commands.
- Identifying running processes and their PIDs.
- Documenting and submitting work using GitHub.
