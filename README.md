name: Generate Snake Animation

on:
  schedule:
    - cron: "0 0 * * *"  # Every day at midnight
  workflow_dispatch:      # Optional: allows you to run it manually

jobs:
  generate:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v3

      - name: Generate GitHub Contribution Snake 🐍
        uses: Platane/snk@v3
        with:
          github_user_name: shyam-dev30
          outputs: |
            dist/github-contribution-grid-snake.svg
            dist/github-contribution-grid-snake-dark.svg

      - name: Push to output branch
        uses: crazy-max/ghaction-github-pages@v3
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
