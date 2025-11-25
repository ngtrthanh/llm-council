# Git Sync Guide - Docker Changes

This guide will help you commit and push the Docker-related changes to your repository.

## Current Changes

The following files have been added/modified:

### New Files (Untracked)
- `.dockerignore` - Excludes unnecessary files from Docker builds
- `.env.example` - Template for environment variables
- `DOCKER.md` - Comprehensive Docker documentation
- `Dockerfile.backend` - Backend container definition
- `Dockerfile.frontend` - Frontend container definition
- `docker-compose.yml` - Docker Compose orchestration file

### Modified Files
- `README.md` - Updated with Docker Compose instructions

## Step-by-Step Sync Process

### Option 1: Push to Your Own Fork (Recommended)

If you want to maintain your own version with Docker support:

1. **Fork the repository** (if you haven't already):
   - Go to https://github.com/karpathy/llm-council
   - Click "Fork" button in the top right
   - This creates a copy under your GitHub account

2. **Update your remote to point to your fork**:
   ```bash
   # Add your fork as a new remote
   git remote add myfork https://github.com/ngtrthanh/llm-council.git
   
   # Or if you want to change the origin
   git remote set-url origin https://github.com/ngtrthanh/llm-council.git
   
   # Keep the original repo as upstream for future updates
   git remote add upstream https://github.com/karpathy/llm-council.git
   ```

3. **Stage all Docker-related changes**:
   ```bash
   git add .dockerignore .env.example DOCKER.md Dockerfile.backend Dockerfile.frontend docker-compose.yml README.md
   ```

4. **Commit the changes**:
   ```bash
   git commit -m "Add Docker Compose support

   - Add Dockerfile for backend (Python 3.11 + uv)
   - Add Dockerfile for frontend (Node 20 + Vite)
   - Add docker-compose.yml for orchestration
   - Add comprehensive Docker documentation
   - Update README with Docker instructions
   - Add .env.example template
   - Add .dockerignore for build optimization"
   ```

5. **Push to your fork**:
   ```bash
   # If you added as 'myfork'
   git push myfork master
   
   # Or if you changed origin
   git push origin master
   ```

### Option 2: Create a Feature Branch

If you want to keep these changes separate:

1. **Create a new branch**:
   ```bash
   git checkout -b feature/docker-support
   ```

2. **Stage and commit changes**:
   ```bash
   git add .dockerignore .env.example DOCKER.md Dockerfile.backend Dockerfile.frontend docker-compose.yml README.md
   
   git commit -m "Add Docker Compose support"
   ```

3. **Push the branch**:
   ```bash
   git push origin feature/docker-support
   ```

### Option 3: Contribute Back to Original Repo

If you want to contribute these changes back to karpathy's repository:

1. **Fork the repository** (if not done already)

2. **Create a feature branch**:
   ```bash
   git checkout -b add-docker-compose-support
   ```

3. **Stage and commit**:
   ```bash
   git add .dockerignore .env.example DOCKER.md Dockerfile.backend Dockerfile.frontend docker-compose.yml README.md
   
   git commit -m "Add Docker Compose support for easier deployment"
   ```

4. **Push to your fork**:
   ```bash
   git push origin add-docker-compose-support
   ```

5. **Create a Pull Request**:
   - Go to your fork on GitHub
   - Click "Pull Request" button
   - Select your branch and create PR to karpathy/llm-council

## Quick Commands Reference

### Check current status
```bash
git status
```

### View changes in a file
```bash
git diff README.md
```

### View all remotes
```bash
git remote -v
```

### Unstage files (if needed)
```bash
git restore --staged <file>
```

### Discard local changes (if needed)
```bash
git restore <file>
```

## Recommended Workflow

For most users, I recommend **Option 1** - maintaining your own fork:

```bash
# 1. Update remote to your fork
git remote set-url origin https://github.com/ngtrthanh/llm-council.git
git remote add upstream https://github.com/karpathy/llm-council.git

# 2. Stage all changes
git add .dockerignore .env.example DOCKER.md Dockerfile.backend Dockerfile.frontend docker-compose.yml README.md

# 3. Commit
git commit -m "Add Docker Compose support"

# 4. Push
git push origin master
```

## Keeping Your Fork Updated

To sync with the original repository later:

```bash
# Fetch updates from original repo
git fetch upstream

# Merge updates into your master
git checkout master
git merge upstream/master

# Push updates to your fork
git push origin master
```

## Notes

- The `.env` file is already in `.gitignore`, so your API key won't be committed
- Your GitHub username is set to `ngtrthanh` in the commands above
- If you encounter conflicts, resolve them before pushing
- Consider adding a note in your README that this is a fork with Docker support

## Troubleshooting

### "Permission denied" when pushing
- Make sure you're pushing to your own fork, not the original repo
- Check your GitHub authentication (SSH key or personal access token)

### "Updates were rejected"
- Pull the latest changes first: `git pull origin master`
- Then push again: `git push origin master`

### Want to start over?
```bash
# Discard all local changes
git restore .
git clean -fd
```
