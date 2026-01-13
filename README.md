# GEI-Ops: GitHub Enterprise Importer IssueOps

A self-service solution for migrating repositories from GitHub Enterprise Server to GitHub Enterprise Cloud (customersuccess.ghe.com) using GitHub Enterprise Importer (GEI).

## Overview

This project provides an IssueOps workflow that allows users to request repository migrations by simply creating an issue. The workflow automatically processes the request and performs the migration using GitHub Enterprise Importer.

## How to Use

### Requesting a Migration

1. Go to the **Issues** tab
2. Click **New Issue**
3. Select **Repository Migration Request**
4. Fill out the form with:
   - Source GitHub Enterprise Server URL
   - Target GitHub Enterprise Cloud organization
   - Migration type (all repositories or specific ones)
   - Repository names (if migrating specific repositories)
5. Submit the issue

### What Happens Next

Once you submit the migration request:

1. The workflow automatically starts processing your request
2. You'll receive updates as comments on your issue:
   - Migration started notification
   - Validation results
   - Progress updates
   - Completion status
3. The issue will be automatically closed when the migration is complete

## Setup Instructions

### Required Secrets

To enable actual migrations, configure these repository secrets:

- `GHES_PAT`: Personal Access Token for source GitHub Enterprise Server
- `GHE_CLOUD_PAT`: Personal Access Token for target GitHub Enterprise Cloud

### PAT Requirements

**Source GHES PAT** needs:
- `repo` (full control)
- `admin:org` (read:org)
- `workflow`

**Target GHE Cloud PAT** needs:
- `repo` (full control)
- `admin:org` (read:org, write:org)
- `workflow`

## Current Status

This is a **simple version** of the workflow that:
- ✅ Collects migration request information via issue form
- ✅ Parses and validates the request
- ✅ Updates the issue with progress
- ✅ Installs the GEI CLI extension
- ⚠️ Does not perform actual migrations yet (requires secrets configuration)

## Next Steps

To enable full migration functionality:

1. Configure the required PAT secrets
2. Implement actual GEI migration commands (`gh gei migrate-repo`)
3. Add comprehensive error handling
4. Implement migration logging and artifact storage
5. Add retry logic for failed migrations
6. Set up email/Slack notifications

## Documentation

- [GitHub Enterprise Importer Documentation](https://docs.github.com/en/migrations/using-github-enterprise-importer)
- [Migrating from GHES to GHE Cloud](https://docs.github.com/en/migrations/using-github-enterprise-importer/migrating-between-github-products/migrating-repositories-from-github-enterprise-server-to-github-enterprise-cloud)

## Support

For issues or questions, please create an issue in this repository.