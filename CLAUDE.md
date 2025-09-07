# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is tuha263's GitHub profile repository that displays a dynamic, gaming-themed personal branding page with real-time statistics from GitHub and various organizations.

## Architecture

### Core Components

**Dynamic Statistics System**
- Automated workflow (`update-stats.yml`) runs every 4 hours via GitHub Actions
- Collects statistics from personal repos and 5+ organizations (The1Studio, StrangeLoopGames, NovalandNFT, etc.)
- Creates JSON badge files (`commits-badge.json`, `prs-badge.json`, `repos-badge.json`) for shields.io endpoints
- Profile stats stored in `profile-stats.json` with full metrics

**Custom Vercel Deployments**
- `github-readme-stats-tuha263.vercel.app` - GitHub stats with organization access
- `github-readme-streak-stats-tuha263.vercel.app` - Streak statistics (uses vercel branch, Node.js 22.x)
- `github-readme-activity-graph-tuha263.vercel.app` - Activity contribution graph
All deployments use `STATS_TOKEN` (PAT with org access) for authentication

**Badge System**
- Dynamic badges use shields.io endpoint URLs reading from JSON files
- Static badges for skills, tools, and frameworks
- Real-time updates without README modifications

## Common Commands

### GitHub Actions Management
```bash
# Manually trigger stats update
gh workflow run update-stats.yml

# Check workflow status
gh run list --workflow=update-stats.yml --limit=5

# View workflow logs
gh run view [RUN_ID] --log

# Check if badge files exist
gh api repos/tuha263/tuha263/contents | jq -r '.[].name' | grep badge
```

### Local Development
```bash
# Test badge endpoints
curl -s "https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/tuha263/tuha263/main/commits-badge.json&style=for-the-badge"

# Verify stats collection locally (requires GITHUB_TOKEN)
export GITHUB_TOKEN=ghp_xxxx
curl -s -H "Authorization: token $GITHUB_TOKEN" "https://api.github.com/users/tuha263"
```

### Deployment Updates
```bash
# Update Vercel environment variables
# 1. Visit deployment dashboard
# 2. Settings > Environment Variables
# 3. Update TOKEN/PAT_1 values
# 4. Redeploy

# Force cache refresh for badges
curl -X PURGE "https://camo.githubusercontent.com/[BADGE_CACHE_URL]"
```

## Key Files and Their Purposes

**README.md**
- Main profile display with dynamic badges at lines 49-51 and 180-182
- The One Game Studio branding at line 131
- Activity section between `<!--START_SECTION:activity-->` markers
- Skills matrix (hardcoded percentages) at lines 145-159

**.github/workflows/update-stats.yml**
- Collects stats from GitHub GraphQL API and REST API
- Iterates through all organization repositories
- Creates/updates 5 JSON files (profile-stats, deployments-config, 3 badge files)
- Uses `[skip ci]` to prevent workflow loops

**Badge JSON Files**
- Follow shields.io endpoint schema v1
- Auto-updated every 4 hours
- Contain formatted display values (e.g., "3.9k" for commits)

## Important Configuration

### Secrets Required
- `STATS_TOKEN`: GitHub PAT with `read:org`, `read:user`, `repo` scopes
- `GITHUB_TOKEN`: Default token (automatically provided)

### External Dependencies
- github-activity-readme action (jamesgeorge007)
- shields.io for dynamic badges
- Vercel for custom stats deployments
- GitHub Actions for automation

## Maintenance Notes

### Stats Not Updating
1. Check workflow runs: `gh run list --workflow=update-stats.yml`
2. Verify STATS_TOKEN validity and permissions
3. Check if JSON files exist on main branch
4. Clear CDN cache if badges appear stale

### Workflow Conflicts
- Workflow only triggers on schedule (cron) or manual dispatch
- No push triggers to avoid conflicts
- Uses rebase and retry logic for commits

### Organization Stats Collection
- Iterates through each org's repositories
- Checks contributor status for each repo
- Aggregates total contributions across all orgs
- May timeout for users with many org memberships

## Current Statistics (as of last update)
- Total Commits: ~3,900 (2,940 personal + 959 org)
- Pull Requests: 300+
- Active Repositories: 87
- Organizations: 5 (The1Studio, StrangeLoopGames, NovalandNFT, GameDevelopmentKit, p00ls-games-hosting)