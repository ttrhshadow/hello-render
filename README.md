# hello-render

最小示例，用来走通 GitHub 到 Render 的完整链路。只有一个 index.html，不需要装依赖，也不需要构建。

## 一次性准备

Git 已装好，版本 2.55。本机还没配置提交身份，先跑这两条，邮箱换成你自己的。

```bash
git config --global user.name "ttrhshadow"
git config --global user.email "ttrhshadow@163.com"
```

GitHub 早就不允许用账号密码推送代码。去网页生成一个 token，右上角头像 → Settings → Developer settings → Personal access tokens → Tokens (classic) → Generate new token (classic) → 勾选 repo → Generate token → 复制。第一次 push 时当密码粘贴一次，Windows 会替你记住。

## 建仓库并推送

1. GitHub 网页右上角加号 → New repository，名字填 hello-render，选 Public，README 和 .gitignore 都不要勾，点 Create repository。
2. 空仓库页面上会直接给出下面这组命令，照着跑即可。

```bash
cd "D:/temp/hello-render"
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/ttrhshadow/hello-render.git
git push -u origin main
```

push 时用户名填 ttrhshadow，密码粘贴刚才的 token。

## 在 Render 上部署

1. 打开 dashboard.render.com，New → Static Site。
2. 列表里如果没有 hello-render，去 github.com/apps/render/installations/new，在 Repository access 里把这个新仓库加进来。
3. 选仓库 hello-render，Branch 填 main。
4. Name 填 hello-render，Build Command 留空，Publish Directory 填一个英文句点 `.`，表示直接发布仓库根目录。
5. 点 Create Static Site，等构建完成，打开分配给你的 onrender.com 网址。

静态站点在 Hobby 免费层，不需要绑卡。

## 以后每次改动

改 index.html，然后 add、commit、push 三连。Render 检测到 push 会自动重新部署，不用再进控制台。

## 常见卡点

推送报认证失败，多半是用了账号密码，换成 token。

Render 找不到仓库，是 GitHub App 的授权没覆盖到新仓库。

网址打开是 404，把 Publish Directory 改成 public，并把 index.html 移进 public 文件夹。
