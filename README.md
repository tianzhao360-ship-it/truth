# truth
## 文件：.github/workflows/ci.yml
```yaml
name: CI
on:
  push:
    branches:
      - '**'
  pull_request:
    branches:
      - '**'
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Set up Node.js (optional)
        uses: actions/setup-node@v4
        with:
          node-version: 'lts/*'
      - name: Set up Python (optional)
        uses: actions/setup-python@v4
        with:
          python-version: '3.x'
      - name: Install and run tests (auto-detect)
        run: |
          set -e
          echo "Detecting project type and running tests..."
          if [ -f package.json ]; then
            echo "Node project detected (package.json). Installing and running npm test..."
            npm ci
            if npm test; then
              echo "npm test succeeded"
            else
              echo "npm test failed"
              exit 1
            fi
          fi
          if [ -f requirements.txt ] || [ -f setup.py ] || [ -f pyproject.toml ]; then
            echo "Python project detected. Installing and running pytest if available..."
            python -m pip install --upgrade pip
            if [ -f requirements.txt ]; then
              python -m pip install -r requirements.txt
            else
              python -m pip install . || true
            fi
            if command -v pytest >/dev/null 2>&1; then
              pytest
            else
              echo "pytest not found; skipping python tests"
            fi
          fi
          if [ ! -f package.json ] && [ ! -f requirements.txt ] && [ ! -f setup.py ] && [ ! -f pyproject.toml ]; then
            echo "No common project files detected (package.json, requirements.txt, setup.py, pyproject.toml). Please update .github/workflows/ci.yml with proper steps for your project."
          fi
```

## 文件：.github/dependabot.yml
```yaml
version: 2
updates:
  - package-ecosystem: "npm"
    directory: "/"
    schedule:
      interval: "weekly"
    open-pull-requests-limit: 5
  - package-ecosystem: "pip"
    directory: "/"
    schedule:
      interval: "weekly"
    open-pull-requests-limit: 5
```

## 文件：.github/ISSUE_TEMPLATE/bug_report.md
```markdown
---
name: Bug report
about: Create a report to help us improve
title: ""
labels: bug
assignees: ""
---

**Describe the bug**
A clear and concise description of what the bug is.

**To Reproduce**
Steps to reproduce the behavior:
1. Go to '...'
2. Click on '...'
3. Scroll down to '...'
4. See error

**Expected behavior**
A clear and concise description of what you expected to happen.

**Screenshots**
If applicable, add screenshots to help explain your problem.

**Desktop (please complete the following information):**
 - OS: [e.g. iOS]
 - Browser [e.g. chrome, safari]
 - Version [e.g. 22]

**Additional context**
Add any other context about the problem here.
```

## 文件：.github/ISSUE_TEMPLATE/feature_request.md
```markdown
---
name: Feature request
about: Suggest an idea for this project
title: ""
labels: enhancement
assignees: ""
---

**Is your feature request related to a problem? Please describe.**
A clear and concise description of what the problem is. Ex. I'm always frustrated when...

**Describe the solution you'd like**
A clear and concise description of what you want to happen.

**Describe alternatives you've considered**
A clear and concise description of any alternative solutions or features you've considered.

**Additional context**
Add any other context or screenshots about the feature request here.
```

## 文件：.github/PULL_REQUEST_TEMPLATE.md
```markdown
```<!-- Please replace the placeholders below with meaningful information -->

### Summary
A short description of what this PR does.

### Type of change
- [ ] Bug fix
- [ ] New feature
- [ ] Documentation update
- [ ] Other (please describe):

### How has this been tested?
Describe the tests that you ran to verify your changes. Provide instructions so we can reproduce.

### Checklist
- [ ] My code follows the style guidelines of this project
- [ ] I have performed a self-review of my own code
- [ ] I have commented my code, particularly in hard-to-understand areas
- [ ] I have added tests that prove my fix is effective or that my feature works
- [ ] New and existing unit tests pass locally with my changes

```
```

## 文件：CONTRIBUTING.md
```markdown
# Contributing

Thanks for your interest in contributing! Please follow these guidelines to make the contribution process smooth for everyone.

1. Fork the repository and create your branch from main/master.
2. Ensure any install or build dependencies are removed before the end of the layer when doing a build.
3. Update the README with details of changes to the interface, this includes new environment variables, exposed ports, useful file locations and container parameters.
4. When making a pull request, include a clear title and description, reference any related issues, and add tests if applicable.
5. Follow the project's code style and linters. If none are defined, prefer readable, well-documented code.

If you're unsure about a change, open an issue or discussion first to get feedback.
```

## 文件：.github/CODEOWNERS
```text
# Default owners for everything
* @tianzhao360-ship-it
```

## 文件：.github/SECURITY.md
```markdown
# Security Policy

If you believe you have found a security vulnerability, please do not open a public issue. Instead:

1. Use GitHub's private security advisories if available.
2. Or contact the maintainers directly. (Create an issue with the "private" or "security" flag if your organization supports private issues.)

We will respond as soon as possible and follow up with a fix and disclosure timeline.
```

## 文件：.gitignore
```text
# Node
node_modules/
npm-debug.log*
yarn-debug.log*
yarn-error.log*

# Python
__pycache__/
*.py[cod]
*.egg-info/
.env
venv/
ENV/

# Visual Studio Code
.vscode/
```

---


