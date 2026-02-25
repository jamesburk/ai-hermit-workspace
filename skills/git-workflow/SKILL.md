# Skill -- Git Workflow

Git operations, PR preparation, and changelog generation.

## Commands

- `/pr-summary` -- Summarize current branch changes vs base, draft PR description
- `/changelog <from>..<to>` -- Generate changelog entries from commit range
- `/branch-status` -- Show divergence from main, list modified files, flag conflicts

## Implementation

### `/pr-summary`

```bash
base=$(git symbolic-ref refs/remotes/origin/HEAD 2>/dev/null | sed 's@^refs/remotes/origin/@@' || echo "main")
echo "=== Branch: $(git branch --show-current) ==="
echo "=== vs base: $base ==="
echo ""
echo "--- Commits ---"
git log --oneline "$base"..HEAD
echo ""
echo "--- Files Changed ---"
git diff --stat "$base"..HEAD
echo ""
echo "--- Full Diff ---"
git diff "$base"..HEAD
```

After running, draft a PR description with:
- **Title:** concise, under 70 chars
- **Summary:** 1-3 bullet points of what changed and why
- **Test plan:** how to verify the changes

### `/changelog <from>..<to>`

```bash
git log --pretty=format:"- %s (%h)" "$1"
```

Group entries by type: Added, Changed, Fixed, Removed. Use conventional commit prefixes if present.

### `/branch-status`

```bash
base=$(git symbolic-ref refs/remotes/origin/HEAD 2>/dev/null | sed 's@^refs/remotes/origin/@@' || echo "main")
echo "=== $(git branch --show-current) vs $base ==="
echo "Ahead: $(git rev-list --count "$base"..HEAD)"
echo "Behind: $(git rev-list --count HEAD.."$base")"
echo ""
echo "--- Modified Files ---"
git diff --name-status "$base"..HEAD
```

Flag merge conflicts if any exist. Suggest rebase if behind by more than 10 commits.
