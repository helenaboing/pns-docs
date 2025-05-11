# GitHub Workflow

## Setting Up Your Development Environment

1. **Fork the Repository**
   ```bash
   # Visit https://github.com/mokita-j/pns
   # Click the "Fork" button in the top right
   ```

2. **Clone Your Fork**
   ```bash
   git clone https://github.com/YOUR-USERNAME/pns.git
   cd pns
   ```

3. **Add Upstream Remote**
   ```bash
   git remote add upstream https://github.com/mokita-j/pns.git
   ```

## Making Changes

1. **Create a Branch**
   ```bash
   git checkout -b feature/your-feature-name
   # or
   git checkout -b fix/your-bug-fix
   ```

2. **Keep Your Branch Updated**
   ```bash
   git fetch upstream
   git rebase upstream/main
   ```

3. **Commit Your Changes**
   ```bash
   git add .
   git commit -m "feat: description of your changes"
   ```

   > **Commit Message Format**:
   > - feat: New feature
   > - fix: Bug fix
   > - docs: Documentation changes
   > - style: Formatting, missing semicolons, etc
   > - refactor: Code restructuring
   > - test: Adding tests
   > - chore: Maintenance tasks

## Submitting Pull Requests

1. **Push Your Changes**
   ```bash
   git push origin feature/your-feature-name
   ```

2. **Create Pull Request**
   - Go to your fork on GitHub
   - Click "New Pull Request"
   - Select your feature branch
   - Fill in the PR template

3. **PR Review Process**
   - Wait for CI checks to pass
   - Address review comments
   - Update your branch if needed
   - Maintain a clean commit history