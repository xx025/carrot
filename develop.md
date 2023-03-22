# Develop

### 向dev分支提交更改


```shell

# 请克隆dev分支

git clone -b dev https://github.com/xx025/carrot.git carrot-dev

```

### GitHubAction自动同步

> GitHubAction每十分钟自动同步 dev 分支[README.md](https://github.com/xx025/carrot/blob/dev/README.md)
> 请开起Action 可读写仓库
>
> 开启方法：
> 1. Actions permissions -->[✔]Allow all actions and reusable workflows # 允许action运行
> 2. Workflow permissions-->[✔]Read and write permissions # 给与action读写权限

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
          ref: main # 要同步的分支
      - name: Download README.md
        run: |
          curl  -o README.md https://raw.githubusercontent.com/xx025/carrot/dev/README.md
          echo "$(cat README.md)"$'\n\n>Last synced:BeiJingT '"$(TZ='Asia/Shanghai' date +'%Y-%m-%d %H:%M:%S')" > README.md
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
            git commit -m "Sync README to mges branch"
            git push origin HEAD:refs/heads/main
          fi
```

## star历史

![star-history](https://api.star-history.com/svg?repos=xx025/carrot&type=Timeline)
