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
- `registry_type`: Type of registry, [OCI | ECR | CHARTMEUSEUM - default is OCI].
- `aws_region`: AWS region, required when registry type is ECR.
