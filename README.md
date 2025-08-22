[GitHub Actions Run – Failed at Step 4](https://github.com/sous-chefs/aws/actions/runs/15302163226/job/43045320969#step:4:1)name: Markdown Lint

on:
  pull_request:
  push:
    branches:
      - main

jobs:
  lint:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Run Markdown Linter
        uses: avto-dev/markdown-lint@v1
        with:
          config: mlc_config.json
          args: |
            ${{ github.event_name == 'pull_request' && github.event.pull_request.base.sha && format('--diff {0}', github.event.pull_request.base.sha) || '.' }}