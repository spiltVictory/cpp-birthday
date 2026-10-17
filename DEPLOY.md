# 部署到 GitHub Pages（免费）

这个项目是纯静态页面：没有后端、没有构建步骤，`index.html` 和 `teacher.html` 放在同一个目录即可。

已经部署好：

- 学生生日页：https://spiltvictory.github.io/cpp-birthday/
- 老师工作台：https://spiltvictory.github.io/cpp-birthday/teacher.html

> 当前仓库已完成 `git init`、首次提交、push，并开启了 Pages。下面是完整流程，换电脑或从零再搭一遍时用；日常更新只需要看第五步。

---

## 一、先确认 git 身份

已经配置好：

```bash
git config --global user.name "yzj"
git config --global user.email "1075305747@qq.com"
```

可以用 `git config --global --list` 检查。

---

## 二、在 GitHub 建一个空仓库

1. 登录 GitHub，点右上角 **+** → **New repository**。
2. Repository name 填：`cpp-birthday`（也可以换，后面地址跟着变）。
3. 选择 **Public**。
   - GitHub Pages 免费版需要仓库是公开的。
   - 学生信息不在仓库里，链接是老师在自己浏览器里生成的；公开仓库不会泄露名单。
4. **不要**勾选 Add a README、.gitignore、license，保持空仓库。
5. 点 **Create repository**。

建好后 GitHub 会显示仓库地址，例如：

```
https://github.com/spiltVictory/cpp-birthday.git
```

---

## 三、把本地仓库推上去

项目目录已经配置好 `origin`，日常更新只需要 `git push`。如果是换一台电脑从零开始：

```bash
cd C:\harness\cpp-birthday

git remote add origin https://github.com/<你的用户名>/cpp-birthday.git
git push -u origin main
```

第一次 push 会弹出 GitHub 登录窗口（Git Credential Manager）：按提示在浏览器里登录/授权即可。授权一次，以后不用再登。

如果已经用 SSH：

```bash
git remote add origin git@github.com:<你的用户名>/cpp-birthday.git
git push -u origin main
```

> 本机 `~/.ssh/id_ed25519.pub` 已存在，但还没有加到 GitHub 账号。想用 SSH，先把公钥贴到 GitHub：Settings → SSH and GPG keys → New SSH key。

---

## 四、开启 GitHub Pages

1. 打开仓库页面 → **Settings**。
2. 左侧 **Pages**。
3. **Build and deployment** → Source 选 **Deploy from a branch**。
4. Branch 选 **main**，目录选 **/ (root)**，点 **Save**。
5. 等 1–2 分钟，页面上方会出现地址：

```
https://spiltvictory.github.io/cpp-birthday/
```

测试：

- 学生页：`https://spiltvictory.github.io/cpp-birthday/`
- 老师页：`https://spiltvictory.github.io/cpp-birthday/teacher.html`

第一次打开老师页，填一位同学的信息，复制链接，手机浏览器打开确认。

---

## 五、以后更新

```bash
cd C:\harness\cpp-birthday

git add .
git commit -m "调整文案"
git push
```

GitHub Pages 会在 1 分钟左右自动更新。手机还看到旧版本时，换个网络或清缓存。

---

## 六、绑定自己的域名（可选）

如果 `github.io` 在国内访问慢，可以绑自己的域名：

1. 仓库 Settings → Pages → **Custom domain**，填 `birthday.example.com`，Save。
2. 在你的域名 DNS 里加一条 CNAME，指向 `<你的用户名>.github.io`。
3. 等证书签发（通常几分钟到几小时），勾选 **Enforce HTTPS**。

> 国内网络环境差异大：`github.io` 在部分地区/运营商可能慢或打不开，微信对未备案域名也可能提示。如果主要给国内家长用，最稳的是绑一个已备案域名；免费方案无法保证国内访问质量。

---

## 常见问题

**Pages 设置里没有地址 / 打开 404？**  
- 确认仓库是 **Public**（免费版私有仓库不能开 Pages）。
- 确认 Pages 的 Branch 是 `main`、目录是 `/ (root)`。
- 确认 `index.html` 在仓库根目录。
- 刚开启 Pages 需要等 1–2 分钟。

**push 时提示没有权限？**  
- 确认远程地址里的用户名和仓库名正确。
- 让 Git Credential Manager 重新登录：Windows 凭据管理器里删掉旧的 `git:https://github.com`，再 push。
- 或者改用 SSH，并把本机公钥加到 GitHub。

**老师页生成的链接是 `file:///C:/...`？**  
说明你打开的是本地文件。请打开部署后的 `https://.../teacher.html` 再生成；本地页面也会显示黄色提示。

**学生页能打开，老师页 404？**  
确认 `teacher.html` 和 `index.html` 在同一个目录、都已提交并 push。

**改了页面但线上没变？**  
看仓库里最新 commit 是否已经 push；Pages 构建有 1 分钟左右延迟；再强制刷新。

---

## 免费额度 & 说明

- GitHub Pages 对公开仓库免费，静态站点，无需服务器和数据库。
- 页面里没有后端，老师页只在浏览器里拼链接，不保存、不上传学生信息。
- 链接里包含学生姓名，只发给对应家长，不要发群，也不要把学生名单提交到仓库。

---

## 备选：以后想换 Cloudflare Pages

如果 `github.io` 访问实在不理想，可以把同一个仓库接到 Cloudflare Pages：Workers & Pages → Create → Pages → 连 Git，构建命令留空，输出目录填 `.`。免费，但国内访问同样有地区差异。
