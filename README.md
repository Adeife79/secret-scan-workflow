# Secret Leak Detection with GitHub Actions.

## Overview
This project demonstrates how to implement automated secret leak detection in a GitHub repository using **GitHub Actions** and **Gitleaks**.
The main goal of this project is to automatically scan the changes introduced by a Pull Request and fail the workflow if a potential secret is detected.
Instead of scanning the entire Git history, the workflow scan only the changes introduced by the Pull Request. This prevents old finding from previous commits from causing a new Pull Request to fail.

## Project Structure
```
.
├── .github/
│   └── workflows/
│       ├── docker-build.yml
│       └── secret-scan.yml
│
├── index.html
├── Dockerfile
└── README.md
```

## Technologies Used
- Git
- GitHub & GitHub Actions
- Gitleaks
- Docker
- HTML & CSS


## Running the Project
Step 1: Clone the Repository
Clone the repository to your local machine:
```bash
git clone https://github.com/Adeife79/secret-scan-workflow.git
```

Move into the project directory:
```bash
cd secret-scan-workflow
```

Step 2: Create a Test Branch
Create a new branch to test the secret scanning workflow:
```bash
git checkout -b <branch_name>
```

Step 3: Make a Change
Make a normal change to the project, you can modify index.html.

Commit the change:
```bash
git add .
git commit -m <commit_message>
```

Push the branch:
```bash
git push -u origin <branch_name>
```

Step 4: Create a Pull Request
Go to the GitHub repository and create a Pull Request:
```
main <- <branch_name>
```
The secret-scan.yml workflow will automatically run.

## Testing Secret Detection
To test that the workflow can detect a leaked secret, add a fake test credential to the project(inside index.html).

**Note: Do not use a real GitHub token or any other real credential.**

Commit and push the change:
```bash
git add .
git commit -m <commit_message>
git push
```
The Pull Request workflow will run again.

Gitleaks will detect the test value and the workflow will show "🛑 Leaks detected

## Testing a Clean Pull Request
Remove the previous branch and make a normal change.

```
git add .
git commit -m <commit_message>
git push 
```
The workflow will run again.
If no secret is introduced by the Pull Request, the workflow will show ✅ PASSED.


