# develop




## GitHubAction自动同步
>GitHubAction每十分钟自动同步 dev分支`README.md`
> 请开起Action 可读写仓库
```yml
name: Sync
on:
  schedule:
    - cron: '*/10 * * * *'
jobs:
  sync-readme:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2
        with:
          ref: main 
      - name: Download README.md
        run: curl  -o README.md https://raw.githubusercontent.com/xx025/carrot/dev/README.md
      - name: Setup Node.js
        uses: actions/setup-node@v2
        with:
          node-version: '16.x'
      - name: Set up Git user
        run: |
          git config --global user.email "actions@github.com"
          git config --global user.name "GitHub Actions"
      - name: Check if changes exist
        run: |
          if git diff-index --quiet HEAD --; then
            echo "No changes to commit. Exiting."
          else
            git add README.md
            git commit -m "Sync README to main branch"
            git push origin HEAD:refs/heads/main
          fi
```


## star-histort
![star-history](https://api.star-history.com/svg?repos=xx025/carrot&type=Timeline)

