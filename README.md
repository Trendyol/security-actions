# security-actions

## Description
Security actions for Trendyol GitHub

## Requirements
* [GitHub Actions](
    https://help.github.com/en/articles/about-github-actions#about-github-actions)
    must be enabled on the repository.
* Using reusable workflows from the organization must be enabled on the repository.
* [GitHub Advanced Security](https://docs.github.com/en/github/getting-started-with-github/about-github-advanced-security) must be enabled on the repository.
* Security Dashboard must be enabled on the repository.
test

## Usage
Please note that `security-gates` should be added after your build job. Below, you can find an example action config for your repositories.

```yaml
name: "your-build-action"
on:
  push:
    branches: ["master", "main"]
  pull_request:
    branches: ["*"]
  workflow_dispatch:

jobs:
  your_build_job: # Assume that this your build or any other job
    runs-on: ubuntu-latest
    steps:
      - name: Print Default Branch
        run: |
          echo ${{ github.event.repository.default_branch }}
          ls -la
          
  security-gates:
    uses: Trendyol/security-actions/.github/workflows/security-gates.yml@master
    needs: your_build_job # Replace with your build job name
    permissions:
      actions: read
      contents: read
      security-events: write # This is required for writing security events to built-in GitHub Security Dashboard

```

## Support
If you have any questions or suggestions, feel free to create an issue on GitHub or reach out to us on Slack.
## License
The scripts and documentation in this project are released under the [Apache 2.0](LICENSE) license.
