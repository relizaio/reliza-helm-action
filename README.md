# `reliza-helm-action`

## About

GitHub Action to version and publish helm chart to an oci compliant registry and submit the release metadata to RelizaHub.

## Usage

```yaml
steps:
- uses: relizaio/reliza-helm-action@1.5
  with:
    reliza_api_id: <api-id-obtained-from-relizahub>
    reliza_api_key: <api-key-obtained-from-relizahub>
    repository_username: <chart-repo-username>
    repository_password: <chart-repo-password>
    repository_host: <chart-repo-host>
    helm_chart_name: <chart-name>
```

## Inputs
The actions supports the following inputs:

- `reliza_api_id`: The project API ID obtained from RelizaHub.
- `reliza_api_key`: The project API Key obtained from RelizaHub.
- `repository_username`: Username for the chart repository.
- `repository_password`: Password for the chart repository.
- `repository_host`: Chart repository host.
- `helm_chart_name`: Name of the helm chart.
- `path`: Path to the relative to root of the repo (default is '.')
- `reliza_project_id`: Project UUID if an org-wide key is used.
- `registry_type`: Type of registry, [OCI | ECR | CHARTMUSEUM - default is OCI].
- `aws_region`: AWS region, required when registry type is ECR.

## Permissions
This action attempts to increment version in the Chart.yaml and make a new commit. This requires write permission to the given to the github-actions bot. To give such permissions, include following section in your workflow:

```
permissions:
  contents: write
```

See a full sample in our Rebom workflow - https://github.com/relizaio/rebom/blob/master/.github/workflows/github_actions.yml

Refer to GitHub documentations for more information - https://docs.github.com/en/actions/security-guides/automatic-token-authentication

If these permissions are not given, the action will still work but it won't be able to commit a new Chart version.

## Security

### Automatic Cleanup of CI Temporary Files

This action automatically protects against accidentally packaging sensitive CI temporary files in your Helm charts. The following files are excluded from the packaged chart:

- `get_latest_release_cmd`
- `get_latest_release_exec`
- `get_version_command`
- `get_version_exec`
- `reliza_command`
- `rlz_cmd_exec`

**These files may contain API keys and should never be distributed.**

The action implements a defense-in-depth approach:

1. **Creates a `.helmignore` file** - Helm's native mechanism to exclude files during packaging
2. **Actively deletes** temporary files before packaging
3. **Verifies cleanup** - Fails the build if any sensitive files remain

This ensures that even if temporary files are created during the CI process, they will never be included in the published Helm chart.
