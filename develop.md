# Develop

### 向dev分支提交更改


```shell

# 请克隆dev分支

git clone -b dev https://github.com/xx025/carrot.git carrot-dev

```


### 模板

当前网站已经超过100个，为了方便管理，则使用模板的形式生成文档，下面是模板

```markdown
# Free ChatGPT Site List

**这儿为你准备了众多免费好用的ChatGPT镜像站点**

**发布网站：** https://www.example.com/   (😃敬请收藏和分享)

**分享站点**、**站点失效**、**标注错误**，请[🌺点此🌺](https://www.example.com/ )告诉我

> <a href="https://www.example.com/ " target="_blank"><font color="red">🔗支持我，给你更长久的陪伴：【🧡赞赏🧡】</font></a>

<br/>


### 站点列表

- 🔑: 需要登录使用

[//]: # (下面是正常的站点)

{% for item in items_zheng_chang %}
{{item.index}}. {{item.content}} {{ item.url }}
{% endfor %}



<details>
  <summary>更多站点</summary>

- 🔑:需要进行**登录**或需要**密码**
    <br/>
- ⛔:有限地使用**次数**或**字数**，需提供key或进行充值进行服务升级
     <br/>
- ❓ :未测试，未进行标注也为未测试
     <br/>

[//]: # ( &#40;下面是更多的站点&#41;)


{% for item in items_xian_zhi %}
{{item.index}}. {{item.content}} {{ item.url }}
    <br/>
{% endfor %}


</details>

[//]: # (下面是失效的站点)

<details>
  <summary>失效站点</summary>

{% for item in items_shi_xiao %}
{{item.index}}. {{item.content}} {{ item.url }}
    <br/>
{% endfor %}

</details>

### 妙站

> 下面这些站点也很有趣

{% for item in items_mian_zhan %}
{{item.index}}. {{item.content}} {{ item.url }}
{% endfor %}


### 欢迎补充

GitHub 仓库地址: https://www.example.com/ 

如果您认为站点可以加⭐、分享你发现的新的站点，反馈失效站点，欢迎[点此](https://www.example.com/ )告诉我


[关于广告位](https://www.example.com/ )

### 协议

如果您正在同步或转载本仓库内容，请遵守以下协议：1. 可以移除广告位 2. 其他部分请保持原文，不作修改

### 最后更新

如果下方时间已经晚于当前时间1h ；请前往[GitHub仓库](https://www.example.com/ )查看最新内容


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
