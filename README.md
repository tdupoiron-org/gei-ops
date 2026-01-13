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

This workflow provides **full migration functionality** and:
- ✅ Collects migration request information via issue form
- ✅ Parses and validates the request
- ✅ Validates required secrets are configured
- ✅ Installs the GEI CLI extension
- ✅ Performs actual repository migrations using GEI
- ✅ Supports both full organization and selective repository migrations
- ✅ Updates the issue with real-time progress
- ✅ Uploads migration logs as workflow artifacts
- ✅ Handles errors and provides troubleshooting guidance
- ✅ Automatically closes issues on successful migration

## Migration Process

The workflow performs the following steps:

1. **Validation**: Checks that required secrets (GHES_PAT, GHE_CLOUD_PAT) are configured
2. **Parsing**: Extracts migration details from the issue form
3. **Installation**: Installs the GitHub Enterprise Importer CLI
4. **Migration**: 
   - For "All repositories": Migrates all repos from the source organization
   - For specific repos: Migrates only the listed repositories
5. **Logging**: Saves detailed logs for each repository migration
6. **Reporting**: Updates the issue with success/failure status
7. **Completion**: Closes the issue automatically on success

## Setup Instructions for Administrators

### 1. Configure Repository Secrets

Add these secrets in repository settings:

```
GHES_PAT - Personal Access Token for source GitHub Enterprise Server
GHE_CLOUD_PAT - Personal Access Token for target GitHub Enterprise Cloud
```

### 2. Create the PATs

**Source GHES PAT** needs:
- `repo` (full control of private repositories)
- `admin:org` (read:org - read organization membership)
- `workflow` (update GitHub Actions workflows)

**Target GHE Cloud PAT** needs:
- `repo` (full control of private repositories)
- `admin:org` (read:org, write:org - manage organization)
- `workflow` (update GitHub Actions workflows)

### 3. Test the Workflow

Create a test migration issue to verify the setup.

## Troubleshooting

### Migration Fails with Authentication Error
- Verify both PATs are correctly configured in repository secrets
- Ensure PATs have the required scopes
- Check that PATs haven't expired

### Repository Not Found
- Verify the source URL is correct
- Ensure the repository name is spelled correctly
- Check that the PAT has access to the source repository

### Migration Logs
All migration logs are automatically uploaded as workflow artifacts and retained for 30 days. Download them from the Actions tab to review detailed migration information.

## Documentation

- [GitHub Enterprise Importer Documentation](https://docs.github.com/en/migrations/using-github-enterprise-importer)
- [Migrating from GHES to GHE Cloud](https://docs.github.com/en/migrations/using-github-enterprise-importer/migrating-between-github-products/migrating-repositories-from-github-enterprise-server-to-github-enterprise-cloud)

## Support

For issues or questions, please create an issue in this repository.