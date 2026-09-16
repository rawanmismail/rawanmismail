name: Metrics

on:
  schedule:
    - cron: "0 0 * * *"   # runs daily at midnight UTC
  workflow_dispatch:        # lets you trigger it manually from the Actions tab

jobs:
  github-metrics:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      # Classic overview card (header, activity, repositories)
      - uses: lowlighter/metrics@latest
        with:
          filename: github-metrics/metrics.classic.svg
          token: ${{ secrets.METRICS_TOKEN }}
          base: header, activity, community, repositories

      # In-depth language breakdown (clones repos to analyze languages precisely)
      - uses: lowlighter/metrics@latest
        with:
          filename: github-metrics/metrics.plugin.languages.indepth.svg
          token: ${{ secrets.METRICS_TOKEN }}
          base: ""
          plugin_languages: yes
          plugin_languages_indepth: yes
          plugin_languages_details: bytes-size, percentage, lines-of-code
          plugin_languages_limit: 8
