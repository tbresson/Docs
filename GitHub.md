# GitHub

## PRE-REQ

- Install Git
- Install VSCode

## CREATE A REPOSITORY

- Logon to GitHub
- Create a repository
- Click "Clone or download"
- Clone with HTTPS (use the copy button)

## CLONE THE REPOSITORY TO YOUR COMPUTER

- Open Visual Studio Code
- Create a folder for all your GitHub projects, e.g. C:\GitHub\
- Right-click on that folder and select "Open in Terminal"
- Enter "git clone " and paste the URL from the GitHub website, e.g. <https://github.com/gituser/project1.git>

## STAGE AND COMMIT CHANGES

- Add or edit files inside your projectfolder (and save it)
- Enter "git add X" where X is either:
  - a filename of a file you've created, e.g. "git add readme.md" or
  - a dot (.) to add all files in the directory, e.g. "git add ."
- Enter "git commit -m "message"" to commit your changes
- Enter "git push" to push/upload your local content to GitHub

## RESTORE/REVERT CHANGES

- Enter "git restore X" where X is either:
  - a filename of a file you've created, e.g. "git restore readme.md" or
  - a dot (.) to add all files in the directory, e.g. "git restore ."

## BRANCHES

- Enter "git branch X" to create a branch named X
- Enter "git checkout X" to switch to the branch named X
- Or enter "git checkout -b X" to create a branch and check it out at the same time
- Stage and commit until complete
- Enter "git push origin X" to push/upload your local branch X to GitHub

## MERGE

- Enter "git checkout master" (or main) to return to the master/main branch
- Enter "git merge X" to merge the branch X with master (or main)
- Enter "git branch -d X" to delete branch X
