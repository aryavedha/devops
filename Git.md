Best Practices to Prevent Sensitive Data Push
1. Use .gitignore Properly

Add sensitive files (e.g., .env, secrets.json, id_rsa) to .gitignore.

Example:
```
# Ignore environment files
*.env
secrets.json
*.pem
*.key
# Ignore build dir also because it has lot of data
build/
# Ignore specific file any as per requirment 
notes.txt
# log files also not required 
*.log

```

This prevents accidental commits of these files.

Setup: Git Hooks + Gitleaks
2. Install Gitleaks
Linux / macOS
```
brew install gitleaks
```

or (cross-platform binary):
```
curl -sSL https://github.com/gitleaks/gitleaks/releases/latest/download/gitleaks_$(uname -s)_x64.tar.gz | tar -xz
sudo mv gitleaks /usr/local/bin/
```

3. Create a Pre-Commit Hook

A pre-commit hook runs automatically before every git commit.

Go to your repo:
```
cd your-repo
mkdir -p .git/hooks
```

Create the file:
```
sudo vi .git/hooks/pre-commit
```

Add this script:
```
#!/bin/sh
echo " Running Gitleaks scan before commit..."

gitleaks detect --source . --no-git --redact
STATUS=$?

if [ $STATUS -ne 0 ]; then
  echo " Gitleaks detected sensitive data! Commit aborted."
  exit 1
fi

echo " No secrets detected. Proceeding with commit."
exit 0
```

Make it executable:
```
chmod +x .git/hooks/pre-commit
```

4. Test the Hook

Try committing a file with a fake secret:
```
echo "AWS_SECRET_ACCESS_KEY=AKIA123456789" >> test.env
git add test.env
git commit -m "add test secret"
```

- The hook should block the commit with an error like:

  (Gitleaks detected sensitive data! Commit aborted.)

