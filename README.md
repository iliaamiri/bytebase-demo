# Bytebase Demo

Database schema migration management using Bytebase and GitHub Actions.

## Structure

```
migrations-semver/     # SQL migration files (semver naming)
.github/workflows/
  ├── release-action.yml    # Auto-deploy on push to main
  └── chatops-migrate.yml   # Deploy via PR comments
```

## Usage

### Automatic Deployment
Push SQL files to `migrations-semver/` on `main` branch. The pipeline will:
1. Create a rollout plan
2. Deploy to test environment
3. Deploy to prod environment

### ChatOps Deployment
Comment on a PR to trigger migrations:
```
/migrate test
/migrate prod
```

## Configuration

Set these in GitHub environment variables/secrets:

| Variable | Description |
|----------|-------------|
| `BYTEBASE_URL` | Bytebase instance URL |
| `BYTEBASE_PROJECT` | Target project name |
| `BYTEBASE_SERVICE_ACCOUNT` | Service account email |
| `BYTEBASE_SERVICE_ACCOUNT_SECRET` | Service account secret |
| `BYTEBASE_TARGETS` | Target databases |
| `FILE_PATTERN` | Migration file pattern |

## Migration File Naming

Use semver format: `v<version>_<description>.sql`

Example: `v1.0.1_modify-accounts-info-table.sql`
